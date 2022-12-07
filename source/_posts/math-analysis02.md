---
title: 数学分析初步（二）：导数与微分
date: 2022-11-12 10:00:00
tags:
	- 大学数学
	- 微积分
categories: 数学分析
top_img: /images/articles/cover_5.png
cover: /images/articles/cover_5.png
katex: true
description: 在本文中，我们研究导数和微分及其应用：微分中值定理，洛必达法则，泰勒公式，最后可以运用这些知识进行函数图像分析。
---

## 导数

导数的定义： $y=f(x)$ 在 $x_0$ 的邻域内有定义，则

$$f'(x)=\lim_{\Delta x\rightarrow 0}\frac{\Delta y}{\Delta x}=\lim_{\Delta x\rightarrow 0}\frac{f(x_0+\Delta x)-f(x_0)}{\Delta x}$$

若 $\lim\limits_{\Delta x\rightarrow 0}\frac{f(x_0+\Delta x)-f(x_0)}{\Delta x}$ 不存在，则导数不存在。

令 $\varepsilon=\frac{\Delta y}{\Delta x}-f'(x_0)$ ，
由于 $\lim\limits_{\Delta x\rightarrow 0}(\frac{\Delta y}{\Delta x}-f'(x_0))=0$ ，所以 $\varepsilon$ 在 $x\rightarrow 0$ 时是无穷小量；
又因为 $\lim\limits_{\Delta x\rightarrow 0}\frac{\varepsilon\Delta x}{\Delta x}=0$ ，所以有 $\Delta x$ 的高阶无穷小 $o(\Delta x)=\varepsilon\Delta x$ ，满足下式：

$$\Delta y=f'(x_0)\Delta x+o(\Delta x)$$

这个式子就被称为**有限增量公式**。

可导是连续的**充分不必要条件**，可导必然连续，连续不一定可导。

> 用 $f(x)\in C^n[a,b]$ 表示 $f(x)$ 在 $[a,b]$ 上 $n$ 阶连续可导。

**左导数和右导数：**

$f(x)$ 在 $[x_0,x_0+\delta)$ 上有定义，左导数为 $f'_-(x_0)=\lim\limits_{\Delta x\rightarrow 0^-}\frac{\Delta y}{\Delta x}=\lim\limits_{\Delta x\rightarrow 0^-}\frac{f(x_0+\Delta x)-f(x_0)}{\Delta x}$ 。

$f(x)$ 在 $[x_0,x_0+\delta)$ 上有定义，右导数为 $f'_+(x_0)=\lim\limits_{\Delta x\rightarrow 0^+}\frac{\Delta y}{\Delta x}=\lim\limits_{\Delta x\rightarrow 0^+}\frac{f(x_0+\Delta x)-f(x_0)}{\Delta x}$ 。

$$在 x_0 处左右导数存在且相等 \Leftrightarrow f'(x_0) 存在$$

**导数的莱布尼茨表示法：**

$$f'(x_0)=y'|_{x=x_0}=\frac{\text{d}y}{\text{d}x}\bigg|_{x=x_0}$$

$$f^{(n)}(x)=\frac{\text{d}^ny}{\text{d}x^n}$$

**导数的几何含义：**

函数上一点的切线： $y-y_0=f'(x_0)(x-x_0)$

函数上一点的法线： $y-y_0=-\frac{1}{f'(x_0)}(x-x_0)$

### 基本求导法则

四则运算：

1. $(u\pm v)'=u'\pm v'$
2. $(ku)'=ku'$
3. $(uv)'=u'v+uv'$
$(uvw)'=u'vw+uv'w+uvw'$
$(\frac{u}{v})'=\frac{u'v-v'u}{v^2}$

初等函数求导：

1. $(k)'=0$
2. $(x^\alpha)'=\alpha x^{\alpha-1}$
$(\sqrt{x})'=\frac{1}{2}\frac{1}{\sqrt{x}}$
$(\frac{1}{x})'=-\frac{1}{x^2}$
3. $(\sin x)'=\cos x$
$(\cos x)'=-\sin x$
$(\tan x)'=\sec^2x$
$(\cot x)'=-\csc^2x$
$(\sec x)'=\sec x\tan x$
$(\csc x)'=-\csc x\cot x$
4. $(\arcsin x)'=\frac{1}{\sqrt{1-x^2}}$
$(\arccos x)'=-\frac{1}{\sqrt{1-x^2}}$
$(\arctan x)'=\frac{1}{1+x^2}$
$(\text{arccot}x)'=-\frac{1}{1+x^2}$
5. $(e^x)'=e^x$
$(a^x)'=a^x\ln a$
6. $(\ln|x|)'=\frac{1}{x}$
$(\log_a|x|)'=\frac{1}{x\ln a}$

高阶导数 莱布尼茨公式（Leibniz formula）：

$$(uv)^{(n)}=\sum_{k=0}^nC_n^ku^{(n-k)}v^{(k)}$$

其中， $C_n^k=\frac{n!}{k!(n-k)!}$ 为组合数， $u^{(0)}=u$ ， $v^{(0)}=v$

### 反函数求导

$f(x)$ 的反函数为 $\varphi(x)$ ，则对反函数求导的公式为：

$$f'(x)=\frac{1}{\varphi'(y)}$$

证明：

原函数 $f'(x)=\lim\limits_{\Delta x\rightarrow 0}\frac{\Delta y}{\Delta x}$ ，导函数 $\varphi'(x)=\lim\limits_{\Delta x\rightarrow 0}\frac{\Delta x}{\Delta y}$ ，则有

$$\lim_{\Delta x\rightarrow 0}\frac{\Delta y}{\Delta x}=\lim_{\Delta x\rightarrow 0}\frac{1}{\frac{\Delta x}{\Delta y}}$$

又因为 $\varphi(y)$ 单调，所以 $\varphi'(y_0)\neq 0$

即 $\Delta y\rightarrow 0$ 时 $\Delta x\rightarrow 0$

**常用反函数求导：**

1. $(a^x)'=\frac{1}{(\log_ay)'}=y\ln a=a^x\ln a$
2. $(\arcsin x)'=\frac{1}{(\sin y)'}=\frac{1}{\cos y}=\frac{1}{\sqrt{1-\sin^2y}}=\frac{1}{\sqrt{1-x^2}}$
$(\arccos x)'=-\frac{1}{\sqrt{1-x^2}}$
3. $(\arctan x)'=\frac{1}{(\tan x)'}=\frac{1}{\sec^2y}=\frac{1}{1+\tan^2y}=\frac{1}{1+x^2}$
$(\text{arccot}x)'=-\frac{1}{1+x^2}$

### 复合函数求导

复合函数求导使用**链式法则（Chain rule）**，先对外层函数求导，再乘上对内层函数求导的结果：

$$(f(\varphi(x)))'=f'(\varphi(x))\varphi'(x)$$

链式法则的莱布尼茨表示法：

$$\frac{\text{d}y}{\text{d}x}=\frac{\text{d}y}{\text{d}u}\cdot\frac{\text{d}u}{\text{d}v}\cdots\frac{\text{d}t}{\text{d}x}$$

### 隐函数求导

1. 对方程两边关于 $x$ 求导，得到一个关于 $y'$ 的方程。
2. 在求导后的方程中求解 $y'$ 既可。

$$\frac{\text{d}}{\text{d}x}(F(x,y(x)))=0$$

**对数求导法：** （常使用在多个函数连乘或连除）

$$\begin{aligned}y=&u^v\\
\ln y=&v\ln u\\
\frac{1}{y}y'=&v'\ln u+\frac{u'v}{u}\\
y'=&u^v\ln u\cdot v'+vu^{v-1}\cdot u'\end{aligned}$$

### 参变量函数求导

$$y=f(x)\qquad\left\{\begin{aligned}&x=\varphi(t)\\&y=\psi(t)\end{aligned}\right.$$

$$\lim_{\Delta x\rightarrow 0}\frac{\Delta y}{\Delta x}=\lim_{\Delta t\rightarrow 0}\frac{\psi(t_0+\Delta t)-\psi(t_0)}{\varphi(t_0+\Delta t)-\varphi(t_0)}=\lim_{\Delta t\rightarrow 0}\frac{\frac{\psi(t_0+\Delta t)-\psi(t_0)}{\Delta t}}{\frac{\varphi(t_0+\Delta t)-\varphi(t_0)}{\Delta t}}=\frac{\psi'(t_0)}{\varphi'(t_0)}$$

莱布尼茨表示法：

$$\frac{\text{d}y}{\text{d}x}=\frac{\frac{\text{d}y}{\text{d}t}}{\frac{\text{d}x}{\text{d}t}}$$

高阶导数：

$$\frac{\text{d}}{\text{d}x}(\frac{\text{d}y}{\text{d}x})=\frac{\text{d}(\frac{\text{d}y}{\text{d}t})/\text{d}t}{\frac{\text{d}x}{\text{d}t}}$$

## 微分

微分表示函数在一段极小区间 $\Delta x\ (\Delta x\rightarrow 0)$ 时的增加量，此时 $\Delta x$ 可以记为 $\text{d}x$ ，微分的定义为：

$$\text{d}y=f'(x)\text{d}x$$

所以由有限增量公式可知， $\Delta y$ 和 $\text{d}y$ 之间的关系是： $\Delta y=\text{d}y+o(\Delta x)$

函数可微与函数可导等价，且求微分与求导的法则大致等价：

1. $\text{d}(u\pm v)=\text{d}u\pm\text{d}v$
2. $\text{d}(ku)=k\text{d}u$
3. $\text{d}(uv)=v\text{d}u+u\text{d}v$
4. $\text{d}(\frac{u}{v})=\frac{v\text{d}u-u\text{d}v}{v^2}$
5. $\text{d}((f\circ g)(x))=f'(u)g'(x)\text{d}x=f'(u)\text{d}u$ （一阶微分的形式不变性）

**高阶微分：**

$$\text{d}^ny=f^{(n)}(x)\text{d}x^n$$

> 容易出错的概念： $\text{d}x^2=(\text{d}x)^2\qquad\text{d}^2x=0\qquad\text{d}(x^2)=2x\text{d}x$

复合函数二阶微分：

$$\begin{aligned}\text{d}^2y=(f(\varphi(t)))''\text{d}t^2=&(f'(\varphi(t))\varphi'(t))'\text{d}t^2\\
=&(f''(\varphi(t))\varphi'(t)\varphi'(t)+f'(\varphi(t))\varphi''(t))\text{d}t^2\\
=&f''(x)\text{d}x^2+f'(x)\text{d}^2x\end{aligned}$$

利用微分进行近似计算：

由 $f(x_0+\Delta x)-f(x_0)=f'(x_0)\Delta x+o(\Delta x)\approx f'(x_0)\Delta x$

可得近似计算式： $f(x_0+\Delta x)\approx f(x_0)+f'(x_0)\Delta x$

误差估计：

测量误差限 $|\Delta x|=|x-x_0|\leq \delta_x$

$$|\Delta y|=|f(x)-f(x_0)|\approx |f'(x_0)\Delta x|\leq|f'(x_0)|\delta_x$$

绝对误差限 $\delta_y=|f'(x_0)|\delta_x$

相对误差限 $\frac{\delta_y}{|y_0|}=|\frac{f'(x_0)}{f(x_0)}|\delta_x$

## 微分中值定理

**费马引理（Fermat’s theorem）：**

费马引理揭示了函数的导数与极值点的关系，是微分中值定理重要的理论基础：

设 $f(x)$ 在 $\xi$ 处极大，所以不论 $\Delta x$ 是正负，总有 $f(\xi+\Delta x)-f(xi)\leq 0$

令 $\Delta x>0$ ，则 $\frac{f(\xi+\Delta x)-f(\xi)}{\Delta x}\leq 0$ ，故由极限的保号性可以得：

$$f'_+(\xi)=\lim_{\Delta x\rightarrow 0^+}\frac{f(\xi+\Delta x)-f(\xi)}{\Delta x}\leq 0$$

令 $\Delta x<0$ ，则 $\frac{f(\xi+\Delta x)-f(\xi)}{\Delta x}\geq 0$ ，同理可得：

$$f'_-(\xi)=\lim_{\Delta x\rightarrow 0^+}\frac{f(\xi+\Delta x)-f(\xi)}{\Delta x}\geq 0$$

当 $f'(\xi)$ 存在时，左导数等于右导数，所以 $f'_+(\xi)=f'_-(\xi)=0$ ，则必有 $f'(\xi)=0$ 。

### 罗尔定理（Rolle’s theorem）

若 $f$ 满足以下条件：

1. $f$ 在 $[a,b]$ 上连续
2. $f$ 在 $(a,b)$ 上可导
3. $f(a)=f(b)$

则必然 $\exists\xi\in(a,b)$ ，使得 $f'(\xi)=0$

**证明：**

令函数在 $(a,b)$ 上最大值为 $M$ ，最小值为 $m$ ，则

1. 若 $M=m$ ，则 $f(x)$ 在 $[a,b]$ 上必为常数，结论成立。
2. 若 $M>N$ ，则由于 $f(a)=f(b)$ ， $M$ 和 $m$ 必然有一个在 $(a,b)$ 某点 $\xi$ 处取得，即 $\xi$ 是极值点，又因为 $f(x)$ 在该点可导，由费马引理可以推得 $f'(\xi)=0$ 。

### 拉格朗日中值定理（Lagrange mean value theorem）

若 $f$ 满足以下条件：

1. $f$ 在 $[a,b]$ 上连续
2. $f$ 在 $(a,b)$ 上可导

则必然 $\exists\xi\in(a,b)$ ，使得

$$f'(\xi)=\frac{f(b)-f(a)}{b-a}$$

**证明：**

构造函数 $g(x)=(f(a)-f(b))x-f(x)(a-b)$

$$g'(x)=f(a)-f(b)-f'(x)(a-b)\\
g(a)=g(b)=bf(a)-af(b)$$

因此，由罗尔定理得， $\exists\xi\in(a,b)$

$$f(a)-f(b)-f'(\xi)(a-b)=0$$

即

$$f'(\xi)=\frac{f(b)-f(a)}{b-a}$$

**导数极限定理：**

$f$ 在 $U(x_0)$ 连续，且在 $\mathring U(x_0)$ 可导，若 $\lim\limits_{x\rightarrow x_0}f'(x)$ 存在，则 $f$ 在 $x_0$ 处可导，且 $f'(x_0)=\lim\limits_{x\rightarrow x_0}f'(x)$ 。

**证明：**

当 $x\in\mathring U_+(x_0)$ 时， $\exists\xi\in(x_0,x)$ ，使 $f'(\xi)=\frac{f(x)-f(x_0)}{x-x_0}$ ，对两边同时取极限，可以得到：

$$\lim_{\xi\rightarrow x_0^+}f'(\xi)=\lim_{x\rightarrow x_0^+}\frac{f(x)-f(x_0)}{x-x_0}$$

等式右侧即 $f(x)$ 在 $x_0$ 处的右导数，因此上式可以写成：

$$f'_+(x_0)=\lim_{x\rightarrow x_0^+}f'(x)$$

同理，当 $x\in\mathring U_-(x_0)$ 时，可得：

$$f'_-(x_0)=\lim_{x\rightarrow x_0^-}f'(x)$$

因为 $f$ 在 $U(x_0)$ 连续，所以 $\lim\limits_{x\rightarrow x_0^+}f'(x)=\lim\limits_{x\rightarrow x_0^-}f'(x)$ 。

综上所述， $f'(x_0)=\lim\limits_{x\rightarrow x_0}f'(x)$ 。

### 达布定理（Darboux’s theorem）

达布定理又称导数介值定理：若 $f$ 在 $[a,b]$ 上可导，且 $f'_+(a)\neq f'_-(b)$ ， $k$ 介于 $f'_+(a),f'_-(b)$ 之间，则 $\exists\xi\in(a,b)$ ，使 $f'(\xi)=k$ 。

**证明：**

令 $F(x)=f(x)-kx$ ， $F(x)$ 在 $[a,b]$ 上可导，有

$$F'_+(a)\cdot F'_-(b)=(f'_+(a)-k)(f'_-(b)-k)<0$$

所以 $F'_+(a)$ 和 $F'_-(b)$ 异号

令 $F'_+(a)>0$ ， $F'_-(b)<0$ ，
则有 $x_1\in\mathring U_+(a)$ ， $x_2\in\mathring U_-(b)$ ，并且 $F(x_1)>F(a)$ ， $F(x_2)>b$ 。

所以必然有 $\xi\in(a,b)$ ，使 $F$ 在 $\xi$ 处取最大值，此时 $F'(\xi)=0$ ， $f'(\xi)=k$ 。

**推论：**

若 $f(x)$ 在 $I$ 上满足 $f'(x)\neq 0$ ，则在 $I$ 上 $f(x)$ 严格单调。

1. 若 $f'(x)>0$ ，函数严增。
2. 若 $f'(x)<0$ ，函数严减。
3. 若 $f'(a)$ 和 $f'(b)$ 异号，则 $\exists\xi\in(a,b)$ ，使 $f'(\xi)=0$ ，与 $f'(x)\neq 0$ 矛盾，该情况不存在。

### 柯西中值定理（Cauchy mean value theorem）

若 $f,g$ 满足以下条件：

1. 在 $[a,b]$ 上连续
2. 在 $(a,b)$ 上可导
3. $f'(x)$ 和 $g'(x)$ 不同时为0
4. $g(a)\neq g(b)$

则必然 $\exists\xi\in(a,b)$ ，使得

$$\frac{f'(\xi)}{g'(\xi)}=\frac{f(b)-f(a)}{g(b)-g(a)}$$

**证明：**

和证明拉格朗日中值定理类似，构造函数 $F(x)=f(x)-f(a)-\frac{f(b)-f(a)}{g(b)-g(a)}(g(x)-g(a))$

$$F'(x)=f'(x)-\frac{f(b)-f(a)}{g(b)-g(a)}g'(x)$$

$$F(a)=F(b)=0$$

因此，由罗尔定理得， $\exists\xi\in(a,b)$

$$f'(\xi)-\frac{f(b)-f(a)}{g(b)-g(a)}g'(\xi)=0$$

假设 $g'(\xi)=0$ ，则 $f'(\xi)=0$ ，与条件 $f'(x)$ 和 $g'(x)$ 不同时为0矛盾，则 $g'(\xi)\neq 0$ ，所以原式可以移项得到：

$$\frac{f'(\xi)}{g'(\xi)}=\frac{f(b)-f(a)}{g(b)-g(a)}$$

**柯西中值定理的几何意义：**

有如下曲线方程

$$\left\{\begin{aligned}x=g(t)\\y=f(t)\end{aligned}\right.$$

该曲线方程两端点构成的弦与曲线上一点的切线斜率相等。

## 洛必达法则

洛必达法则（L’Hôpital’s rule）常用于未定式求极限，所谓未定式，是指两个函数的极限都趋于0或无穷，求它们相除的极限，即 $\frac{0}{0}$ 或 $\frac{\infty}{\infty}$ 。

若 $f,g$ 满足以下条件：

1. $\lim\limits_{x\rightarrow x_0}f(x)=\lim\limits_{x\rightarrow x_0}g(x)=0$ 或 $\lim\limits_{x\rightarrow x_0}g(x)=\infty$
2. 在 $\mathring U(x_0)$ 上 $f,g$ 可导，且 $g'(x)\neq 0$
3. $\lim\limits_{x\rightarrow x_0}\frac{f'(x)}{g'(x)}=A$ ， $A$ 是实数或 $\infty$

则

$$\lim_{x\rightarrow x_0}\frac{f(x)}{g(x)}=\lim_{x\rightarrow x_0}\frac{f'(x)}{g'(x)}=A$$

**$\frac{0}{0}$ 型证明：**

补充定义 $f(x_0)=g(x_0)=0$ ，保证 $f,g$ 在 $[x_0,x]\subset[x_0,x_0+\delta)$ 上的连续性。应用柯西中值定理，得到：

$$\frac{f'(\xi)}{g'(\xi)}=\frac{f(x)-f(x_0)}{g(x)-g(x_0)}$$

两边求极限得：

$$\lim_{x\rightarrow x_0^+}\frac{f'(\xi)}{g'(\xi)}=\lim_{x\rightarrow x_0^+}\frac{f(x)-f(x_0)}{g(x)-g(x_0)}$$

因为， $x_0<\xi<x$ ，所以当 $x\rightarrow x_0$ 时， $\xi\rightarrow x_0$ ，即

$$\lim_{x\rightarrow x_0^+}\frac{f(x)}{g(x)}=\lim_{x\rightarrow x_0^+}\frac{f'(x)}{g'(x)}=A$$

**$\frac{*}{\infty}$ 型证明：**

由于无法在 $x_0$ 处补充定义，所以取子区间 $[x,a]\subset(x_0,x_0+\delta)$ ， $\xi\in[x,a]$ ，应用柯西中值定理，得到：

$$\frac{f'(\xi)}{g'(\xi)}=\frac{f(x)-f(a)}{g(x)-g(a)}$$

即

$$A-\delta<\frac{f(x)-f(a)}{g(x)-g(a)}<A+\delta$$

将等号右侧上下同除 $g(x)$ ，可以得到：

$$A-\delta<\frac{\frac{f(x)}{g(x)}-\frac{f(a)}{g(x)}}{1-\frac{g(a)}{g(x)}}<A+\delta$$

对该式求上下极限，得到：

$$A\leq\varliminf_{x\rightarrow x_0^+}\frac{f(x)}{g(x)}\leq\varlimsup_{x\rightarrow x_0^+}\frac{f(x)}{g(x)}\leq A$$

因此， $\frac{f(x)}{g(x)}$ 的极限存在，并且

$$\lim_{x\rightarrow x_0^+}\frac{f(x)}{g(x)}=\lim_{x\rightarrow x_0^+}\frac{f'(x)}{g'(x)}=A$$

**其它未定式类型：**

四则型未定式：

1. $\infty-\infty=\frac{1}{0}-\frac{1}{0}=\frac{0-0}{0\cdot 0}=\frac{0}{0}$
2. $0\cdot\infty=0\cdot\frac{1}{0}=\frac{0}{0}$

指数型未定式：

3. $0^0=e^{\ln 0^0}=e^{0\cdot\ln 0}=e^{0\cdot\infty}$
4. $1^\infty=e^{\ln 1^\infty}=e^{\infty\cdot\ln 1}=e^{\infty\cdot 0}$
5. $\infty^0=e^{\ln\infty^0}=e^{0\cdot\ln\infty}=e^{0\cdot\infty}$

## 泰勒公式

令 $f(x)$ 在 $x=x_0$ 处可导，由有限增量公式可以得到：

$$f(x)=f(x_0)+f'(x_0)(x-x_0)+o(x-x_0)$$

当 $|x-x_0|$ 充分小时， $f(x)$ 可以用一次多项式 $f(x_0)+f'(x_0)(x-x_0)$ 来近似代替。

为了降低误差至 $o((x-x_0)^n)$ 的程度，我们需要用更高阶的多项式来逼近 $f$ ，其中 $o((x-x_0)^n)$ 被称作**皮亚诺型余项（Peano remainder）**，这种逼近的方法就被称为**泰勒展开公式（Taylor’s formula）**：

$$f(x)=f(x_0)+\frac{f'(x_0)}{1!}(x-x_0)+\cdots +\frac{f^{(n)}(x_0)}{n!}(x-x_0)^n+o((x-x_0)^n)$$

**证明：**

假设当 $f(x)$ 在点 $x_0$ 有 $n$ 阶导数时，存在一个 $n$ 次多项式 $P_n(x)$ ，使得 $f(x)-P_n(x)=o((x-x_0)^n)$ ，此时 $\lim_{x\rightarrow x_0}\frac{f(x)-P_n(x)}{(x-x_0)^n}=0$

设 $P_n(x)=a_0+a_1(x-x_0)+\cdots +a_n(x-x_0)^n$

则 $P_n(x_0)=a_0,P_n'(x_0)=a_1,P_n''(x_0)=2!a_2,\cdots ,P_n^{(n)}(x_0)=n!a_n$

即 $a_0=P_n(x_0),a_1=\frac{P_n'(x_0)}{1!},a_2=\frac{P_n''(x_0)}{2!},\cdots ,a_n=\frac{P_n^{(n)}(x_0)}{n!}$

上式表明 $P_n(x)$ 的各项系数是由其在点 $x_0$ 的各阶导数所确定的。由此可得：

$$f^{(k)}(x_0)=P_n^{(k)}(x_0),\quad k=0,1,2,\cdots ,n$$

其中 $k=0$ 表示不求导。

最终得到 $f(x)$ 在 $x_0$ 处的 $n$ 阶泰勒多项式（Taylor polynomial）：

$$T_n(x)=f(x_0)+\frac{f'(x_0)}{1!}(x-x_0)+\cdots +\frac{f^{(n)}(x_0)}{n!}(x-x_0)^n$$

其中 $\frac{f^{(k)}(x_0)}{k!}\ (k=0,1,\cdots ,n)$ 被称为泰勒系数。

$$f(x)=T_n(x)+o((x-x_0)^n)$$

### 麦克劳林展开

当取 $x_0=0$ 时，这个泰勒公式的特殊形式就被称为麦克劳林展开公式（Maclaurin’s series）：

$$f(x)=f(0)+\frac{f'(0)}{1!}x+\cdots +\frac{f^{(n)}(0)}{n!}x^n+o(x^n)$$

常用麦克劳林展开：

1. $e^x=1+\frac{x}{1!}+\frac{x^2}{2!}+\cdots +\frac{x^n}{n!}+o(x^n)$
2. $\sin x=x-\frac{x^3}{3!}+\cdots +(-1)^{m-1}\frac{x^{2m-1}}{(2m-1)!}+o(x^{2m})$
3. $\cos x=1-\frac{x^2}{2!}+\cdots +(-1)^{m}\frac{x^{2m}}{(2m)!}+o(x^{2m+1})$
4. $\ln(1+x)=x-\frac{x^2}{2}+\frac{x^3}{3}+\cdots +(-1)^{n-1}\frac{x^n}{n}+o(x^n)$
5. $(1+x)^\alpha=1+\alpha x+\frac{\alpha(\alpha-1)}{2!}x^2+\cdots +\frac{\alpha(\alpha-1)\cdots (\alpha-n+1)}{n!}x^n+o(x^n)$
6. $\frac{1}{1-x}=1+x+x^2+\cdots +x^n+o(x^n)$

### 拉格朗日型余项

之前我们使用的都是皮亚诺型余项 $o((x-x_0)^n)$ ，在 $x\rightarrow x_0$ 时成立，除此以外，还有**拉格朗日型余项（Lagrange remainder）**，并在任何情况下都成立：

$$f(x)=T_n(x)+\frac{f^{n+1}(\xi)}{(n+1)!}(x-x_0)^{n+1}\quad(\xi在x_0和x间)$$

令 $x_0=0$ ， $\xi=\theta x(0<\theta<1)$ ，可以将拉格朗日型余项改写为 $\frac{f^{n+1}(\theta x)}{(n+1)!}x^{n+1}$ ，该形式广泛用于泰勒公式近似计算的误差估计中。

**证明：**

令 $F(t)=f(x)-T_n(x,t)=f(x)-[f(t)+f'(t)(x-t)+\cdots +\frac{f^{(n)}(t)}{n!}(x-t^n)]$

则 $F(x)=f(x)-f(x)=0$

并且 $F'(t)=-[f'(t)+f''(t)(x-t)-f'(t)+\frac{f'''(t)}{2!}(x-t)^2-\frac{f''(t)}{2!}\cdot 2\cdot(x-t)+\cdots +\frac{f^{(n+1)}(t)}{n!}(x-t)^n-\frac{f^{(n)}(t)}{(n-1)!}(x-t)^{n-1}]$

将导函数中的相同项消去，可以得到： $F'(t)=-\frac{f^{(n+1)}(t)}{n!}(x-t)^n$

令 $G(t)=(x-t)^{n+1}$ 并且 $G(x)=0$

则 $G'(t)=-(n+1)(x-t)^n$

有

$$\frac{F(x_0)}{G(x_0)}=\frac{f(x)-[f(x_0)+f'(x_0)(x-x_0)+\cdots +\frac{f^{(n)}(x_0)}{n!}(x-x_0^n)]}{(x-x_0)^{n+1}}$$

并且由前面所推知，可得：

$$\frac{F(x_0)}{G(x_0)}=\frac{F(x_0)-F(x)}{G(x_0)-G(x)}=\frac{F'(\xi)}{G'(\xi)}=\frac{-\frac{f^{(n+1)}(\xi)}{n!}(x-\xi)^n}{-(n+1)(x-\xi)^n}=\frac{f^{(n+1)}(\xi)}{(n+1)!}$$

综上所述，可证得：

$$f(x)-[f(x_0)+f'(x_0)(x-x_0)+\cdots +\frac{f^{(n)}(x_0)}{n!}(x-x_0^n)]=\frac{f^{(n+1)}(\xi)}{(n+1)!}(x-x_0)^{n+1}$$

即

$$f(x)=f(x_0)+f'(x_0)(x-x_0)+\cdots +\frac{f^{(n)}(x_0)}{n!}(x-x_0^n)+\frac{f^{(n+1)}(\xi)}{(n+1)!}(x-x_0)^{n+1}$$

## 函数图像分析

函数图像的分析步骤：

1. 定义域
2. 奇偶性，周期性
3. 和坐标轴的交点，不连续/不可导的点
4. 单调性，导函数，极值，最值，凹凸性，拐点
5. 渐进线

### 极值和最值

**驻点的定义：**

函数斜率为0的点被称为驻点（Stationary point），即在驻点处函数的一阶导数为0。函数的极值点必定是驻点，但反过来，函数的驻点不一定是极值点。

**极值第一充分条件：**

$f$ 在 $x_0$ 处连续，在 $\mathring U(x_0,\delta)$ 上可导。

1. $x\in(x_0-\delta,x_0)\quad f'(x_0)\leq 0;x\in(x_0,x_0+\delta)\quad f'(x)\geq 0\qquad$ 在 $x_0$ 处取极小值
2. $x\in(x_0-\delta,x_0)\quad f'(x_0)\geq 0;x\in(x_0,x_0+\delta)\quad f'(x)\leq 0\qquad$ 在 $x_0$ 处取极大值

**极值第二充分条件：**

$f$ 在 $x_0$ 处连续，在 $\mathring U(x_0,\delta)$ 上一阶可导，在 $x=x_0$ 上二阶可导，且 $f'(x_0)=0$ ， $f''(x_0)\neq 0$ 。

1. $f''(x_0)<0\qquad$ 在 $x_0$ 处取极大值
2. $f''(x_0)>0\qquad$ 在 $x_0$ 处取极小值

证明：

将 $f(x)$ 在 $x\rightarrow x_0$ 的条件下进行二阶泰勒展开，得到：

$$\begin{aligned}
f(x)=&f(x_0)+f'(x_0)(x-x_0)+\frac{f''(x_0)}{2!}(x-x_0)^2+o((x-x_0)^2)\\
=&f(x_0)+(\frac{f''(x_0)}{2}+o(1))(x-x_0)^2
\end{aligned}\\
f(x)-f(x_0)=(\frac{f''(x_0)}{2}+o(1))(x-x_0)^2$$

假如 $f''(x_0)<0$ 则 $\frac{f''(x_0)}{2}+o(1)<0$ ，又因为 $(x-x_0)^2>0$ ，所以可得 $f(x)<f(x_0)$ ，即 $f$ 在 $x_0$ 处取极大值，反之同理。

**极值第三充分条件：**

$f$ 在 $x_0$ 的某邻域内存在直到 $(n-1)$ 阶的导数，且 $f^{(n)}(x_0)$ 存在。若 $f'(x_0)=f''(x_0)=\cdots =f^{(n-1)}(x_0)=0,f^{(n)}(x_0)\neq 0$ ，则有：

1. $n$ 为偶数时，当 $f^{(n)}(x_0)>0$ 时， $x_0$ 是极小值点；当 $f^{(n)}(x_0)<0$ 时， $x_0$ 是极大值点。
2. $n$ 为奇数时， $x_0$ 不是极值点。

> 极值第三充分条件不是必要条件，并不能保证所有极值点都满足。

证明：

由泰勒公式和 $f'(x_0)=f''(x_0)=\cdots =f^{(n-1)}(x_0)=0$ 可以得到：

$$f(x)=f(x_0)+\frac{f^{(n)}(x_0)}{n!}(x-x_0)^n+o((x-x_0)^n)\\
f(x)-f(x_0)=(\frac{f^{(n)}(x_0)}{n!}+o(1))(x-x_0)^n$$

若 $n$ 为奇数，则 $x_0$ 两侧 $f(x)-f(x_0)$ 异号，无极值点。

若 $n$ 为偶数，当 $f^{(n)}(x_0)>0$ 时， $f(x)-f(x_0)>0$ ，$x=x_0$ 为极小值点，反之同理。

**求函数最值的步骤：**

1. 求出 $f(x)$ 的驻点。
2. 求出 $f'(x)$ 不存在的点。
3. 将上述得到的所有点进行比较大小。

### 凹凸性

$f(x)$ 在区间 $I$ 上连续， $\forall x_1,x_2\in I\ (x_1\neq x_2)$ 及任意实数 $\lambda\in(0,1)$ 。

1. $f[\lambda x_1+(1-\lambda)x_2]\leq\lambda f(x_1)+(1-\lambda)f(x_2)$ ，则称 $f(x)$ 是 $I$ 上的下凸函数（与上凹函数等价）。
2. $f[\lambda x_1+(1-\lambda)x_2]\geq\lambda f(x_1)+(1-\lambda)f(x_2)$ ，则称 $f(x)$ 是 $I$ 上的下凹函数（与上凸函数等价）。

将上式中的不等号改为严格不等号是严格凹（凸）函数的定义。

若 $f(x)$ 为区间 $I$ 上的可导函数，则以下三论断等价：

1. $f(x)$ 为 $I$ 上的下凸（凹）函数。
2. $f'(x)$ 为 $I$ 上的增（减）函数。
3. 对于 $I$ 上的任意两点 $x_1,x_2$ 有

$$f(x_2)\geq f(x_1)+f'(x_1)(x_2-x_1)\\
(\ f(x_2)\leq f(x_1)+f'(x_1)(x_2-x_1)\ )$$

若 $f(x)$ 二阶可导，则 $f(x)$ 在 $I$ 上是下凸（凹）函数的充要条件是 $f''(x)\geq 0$ （ $f''(x)\leq 0$ ） ）。

**詹森不等式（Jensen’s inequality）：**

$f(x)$ 在 $I$ 上是下凸函数的充要条件是：任意 $x_1,\cdots ,x_n\in I$ ， $0<\lambda_i<1\ (i=1,2,\cdots ,n)$ ， $\lambda_1+\lambda_2+\cdots +\lambda_n=1$ ，必有

$$f(\lambda_1x_1+\cdots +\lambda_nx_n)\leq\lambda_1f(x_1)+\cdots \lambda_nf(x_n)$$

特别地，取 $\lambda_i=\frac{1}{n}$ ，则有

$$f(\frac{1}{n}\sum_{i=1}^nx_i)\leq\frac{1}{n}\sum_{i=1}^nf(x_i)$$

对于下凹函数，以上不等号方向全反。

**拐点（Inflection point）：**

函数经过一个点后严格凹凸性发生改变，这个点就被称为拐点。

1. 若 $f(x)$ 在 $x_0$ 处二阶可导，则 $(x_0,f(x_0))$ 为曲线 $y=f(x)$ 的拐点的必要条件是 $f''(x_0)=0$ 。
2. 设 $f(x)$ 在 $x_0$ 处可导，在 $\mathring U(x_0)$ 上二阶可导，若 $f''(x)$ 在 $\mathring U_+(x_0),\mathring U_-(x_0)$ 上的符号相反，那么 $(x_0,f(x_0))$ 为曲线 $y=f(x)$ 的拐点。

> 由 $f''(x_0)=0$ 确定的点 $(x_0,f(x_0))$ 未必是拐点。
> 当 $f''(x_0)$ 不存在时， $(x_0,f(x_0))$ 也可能是拐点。