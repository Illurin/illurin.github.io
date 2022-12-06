---
title: 线性方程组与行列式代数
date: 2022-12-2 8:38:00
tags:
	- 大学数学
	- 代数学
categories: 线性代数
top_img: /images/articles/cover_6.jpg
cover: /images/articles/cover_6.jpg
katex: true
---

## 行列式代数

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

