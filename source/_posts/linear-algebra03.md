---
title: 矩阵代数（二）：秩与线性方程组
date: 2022-12-2 8:38:00
tags:
	- 大学数学
	- 代数学
categories: 线性代数
top_img: /images/articles/cover_6.jpg
cover: /images/articles/cover_6.jpg
katex: true
description: 在本文中，我们主要研究秩的概念（矩阵的秩和向量组的秩），以及通过将线性方程组转化为矩阵的形式求解线性方程组。
---

## 秩（Rank）

### 矩阵的秩

任一矩阵可以经过初等行变换化成行阶梯形矩阵，这个行阶梯形矩阵所含非零行的行数实际上就是矩阵的秩，它是矩阵的一个数字特征，对研究矩阵的性质有着重要的作用。

如果矩阵 $\bm A$ 中有一个 $r$ 阶子式 $D_r$ 不等于零，而所有 $r+1$ 阶子式（如果存在的话）全等于零，则称数 $r$ 是矩阵 $\bm A$ 的秩，记作 $R(\bm A)$ ，规定零矩阵的秩为零。

显然，对于 $m\times n$ 矩阵 $\bm A$ ，有：

1. $R(\bm A_{m\times n})\leq\min\{m,n\}$
2. $R(\bm A^T)=R(\bm A)$

为什么行阶梯形矩阵所含非零行的行数就是矩阵的秩？这就要涉及到矩阵的秩的另外一个性质：

* 设矩阵 $\bm A$ 经过有限次初等变换化为矩阵 $\bm B$ ，则 $R(\bm A)=R(\bm B)$ 。

上面这个定理也可以理解为等价矩阵具有相同的秩：设 $\bm A$ 为 $m\times n$ 矩阵， $\bm P$ 是 $m$ 阶可逆矩阵， $\bm Q$ 是 $n$ 阶可逆矩阵，则 $R(\bm A)=R(\bm P\bm A)=R(\bm A\bm Q)=R(\bm P\bm A\bm Q)$

**两个重要结论**（在后文证明）：

* $R(\bm A\bm B)\leq\min\{R(\bm A),R(\bm B)\}$
* $R(\bm A+\bm B)\leq R(\bm A)+R(\bm B)$

当矩阵的秩和行数相等时，称作**行满秩矩阵**；当矩阵的秩和列数相等时，称作**列满秩矩阵**。
当矩阵 $\bm A$ 为 $n$ 阶方阵时，若 $R(\bm A)=n$ ，则称 $\bm A$ 为**满秩矩阵**；若 $R(\bm A)<n$ ，则称 $\bm A$ 为**降秩矩阵**。
矩阵可逆的充要条件是 $|\bm A|\neq 0$ ，因此满秩矩阵可逆，降秩矩阵不可逆。

关于行、列满秩矩阵，有以下定理：

* 对行满秩矩阵 $\bm A_{m\times n}$ ，必有列满秩矩阵 $\bm B_{n\times m}$ ，使得 $\bm A\bm B=\bm I$ 。

证明：

当 $m=n$ 时，由满秩矩阵可逆，定理显然成立。

当 $m<n$ 时，由 $R(\bm A)=m$ ，可知 $\bm A$ 中存在 $m$ 个列，使它们构成的 $m$ 阶子式 $|\bm A_1|\neq 0$ ，不管它们处于矩阵的什么位置，都可以通过换法变换将它们移到矩阵的前 $m$ 列，即有 $n$ 阶可逆矩阵 $\bm P$ ，使得

$$\bm A\bm P=[\bm A_1,\bm A_2]$$

其中 $\bm A_1$ 可逆，令

$$\bm B=\begin{bmatrix}\bm A_1^{-1}\\\bm O\end{bmatrix}$$

又因为 $R(\bm B)=R(\bm A_1^{-1})=m$ ，于是 $\bm B$ 为 $n\times m$ 列满秩矩阵，且有

$$\bm A\bm B=[\bm A_1,\bm A_2]\begin{bmatrix}\bm A_1^{-1}\\\bm O\end{bmatrix}=\bm I$$

**矩阵乘积的秩的性质：**

* 设矩阵 $\bm A_{m\times n},\bm B_{n\times p}$ ，则 $R(\bm A\bm B)\geq R(\bm A)+R(\bm B)-n$ 。

证明：

设 $R(\bm A)=r$ ，存在 $m$ 阶可逆矩阵 $\bm P$ 和 $n$ 阶可逆矩阵 $\bm Q$ ，使得有以下标准形矩阵：

$$\bm P\bm A\bm Q=\begin{bmatrix}\bm I_r&\bm O\\\bm O&\bm O\end{bmatrix}$$

将矩阵 $\bm Q^{-1}\bm B$ 分块为

$$\bm Q^{-1}\bm B=\begin{bmatrix}\bm B_1\\\bm B_2\end{bmatrix}$$

其中 $\bm B_1$ 是 $r\times p$ 矩阵， $\bm B_2$ 是 $(n-r)\times p$ 矩阵。由于

$$\bm P\bm A\bm B=\bm P\bm A\bm Q\bm Q^{-1}\bm B=\begin{bmatrix}\bm I_r&\bm O\\\bm O&\bm O\end{bmatrix}\begin{bmatrix}\bm B_1\\\bm B_2\end{bmatrix}=\begin{bmatrix}\bm B_1\\\bm O\end{bmatrix}$$

所以

$$R(\bm A\bm B)=R(\bm P\bm A\bm B)=R\begin{bmatrix}\bm B_1\\\bm O\end{bmatrix}=R(\bm B_1)$$

$\bm B_1$ 是 $\bm Q^{-1}\bm B$ 去掉 $n-r$ 行得到的矩阵，而矩阵每去掉一行秩减一或不变，因此

$$R(\bm B_1)\geq R(\bm Q^{-1}\bm B)-(n-r)=R(\bm B)-(n-r)$$

从而

$$R(\bm A\bm B)\geq R(\bm A)+R(\bm B)-n$$

**伴随矩阵的秩的性质：**

设 $\bm A$ 为 $n\ (n\geq 2)$ 阶方阵， $\bm A^*$ 是 $\bm A$ 的伴随矩阵，则：

1. 当 $R(\bm A)=n$ 时， $R(\bm A^*)=n$
2. 当 $R(\bm A)=n-1$ 时， $R(\bm A^*)=1$
3. 当 $R(\bm A)<n-1$ 时， $R(\bm A^*)=0$

证明：

当 $R(\bm A)=n$ 时，即 $\bm A$ 为满秩矩阵，所以 $|\bm A^*|=|\bm A|^{n-1}\neq 0$ ，从而 $R(\bm A^*)=n$ 。

当 $R(\bm A)=n-1$ 时， $|\bm A|=0$ ，所以 $\bm A\bm A^*=|\bm A|\bm I=\bm O$ ，
由 $R(\bm A)+R(\bm A^*)\leq n$ ，得 $R(\bm A^*)\leq 1$ ，
又因为 $R(\bm A)=n-1\geq 1$ ，所以 $\bm A^*$ 是非零矩阵，从而有 $R(\bm A^*)\geq 1$ ，故 $R(\bm A^*)=1$ 。

当 $R(\bm A)<n-1$ 时， $\bm A$ 的每一个 $n-1$ 阶子式都等于零，因而 $\bm A$ 的所有代数余子式均为零，即 $\bm A^*$ 是零矩阵，故 $R(\bm A^*)=0$ 。

### 向量组的线性相关性

**向量组的等价关系：**

设 $\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s$ 为 $n$ 维向量组， $k_1,k_2,\cdots,k_s$ 为一组数，则下式

$$k_1\bm\alpha_1+k_2\bm\alpha_2+\cdots+k_s\bm\alpha_s$$

称为该向量组的一个**线性组合**， $k_1,k_2,\cdots,k_s$ 称为该线性组合的系数。若一个向量 $\bm\alpha$ 可以被表示为一个向量组的线性组合，则称向量 $\bm\alpha$ 可以被该向量组**线性表示**。

若一个向量组中的每一个向量都能由另一个向量组线性表示，即两个向量组能够互相线性表示，则称这两个向量组**等价**。

向量组的等价关系具有反身性，对称性和传递性。

**线性相关：**

若对于向量组 $\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s$ ，存在不全为零的数 $\lambda_1,\lambda_2,\cdots,\lambda_s$ ，使得

$$\lambda_1\bm\alpha_1+\lambda_2\bm\alpha_2+\cdots+\lambda_s\bm\alpha_s=0$$

则称向量组 $\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s$ **线性相关**，否则，称 $\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s$ **线性无关**。

线性无关的判别方法：如果存在数 $\lambda_1,\lambda_2,\cdots,\lambda_s$ ，使得 $\lambda_1\bm\alpha_1+\lambda_2\bm\alpha_2+\cdots+\lambda_s\bm\alpha_s=0$ ，则必然 $\lambda_1=\lambda_2=\cdots=\lambda_s=0$ 。

1. 单个向量 $\bm\alpha$ 线性相关的充分条件是 $\bm\alpha=\bm 0$ 。
2. 两个向量线性相关的充要条件是它们对应的分量成比例。
3. 线性相关向量组的任何扩大组必线性相关，即若 $\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s$ 线性相关，任意增加有限个向量 $\bm\alpha_{s+1},\cdots,\bm\alpha_m$ 所构成的新向量组 $\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s,\bm\alpha_{s+1},\cdots,\bm\alpha_m$ 仍然线性相关。
4. 线性无关向量组的任何以一个非空部分向量组仍线性无关。

向量组 $\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s$ 线性相（无）关的充要条件是齐次线性方程组 $x_1\bm\alpha_1+x_2\bm\alpha_2+\cdots+x_s\bm\alpha_s=\bm 0$ 有（无）非零解。

**推论：**

1. 存在向量组 $\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s$ ， 矩阵 $\bm A=[\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s]$
向量组线性相关的充要条件是 $R(\bm A)<s$
向量组线性无关的充要条件是 $R(\bm A)=s$
2. $n$ 个 $n$ 维向量线性无关的充要条件是它们排成的 $n$ 阶行列式值不为零。
3. $m>n$ 时， $m$ 个 $n$ 维向量一定线性相关。

**线性相关与线性表示的关系：**

1. 向量组 $\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s$ 线性相关的充要条件是该向量组中至少存在一个向量能由其余的 $s-1$ 个向量线性表示。
2. 设向量组 $\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s$ 线性无关，且向量 $\bm\beta$ 能由 $\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s$ 线性表示，则表示法是唯一的。
3. 设向量组 $\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s$ 线性无关, 且向量组 $\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s,\bm\beta$ 线性相关，则向量 $\bm\beta$ 能由 $\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s$ 唯一线性表示。

### 向量组的秩

对于向量组 $A:\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s$ ，如果存在 $A$ 的部分向量组 $A_0:\bm\alpha_{j_1},\bm\alpha_{j_2},\cdots,\bm\alpha_{j_r}$ ，满足：

1. 向量组 $A_0$ 线性无关；
2. 向量组 $A$ 中的任一向量可用 $A_0$ 线性表示。

则称 $A_0$ 是 $A$ 的一个**极大线性无关向量组**，简称**极大无关组**，极大无关组所含的向量的个数 $r$ 称为向量组 $A$ 的秩，记作 $R(\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s)$ ，向量组的秩是唯一确定的。

由上述定义我们可以推得如下结论：

1. 向量组线性无关的充要条件是向量组的秩等于该组向量的个数；
向量组线性相关的充要条件是向量组的秩小于该组向量的个数。
2. 向量组 $A$ 的部分向量组 $A_0$ 为 $A$ 的极大无关组的充要条件是：
1）向量组 $A_0$ 线性无关；
2）$A$ 中任意 $r+1$ 个向量都线性相关。
3. 若向量组 $A$ 的秩为 $r\ (r>0)$ ，则 $A$ 中任意 $r$ 个线性无关的向量都是 $A$ 的一个极大无关组。

**性质：**

1. 向量组与它的任意一个极大无关组等价。
推论：一向量组的任意两个极大无关组等价。
2. 设向量组 $A$ 能由向量组 $B$ 线性表示，则 $R(A)\leq R(B)$ 。
3. 等价向量组的秩相同。

### 矩阵的行秩与列秩

有了向量组的秩的概念后，我们就可以定义矩阵的行秩和列秩：矩阵的行向量组的秩称为矩阵的**行秩**，列向量组的秩称为**列秩**。

事实上，矩阵的秩 $=$ 矩阵的行秩 $=$ 矩阵的列秩。

证明：

设矩阵 $\bm A$ 的秩 $R(\bm A)=r$ ，并设 $r$ 阶子式 $D_r\neq 0$ 。

由 $D_r\neq 0$ 可知 $D_r$ 所在的 $r$ 个列向量都线性无关；又由 $\bm A$ 中所有 $r+1$ 阶子式的值均为零，可知 $\bm A$ 中任意 $r+1$ 个列向量都线性相关，
因此， $D_r$ 所在的 $r$ 个列是 $\bm A$ 的列向量组的一个极大无关组，所以 $\bm A$ 的列秩等于 $r$ ，即矩阵 $\bm A$ 的秩等于列秩。

由 $R(\bm A)=R(\bm A^T)$ ，而 $\bm A^T$ 的列秩就是 $\bm A$ 的行秩，同理可证得，矩阵 $\bm A$ 的秩等于行秩。

因为初等变换不改变矩阵的秩，从而不改变行秩和列秩，因此可以用初等变换来求向量组的秩和极大无关组：

**例：** 有一向量组 $\{\bm\alpha_1,\bm\alpha_2,\bm\alpha_3,\bm\alpha_4,\bm\alpha_5\}$ ，将该向量组写成矩阵形式，并进行初等行变换，得到：

$$[\bm\alpha_1,\bm\alpha_2,\bm\alpha_3,\bm\alpha_4,\bm\alpha_5]\rightarrow\begin{bmatrix}1&a_1&a_2&a_3&a_4\\0&1&b_1&b_2&b_3\\0&0&0&1&c_1\\0&0&0&0&0\end{bmatrix}$$

取非零行的首非零元所在的列，可以得到一个三阶非零子式：

$$D=\begin{vmatrix}1&a_1&a_3\\0&1&b_2\\0&0&1\end{vmatrix}$$

从而该向量组的秩为3， $\bm\alpha_1,\bm\alpha_2,\bm\alpha_4$ 是该向量组的一个极大无关组。

有了前面的理论，我们将方便地用向量组地秩地结论讨论矩阵秩的有关结论：

**证明：** $R(\bm A\bm B)\leq\min\{R(\bm A),R(\bm B)\}$

记 $\bm C_{m \times n}=\bm A_{m \times n}\bm B_{n \times p}$ ，并设

$$\bm C=[\bm c_1,\bm c_2,\cdots,\bm c_p]\\
\bm A=[\bm a_1,\bm a_2,\cdots,\bm a_n]\\
\bm B=[b_{ij}]$$

由

$$[\bm c_1,\bm c_2,\cdots,\bm c_p]=[\bm a_1,\bm a_2,\cdots,\bm a_n]\begin{bmatrix}b_{11}&&\\&\ddots&\\&&b_{np}\end{bmatrix}$$

可知，矩阵 $\bm C$ 的列向量能用 $\bm A$ 的列向量线性表示，所以

$$R(\bm C)\leq R(\bm A)$$

又因为 $\bm C^T=\bm B^T\bm A^T$ ，用类似的方法证明可得 $R(\bm C^T)\leq R(\bm B^T)$ ，即

$$R(\bm C)\leq R(\bm B)$$

综上所述，可以证得：

$$R(\bm A\bm B)\leq\min\{R(\bm A),R(\bm B)\}$$

**证明：** $R(\bm A+\bm B)\leq R(\bm A)+R(\bm B)$

显然 $\bm A+\bm B$ 的列向量组可由 $\bm A$ 的列向量组和 $\bm B$ 的列向量组线性表示。
设 $R(\bm A)=s,R(\bm B)=t$ ，不妨设 $\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s$ 是 $\bm A$ 的一个极大无关组， $\bm\beta_1,\bm\beta_2,\cdots,\bm\beta_t$ 是 $\bm B$ 的一个极大无关组。
由于向量组和它的极大无关组等价，由传递性可知 $\bm A+\bm B$ 的列向量组可由向量组 $\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s$ 和 $\bm\beta_1,\bm\beta_2,\cdots,\bm\beta_t$ 线性表示，因此

$$\begin{aligned}R(\bm A+\bm B)&\leq R(\bm\alpha_1,\cdots,\bm\alpha_s,\bm\beta_1,\cdots,\bm\beta_t)\\
&\leq s+t\\
&=R(\bm A)+R(\bm B)\end{aligned}$$

### 秩的几何意义

我们可以将矩阵写成列向量组的形式 $\bm A=[\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_n]$ ，这些列向量可以张成一个**列空间**，即线性表示出的向量

$$\bm\alpha=x_1\bm\alpha_1+x_2\bm\alpha_2+\cdots+x_n\bm\alpha_n$$

所形成的空间。而秩所代表的，就是这样一个列空间的维度。

而矩阵变换就是将原来的向量变换到列空间中，因此列空间的维度就是变换后向量的维度，即矩阵的秩就是向量在经过这一矩阵变换后所处的空间维度。

由此，我们可以得到秩的几何意义：

1. 秩是列空间的维度。
2. 秩是图像经过矩阵变换后的空间维度。

## 解线性方程组

一般地， $n$ 个未知量 $m$ 个方程的线性方程组可以表示为：

$$\left\{\begin{aligned}
&a_{11}x_1+a_{12}x_2+\cdots+a_{1n}x_n=b_1\\
&a_{21}x_1+a_{22}x_2+\cdots+a_{2n}x_n=b_1\\
&\qquad\qquad\qquad\cdots\\
&a_{m1}x_1+a_{m2}x_2+\cdots+a_{mn}x_n=b_1
\end{aligned}\right.$$

可以记作

$$\bm A=\begin{bmatrix}a_{11}&&\\&\ddots&\\&&a_{mn}\end{bmatrix},\bm x=\begin{bmatrix}x_1\\x_2\\\vdots\\x_n\end{bmatrix},\bm b=\begin{bmatrix}b_1\\b_2\\\vdots\\b_n\end{bmatrix}$$

$$\bm{Ax}=\bm b$$

称 $m\times n$ 矩阵 $\bm A$ 为线性方程组的**系数矩阵（Coefficient matrix）**，称 $m\times(n+1)$ 矩阵 $\bm B=[\bm A,\bm b]$ 为线性方程组的**增广矩阵（Augmented matrix）**。

当 $\bm b=0$ 时，该线性方程组称作**齐次线性方程组（Homogeneous linear equations）**；反之，当 $\bm b\neq 0$ 时，该线性方程组称作**非齐次线性方程组（Nonhomogeneous linear equations）**。

若找到常数 $\xi_1,\xi_2,\cdots,\xi_n$ 依次代替未知量 $x_1,x_2,\cdots,x_n$ ，使方程组中所有方程均为恒等式，则此时方程组有解，并称向量

$$\bm\xi=\begin{bmatrix}x_1\\x_2\\\vdots\\x_n\end{bmatrix}$$

为方程组的**解向量**，或说 $\bm x=\bm\xi$ 是 $\bm{Ax}=\bm b$ 的解。

线性方程组有解时，该线性方程组是**相容的（Consistent）**，否则是**不相容的（Inconsistent）**。

### 克莱姆法则（Cramer's rule）

$n$ 个未知量 $n$ 个方程的线性方程组 $\bm{Ax}=\bm b$ ，若 $|\bm A|\neq 0$ ，则方程组有唯一解：

$$x_j=\frac{D_j}{|\bm A|},\quad j=1,2,\cdots,n$$

其中 $D_j$ 是以 $\bm b$ 的元素代替 $|\bm A|$ 中第 $j$ 列所得到的行列式。

这实际上就是 $\bm x=\bm A^{-1}\bm b$ 的展开形式。

**证明：**

充分性：

因为 $|\bm A|\neq 0$ ，所以 $\bm A$ 可逆，那么显然 $\bm x_0=\bm A^{-1}\bm b$ 是方程组的一个解，又设有另一个不同于 $\bm x_1$ 的解 $\bm x_1$ 使得 $\bm{Ax}_1=\bm b$ ，两边同时左乘 $\bm A^{-1}$ 得

$$\bm A^{-1}(\bm{Ax}_1)=\bm A^{-1}\bm b=\bm x_0$$

又因为

$$\bm A^{-1}(\bm{Ax}_1)=(\bm A^{-1}\bm A)\bm x_1=\bm I\bm x_1=\bm x_1$$

则 $\bm x_1=\bm x_0$ 产生矛盾，因此不存在和 $\bm x_0$ 不同的解。

必要性：

设方程组存在唯一解 $\bm x_0$ ，若 $\bm A$ 不可逆，则齐次线性方程组 $\bm{Ax}=\bm 0$ 有非零解 $\bm x_1$ ，使得

$$\bm A(\bm x_0+\bm x_1)=\bm{Ax}_0+\bm{Ax}_1=\bm b+\bm 0=\bm b$$

因此 $\bm x_0+\bm x_1$ 也是方程组的解，与方程组有唯一解产生矛盾，故 $\bm A$ 必然可逆。

### 消元法

设非齐次线性方程组 $\bm{Ax}=\bm b$ ，其中 $\bm A=(a_{ij})_{m\times n}$ ，且 $R(\bm A)=r$ 。

不妨设矩阵 $\bm A$ 的前 $r$ 列中有 $r$ 阶非零子式，对增广矩阵 $\bm B=[\bm A,\bm b]$ 施以行的换法变换，将非零子式所在的行调整至前 $r$ 行，再经过若干次初等行变换，将 $\bm B$ 化为行最简矩阵：

$$(\bm C,\bm d)=\begin{bmatrix}
1&0&\cdots&0&c_{1,r+1}&\cdots&c_{1n}&d_1\\
&1&\ddots&\vdots&\vdots&&\vdots&\vdots\\
&&\ddots&0&c_{r-1,r+1}&\cdots&c_{r-1,n}&d_{r-1}\\
&&&1&c_{r,r+1}&\cdots&c_{rn}&d_r\\
&&&&0&\cdots&0&d_{r+1}\\
&&&&0&\cdots&0&0\\
&&&&\vdots&&\vdots&\vdots\\
&&&&0&\cdots&0&0
\end{bmatrix}$$

它所对应的与原方程 $\bm{Ax}=\bm b$ 同解的方程组为：

$$\left\{\begin{matrix}
x_1&&&+c_{1,r+1}x_{r+1}&+\cdots&c_{1n}x_n&=&d_1\\
&x_2&&+c_{2,r+1}x_{r+1}&+\cdots&c_{1n}x_n&=&d_2\\
&&&&&\cdots\\
&&x_r&+c_{r,r+1}x_{r+1}&+\cdots&+c_{rn}&=&d_r\\
&&&&&0&=&d_{r+1}\\
&&&&&0&=&0\\
&&&&&\cdots\\
&&&&&0&=&0\\
\end{matrix}\right.$$

由于初等变换不改变矩阵的秩，所以

$$R(\bm A)=R(\bm C)=r$$

从而

$$R(\bm A,\bm b)=R(\bm C,\bm d)=\left\{\begin{aligned}&r,&d_{r+1}=0\\&r+1,&d_{r+1}\neq 0\end{aligned}\right.$$

当 $d_{r+1}\neq 0$ 时，方程组的第 $r+1$ 个方程产生矛盾，故方程组无解。

当 $d_{r+1}=0$ 时， $R(\bm A,\bm b)=R(\bm A)=r$ ，若 $r=n$ ，则方程组有唯一解

$$x_j=d_j\quad(j=1,2,\cdots,n)$$

若 $r<n$ ，则原式可以改写为

$$\left\{\begin{aligned}
x_1=d_1-c_{1,r+1}x_{r+1}-\cdots-c_{1n}x_n\\
x_2=d_2-c_{2,r+1}x_{r+1}-\cdots-c_{2n}x_n\\
\cdots\qquad\qquad\qquad\qquad\\
x_r=d_r-c_{r,r+1}x_{r+1}-\cdots-c_{rn}x_n\\
\end{aligned}\right.$$

由此可见，任给 $x_{r+1},x_{r+2},\cdots,x_n$ 的一组值，就可以确定对应的 $x_1,x_2,\cdots,x_r$ 的值，由此得到方程组的一个解。此时，方程组拥有无穷多个解，称 $x_{r+1},x_{r+2},\cdots,x_n$ 为一组**自由未知量**。

综合以上讨论，我们可以得到以下几个定理。

**线性方程组解的存在定理：**

$n$ 元非齐次线性方程组 $\bm{Ax}=\bm b$ 有解的充要条件是 $R(\bm A)=R(\bm A,\bm b)$
有无穷多解： $R(\bm A)=R(\bm A,\bm b)<n$
有唯一解： $R(\bm A)=R(\bm A,\bm b)=n$

$n$ 元齐次线性方程组 $\bm{Ax}=\bm 0$ 有非零解的充要条件是 $R(\bm A)<n$
仅有零解的充要条件是 $R(\bm A)=n$

### 解的结构

针对方程组具有无穷多解的情况，我们需要讨论解的结构。

**齐次线性方程组解的结构：**

设 $\bm\xi_1,\bm\xi_2,\cdots,\bm\xi_t$ 是齐次线性方程组的解，并且

1. $\bm\xi_1,\bm\xi_2,\cdots,\bm\xi_t$ 线性无关；
2. 方程组的任一解都可以用 $\bm\xi_1,\bm\xi_2,\cdots,\bm\xi_t$ 线性表示，

则称 $\bm\xi_1,\bm\xi_2,\cdots,\bm\xi_t$ 是方程组的一个**基础解系**。
基础解系实际上就是全体解向量的一个极大无关组。

当方程组 $\bm{Ax}=\bm 0$ 有非零解时，求其基础解系：

$R(\bm A)=r<n$ ，不妨设 $\bm A$ 的前 $r$ 个列向量线性无关，进行初等行变换，得到行最简形矩阵：

$$\bm C=\begin{bmatrix}
1&\cdots&0&c_{11}&\cdots&c_{1,n-r}\\
\vdots&&\vdots&\vdots&&\vdots\\
0&\cdots&1&c_{r1}&\cdots&c_{r,n-r}\\
0&\cdots&0&0&\cdots&0\\
\vdots&&\vdots&\vdots&&\vdots\\
0&\cdots&0&0&\cdots&0\\
\end{bmatrix}$$

与 $\bm C$ 对应的方程组为：

$$\left\{\begin{aligned}
x_1=-c_{11}x_{r+1}-\cdots-c_{1,n-r}x_n\\
x_2=-c_{21}x_{r+1}-\cdots-c_{2,n-r}x_n\\
\cdots\qquad\qquad\qquad\\
x_r=-c_{r1}x_{r+1}-\cdots-c_{r,n-r}x_n\\
\end{aligned}\right.$$

这个方程组是原方程组的一个同解方程组。

现在令 $x_{r+1},\cdots,x_n$ 分别取下列数：

$$\begin{bmatrix}x_{r+1}\\x_{r+2}\\\vdots\\x_n\end{bmatrix}=\begin{bmatrix}1\\0\\\vdots\\0\end{bmatrix},\begin{bmatrix}0\\1\\\vdots\\0\end{bmatrix},\cdots,\begin{bmatrix}0\\0\\\vdots\\1\end{bmatrix}$$

则由上述方程组可以依次求得：

$$\begin{bmatrix}x_{r+1}\\x_{r+2}\\\vdots\\x_n\end{bmatrix}=\begin{bmatrix}-c_{11}\\-c_{21}\\\vdots\\-c_{r1}\end{bmatrix},\begin{bmatrix}-c_{12}\\-c_{22}\\\vdots\\-c_{r2}\end{bmatrix},\cdots,\begin{bmatrix}-c_{1,n-r}\\-c_{2,n-r}\\\vdots\\-c_{r,n-r}\end{bmatrix}$$

从而求得方程组的 $n-r$ 个解：

$$\bm\xi_1=\begin{bmatrix}-c_{11}\\-c_{21}\\\vdots\\-c_{r1}\\1\\0\\\vdots\\0\end{bmatrix},\bm\xi_2=\begin{bmatrix}-c_{12}\\-c_{22}\\\vdots\\-c_{r2}\\0\\1\\\vdots\\0\end{bmatrix},\cdots,\bm\xi_{n-r}=\begin{bmatrix}-c_{1,n-r}\\-c_{2,n-r}\\\vdots\\-c_{r,n-r}\\0\\0\\\vdots\\1\end{bmatrix}$$

$\bm\xi_1,\bm\xi_2,\cdots,\bm\xi_{n-r}$ 就是方程组的一个基础解系，方程组的所有解都可以由其线性表示，称之为方程组的**通解**：

$$\bm x=k_1\bm\xi_1+k_2\bm\xi_2+\cdots+k_{n-r}\bm\xi_{n-r}$$

基础解系并不是唯一的，对于有非零解的齐次线性方程组，它的任意 $n-r$ 个线性无关的解向量都可以构成一个基础解系，在实际求解方程组时，自由未知量的选择也并不是唯一的。

**非齐次线性方程组解的结构：**

设 $\bm x=\bm\eta$ 和 $\bm x=\bm\eta_0$ 是非齐次线性方程组 $\bm{Ax}=\bm b$ 的解，则

$$\bm A(\bm\eta-\bm\eta_0)=\bm{A\eta}-\bm{A\eta}_0=\bm b-\bm b=\bm 0$$

因此 $\bm x=\bm\eta-\bm\eta_0$ 是其对应的齐次线性方程组 $\bm{Ax}=\bm 0$ 的解。

设 $\bm x=\bm\eta$ 是非齐次线性方程组 $\bm{Ax}=\bm b$ 的解， $\bm x=\bm\xi$ 是其对应的齐次线性方程组 $\bm{Ax}=\bm 0$ 的解，则

$$\bm A(\bm\xi+\bm\eta)=\bm{A\xi}+\bm{A\eta}=\bm 0+\bm b=\bm b$$

因此 $\bm x=\bm\xi+\bm\eta$ 也是 $\bm{Ax}=\bm b$ 的解。

由此，我们可以证得非齐次线性方程组解的结构定理：

设 $\bm\xi_1,\bm\xi_2,\cdots,\bm\xi_{n-r}$ 是 $\bm{Ax}=\bm 0$ 的基础解系，存在一组常数 $k_1,k_2,\cdots,k_{n-r}$ ，使得

$$\bm\eta-\bm\eta_0=k_1\bm\xi_1+k_2\bm\xi_2+\cdots+k_{n-r}\bm\xi_{n-r}$$

所以 $\bm{Ax}=\bm b$ 的通解为：

$$\bm\eta=k_1\bm\xi_1+k_2\bm\xi_2+\cdots+k_{n-r}\bm\xi_{n-r}+\bm\eta_0$$

综上所述，只要找到非齐次线性方程组对应的齐次线性方程组的基础解系和非齐次线性方程组的一个解，就可以求出非齐次线性方程组的通解。