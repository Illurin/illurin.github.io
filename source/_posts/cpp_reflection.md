---
title: 使用模板技巧和LibClang实现简易C++静态反射系统
date: 2022-12-16 20:30:00
tags: 
    - C++
    - 游戏引擎设计
categories: Modern C++
top_img: /images/articles/cpp_reflection/image_1.png
cover: /images/articles/cpp_reflection/image_1.png
---

在游戏引擎的设计中，我们经常会需要从外部去修改在程序代码中定义的变量，例如在代码中定义一个角色的速度，将其曝露在编辑器中，使我们在调试的时候只需要在编辑器中修改对应的值，而不需要每次都修改对应的代码，这种使数据和实现分离的思想是游戏引擎设计中的核心一环。

为了实现这个功能，我们就需要引入**反射（Reflection）** 的概念。所谓反射，就是指程序可以访问，检测和修改它本身状态或行为的一种能力，而在C++里，就是可以通过字符串表示的类名找到程序中对应的类，以及访问和修改类中的成员变量/成员函数的功能。

反射的实现主要有以下两个方法：

1. 运行时反射：在运行时创建反射的注册表，将所有要反射的类写入注册表中。
2. 编译期反射：给所有要反射的类指定宏，并在编译期自动生成反射类的代码。

这里我选择以运行时反射为基础，先成功获取所有的反射信息，之后要进行代码生成或者静态反射就十分容易了。

## 运行时反射

> 以下代码部分参考RTTR库以及 <https://github.com/taichi-dev/cpp-training-season1> 实现。

### 创建全局注册表

我们需要一个基本的数据结构来描述反射出的类是什么样的，一般而言，它会包括：类名，类的成员变量，类的成员函数。成员变量和成员函数我们分别采用类`MemberVariable`和`MemberFunction`来存储，代码如下：

```C++
class TypeDescriptor {
public:
	const ::std::string& GetName() const {
		return name;
	}

	const ::std::vector<MemberVariable>& GetMemberVariables() const {
		return memberVars;
	}

	const ::std::vector<MemberFunction>& GetMemberFunctions() const {
		return memberFuncs;
	}

	MemberVariable GetMemberVariable(const ::std::string& name) const {
		for (auto& var : memberVars) {
			if (var.GetName() == name)
				return var;
		}
		return MemberVariable{};
	}

	MemberFunction GetMemberFunction(const ::std::string& name) const {
		for (auto& func : memberFuncs) {
			if (func.GetName() == name)
				return func;
		}
		return MemberFunction{};
	}

private:
	::std::string name;

	::std::vector<MemberVariable> memberVars;
	::std::vector<MemberFunction> memberFuncs;
};
```

接下来，我们创建一个静态的全局注册表，所有需要反射的类都会写入到注册表中，我们可以采用`std::unique_ptr`来管理全局唯一`TypeDescriptor`对象，并且使用哈希表方便查找，代码如下：

```C++
class Registry {
public:
	static Registry& Instance() {
		static Registry instance;
		return instance;
	}

	std::vector<TypeDescriptor*> Get() const {
		std::vector<TypeDescriptor*> tmpDescs;
		for (auto& desc : descs) {
			tmpDescs.push_back(desc.second.get());
		}
		return tmpDescs;
	}

	TypeDescriptor* Find(const ::std::string& name) const {
		return descs.find(name)->second.get();
	}

	void Register(::std::unique_ptr<TypeDescriptor> desc) {
		auto name = desc->GetName();
		descs[name] = ::std::move(desc);
	}

	void Clear() {
		decltype(descs) temp;
		descs.swap(temp);
	}

private:
	::std::unordered_map<::std::string, ::std::unique_ptr<TypeDescriptor>> descs;
};
```

> 在`Clear`函数中使用了`swap`来清空容器，这样的好处是可以使容器完全重置，如果直接使用`clear`的话会保留原来的容器大小。

### 类型擦除（Type Erasure）

在实现反射类成员量的过程中，我们不关心变量/函数的具体类型，我们希望最终写出来的代码可以做到类型无关，泛用性很强，这时候就需要用到**类型擦除**的概念，

类型擦除的一个典型做法就是使用`template`模板，我们通常使用模板来处理任何类型的变量，也可以用模板来处理任何类型的类，参考以下代码：

```C++
template<class Class, typename Var>
void Function(Var Class::* var) {}
```

这个模板函数的形参`var`是一个指针，它指向`Class`类型中的任意一个`Var`类型的成员变量。假设有一个类`Foo`，里面有一个`int`类型的成员变量`x`，那么我们可以这样调用这个函数：

```C++
template<class Class, typename Var>
void Function(Var Class::* var, Class obj) {
	std::cout << obj.*var << std::endl;
}

class Foo {
public:
	int x;
};

int main() {
	Foo foo;
	foo.x = 1;

	Function(&Foo::x, foo);

	return 0;
}
```

这个模板函数写法让我们可以读写任何类中的任何成员变量，这样就成功将具体的类擦除了。

C++11中的lambda匿名函数可以用于实现类型无关的抽象，参考以下代码：

```C++
class Foo {
public:
	Foo(void* var) {
		func = [var]() -> void* {
			return var;
		};
	}
	
	void* Func() {
		return func();
	}
	
private:
	std::function<void* ()> func;
};

int main() {
	int var = 1;
	Foo foo(&var);

	std::cout << *static_cast<int*>(foo.Func()) << std::endl;

	return 0;
}
```	

C++17在STL库中新增的万能容器`std::any`和`std::any_cast`可以更方便地实现类型擦除，参考以下代码：

```C++
int main() {
	std::vector<std::any> values;

	values.push_back(1);
	values.push_back("Hello, world!");
	
	auto print = [](const std::any& value) {
		//判断 value 是否为 int 类型
		if (value.type() == typeid(int)) {
			std::cout << "int: " << std::any_cast<int>(value) << std::endl;
		}
		//判断 value 是否为 string 类型
		else if (value.type() == typeid(const char*)) {
			std::cout << "string: " << std::any_cast<const char*>(value) << std::endl;
		}
		//如果是其它类型，则输出错误信息
		else {
			std::cout << "unkown type" << std::endl;
		}
	};

	for (const auto& value : values) {
		print(value);
	}

	return 0;
}
```

如果`std::any_cast`转换的类型与`std::any`中存储的值的实际类型不符，则会抛出`bad_any_cast`异常，这也说明`std::any_cast`本身并不能实现任何类型转换。

值得一提的是，标准中规定以下写法：

```C++
std::any var = 1;
auto ptr = std::any_cast<int>(&var);
```

得到的`ptr`是一个指向`var`的指针，即此处cast出的实际类型为`int*`。

在进行未定类型函数传参时，`std::any`是对于`void*`和`std::shared_ptr<void>`的一个上位替代。

### 反射成员变量

接下来完善我们的`MemberVariable`类，在此类中我们需要：变量名，获取变量的方法，修改变量的方法。代码如下：

```C++
class MemberVariable {
public:
	MemberVariable() = default;

	template<class Class, typename Var>
	MemberVariable(Var Class::* var) {
		getter = [var](::std::any obj) -> ::std::any {
			return ::std::any_cast<const Class*>(obj)->*var;
		};

		setter = [var](::std::any obj, ::std::any val) {
			auto* self = ::std::any_cast<Class*>(obj);
			self->*var = ::std::any_cast<Var>(val);
		};
	}

	const ::std::string& GetName() const {
		return name;
	}

	template<typename Var, class Class>
	Var GetValue(const Class& obj) const {
		return ::std::any_cast<Var>(getter(&obj));
	}

	template<typename Var, class Class>
	void SetValue(Class& obj, Var value) {
		setter(&obj, value);
	}

private:
	::std::string name;

	::std::function<::std::any(::std::any)> getter{ nullptr };
	::std::function<void(::std::any, ::std::any)> setter{ nullptr };
};
```

在此处我们就使用了类型擦除的技巧，为什么要使用类型擦除，原因也很简单，因为我们的反射是在运行时执行的，在编译期我们并不知道具体的类型，因此不能写出`MemberVariable<Class, Var>`的形式，这也是便于塞进同一个容器中。

这个类中比较难理解的就是构造函数的代码。在构造函数中，我们首先获得指向类中一个成员变量的指针，并用lambda表达式捕获这个指针，然后初始化`getter`和`setter`方法。`getter`方法输入一个类实例，返回类中对应成员变量的值；`setter`输入一个类实例和值，修改类实例中对应成员变量的值。

### 反射成员函数

接下来完善我们的`MemberFunction`类，它和构造`MemberVariable`的大致思路相同，只不过复杂度要高了一些。我们首先来考虑构造函数：

**无返回值，非const成员函数：**

```C++
template<class Class, typename... Args>
explicit MemberFunction(void (Class::* func)(Args...)) {
	function = [this, func](::std::any objArgs) -> ::std::any {
		using tuple = ::std::tuple<Class&, Args...>;
		auto* pTuple = ::std::any_cast<tuple*>(objArgs);
		::std::apply(func, *pTuple);
		return ::std::any{};
	};
} 
```

构造函数的参数是一个指向类中成员函数的指针，在这里，我们使用了可变参数模板，代表成员函数可以接纳任意数量的参数。

这里的`function`依旧是一个`std::function<::std::any(::std::any)>`类型的函数容器，我们实际去调用成员函数的过程就是在调用`function`。为了使`function`可以传入多个参数，可以考虑使用C++11中的可变参数元组`std::tuple`作为`std::any`的指代对象，因此，我们可以写出如下代码：

```C++
using tuple = ::std::tuple<Class&, Args...>;
tuple* pTuple = ::std::any_cast<tuple*>(objArgs);
::std::apply(func, *pTuple);
```

`std::apply`是在C++17中引入的功能，它的作用是将传入一个函数包装和一个参数（这个参数可以是`std::tuple`，`std::array`或`std::pair`），并将这个参数当作函数的实参去调用函数，当apply的那个函数是非静态成员函数时，我们必须为其指定实例，而这个实例就放在tuple的第一个位置，这也就是为什么要写成`std::tuple<Class&, Args...>`的形式。

由于该函数无返回值，所以最后返回一个空的`std::any{}`。

**无返回值，const成员函数：**

```C++
template<class Class, typename... Args>
explicit MemberFunction(void (Class::* func)(Args...) const) {
	function = [this, func](::std::any objArgs) -> ::std::any {
		using tuple = ::std::tuple<const Class&, Args...>;
		tuple* pTuple = ::std::any_cast<tuple*>(objArgs);
		::std::apply(func, *pTuple);
		return ::std::any{};
	};

	isConst = true;
}
```

这里除了使用常量引用`const Class&`和设置`isConst`标志以外，和上述代码并无区别。

**有返回值，非const成员函数：**

```C++
template<class Class, typename Return, typename... Args>
explicit MemberFunction(Return (Class::* func)(Args...)) {
	function = [this, func](::std::any objArgs) -> ::std::any {
		using tuple = ::std::tuple<Class&, Args...>;
		tuple* pTuple = ::std::any_cast<tuple*>(objArgs);
		return ::std::apply(func, *pTuple);
	};
}
```

定义一个新的模板类型作为返回值类型，同时将执行`std::apply`得到的值返回出去。

**有返回值，const成员函数：**

```C++
template<class Class, typename Return, typename... Args>
explicit MemberFunction(Return (Class::* func)(Args...) const) {
	function = [this, func](::std::any objArgs) -> ::std::any {
		using tuple = ::std::tuple<const Class&, Args...>;
		tuple* pTuple = ::std::any_cast<tuple*>(objArgs);
		return ::std::apply(func, *pTuple);
	};

	isConst = true;
}
```

**Invoke函数：**

在调用构造函数后，我们已经将`function`存储在了`MemberFunction`类当中，接下来我们需要一个调用`function`的方法，于是编写一个Invoke函数，代码如下：

```C++
template<class Class, typename... Args>
::std::any Invoke(Class& obj, Args&&... args) {
	if (isConst) {
		auto argsTuple = ::std::make_tuple(::std::reference_wrapper<const Class>(obj), args...);
		return function(&argsTuple);
	}
	auto argsTuple = ::std::make_tuple(::std::reference_wrapper<Class>(obj), args...);
	return function(&argsTuple);
}
```

这里用万能引用的方式传入了参数包，然后将该参数包再次用`std::make_tuple`包装成了tuple传入`function`中，完成了调用。

注意这里在包装参数时用到了`std::reference_wrapper<Class>`，它是一个引用的包装器，行为和`Class&`类似，但是不同的是它可以被拷贝或复制。在使用`std::make_tuple`的时候默认会把每个参数进行一次拷贝，将其转化为原始值类型，而使用`std::reference_wrapper`进行包装可以规避掉拷贝，从而确保传入的值是引用。

另一个需要注意的点是，当函数参数出现引用时，考虑以下代码：

```C++
class Foo {
public:
	void Func(const ::std::string& str) { ::std::cout << str << ::std::endl; }
};

int main() {
	reflect::MemberFunction func(&Foo::Func);

	::std::string str = "Hello, world!";

	Foo foo;
	func.Invoke(foo, str);

	return 0;
}
```

这样在进行Invoke时会抛出`bad_any_cast`异常，原因是上面说过的`std::make_tuple`会将参数转化为原始值类型，因此这里的`argsTuple`类型为`std::tuple<Foo&, ::std::string>`，与成员函数所期望的`std::tuple<Foo&, const ::std::string&>`不符，无法进行`std::any_cast`转换，解决方案是使用`std::ref`和`std::cref`规定传入的值为引用，将上述代码修改如下：

```C++
func.Invoke(foo, ::std::cref(str));
```

### 优化：ArgWrap包装参数

使用`std::ref`和`std::cref`手动指定引用有时会带来不必要的错误，因此利用一个ArgWrap中间层对其进行包装是十分必要的，ArgWrap的基本功能是实现值和引用的双向映射。

考虑值类型和左值引用两种情况，此处用到了模板的特化：

```C++
template<typename T>
struct RefTrait {
	static constexpr int value = 0;
};

template<typename T>
struct RefTrait<T&> {
	static constexpr int value = 1;
};
```

考虑非const和const两种情况，设非const为假，const为真：

```C++
template<typename T>
struct IsConst : ::std::false_type {};

template<typename T>
struct IsConst<T&> : ::std::false_type {};

template<typename T>
struct IsConst<T*> : ::std::false_type {};

template<typename T>
struct IsConst<const T> : ::std::true_type {};

template<typename T>
struct IsConst<const T&> : ::std::true_type {};

template<typename T>
struct IsConst<const T*> : ::std::true_type {};
```

`ArgWrap`类的基本结构如下：

```C++
class ArgWrap {
public:
	template<typename T>
	ArgWrap(T&& value) {
		refType = RefTrait<T>::value;
		isConst = IsConst<T>::value;

		if (refType == 1) {
			storage = &value;
		}
		else {
			storage = value;
		}
	}

	template<typename T>
	T Cast() {
		//TODO
	}

private:
	int refType{ 0 };
	bool isConst{ false };

	::std::any storage{};
};
```

其中`refType`代表存储的值的具体类型（值或引用），`isConst`代表存储的值类型是否具有常量限定符。如果传入的是值类型，那么存储值本身；如果传入的是引用，那么存储值的地址。

向`Cast`函数中添加如下代码：

```C++
using RawT = ::std::remove_cv_t<::std::remove_reference_t<T>>;
constexpr int castRefType = RefTrait<T>::value;
constexpr bool castIsConstant = IsConst<T>::value;
```

> `std::move_reference`用于将引用类型还原为值类型，`std::move_reference_t<T>`与`std::remove_reference<T>::value`同义。

> `std::move_cv`用于去掉类型的`const`限定符和`volatile`限定符，`std::remove_cv_t<T>`与`std::remove_cv<T>::value`同义。

`castRefType`代表转换的具体类型（值或引用），`castIsConst`代表转换的类型是否具有常量限定符。由于模板实例是在编译期创建的，所以此处的代码都用`constexpr`修饰，放在编译期处理。

考虑以下几种不同的Cast转换情形：

```C++
if constexpr (castRefType == 0) {
	if (refType == 1) {
		//引用类型转换为值类型
		if (isConst)
			return *::std::any_cast<const RawT*>(storage);
		else
			return *::std::any_cast<RawT*>(storage);
	}
	//值类型转换为值类型
	return ::std::any_cast<RawT>(storage);
}

//值类型转换为引用类型
if (refType == 0) {
	return *::std::any_cast<RawT>(&storage);
}

//引用类型转换为引用类型
if constexpr (castIsConstant) {
	if (isConst)
		return *::std::any_cast<const RawT*>(storage);
	else
		return *::std::any_cast<RawT*>(storage);
}
else {
	if (isConst) {
		//无法将常量引用转换为非常量引用
		throw ::std::runtime_error("Cannot cast const ref to non-const ref");
	}

	return *::std::any_cast<RawT*>(storage);
}

```

编写一个`AsTuple`函数，以array作为传入参数构建tuple：

```C++
template<typename... Args, size_t N, size_t... Is>
::std::tuple<Args...> AsTuple(::std::array<ArgWrap, N>& array, ::std::index_sequence<Is...>) {
	return ::std::forward_as_tuple(array[Is].Cast<Args>()...);
}

template<typename... Args, size_t N, typename = ::std::enable_if_t<N == sizeof...(Args)>>
::std::tuple<Args...> AsTuple(::std::array<ArgWrap, N>& array) {
	return AsTuple<Args...>(array, ::std::make_index_sequence<N>());
}
```

`AsTuple`的第一个重载提供了两个整型的模板参数`N`和`Is`，其中`N`指定了模板参数包`Args`的参数个数，`Is`是一个用`std::index_sequence`填充的参数包。

> `std::index_sequence`和`std::make_index_sequence`是C++14提供的一个模板元编程工具，作用是产生用作编译期常量的整数序列，此处我们用它来生成索引。

用`std::forward_as_tuple`将参数包`Args`中的每一个参数都经过Cast之后转发为tuple。

`AsTuple`的第二个重载是第一个重载的一个接口，我们实际使用时就是调用的这一个重载。

> `std::enable_if_t`是C++14提供的一个模板元编程工具，与`std::enable_if<>::type`同义，作用是使类型在满足条件时有效，这里只是单纯用来确保`N`和`Args`的参数个数匹配。

完成了`ArgWrap`类的构建，改写原来的`MemberFunction`构造函数中的代码如下：

```C++
argsNum = sizeof...(Args);

function = [this, func](void* argsPtr) -> ::std::any {
	auto& args = *static_cast<::std::array<ArgWrap, sizeof...(Args) + 1>*>(argsPtr);
	auto tp = AsTuple<Class&, Args...>(args);
	
	::std::apply(func, tp);
	return ::std::any{};
};
```

用一个`argsNum`来存储成员函数应传入的参数个数。`function`的参数从`std::any`改成了`void*`，实际上传入的是被包装为array的参数（array的大小为`sizeof...(Args) + 1`，因为还要塞一个类实例进去），通过`AsTuple`转换为tuple，最后再通过`std::apply`调用。

改写原来的`MemberFunction::Invoke`中的代码如下：

```C++
if (argsNum != sizeof...(Args)) {
	throw ::std::runtime_error("Mismatching number of arguments");
}

::std::array<ArgWrap, sizeof...(Args) + 1> argsArray = {
	ArgWrap(obj),
	ArgWrap(std::forward<Args>(args))...
};

return function(&argsArray);
```

首先判断传入的参数个数是否准确，否则抛出异常。

将输入的参数用数组包装起来，这里使用了`std::forward`去实现参数包转发，通过C++17的折叠表达式展开了`ArgWrap`构造函数。最后将`argsArray`用指针的方式传入`function`中完成调用。

有了以上的铺垫，以后在调用Invoke时就可以实现值类型和引用类型的自动转换，不用任何`std::ref`或`std::cref`。

### 写入全局注册表

构建一个`RawTypeDescriptorBuilder`类来将反射信息写入注册表中，类的结构如下：

```C++
class RawTypeDescriptorBuilder {
public:
	explicit RawTypeDescriptorBuilder(const ::std::string& name);
	RawTypeDescriptorBuilder(const RawTypeDescriptorBuilder&) = delete;
	~RawTypeDescriptorBuilder();

	template<class Class, typename Var>
	void AddMemberVariable(const ::std::string& name, Var Class::* var) {
		MemberVariable variable(var);
		var.name = name;
		desc->memberVars.push_back(var);
	}

	template<class Class, typename Func>
	void AddMemberFunction(const ::std::string& name, Func Class::* func) {
		MemberFunction function(func);
		function.name = name;
		desc->memberFuncs.push_back(function);
	}

private:
	::std::unique_ptr<TypeDescriptor> desc{ nullptr };
};
```

将`RawTypeDescriptorBuilder`设为`TypeDescriptor`，`MemberVariable`和`MemberFunction`的友元类，以便访问这些类中的私有成员：

```C++
friend class RawTypeDescriptorBuilder;
```

在构造函数中，新建一个`TypeDescriptor`实例，并设置类名字符串：

```C++
RawTypeDescriptorBuilder::RawTypeDescriptorBuilder(const ::std::string& name)
	: desc(::std::make_unique<TypeDescriptor>()) {
	desc->name = name;
}
```

在析构函数中，将`TypeDescriptor`实例添加到注册表中，同时销毁`RawTypeDescriptorBuilder`中的内容：

```C++
RawTypeDescriptorBuilder::~RawTypeDescriptorBuilder() {
	Registry::Instance().Register(::std::move(desc));
}
```

在`RawTypeDescriptorBuilder`类上再封装一层`TypeDescriptorBuilder`，采用类模板定义，代码如下：

```C++
template<class Class>
class TypeDescriptorBuilder {
public:
	explicit TypeDescriptorBuilder(const ::std::string& name) : rawBuilder(name) {}

	template<typename Var>
	TypeDescriptorBuilder& AddMemberVariable(const ::std::string& name, Var Class::* var) {
		rawBuilder.AddMemberVariable(name, var);
		return *this;
	}

	template<typename Func>
	TypeDescriptorBuilder& AddMemberFunction(const ::std::string& name, Func Class::* func) {
		rawBuilder.AddMemberFunction(name, func);
		return *this;
	}

private:
	RawTypeDescriptorBuilder rawBuilder;
};
```

这个类中的`AddMemberVariable`和`AddMemberFunction`函数都返回一个实例自身的引用，这是为了方便以这样的形式调用函数：

```C++
reflect::AddClass<Foo>("Foo")
	.AddMemberVariable("var", &Foo::var)
	.AddMemberFunction("Func", &Foo::Func);
```

用`AddClass`函数去实际上创建出一个`TypeDescriptorBuilder`实例：

```C++
template<class Class>
TypeDescriptorBuilder<Class> AddClass(const ::std::string& name) {
	return TypeDescriptorBuilder<Class>(name);
}
```

使用`Get`函数获取存储了所有反射信息的vector：

```C++
std::vector<TypeDescriptor*> Get() {
	return Registry::Instance().Get();
}
```

使用`GetByName`函数去查找一个已经添加到注册表中的类：

```C++
TypeDescriptor& GetByName(const ::std::string& name) {
	return *Registry::Instance().Find(name);
}
```

下面的代码演示了这个反射系统的使用方法：

```C++
class Foo {
public:
	void Func()const {
		std::cout << str << std::endl;
	}

	std::string str;
};

int main() {
	reflect::AddClass<Foo>("Foo")
		.AddMemberVariable("str", &Foo::str)
		.AddMemberFunction("Func", &Foo::Func);

	Foo foo;

	auto str = reflect::GetByName("Foo").GetMemberVariable("str");
	str.SetValue<::std::string>(foo, "Hello, world!");

	std::cout << str.GetValue<std::string>(foo) << std::endl;

	reflect::GetByName("Foo").GetMemberFunction("Func").Invoke(foo);
	std::cout << reflect::GetByName("Foo").GetMemberFunction("Func").IsConst() << std::endl;

	return 0;
}
```

## 代码渲染

我们构建的运行时反射工具需要手动用`AddClass`去添加反射信息，小项目还好，假如是在一个庞大的工程当中，每次都要手动添加信息就太过繁琐了，因此我们可以考虑设计一个自动解析源代码并生成反射代码的系统，这套自动生成代码的系统就称作**代码渲染（Code rendering）**。因为Clang可以参考的资料相对较多，所以在这里我们选择Clang去做这个工作。

### Clang AST

Clang是一个开源的C++编译前端，作为LLVM的一部分，它提供了一些接口能够帮助我们解析C++代码。安装完LLVM开发环境后，在Shell中输入以下命令行代码以dump出source.hpp的AST：

```
clang -Xclang -ast-dump -fsyntax-only source.hpp
```

AST（Abstract syntax tree，抽象语法树）是源代码的抽象语法结构的树状表示，树上的每个节点都表示源代码中的一种结构，不同的编译器都有各自的AST实现方式，Clang的AST结构大概长这样：

![Clang AST 结构](/images/articles/cpp_reflection/image_0.png)

简单介绍一下AST常用节点类型的意义：

| 节点类型                | 意义                                                                        |
|-------------------------|-----------------------------------------------------------------------------|
| TranslationUnitDecl     | Clang AST的顶层节点，遍历AST实际上就是对TranslationUnitDecl的子节点进行遍历 |
| CompoundStmt            | 代码块，函数实现、struct、enum、for的body一般会用它包起来                   |
| DeclStmt                | 定义语句，VarDecl等类型的定义一般会用它包起来                               |
| VarDecl                 | 变量定义语句                                                                |
| MethodDecl              | 函数定义语句                                                                |
| FieldDecl               | 成员变量定义语句                                                            |
| IfStmt                  | if语句，包括Cond、TrueBody、FalseBody三部分。                               |
| ForStmt                 | for语句                                                                     |
| UnaryOperator           | 一元操作符                                                                  |
| BinaryOperator          | 二元操作符，包括=、>、<、<=、>=、==等各种二元操作                           |
| ImplicitCastExpr        | 隐式转换表达式                                                              |
| CallExpr                | 函数调用表达式                                                              |
| ReturnStmt              | 函数返回语句                                                                |
| ParenExpr               | 括号表达式                                                                  |
| TypedefDecl             | 类型转换语句，如遇指针类型会内建PointerType和BuiltinType实现转换            |
| RecordDecl              | class或struct的定义，使用InitExpr或InitListExpr初始化成员                   |
| AccessSpecDecl          | 类的public、private、protected访问权限                                      |
| Constructor、Destructor | 类的构造与析构函数                                                          |
| Literal                 | 不同类型的字面量，包含IntegerLiteral和FloatingLiteral等                     |

### LibClang解析工具

LibClang库使我们能在C++程序中使用Clang的功能，只需`#include "clang-c\Index.h"`，并且链接相关的lib和dll。

从以下代码开始我们的解析工作：

```C++
std::vector<const char*> arguments = {
	"c++",
	"-std=c++17"
	"-D __clang__",
	"-D __META_PARSER__"
};

auto index = clang_createIndex(0, 0);
auto translator = clang_parseTranslationUnit(
	index, "source.hpp", arguments.data(), (int)arguments.size(), nullptr, 0, CXTranslationUnit_None);
if (!translator) {
	throw std::runtime_error("Failed to parse translation unit.");
}

//TODO

clang_disposeTranslationUnit(translator);
clang_disposeIndex(index);
```

在调用`clang_parseTranslationUnit`时，可以传入`command_line_args`命令行参数，这里我们主要用它来定义编译器宏，比如这里的`__META_PARSER__`宏就告诉程序此时我们是在进行解析工作。

在`clang_parseTranslationUnit`成功完成后，我们将得到source.hpp解析出的AST，之后的工作就是遍历和检查AST。

Cursors对象是指向AST的指针，通过以下方法获取翻译单元的Cursor：

```C++
auto rootCursor = clang_getTranslationUnitCursor(translator);
```

重载<<运算符用于将parse出的`CXString`信息打印出来：

```C++
std::string GetClangString(const CXString& str) {
	auto c_str = clang_getCString(str);
	clang_disposeString(str);
	return c_str;
}

std::ostream& operator<<(std::ostream& stream, const CXString& str) {
	auto c_str = GetClangString(str);
	stream << c_str;
	return stream;
}
```

通过遍历Cursor的子节点将Cursor指向的信息和节点的类型打印出来：

```C++
auto childVisitor = [](CXCursor cursor, CXCursor parent, CXClientData data) {
	std::cout << "Kind: " << std::setw(20) << clang_getCursorKindSpelling(clang_getCursorKind(cursor)) << "\t"
		<< "Cursor: " << std::setw(20) << clang_getCursorSpelling(cursor) << std::endl;
	return CXChildVisit_Recurse;
};

clang_visitChildren(rootCursor, childVisitor, nullptr);
```

解析的source.hpp的代码如下：

```C++
//source.hpp

class MyClass {
public:
	void Func() {
		int a = 1;
	}

	int field{ 0 };
};
```

运行解析程序，可以看到控制台中已经能打印出AST信息了：

```
Kind:            ClassDecl      Cursor:              MyClass
Kind:   CXXAccessSpecifier      Cursor:
Kind:            CXXMethod      Cursor:                 Func
Kind:         CompoundStmt      Cursor:
Kind:             DeclStmt      Cursor:
Kind:              VarDecl      Cursor:                    a
Kind:       IntegerLiteral      Cursor:
Kind:            FieldDecl      Cursor:                field
Kind:         InitListExpr      Cursor:
Kind:       IntegerLiteral      Cursor:
```

现在我们来考虑以下问题：AST所包含的信息是很多的，我们只需要获得反射要用到的信息就够了，具体的实现方法就是打上Clang的编译器标记：

```C++
__attribute__((annotate("reflect-infomation")))
```

修改source.hpp的代码如下：

```C++
#ifdef __META_PARSER__
#define META __attribute__((annotate("reflect-class")))
#define PROPERTY() __attribute__((annotate("reflect-property")))
#define FUNCTION() __attribute__((annotate("reflect-function")))
#else 
#define META
#define PROPERTY()
#define FUNCTION()
#endif

class META MyClass {
public:
	FUNCTION()
	void Func() {
		int a = 1;
	}

	PROPERTY()
	int field{ 0 };
};
```

这样我们就成功在`MyClass`，`Func`和`field`处打入了三个标记，再次运行解析程序，可以发现我们输入的annotate信息已经出现在了Cursor处。

在Shell中对修改后的source.hpp进行dump，AST结构看起来是这样的：

![](/images/articles/cpp_reflection/image_1.png)

我们也可以用`__VA_ARGS__`可变参数宏来传入一些额外的信息：

```C++
#define PROPERTY(...) __attribute__((annotate("reflect-property;" #__VA_ARGS__)))
```

接下来要做的就是通过标记找到有用的信息：

```C++
auto childVisitor = [](CXCursor cursor, CXCursor parent, CXClientData data) {
	auto cursors = reinterpret_cast<std::vector<CXCursor>*>(data);

	if (clang_getCursorKind(cursor) == CXCursor_AnnotateAttr) {
		if (GetClangString(clang_getCursorSpelling(cursor)) == "reflect-class") {
			cursors->push_back(parent);
		}
	}

	return CXChildVisit_Recurse;
};

std::vector<CXCursor> metaCursors;
clang_visitChildren(rootCursor, childVisitor, reinterpret_cast<CXClientData>(&metaCursors));
```

找到类型为`CXCursor_AnnotateAttr`的Cursor，访问父节点`parent`找到我们需要的Cursor，通过传入一个`CXClientData`指针可以把我们要用的Cursor节点取出。

### 生成代码

用`MetaData`来盛装需要的信息：

```C++
struct MetaData {
	std::string key;
	std::string value;
};

std::unordered_map<std::string, std::vector<MetaData>> metaData;

for (auto& cursor : metaCursors) {
	auto visitor = [](CXCursor cursor, CXCursor parent, CXClientData data) {
		auto rawData = reinterpret_cast<std::vector<MetaData>*>(data);

		if (clang_getCursorKind(cursor) == CXCursor_AnnotateAttr) {
			MetaData meta;
			
			if (clang_getCursorKind(parent) == CXCursor_FieldDecl)
				meta.key = "field";
			else if (clang_getCursorKind(parent) == CXCursor_CXXMethod)
				meta.key = "method";
			else
				return CXChildVisit_Recurse;

			meta.value = GetClangString(clang_getCursorSpelling(parent));
			
			rawData->push_back(meta);
		}

		return CXChildVisit_Recurse;
	};

	std::vector<MetaData> data;
	clang_visitChildren(cursor, visitor, reinterpret_cast<CXClientData>(&data));

	metaData[GetClangString(clang_getCursorSpelling(cursor))] = data;
}
```

以source.hpp为例，我们生成一个source.generated.hpp，向里面写入注册反射的代码：

```C++
#include "reflection.hpp"
#include "source.hpp"

class MyClass_Ref {
public:
	MyClass_Ref() {
		reflect::AddClass<MyClass>("MyClass")
			.AddMemberVariable("field", &MyClass::field)
			.AddMemberFunction("Func", &MyClass::Func);
	}
};
```

自动生成以上代码的方法如下：

```C++
const char* header = {"\
#include \"reflection.hpp\"\n\
#include \"source.hpp\"\n\
\n\
"};

MetaCompiler compiler("../source/source.hpp");
auto metaData = compiler.Get();

std::string output(header);

for (auto& [key, value] : metaData) {
	output += "class " + key + "_Ref {\n";
	output += "public:\n";
	output += "\t" + key + "_Ref() {\n";
	output += "\t\treflect::AddClass<" + key + ">(\"" + key + "\")";

	for (auto& member : value) {
		output += "\n\t\t\t.AddMember";

		if (member.key == "field")
			output += "Variable";
		else if (member.key == "method")
			output += "Function";

		output += "(\"" + member.value + "\", &" + key + "::" + member.value + ")";
	}

	output += ";\n\t}\n};\n\n";
}

std::ofstream file("../source/source.generated.hpp", std::ios::out | std::ios::trunc);
file << output;
file.close();
```

## 序列化

**序列化（Serialization）** 是将对象的状态信息转换为可以存储或传输的形式的过程，通常我们会将实例数据以可被读取的字节数组存入静态数据文件中，一个常规的选择就是JSON。

基于JSON的C++序列化/反序列化已经有很多现成的库，我们不必重复造轮子。此处我选择的是 <https://github.com/nlohmann/json> ，一个基于C++11的轻量级JSON读写库，是纯头文件的形式，使用只需`#include<nlohmann/json.hpp>`，非常方便。

下面介绍一下这个库的基本语法：

该库中的JSON对象以`nlohmann::json`类型存储。

用`fstream`从文件中读入JSON数据：

```C++
nlohmann::json metadata;

std::ifstream in("metadata.json");
in >> metadata;
in.close();
```

用`fstream`向文件中写入JSON数据：

```C++
std::ofstream out("metadata.json");
out << std::setw(4) << metadata;
out.close();
```

读出JSON中的键值对：

```C++
//写法一
auto str = metadata["str"].get<std::string>();

//写法二
std::string str;
metadata["str"].get_to(str);
```

该库提供了类似STL容器和迭代器的语法：

```C++
//JSON数组
metadata["array"] = { "meta_0", "meta_1" };
metadata["array"].push_back("meta_2");
metadata["array"].emplace_back("meta_3");
metadata["array"].erase("meta_3");

//JSON对象
if (metadata["object"].find("data") != metadata.end()) {
	metadata["object"]["data"].get_to(data);
}

//遍历
for (auto& data : metadata) {
	std::cout << data << std::endl;
}

//C++17
for (auto [key, value] : metadata.items()) {
	std::cout << key << std::endl;
	std::cout << value << std::endl;
}
```

考虑我们要序列化的类结构，可以写出以下JSON结构：

```JSON
{
    "MyClass": {
        "obj1": {
            "fields": {
                "value": 0.25,
                "str": "Hello, world!"
            }
        },

        "obj2": {
            "fields": {
                "value": 3.0,
                "str": "Another object!"
            }
        }
    }
}
```

构建一个序列化`Serializer`工具类，该类的基本结构如下：

```C++
class Serializer {
public:
	static void Read(const std::string& filePath, nlohmann::json& metadata) {
		std::ifstream in(filePath);
		in >> metadata;
		in.close();
	}

	static void Write(const std::string& filePath, const nlohmann::json& metadata) {
		std::ofstream out(filePath);
		out << std::setw(4) << metadata;
		out.close();
	}

	template<class T>
	static void Serialize(const T& obj, nlohmann::json& metadata) {}

	template<class T>
	static void Deserialize(T& obj, const nlohmann::json& metadata) {}
};
```

其中`Serialize`和`Deserialize`是留空的模板函数，对于不同类的序列化和反序列化方法，我们可以为其进行对应的模板特化：

```C++
template<>
void Serializer::Serialize(const MyClass& obj, nlohmann::json& metadata) {
	metadata.at("fields")["value"] = obj.value;
	metadata.at("fields")["str"] = obj.str;
}

template<>
void Serializer::Deserialize(MyClass& obj, const nlohmann::json& metadata) {
	metadata.at("fields").at("value").get_to(obj.value);
	metadata.at("fields").at("str").get_to(obj.str);
}
```

经过特化后就可以直接使用了：

```C++
nlohmann::json metadata;
Serializer::Read("metadata.json", metadata);

MyClass obj1;
Serializer::Deserialize(obj1, metadata["MyClass"]["obj1"]);

MyClass obj2;
Serializer::Deserialize(obj2, metadata["MyClass"]["obj2"]);
```

如果觉得为每一个类都进行对应的模板特化太过繁琐，也可以考虑将其纳入自动生成的范畴，和上面自动生成反射代码类似，写起来也并不难，这里不再过多赘述。

以上，做好了反射和序列化的工作后，我们对C++的掌控就更加全面了。