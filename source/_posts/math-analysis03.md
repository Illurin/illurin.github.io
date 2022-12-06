---
title: 数学分析初步（三）：积分
date: 2022-11-12 20:00:00
tags:
	- 大学数学
	- 微积分
categories: 数学分析
top_img: /images/articles/cover_5.png
cover: /images/articles/cover_5.png
katex: true
---

## 不定积分

对于任意一个由函数求导后得到的导函数，可以求出其原函数，原函数可以有无穷多个。假如 $F$ 是 $f$ 的一个原函数，那么 $F+C$ 也是 $f$ 的原函数， $C$ 被称为积分常数， $f$ 的任何两个原函数之间都相差一个常数。

> 连续函数必有原函数，如果一个函数在区间上存在间断点，则其在区间上必没有原函数。

原函数的全体被称作不定积分（Indefinite integral），它是微分的逆运算，记作：$\int f(x)\text{d}x=F(x)+C$

不定积分和微分满足以下关系：

$$\frac{\text{d}}{\text{d}x}\int f(x)\text{d}x=f(x)\\
\text{d}\int f(x)\text{d}x=f(x)\text{d}x\\
\int F'(x)\text{d}x=F(x)+C\\
\int \text{d}F(x)=F(x)+C$$

不定积分具有线性运算的性质：

$$\int(k_1f_1(x)+k_2f_2(x))\text{d}x=k_1\int f_1(x)\text{d}x+k_2\int f_2(x)\text{d}x$$

### 基本积分表

1. $\int k\text{d}x=kx+C$

指对幂形式：

2. $\int x^\alpha\text{d}x=\frac{x^{\alpha+1}}{\alpha+1}+C$
3. $\int\frac{1}{x}\text{d}x$=$\ln|x|+C$
4. $\int e^x\text{d}x=e^x+C$
5. $\int a^x\text{d}x=\frac{a^x}{\ln x}+C$
6. $\int\ln x\text{d}x=x\ln x-x+C$

三角函数形式：

7. $\int\cos ax\text{d}x=\frac{1}{a}\sin x+C$
8. $\int\sin ax\text{d}x=-\frac{1}{a}\cos x+C$
9. $\int\sec^2x=\tan x+C$
10. $\int\csc^2x\text{d}x=-\cot x+C$
11. $\int\sec x\tan x\text{d}x=\sec x+C$
12. $\int\csc x\cot x\text{d}x=-\csc x+C$

反三角函数形式：

13. $\int\frac{\text{d}x}{\sqrt{1-x^2}}=\arcsin x+C=-\arccos x+C_1$
14. $\int\frac{\text{d}x}{1+x^2}=\arctan x+C=-\text{arccot} x+C_1$

复合形式：

15. $\int\tan x\text{d}x=-\ln|\cos x|+C$
16. $\int\cot x\text{d}x=\ln|\sin x|+C$
17. $\int\sec x\text{d}x=\ln|\sec x+\tan x|+C=\frac{1}{2}\ln|\frac{1+\sin x}{1-\sin x}|+C$
18. $\int\csc x\text{d}x=\ln|\csc x-\cot x|+C=\ln|\tan\frac{x}{2}|+C$
19. $\int\frac{1}{a^2+x^2}\text{d}x=\frac{1}{a}\arctan\frac{x}{a}+C$
20. $\int\frac{1}{x^2-a^2}\text{d}x=\frac{1}{2a}\ln|\frac{x-a}{x+a}|+C$
21. $\int\frac{1}{\sqrt{a^2-x^2}}\text{d}x=\arcsin\frac{x}{a}+C$
22. $\int\frac{1}{\sqrt{x^2+a^2}}\text{d}x=\ln|x+\sqrt{x^2+a^2}|+C$
23. $\int\frac{1}{\sqrt{x^2-a^2}}\text{d}x=\ln|x+\sqrt{x^2-a^2}|+C$
24. $\int\sqrt{a^2-x^2}\text{d}x=\frac{a^2}{2}\arcsin\frac{x}{a}+\frac{1}{2}x\sqrt{a^2-x^2}+C$

**常见的原函数不是初等函数的情形：**

1. $\int e^{ax^2}\text{d}x\quad(a\neq 0)$
2. $\int\frac{\sin x}{x}\text{d}x$
3. $\int\frac{\cos x}{x}\text{d}x$
4. $\int\sin x^2\text{d}x$
5. $\int\cos x^2\text{d}x$
6. $\int\frac{x^n}{\ln x}\text{d}x\quad(n\neq-1)$
7. $\int\frac{\ln x}{x+a}\text{d}x\quad(a\neq 0)$
8. $\int(\sin x)^n\text{d}x\quad(n\notin\mathbb{Z})$
9. $\int\frac{1}{\sqrt{x^4+a}}\text{d}x\quad(a\neq 0)$
10. $\int\sqrt{1+k(\sin x)^2}\text{d}x\quad(k\neq 0,k\neq -1)$
11. $\int\frac{1}{\sqrt{1+k(\sin x)^2}}\text{d}x\quad(k\neq 0,k\neq -1)$

### 换元积分法

**第一换元积分法：**

我们由复合函数求导法则 $(f(\varphi(t)))'=f'(\varphi(t))\varphi'(t)$ 可知：

$$\int f'(\varphi(t))\varphi'(t)=f(\varphi(t))+C$$

由此得到第一换元积分法的基本公式，这个不定积分也可以记作：

$$\int f(\varphi(t))\varphi'(t)\text{d}t=\int f(\varphi(t))\text{d}\varphi(t)$$

可以看出，由 $\varphi'(t)\text{d}t$ 转化为 $\text{d}\varphi(t)$ 是一个求原函数的过程，由 $\text{d}\varphi(t)$ 转化为 $\varphi'(t)\text{d}t$ 是一个求导的过程。

常数可以在积分号和微分号中随意移动，例如：

$$a\int f(x)\text{d}x=\int af(x)\text{d}x=\int f(x)\text{d}ax$$

微分号后面随意加减常数不会对式子产生影响（因为常数项求导后消去）：

$$\int f(x)\text{d}x=\int f(x)\text{d}(x\pm a)$$

**常用的配元形式：**

1. $\int f(ax+b)\text{d}x=\frac{1}{a}\int f(ax+b)\text{d}(ax+b)$

万能凑幂法：

2. $\int f(x^n)x^{n-1}\text{d}x=\frac{1}{n}\int f(x^n)\text{d}x^n$
3. $\int f(x^n)\frac{1}{x}\text{d}x=\frac{1}{n}\int f(x^n)\frac{1}{x^n}\text{d}x^n$

含自然常数：

4. $\int f(e^x)e^x\text{d}x=\int f(e^x)\text{d}e^x$
5. $\int f(\ln x)\frac{1}{x}\text{d}x=\int f(\ln x)\text{d}\ln x$

含三角函数：

6. $\int f(\sin x)\cos x\text{d}x=\int f(\sin x)\text{d}\sin x$
7. $\int f(\cos x)\sin x\text{d}x=-\int f(\cos x)\text{d}\cos x$
8. $\int f(\tan x)\sec^2x\text{d}x=\int f(\tan x)\text{d}\tan x$

**第二换元积分法：**

第二换元积分法将非复合函数积分转化为复合函数积分的形式，公式如下：

$$\int f(x)\text{d}x=\int f(\varphi(t))\text{d}\varphi(t)=\int f(\varphi(t))\varphi'(t)\text{d}t=F(t)+C$$

完成积分后将原变量进行回代，得到：

$$F(t)+C=F(\varphi^{-1}(x))+C$$

常见类型：

1. $\int f(x,\sqrt[n]{ax+b})\text{d}x$ ，令 $t=\sqrt[n]{ax+b}$
2. $\int f(x,\sqrt[n]{\frac{ax+b}{cx+d}})\text{d}x$ ，令 $t=\sqrt[n]{\frac{ax+b}{cx+d}}$
3. $\int f(x,\sqrt{a^2-x^2})\text{d}x$ ，令 $x=a\sin t$ 或 $x=a\cos t$
4. $\int f(x,\sqrt{a^2+x^2})\text{d}x$ ，令 $x=a\tan t$ 或 $x=a\sh t$
5. $\int f(x,\sqrt{x^2-a^2})\text{d}x$ ，令 $x=a\sec t$ 或 $x=a\ch t$
6. $\int f(a^x)\text{d}x$ ，令 $t=a^x$

分母中因子次数较高时，可以尝试**倒代换**。

### 分部积分法

我们由函数乘积求导法则 $(uv)'=u'v+uv'$ 可知：

$$\int u(x)v'(x)\text{d}x+\int u'(x)v(x)\text{d}x=u(x)v(x)$$

由此得到分部积分法的基本公式：

$$\int u(x)v'(x)\text{d}x=u(x)v(x)-\int u'(x)v(x)\text{d}x$$

将 $v'(x)$ 和 $u'(x)$ 拿到微分号后面，也可以记作：

$$\int u(x)\text{d}v(x)=u(x)v(x)-\int v(x)\text{d}u(x)$$

在分部积分时选取 $u$ 和 $v$ 的原则：$v'$ 的原函数容易求， $\int v\text{d}u$ 的形式比 $\int u\text{d}v$ 更简单。

选取 $v'$ 的优先级顺序（从大到小）：

1. 指数函数
2. 三角函数
3. 幂函数
4. 对数函数
5. 反三角函数

**循环积分：**

以下演示了一个循环积分的经典例子：

$$\begin{aligned}
\int e^x\cos x\text{d}x=&\int \cos x\text{d}e^x\\
=&e^x\cos x-\int e^x\text{d}\cos x\\
=&e^x\cos x+\int\sin x\text{d}e^x\\
=&e^x\cos x+e^x\sin x-\int e^x\cos x\text{d}x\\
\end{aligned}\\
2\int e^x\cos x\text{d}x=e^x\cos x+e^x\sin x\\
\int e^x\cos x\text{d}x=\frac{1}{2}e^x(\cos x+\sin x)$$

当多次分部积分后出现重复的积分项时，就可以藉由重复项求出所要求积分的值。

## 有理函数积分

有理函数又被称作有理分式（Rational fraction），是指分子和分母都是多项式的分式，一般形式如下：

$$R(x)=\frac{P(n)}{Q(n)}=\frac{\alpha_0x^n+\alpha_1x^{n-1}+\cdots +\alpha_n}{\beta_0x^m+\beta_1x^{m-1}+\cdots +\beta_m}$$

有理分式被分为真分式和假分式两种：

真分式：分母上多项式的最高次数大于分子上多项式的最高次数，即 $m>n$ ；
假分式：分母上多项式的最高次数小于等于分子上多项式的最高次数，即 $m\leq n$ 。

所谓有理函数求积分，就是指将原来的假分式拆成真分式和多项式相加的形式，再将真分式拆成多个部分分式，以便于求解积分，有理函数的原函数都是初等函数。

### 多项式除法

多项式除法是代数中的一种算法，用一个同次或低次的多项式去除另一个多项式，是一个经常被用于因式分解的技巧，这里我们将它用于分解假分式。

多项式除法的基本思路：

1. 把被除式，除式按某个字母作降幂排列，缺项补零。
2. 将分子的第一项除以分母的最高次项，得到首商，写在横线之上。
3. 将分母乘以首商，乘积写在分子前两项之下（同类项对齐）。
4. 从分子的相应项中减去刚得到的乘积（消去相等项，把不相等的项结合起来），得到的余式写在下面。
5. 重复以上步骤，直到最后只剩常数，得出结果。

**例：** 计算 $\frac{x^3-12x^2-42}{x-3}$ 。

$$\begin{array}{ll} 
&\ x^2-9x-27\\ 
x-3  \!\!\!\!\!\!&\overline{)x^3-12x^2+0x-42} \\ 
&\underline{\ x^3-\ \ 3x^2}\\ 
&\quad\quad\ -9x^2+0x\\
&\quad\quad\ \underline{-9x^2+27x}\\
&\quad\quad\quad\quad\quad-27x^2-42\\
&\quad\quad\quad\quad\quad\underline{-27x^2+81}\\
 &\quad\quad\quad\quad\quad\quad\quad\ \ \ -123\\
\end{array}$$

综上所述：

$$\frac{x^3-12x^2-42}{x-3}=x^2-9x-27-\frac{123}{x-3}$$

### 真分式分解

当分母上的多项式形如多个一次式和二次式相乘时，可以进行真分式分解：

$$Q(x)=(a_1x-b_1)^{\lambda_1}\cdots (a_sx-b_s)^{\lambda_s}(m_1x^2+p_1x+q_1)^{u_1}\cdots (m_tx^2+p_tx+q_t)^{u_t}$$

其中对于任意二次式，满足 $\Delta=p_j^2-4q_j<0$ ，这代表它是一个无法进行因式分解的二次式（如果可以因式分解，则需要分解后充当一次式）。

**一次式分解：**

对于形如 $\frac{P(x)}{(ax+b)^k}$ 的 $k$ 重一次式，可以采用如下分解方式：
当 $k=1$ 时：

$$\frac{P(x)}{(a_1x+b_1)(a_2x+b_2)\cdots (a_nx+b_n)}=\frac{A_1}{a_1x+b_1}+\frac{A_2}{a_2x+b_2}+\cdots +\frac{A_n}{a_nx+b_n}$$

当 $k>1$ 时：

$$\frac{P(x)}{(ax+b)^k}=\frac{A_1}{ax+b}+\frac{A_2}{(ax+b)^2}+\cdots +\frac{A_k}{(ax+b)^k}$$

**二次式分解：**

对于形如 $\frac{P(x)}{(mx^2+px+q)^k}$ 的 $k$ 重二次式，可以采用如下分解方式：

当 $k=1$ 时：

$$\frac{P(x)}{(m_1x^2+p_1x+q_1)\cdots (m_nx^2+p_nx+q_n)}=\frac{A_1x+B_1}{m_1x^2+p_1x+q_1}++\cdots +\frac{A_nx+B_n}{m_nx^2+p_nx+q_n}$$

当 $k>1$ 时：

$$\frac{P(x)}{(mx^2+px+q)^k}=\frac{A_1x+B_1}{mx^2+px+q}+\frac{A_2x+B_2}{(mx^2+px+q)^2}+\cdots +\frac{A_kx+B_k}{(mx^2+px+q)^k}$$

**例：** 求 $\int\frac{x^2+1}{(x+2)(x+1)^2}\text{d}x$

首先进行真分式分解：

$$\frac{x^2+1}{(x+2)(x+1)^2}=\frac{A}{x+2}+\frac{B}{x+1}+\frac{C}{(x+1)^2}$$

将各分式通分后合并：

$$\frac{A}{x+2}+\frac{B}{x+1}+\frac{C}{(x+1)^2}=\frac{A(x+1)^2+B(x+1)(x+2)+C(x+2)}{(x+2)(x+1)^2}$$

接下来求解待定系数，主要使用以下两种方法：

**反解方程法：**

将分子与原式的分子系数作比对, 写出关于待定系数的方程, 进行求解。

$$A(x+1)^2+B(x+1)(x+2)+C(x+2)=(A+B)x^2+(2A+3B+C)x+A+2B+2C\\
(A+B)x^2+(2A+3B+C)x+A+2B+2C=x^2+1$$

$$\left\{\begin{aligned}&A+B=1\\&2A+3B+C=0\\&A+2B+2C=1\end{aligned}\right.$$

$$\left\{\begin{aligned}&A=5\\&B=-4\\&C=2\end{aligned}\right.$$

**实根代入法：**

向原式中代入 $x=-1$ ，可以消掉 $A,B$ 项，解得：

$$C=(-1)^2+1=2$$

向原式中代入 $x=-2$ ，可以消掉 $B,C$ 项，解得：

$$A(-1)^2=(-2)^2+1\\A=5$$

将 $A,C$ 的值代回原式中，求出 $B=-4$ 。

综上所述：

$$\int\frac{x^2+1}{(x+2)(x+1)^2}\text{d}x=\int\frac{5}{x+2}\text{d}x-\int\frac{4}{x+1}\text{d}x+\int\frac{2}{(x+1)^2}\text{d}x$$

### 部分分式积分

**一次式积分：**

$\int\frac{A}{x-a}\text{d}x=A\ln|x-a|+C\\
\int\frac{A}{(x-a)^k}\text{d}x=\frac{A}{1-n}(x-a)^{1-n}+C\quad(n\neq 1)$

**二次式积分：**

对于 $\int\frac{Cx+D}{(x^2+px+q)^k}\text{d}x\ (p^2-4q<0)$ ，先将二次式进行配方：

$$\begin{aligned}x^2+px+q=&x^2+2\cdot\frac{p}{2}x+\frac{p^2}{4}-\frac{p^2}{4}+q\\=&(x+\frac{p}{2})^2+q-\frac{p^2}{4}\end{aligned}$$

令 $t=x+\frac{p}{2},r^2=q-\frac{p^2}{4}$

然后对分母进行配凑：

$$\begin{aligned}Cx+D=&C(x+\frac{p}{2})-C\frac{p}{2}+D\\=&Ct-\frac{Cp}{2}+D\end{aligned}$$

因此原式可以换元成：

$$\begin{aligned}\int\frac{Cx+D}{(x^2+px+q)^k}\text{d}x=&\int\frac{Ct-\frac{Cp}{2}+D}{(t^2+r^2)^k}\text{d}x\\
=&C\int\frac{t\text{d}t}{(t^2+r^2)^k}+(D-\frac{Cp}{2})\int\frac{\text{d}t}{(t^2+r^2)^k}\end{aligned}$$

当 $k=1$ 时：

$$\int\frac{t\text{d}t}{t^2+r^2}=\frac{1}{2}\int\frac{\text{d}(t^2+r^2)}{t^2+r^2}=\frac{1}{2}\ln(t^2+r^2)+C$$

$$\int\frac{\text{d}t}{t^2+r^2}=\frac{1}{r}\int\frac{1}{(\frac{t}{r})^2+1}\text{d}(\frac{t}{r})=\frac{1}{r}\arctan\frac{t}{r}+C$$

当 $k>1$ 时：

$$\int\frac{t\text{d}t}{(t^2+r^2)^k}=\frac{1}{2}\int\frac{\text{d}(t^2+r^2)}{(t^2+r^2)^k}=\frac{1}{2}\frac{1}{1-k}(t^2+r^2)^{1-k}+C$$

$$\begin{aligned}I_k=\int\frac{\text{d}t}{(t^2+r^2)^k}=&\frac{1}{r^2}\int\frac{t^2+r^2-t^2}{(t^2+r^2)^k}\text{d}t\\
=&\frac{1}{r^2}\int\frac{\text{d}t}{(t^2+r^2)^{k-1}}-\frac{1}{r^2}\int\frac{t^2\text{d}t}{(t^2+r^2)^k}\\
=&\frac{1}{r^2}I_{k-1}-\frac{1}{1-k}\frac{1}{2}\int t\text{d}(t^2+r^2)^{1-k}\\
=&\frac{1}{r^2}I_{k-1}-\frac{1}{2r^2(k-1)}\left[\frac{t}{(t^2+r^2)^{k-1}}-I_{k-1}\right]
\end{aligned}$$

### 有理代换

对于一些非有理函数积分，我们也可以将其转换为有理函数求解，常见的有三角代换和根式代换。

**三角代换：**

设 $R(\sin x,\cos x)$ 表示三角函数有理式，要求 $\int R(\sin x,\cos x)\text{d}x$ ，则令 $t=\tan\frac{x}{2}$ ，将原积分转换为 $t$ 的有理函数的积分，这种换元方法被称为**万能代换**。

$$\sin x=\frac{2\sin\frac{x}{2}\cos\frac{x}{2}}{\sin^2\frac{x}{2}+\cos^2\frac{x}{2}}=\frac{2\tan\frac{x}{2}}{1+\tan^2\frac{x}{2}}=\frac{2t}{1+t^2}$$

$$\cos x=\frac{\cos^2\frac{x}{2}-\sin^2\frac{x}{2}}{\sin^2\frac{x}{2}+\cos^2\frac{x}{2}}=\frac{1-\tan^2\frac{x}{2}}{1+\tan^2\frac{x}{2}}=\frac{1-t^2}{1+t^2}$$

但在某些情况下，可以选择更方便的变量进行代换，例如以下三种情况：

1. 若被积函数是关于 $\sin x$ 的奇函数，即 $R(-\sin x,\cos x)=-R(\sin x,\cos x)$ ，可令 $t=\cos x$ 。
2. 若被积函数是关于 $\cos x$ 的奇函数，即 $R(\sin x,-\cos x)=-R(\sin x,\cos x)$ ，可令 $t=\sin x$ 。
3. 若被积函数同时是关于 $\sin x$ 和 $\cos x$ 的偶函数，即 $R(-\sin x,-\cos x)=R(\sin x,\cos x)$ ，可令 $t=\tan x$ 。

**根式代换：**

被积函数为简单根式的有理式，可通过根式代换转换为有理函数的积分：

1. $\int R(x,\sqrt[n]{ax+b})\text{d}x$ ，令 $t=\sqrt[n]{ax+b}$
2. $\int R(x,\sqrt[n]{\frac{ax+b}{cx+d}})\text{d}x$ ，令 $t=\sqrt[n]{\frac{ax+b}{cx+d}}$
3. $\int R(x,\sqrt[n]{ax+b},\sqrt[m]{ax+b})\text{d}x$ ，令 $t=\sqrt[p]{ax+b}$ ， $p$ 为 $m,n$ 的最小公倍数。

## 定积分

在很多数学和物理问题中，经常需要求解一种特殊和式的极限：

$$\lim_{||T||\rightarrow 0}\sum_{i=1}^nf(\xi_i)\Delta x_i$$

这就引出了**定积分（Definite integral）** 的概念。

![](/images/articles/math-analysis03/image_0.png)

求函数图像与坐标轴之间围成的图形的面积：

**1. 分割**

在区间 $[a,b]$ 中任意插入 $n-1$ 个分点：

$$a=x_0<x_1<x_2<\cdots <x_{n-1}<x_n=b$$

$$\Delta_i=[x_i,x_i],\Delta x_i=x_i-x_{i-1},i=1,2,3,\cdots ,n$$

用直线 $x=x_i$ 将曲边梯形分成 $n$ 个小曲边梯形。

这个分割记作 $T=\{x_0,x_1,\cdots ,x_n\}$ 或 $T=\{\Delta_0,\cdots ,\Delta_n\}$ 。

**2. 近似**

把小曲边梯形 $A_i$ 近似看作矩形，即任取 $\xi\in[x_{i-1},x_i]$ ，在 $[x_{i-1},x_i]$ 上把 $f(x)$ 近似看作常数 $f(\xi_i)$ ，此时 $A_i$ 的面积 $S_i$ 约为 $f(\xi_i)\Delta x_i$ ，所以：

$$S(A)=\sum_{i=1}^nS_i\approx\sum_{i=1}^nf(\xi_i)\Delta x_i$$

上述和式 $\sum_{i=1}^nf(\xi_i)\Delta x_i$ 称为积分和或黎曼和。

**3. 逼近**

近似得出的黎曼和和曲边梯形的面积 $S$ 总有差别，当分割越来越细时，黎曼和与 $S$ 的差距就会越来越小。

分割 $T$ 的细度（模）：

$$||T||=\max\{\Delta x_i|i=1,2,\cdots ,n\}$$

则当 $||T||\rightarrow 0$ 时，就能保证分割越来越细。

对于给定的 $\varepsilon>0$ ，能够找到 $\delta>0$ ，使得当
$||T||<\delta$ 时，对任意 $\xi_i\in[x_{i-1},x_i]$ ，都有：

$$|\sum_{i=1}^nf(\xi_i)\Delta x_i-S|<\varepsilon$$

**定积分的定义：**

设 $f$ 是定义在 $[a,b]$ 上的函数， $J\in R$ ，
若 $\forall\varepsilon>0$ ， $\exists\delta>0$ ，对任意分割

$$T:a=x_0<x_1<\cdots <x_{n-1}<x_n=b$$

及任意 $\xi_i\in[x_{i-1},x_i],i=1,2,\cdots ,n$ ，
当 $||T||=\max{\Delta x_i}<\delta$ 时，必有

$$|\sum_{i=1}^nf(\xi_i)\Delta x_i-J|<\varepsilon$$

则称 $f$ 在 $[a,b]$ 上可积，并称 $J$ 为 $f$ 在 $[a,b]$ 上的定积分，记作：

$$J=\int_a^bf(x)\text{d}x=\lim_{||T||\rightarrow 0}\sum_{i=1}^nf(\xi_i)\Delta x_i$$

$[a,b]$ 是积分区间， $b$ 称为积分上限， $a$ 称为积分下限， $f(x)\text{d}x$ 称为被积表达式。

定积分的值仅与被积函数和积分区间有关，而与积分量无关。

**定积分存在定理：**

1. 函数在闭区间内连续。
2. 函数在闭区间内有界，且只有有限个间断点。
3. 函数在闭区间上单调。

### 定积分的估值

设 $f(x)\in C[a,b]$ ，则 $\int_a^bf(x)\text{d}x$ 存在，根据定积分定义可得如下近似计算方法：

将 $[a,b]$ 分成 $n$ 等份， $\Delta x=\frac{b-a}{n}$ ， $x_i=a+i\cdot\Delta x\ (i=0,1,\cdots ,n)$

记 $f(x_i)=y_i$ ，有以下三种定积分估值方法：

左矩形公式：

$$\begin{aligned}\int_a^bf(x)\text{d}x\approx&y_0\Delta x+y_1\Delta x+\cdots +y_{n-1}\Delta x\\=&\frac{b-a}{n}(y_0+y_1+\cdots +y_{n-1})\end{aligned}$$

右矩形公式：

$$\begin{aligned}\int_a^bf(x)\text{d}x\approx&y_1\Delta x+y_2\Delta x+\cdots +y_n\Delta x\\=&\frac{b-a}{n}(y_1+y_2+\cdots +y_n)\end{aligned}$$

梯形公式：
$$\begin{aligned}\int_a^bf(x)\text{d}x\approx&\sum_{i=1}^{n-1}\frac{1}{2}[y_{i-1}+y_i]\Delta x\\=&\frac{b-a}{n}\left[\frac{1}{2}(y_0+y_n)+(y_1+\cdots +y_{n-1})\right]\end{aligned}$$

**沃利斯公式（Wallis formula）：**

$$\frac{\pi}{2}=\lim_{n\rightarrow\infty}\left[\frac{(2n)!!}{(2n-1)!!}\right]^2\frac{1}{2n+1}$$

其中 $n!!$ 为双阶乘，表示不超过这个正整数且与它有相同奇偶性的所有正整数乘积。
沃里斯公式通常用来简化定积分计算：

$$\int_0^{\frac{\pi}{2}}\sin^nx=\int_0^{\frac{\pi}{2}}\cos^nx=\left\{\begin{aligned}&\frac{(n-1)!!}{n!!}\cdot\frac{\pi}{2}&,n为偶数\\&\frac{(n-1)!!}{n!!}&,n为奇数\end{aligned}\right.$$

### 定积分的性质

（以下所列定积分均存在）

1. 上下限可换： $\int_a^bf(x)\text{d}x=-\int_b^af(x)\text{d}x\qquad\int_a^af(x)\text{d}x=0$

<br>

2. 常值函数积分： $\int_a^bk\text{d}x=k(b-a)$

<br>

3. 常数可分离到积分号外部： $\int_a^bkf(x)\text{d}x=k\int_a^bf(x)\text{d}x$

<br>

4. 线性运算： $\int_a^b[f(x)\pm g(x)]\text{d}x=\int_a^bf(x)\text{d}x\pm\int_a^bg(x)\text{d}x$
藉由定积分的极限定义可以证明线性运算性质：

$$\begin{aligned}左端=&\lim_{||T||\rightarrow 0}\sum_{i=1}^n[f(\xi_i)\pm g(\xi_i)]\Delta x_i\\
=&\lim_{||T||\rightarrow 0}\sum_{i=1}^nf(\xi_i)\Delta x_i\pm\lim_{||T||\rightarrow 0}\sum_{i=1}^ng(\xi_i)\Delta x_i=右端\end{aligned}$$

5. 函数 $f,g$ 在区间上可积，其乘积 $f\cdot g$ 在该区间上依旧可积。

<br>

6. 积分区间的可加性： $f$ 在 $[a,b]$ 上可积的充要条件是 $\forall c\in(a,b)$ ， $f$ 在 $[a,c]$ 和 $[c,b]$ 上都可积，此时有：

$$\int_a^bf(x)\text{d}x=\int_a^cf(x)\text{d}x+\int_c^bf(x)\text{d}x$$

7. 积分的保号性：若在 $[a,b]$ 上 $f(x)\geq 0$ ，则 $\int_a^bf(x)\text{d}x\geq 0$ 。
证明：

$$\begin{aligned}由&\sum_{i=1}^ng(\xi_i)\Delta x_i\geq 0\\
可得&\int_a^bf(x)\text{d}x=\lim_{||T||\rightarrow 0}\sum_{i=1}^ng(\xi_i)\Delta x_i\geq 0\end{aligned}$$

* 推论：若在 $[a,b]$ 上 $f(x)\leq g(x)$ ，则 $\int_a^bf(x)\text{d}x\leq\int_a^bg(x)\text{d}x$

<br>

8. 绝对值定理： $|\int_a^bf(x)\text{d}x|\leq\int_a^b|f(x)|\text{d}x\quad(a<b)$
证明：

$$\begin{aligned}由&-|f(x)|\leq f(x)\leq|f(x)|\\
可得&-\int_a^b|f(x)|\text{d}x\leq\int_a^bf(x)\text{d}x\leq\int_a^b|f(x)|\text{d}x\\
即&|\int_a^bf(x)\text{d}x|\leq\int_a^b|f(x)|\text{d}x\end{aligned}$$

9. 估值定理：设 $M=\max\limits_{[a,b]}f(x),m=\min\limits_{[a,b]}f(x)$ ，则

$$m(b-a)\leq\int_a^bf(x)\text{d}x\leq M(b-a)\quad(a<b)$$

  证明：由连续函数最值定理可以得到 $f(x)$ 必存在最大值 $M$ 和最小值 $m$ ，即 $\exists x\in[a,b]$ ，使得 $m\leq f(x)\leq M$ ，所以：

$$\int_a^bm\text{d}x\leq\int_a^bf(x)\text{d}x\leq\int_a^bM\text{d}x\\
m(b-a)\leq\int_a^bf(x)\text{d}x\leq M(b-a)$$

### 积分中值定理

**积分第一中值定理：**

若 $f(x)\in C[a,b]$ ，则存在至少一点 $\xi\in[a,b]$ ，使

$$\int_a^bf(x)\text{d}x=f(\xi)(b-a)$$

证明：

设 $f(x)$ 在 $[a,b]$ 上的最小值和最大值分别是 $m$ 和 $M$ ，则由估值定理可得：

$$m\leq\frac{1}{a-b}\int_a^bf(x)\text{d}x\leq M$$

根据闭区间上连续函数介值定理，在 $[a,b]$ 上至少存在一点 $\xi\in[a,b]$ ，使得

$$f(\xi)=\frac{1}{a-b}\int_a^bf(x)\text{d}x$$

因此

$$\int_a^bf(x)\text{d}x=f(\xi)(b-a)$$

其中 $f(\xi)$ 可以理解为 $f(x)$ 在 $[a,b]$ 上所有函数值的平均值，称作积分均值，这是有限个数的算术平均数的推广。

**推论：** 若 $f,g$ 在 $[a,b]$ 上连续，且 $g(x)$ 在 $[a,b]$ 上不变号，则 $\exists\xi\in[a,b]$ ，使

$$\int_a^bf(x)g(x)\text{d}x=f(\xi)\int_a^bg(x)\text{d}x$$

## 微积分学基本定理

### 变限积分

设 $f(x)$ 在 $[a,b]$ 上连续，并且设 $x$ 为 $[a,b]$ 上的一点，有这样的一个定积分： $\int_a^xf(t)\text{d}t$ 。

如果上限 $x$ 在区间上任意变动，则对于每一个给定的 $x$ 值，都有一个对应得定积分值，这些值在区间上定义了一个函数，称为**积分上限函数**：

$$\Phi(x)=\int_a^xf(t)\text{d}t$$

若 $f(x)\in C[a,b]$ ，则积分上限函数是 $f(x)$ 在 $[a,b]$ 上的一个原函数。

证明：$\forall x,x+h\in[a,b]$ ，则有

$$\begin{aligned}\frac{\Phi(x+h)-\Phi(x)}{h}=&\frac{1}{h}\left[\int_a^{x+h}f(t)\text{d}t-\int_a^xf(t)\text{d}t\right]\\
=&\frac{1}{h}\int_x^{x+h}f(t)\text{d}t=f(\xi)\quad(x<\xi<x+h)\end{aligned}$$

由于 $f(x)\in C[a,b]$

$$\Phi'(x)=\lim_{h\rightarrow 0}\frac{\Phi(x+h)-\Phi(x)}{h}=\lim_{h\rightarrow 0}f(\xi)=f(x)$$

该定理为通过原函数计算定积分开辟了道路。

**变限积分求导：**

1. $\displaystyle\frac{\text{d}}{\text{d}x}\int_a^xf(t)\text{d}t=f(x)$
2. $\displaystyle\frac{\text{d}}{\text{d}x}\int_x^bf(t)\text{d}t=-f(x)$
3. $\displaystyle\frac{\text{d}}{\text{d}x}\int_a^{\varphi(x)}f(t)\text{d}t=f[\varphi(x)]\varphi'(x)$
4. $\displaystyle\frac{\text{d}}{\text{d}x}\int_{\psi(x)}^{\varphi(x)}f(t)\text{d}t=\dfrac{\text{d}}{\text{d}x}\left[\int_{\psi(x)}^af(t)\text{d}t+\int_a^{\varphi(x)}f(t)\text{d}t\right]=f[\varphi(x)]\varphi'(x)-f[\psi(x)]\psi'(x)$

变限积分求导时，被积函数中若含有 $x$ ，要先将其从积分号中分离出来，再求导。

### 牛顿-莱布尼茨公式

设 $f(x)\in C[a,b]$ ，且 $F(x)$ 是 $f(x)$ 的原函数。

对于 $[a,b]$ 的任一分割 $T=\{a=x_0,x_1,\cdots ,x_n=b\}$ ，在每个小区间 $[x_{i-1},x_i]$ 上对 $F(x)$ 使用拉格朗日中值定理，则分别存在 $\eta_i\in(x_{i-1},x_i),i=1,2,\cdots ,n$ ，使得

$$\begin{aligned}F(b)-F(a)=&\sum_{i=1}^n[F(x_i)-F(x_{i-1})]\\
=&\sum_{i=1}^nF'(\eta_i)\Delta x_i\\
=&\sum_{i=1}^nf(\eta_i)\Delta x_i\end{aligned}$$

因为 $f(x)\in C[a,b]$ ，从而 $f(x)$ 在 $[a,b]$ 上一致连续，
所以 $\forall\varepsilon>0,\exists\delta>0$ ，当 $x',x''\in[a,b]$ 且 $|x'-x''|<\delta$ 时，有

$$|f(x')-f(x'')|<\frac{\varepsilon}{b-a}$$

于是，当 $\Delta x_i\leq||T||<\delta$ 时，任取 $\xi_i\in[x_{i-1},x_i]$ ，有 $|\xi_i-\eta_i|<\delta$ ，可证得：

$$\begin{aligned}&\left|\sum_{i=1}^nf(\xi_i)\Delta x_i-[F(b)-F(a)]\right|\\
=&\left|\sum_{i=1}^n[f(\xi_i)-f(\eta_i)]\Delta x_i\right|\\
\leq&\sum_{i=1}^n|f(\xi_i)-f(\eta_i)|\Delta x_i\\
<&\frac{\varepsilon}{b-a}\cdot\sum_{i=1}^n\Delta x_i=\varepsilon\end{aligned}$$

综上所述，当 $F(x)$ 是连续函数 $f(x)$ 在 $[a,b]$ 上的一个原函数时，有以下公式成立：

$$\int_a^bf(x)\text{d}x=F(x)|_a^b=F(b)-F(a)$$

这便是**牛顿-莱布尼茨公式（Newton-Leibniz formula）** 的完整形式。

### 定积分换元积分法

若 $f(x)\in C[a,b]$ ，单值函数 $x=\varphi(t)$ ，满足：

1. $\varphi(t)\in C^1[\alpha,\beta]$ 且单调
2. 在 $[\alpha,\beta]$ 上 $a\leq\varphi(t)\leq b,\varphi(\alpha)=a,\varphi(\beta)=b$ 

则

$$\int_a^bf(x)\text{d}x=\int_\alpha^\beta f[\varphi(t)]\varphi'(t)\text{d}t$$

证明：

设 $F(x)$ 是 $f(x)$ 的一个原函数，则 $F[\varphi(t)]$ 是 $f[\varphi(t)]\varphi'(t)\text{d}t$ 的原函数，因此

$$\begin{aligned}\int_a^bf(x)\text{d}x=&F(b)-F(a)=F[\varphi(\beta)]-F[\varphi(\alpha)]\\
=&\int_\alpha^\beta f[\varphi(t)]\varphi'(t)\text{d}t\end{aligned}$$

> 当区间换为 $[\beta,\alpha]$ 时，定理仍成立。
> 换元必换限，原函数中的变量不必代回。
> 令 $x=\varphi(t)$ ，换元公式反过来使用依然成立。

**偶倍奇零：**

设 $f(x)\in C[-a,a]$

1. 若 $f(x)$ 是偶函数，则 $\int_{-a}^af(x)\text{d}x=2\int_0^af(x)\text{d}x$
2. 若 $f(x)$ 是奇函数，则 $\int_{-a}^af(x)\text{d}x=0$

**周期函数积分：**

设 $f(x)\in C(\mathbb R)$ ，且有一周期为 $T$ ，则 $\forall a\in\mathbb R$ ，有

$$\int_a^{a+T}f(x)\text{d}x=\int_0^Tf(x)\text{d}x$$

### 定积分分部积分法

设 $u(x),v(x)\in C^1[a,b]$ ，则

$$\int_a^bu(x)v'(x)\text{d}x=u(x)v(x)\bigg|_a^b-\int_a^bu'(x)v(x)\text{d}x$$

证明：

由

$$[u(x)v(x)]'=u'(x)v(x)+u(x)v'(x)$$

两边积分得：

$$u(x)v(x)\bigg|_a^b=\int_a^bu'(x)v(x)\text{d}x+\int_a^bu(x)v'(x)\text{d}x$$

所以可以移项得：

$$\int_a^bu(x)v'(x)\text{d}x=u(x)v(x)\bigg|_a^b-\int_a^bu'(x)v(x)\text{d}x$$

## 曲率

### 弧微分

弧微分是用一条线段的长度来近似代表一段弧的长度，设一段弧 $MM'$ ，弧长表示为 $\overset{\LARGE\frown}{MM'}$ ，直线距离表示为 $|MM'|$ ，则弧微分的计算式如下：

$$\begin{aligned}\frac{\Delta s}{\Delta x}=&\frac{\overset{\LARGE\frown}{MM'}}{|MM'|}\cdot\frac{|MM'|}{\Delta x}\\
=&\frac{\overset{\LARGE\frown}{MM'}}{|MM'|}\cdot\frac{\sqrt{(\Delta x)^2+(\Delta y)^2}}{\Delta x}\\
=&\frac{\overset{\LARGE\frown}{MM'}}{|MM'|}\cdot\sqrt{1+(\frac{\Delta y}{\Delta x})^2}\end{aligned}$$

当 $\Delta x\rightarrow 0$ 时， $\frac{\overset{\LARGE\frown}{MM'}}{|MM'|}=1$ ，即

$$\frac{\text{d}s}{\text{d}x}=\lim_{\Delta s\rightarrow 0}\frac{\Delta s}{\Delta x}=\sqrt{1+(\frac{\text{d}y}{\text{d}x})^2}=\sqrt{1+(y')^2}$$

$$\text{d}s=\sqrt{1+(y')^2}\text{d}x$$

特别地，对参数方程有以下弧微分计算式：

$$\text{d}s=\sqrt{[x'(t)]^2+[y'(t)]^2}\text{d}t$$

对极坐标方程有以下弧微分计算式：

$$\text{d}s=\sqrt{[r(\theta)]^2+[r'(\theta)]^2}\text{d}\theta$$

### 曲率

曲率（Curvature）是用于描述曲线弯曲程度的量，我们通常使用弧微分来定义曲率，将一段弧上的弧长表示为 $\Delta s$ ，切线变化的角度表示为 $\Delta\alpha$ ，则这段弧的平均曲率的计算式为：

$$\overline{K}=|\frac{\Delta\alpha}{\Delta s}|$$

在一点处的曲率的定义为：

$$K=\lim_{\Delta s\rightarrow 0}|\frac{\Delta\alpha}{\Delta s}|=|\frac{\text{d}\alpha}{\text{d}s}|$$

对于给定曲线 $y=f(x)$ ，推导曲率的计算方式：

$$\begin{aligned}y'=&\tan\alpha\\
y''=&\sec^2\alpha\cdot\frac{\text{d}\alpha}{\text{d}x}\\
\frac{\text{d}\alpha}{\text{d}x}=&\frac{y''}{\sec^2\alpha}=\frac{y''}{1+\tan^2\alpha}=\frac{y''}{1+(y')^2}\\
\text{d}\alpha=&\frac{y''}{1+(y')^2}\text{d}x\end{aligned}$$

由前面的弧微分公式可以推得：

$$K=|\frac{\text{d}\alpha}{\text{d}s}|=\frac{|y''|}{[1+(y')^2]^{\frac{3}{2}}}$$

当 $|y'|<<1$ 时， $K\approx|y''|$

特别地，对参数方程有以下曲率计算式：

$$K=\frac{|x'(t)y''(t)-x''(t)y'(t)|}{((x'(t))^2+(y'(t))^2)^{\frac{3}{2}}}$$

对极坐标方程有以下曲率计算式：

$$K=\frac{|2(r')^2-rr''+r^2|}{(r^2+(r')^2)^{\frac{3}{2}}}$$

**曲率半径的定义：**

曲率的倒数即曲率半径（Radius of curvature）：

$$r=\frac{1}{K}$$