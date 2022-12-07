---
title: 线性空间与线性变换概念浅析
date: 2022-11-29 20:00:00
tags:
	- 大学数学
	- 代数学
categories: 线性代数
top_img: /images/articles/cover_6.jpg
cover: /images/articles/cover_6.jpg
katex: true
description: 在本文中，我们简单了解线性空间与线性变换的概念，并理解向量、矩阵和它们的关系。
---

## 线性空间

### 向量组与向量空间

设 $\mathbb{R}$ 是实数域， $V$ 是由 $n$ 维向量全体组成的集合，记作 $\mathbb{R}^n$ ，对于任意 $\boldsymbol\alpha,\boldsymbol\beta,\boldsymbol\gamma\in V$ ，总有以下运算性质成立：

1. $\boldsymbol\alpha+\boldsymbol\beta=\boldsymbol\beta+\boldsymbol\alpha$
2. $(\boldsymbol\alpha+\boldsymbol\beta)+\boldsymbol\gamma=\boldsymbol\beta+(\boldsymbol\alpha+\boldsymbol\gamma)$
3. $V$ 中存在零元素，通常记为 $\boldsymbol 0$ ，恒有 $\boldsymbol\alpha+\boldsymbol 0=\boldsymbol\alpha$
4. 存在 $\boldsymbol\alpha$ 的负元素 $\boldsymbol\alpha'$ ，使得 $\boldsymbol\alpha+\boldsymbol\alpha'=\boldsymbol 0$
5. $1\boldsymbol\alpha=\boldsymbol\alpha$
6. $k(l\boldsymbol\alpha)=(kl)\boldsymbol\alpha$
7. $(k+l)\boldsymbol\alpha=k\boldsymbol\alpha+l\boldsymbol\alpha$
8. $k(\boldsymbol\alpha+\boldsymbol\beta)=k\boldsymbol\alpha+k\boldsymbol\beta$

这说明向量组 $V$ 是在 $\mathbb{R}$ 上的**线性空间（Linear space）**。

线性空间又称为向量空间（Vector space），线性空间中的元素称为向量，零元素称为零向量，负元素称为负向量。

> 在此处讨论线性空间时所说的向量是一般意义上的数组向量的推广。

若对于一个非空集合 $V$ ，它在数域 $\mathbb{F}$ 上拥有和以上向量组相同的运算性质，则称 $V$ 为数域 $\mathbb{F}$ 上的线性空间。

**线性空间的性质：**

1. 线性空间的零元素唯一。
2. 线性空间中任一元素的负元素唯一。
3. $0\boldsymbol\alpha=\boldsymbol 0$
$k\boldsymbol 0=\boldsymbol 0$
当 $k\neq 0$ 且 $\boldsymbol\alpha\neq 0$ 时，必然 $k\boldsymbol\alpha\neq 0$
4. $(-k)\boldsymbol\alpha=k(-\boldsymbol\alpha)=-(k\boldsymbol\alpha)$

### 子空间

设 $V$ 为数域 $\mathbb{F}$ 上的线性空间， $V_1$ 是 $V$ 的一个非空子集，若 $V_1$ 对于 $V$ 的加法和数乘运算也构成 $\mathbb{F}$ 上的线性空间，则称 $V_1$ 是 $V$ 的一个**线性子空间（Linear subspace**）。

若对任意 $\boldsymbol\alpha,\boldsymbol\beta\in V_1$ ，满足：

1. $\boldsymbol\alpha+\boldsymbol\beta\in V_1$
2. $\forall k\in \mathbb{F}\quad k\boldsymbol\alpha\in V_1$

则说明 $V_1$ 是 $V$ 的子空间。

若 $V_1$ 是由 $V$ 中的元素 $\boldsymbol\alpha_1,\boldsymbol\alpha_2,\cdots,\boldsymbol\alpha_s$ 生成的子空间，则称 $\boldsymbol\alpha_1,\boldsymbol\alpha_2,\cdots,\boldsymbol\alpha_s$ 为该子空间的生成元素，记作 $L(\boldsymbol\alpha_1,\boldsymbol\alpha_2,\cdots,\boldsymbol\alpha_s)$ 。

在实数域 $\mathbb{R}$ 上的线性空间 $\mathbb{R}^n$ 中，齐次线性方程组

$$\left\{\begin{aligned}
&a_{11}x_1+a_{12}x_2+\cdots+a_{1n}x_n=0,\\
&a_{21}x_1+a_{22}x_2+\cdots+a_{2n}x_n=0,\\
&\qquad\qquad\qquad\cdots\\
&a_{m1}x_1+a_{m2}x_2+\cdots+a_{mn}x_n=0,
\end{aligned}\right.$$

的全体解向量组成一个子空间，这个子空间称作齐次线性方程组的**解空间**，是由齐次线性方程组的基础解系生成的子空间。

**平凡子空间：**

1. $V$ 是其自身的子空间。
2. $\{\boldsymbol 0\}$ 是任何线性空间的零子空间。

**子空间的交与和：**

设 $V$ 为数域 $\mathbb{F}$ 上的线性空间， $V_1,V_2$ 都是 $V$ 的子空间，则集合

$$V_1\cap V_2=\{\boldsymbol\alpha|\boldsymbol\alpha\in V_1且\boldsymbol\alpha\in V_2\}$$

称为 $V_1,V_2$ 的**交空间**，

$$V_1+V_2=\{\boldsymbol\alpha_1+\boldsymbol\alpha_2|\boldsymbol\alpha_1\in V_1,\boldsymbol\alpha_2\in V_2\}$$

称为 $V_1,V_2$ 的**和空间**。

子空间在经过交与和后依然是原线性空间的子空间。

若对于和空间中的任一向量 $\boldsymbol\alpha$ ，都有唯一的 $\boldsymbol\alpha_1\in V_1,\boldsymbol\alpha_2\in V_2$ ，使得

$$\boldsymbol\alpha=\boldsymbol\alpha_1+\boldsymbol\alpha_2$$

则称和 $V_1+V_2$ 为**直和（Direct sum）**，记作 $V_1\oplus V_2$ 。

$V_1+V_2$ 为直和的充分必要条件是 $V_1\cap V_2=\{\boldsymbol 0\}$ 。

### 基与维数

设 $V$ 为数域 $\mathbb{F}$ 上的线性空间，如果 $V$ 中存在 $n$ 个线性无关的向量，并且可以线性表示 $V$ 中的任何向量，则称这些向量是 $V$ 的一个**基（Basis）**，基的向量个数 $n$ 称为线性空间 $V$ 的**维数（Dimensionality）**，记作 $n = \dim V$ 。

对于能找到无限个线性无关向量的线性空间，称为无限维线性空间；零空间是不存在基的线性空间，其维数为零。

实际上，维数反映了线性空间的“自由度”，基则相当于线性空间所有向量的一个“极大无关组”；线性空间的基是个有序的向量组，一个基中向量次序改变后，应当视为与原基不同的一个基。

**性质：**

1. $n$ 维线性空间 $V$ 中的任一向量必可由 $V$ 的基线性表示，并且表示法唯一。
2. 线性空间的基（只要存在）比不唯一，并且两个不同的基可以互相线性表示。
3. 有限维线性空间的维数是唯一确定的。
4. $n$ 维线性空间中任意 $n$ 个线性无关的向量均可构成基。

## 线性变换

对于线性空间 $V$ ，若存在规则 $\sigma$ ，使对于 $V$ 中任意元素 $\bm\alpha$ ，都有一个确定的元素 $\bm\alpha'\in V$ 与之对应，记作 $\sigma(\bm\alpha)=\bm\alpha'\in V$ ，则称 $\omicron$ 为线性空间 $V$ 的一个变换。

$\bm\alpha'$ 称作 $\bm\alpha$ 在变换 $\sigma$ 下的像，$\bm\alpha$ 称作 $\bm\alpha'$ 在变换 $\sigma$ 下的一个原像。

$V$ 中元素在变换 $\sigma$ 下的像的全体，称作 $\sigma$ 的像集或值域，记作 $\sigma(V)$ ， $\sigma(V)\subseteq V$ 。

恒等变换： $1^*:1^*(\bm\alpha)=\bm\alpha$
零变换： $0^*:0^*(\bm\alpha)=\bm 0$
数乘变换： $k^*:k^*(\bm\alpha)=k\bm\alpha$

和变换： $(\sigma+\tau)(\bm\alpha)=\sigma(\bm\alpha)+\tau(\bm\alpha)$
乘积变换： $(\sigma\tau)(\bm\alpha)=\sigma[\tau(\bm\alpha)]$
数积变换： $(k\sigma)(\bm\alpha)=k[\sigma(\bm\alpha)]$
负变换： $(-\sigma)(\bm\alpha)=(-1)^*[\sigma(\bm\alpha)]=-\sigma(\bm\alpha)$

若 $\sigma$ 为可逆变换，其逆变换为 $\tau$ ，则有： $\sigma\tau=\tau\sigma=1^*$
可逆变换的逆变换是唯一的，可以简记为 $\sigma^{-1}$ 。

若变换 $\sigma$ 满足以下性质：

1. $\sigma(\bm\alpha+\bm\beta)=\sigma(\bm\alpha)+\sigma(\bm\beta)$
2. $\sigma(k\bm\alpha)=k\sigma(\bm\alpha)$

则称该变换是线性变换。

**线性变换的性质：**

1. $\sigma(\bm 0)=\bm 0\quad\sigma(-\bm\alpha)=-\sigma(\bm\alpha)$
2. 线性变换 $\sigma$ 始终保持线性组合关系，如下所示：

$$\sigma(k_1\bm\alpha_1+k_2\bm\alpha_2+\cdots+k_s\bm\alpha_s)=k_1\sigma(\bm\alpha_1)+k_2\sigma(\bm\alpha_2)+\cdots+k_s\sigma(\bm\alpha_s)$$

3. 线性变换 $\sigma$ 将线性相关向量组化为线性相关向量组，即若 $\bm\alpha_1,\bm\alpha_2,\cdots,\bm\alpha_s$ 线性相关， $\sigma(\bm\alpha_1),\sigma(\bm\alpha_2),\cdots,\sigma(\bm\alpha_s)$ 一定也线性相关。
4. 若 $\sigma,\tau$ 都是线性变换，则 $\sigma+\tau$ ， $\sigma\tau$ 和 $k\sigma\ (k\in\mathbb F)$ 也是线性变换。
5. 若 $\sigma$ 是可逆线性变换，则 $\sigma^{-1}$ 也是可逆线性变换。

### 坐标

设 $V$ 为数域 $\mathbb{F}$ 上的线性空间， $\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n$ 是 $V$ 的一个基， $\boldsymbol\alpha$ 是 $V$ 中任一向量，则有数域 $\mathbb{F}$ 中唯一的一组数 $a_1,a_2,\cdots,a_n$ ，使得

$$\boldsymbol\alpha=a_1\bm\varepsilon_1+a_2\bm\varepsilon_2+\cdots+a_n\bm\varepsilon_n$$

则称有序数对 $a_1,a_2,\cdots,a_n$ 为向量 $\boldsymbol\alpha$ 在基 $\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n$ 下的坐标，记为 $\hat{\boldsymbol\alpha}$ 。

矩阵乘积表示法：

$$a_1\bm\varepsilon_1+a_2\bm\varepsilon_2+\cdots+a_n\bm\varepsilon_n=[\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n]\begin{bmatrix}a_1\\a_2\\\vdots\\a_n\end{bmatrix}$$

数组向量表示法：

$$\hat{\boldsymbol\alpha}=\begin{bmatrix}a_1\\a_2\\\vdots\\a_n\end{bmatrix}$$

在线性空间中，唯一零向量的坐标表示为：$\hat{\boldsymbol 0}=[0,0,\cdots,0]^T$

因为坐标是由基底向量线性表示得到的，所以坐标的运算满足线性运算的规律；并且若向量的坐标线性相关，则向量本身也线性相关。

### 基变换和坐标变换

由基的性质可知，两个不同的基可以互相线性表示，则对于基 $\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n$ 及 $\bm\varepsilon_1',\bm\varepsilon_2',\cdots,\bm\varepsilon_n'$ ，有以下线性方程组：

$$\left\{\begin{aligned}
&\bm\varepsilon_1'=a_{11}\bm\varepsilon_1+a_{12}\bm\varepsilon_2+\cdots+a_{1n}\bm\varepsilon_n,\\
&\bm\varepsilon_2'=a_{21}\bm\varepsilon_1+a_{22}\bm\varepsilon_2+\cdots+a_{2n}\bm\varepsilon_n,\\
&\qquad\qquad\qquad\cdots\\
&\bm\varepsilon_n'=a_{m1}\bm\varepsilon_1+a_{m2}\bm\varepsilon_2+\cdots+a_{mn}\bm\varepsilon_n,
\end{aligned}\right.$$

根据方程组，可以写出对应的系数矩阵：

$$\bm A=\begin{bmatrix}
a_{11}&a_{12}&\cdots&a_{1n}\\
a_{21}&a_{22}&\cdots&a_{2n}\\
\vdots&\vdots&&\vdots\\
a_{n1}&a_{n2}&\cdots&a_{nn}\\
\end{bmatrix}$$

矩阵 $\bm A$ 是唯一确定且可逆的。在形式上，我们可以将上述方程组表示为：

$$(\bm\varepsilon_1',\bm\varepsilon_2',\cdots,\bm\varepsilon_n')=(\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n)\bm A$$

这个式子就称作由基 $\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n$ 到基 $\bm\varepsilon_1',\bm\varepsilon_2',\cdots,\bm\varepsilon_n'$ 的变换公式，矩阵 $\bm A$ 称作**过渡矩阵（或变换矩阵）**。

对于数组向量，则上述表示法可以改写为矩阵乘积的形式：

$$\begin{bmatrix}\bm\varepsilon_1'\\\bm\varepsilon_2'\\\vdots\\\bm\varepsilon_n'\end{bmatrix}=\bm A\begin{bmatrix}\bm\varepsilon_1\\\bm\varepsilon_2\\\vdots\\\bm\varepsilon_n\end{bmatrix}$$

变换矩阵满足结合率，即：

$$\begin{bmatrix}\bm\varepsilon_1'\\\bm\varepsilon_2'\\\vdots\\\bm\varepsilon_n'\end{bmatrix}=\bm B(\bm A\begin{bmatrix}\bm\varepsilon_1\\\bm\varepsilon_2\\\vdots\\\bm\varepsilon_n\end{bmatrix})=(\bm{BA})\begin{bmatrix}\bm\varepsilon_1\\\bm\varepsilon_2\\\vdots\\\bm\varepsilon_n\end{bmatrix}$$

两边左乘 $\bm A^{-1}$ ，可以得到：

$$\bm A^{-1}\begin{bmatrix}\bm\varepsilon_1'\\\bm\varepsilon_2'\\\vdots\\\bm\varepsilon_n'\end{bmatrix}=\begin{bmatrix}\bm\varepsilon_1\\\bm\varepsilon_2\\\vdots\\\bm\varepsilon_n\end{bmatrix}$$

这说明变换是可逆的。

同一向量用不同的基底可以表示为：

$$\bm\alpha=[\bm\varepsilon_1',\bm\varepsilon_2',\cdots,\bm\varepsilon_n']\begin{bmatrix}x_1'\\x_2'\\\vdots\\x_n'\end{bmatrix}=[\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n]\bm A\begin{bmatrix}x_1\\x_2\\\vdots\\x_n\end{bmatrix}$$

根据向量在取定基下坐标的唯一性，可以得到坐标变换公式：

$$\begin{bmatrix}x_1\\x_2\\\vdots\\x_n\end{bmatrix}=\bm A\begin{bmatrix}x_1'\\x_2'\\\vdots\\x_n'\end{bmatrix}$$

或写成：

$$\begin{bmatrix}x_1'\\x_2'\\\vdots\\x_n'\end{bmatrix}=\bm A^{-1}\begin{bmatrix}x_1\\x_2\\\vdots\\x_n\end{bmatrix}$$

### 线性变换矩阵

设 $V$ 为数域 $\mathbb{F}$ 上的线性空间，在取定基 $\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n$ 下，有变换 $\sigma$ 和矩阵 $\bm A$ 唯一对应：

$$\sigma(\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n)=(\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n)\bm A$$

则矩阵同样具有变换的性质：

1. $(\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n)(\bm A+\bm B)=(\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n)\bm A+(\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n)\bm B$
2. $(\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n)(\bm A\bm B)=(\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n)\bm A\bm B$
3. $(\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n)(k\bm A)=k(\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n)\bm A$

$\sigma$ 可逆的充要条件是 $\bm A$ 可逆，并且当 $\sigma$ 可逆时， $\sigma^{-1}$ 在基 $(\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n)$ 下的矩阵恰为 $\bm A^{-1}$ 。

**线性变换矩阵的相似性：**

同一线性变换在不同基下的矩阵是相似的。

若线性变换 $\sigma$ 在两个基 $\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n$ 和 $\eta_1,\eta_2,\cdots,\eta_n$ 下的矩阵分别为 $\bm A$ 和 $\bm B$ ，由 $\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n$ 到 $\eta_1,\eta_2,\cdots,\eta_n$ 的变换矩阵为 $\bm P$ ，则

$$\bm B=\bm P^{-1}\bm A\bm P$$

证明：由已知条件得

$$\begin{aligned}\sigma(\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n)&=(\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n)\bm A\\
\sigma(\eta_1,\eta_2,\cdots,\eta_n)&=(\eta_1,\eta_2,\cdots,\eta_n)\bm B\\
(\eta_1,\eta_2,\cdots,\eta_n)&=(\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n)\bm P\end{aligned}$$

此时

$$(\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n)=(\eta_1,\eta_2,\cdots,\eta_n)\bm P^{-1}$$

于是

$$\sigma(\eta_1,\eta_2,\cdots,\eta_n)=\sigma[(\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n)\bm P]$$

利用线性变换的性质，得

$$\begin{aligned}\sigma[(\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n)\bm P]&=[\sigma(\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n)]\bm P\\
&=(\bm\varepsilon_1,\bm\varepsilon_2,\cdots,\bm\varepsilon_n)\bm A\bm P\\
&=(\eta_1,\eta_2,\cdots,\eta_n)\bm P^{-1}\bm A\bm P\end{aligned}$$

综上所述：

$$\bm B=\bm P^{-1}\bm A\bm P$$

**线性变换的特征值和特征向量：**

由于同一线性变换在不同基下的矩阵相似，而相似矩阵的特征多项式相同，所以我们规定：将线性变换 $\sigma$ 对应矩阵 $\bm A$ 的特征多项式及其在数域 $\mathbb F$ 上的特征值，分别定义为 $\sigma$ 的特征多项式及特征值。如果 $n$ 维数组向量

$$\bm x=\begin{bmatrix}x_1\\x_2\\\vdots\\x_n\end{bmatrix}$$

是矩阵 $\bm A$ 对应于数域 $\mathbb F$ 上特征值 $\lambda_0$ 的特征向量，则把 $V$ 中以 $\bm x$ 为坐标的向量

$$\bm\alpha=x_1\bm\varepsilon_1+x_2\bm\varepsilon_2+\cdots+x_n\bm\varepsilon_n$$

称为线性变换 $\sigma$ 对应于特征值 $\lambda_0$ 的特征向量。