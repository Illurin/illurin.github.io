---
title: 矩阵代数（一）：行列式与矩阵求逆
date: 2022-12-2 8:37:00
tags:
	- 大学数学
	- 代数学
categories: 线性代数
top_img: /images/articles/cover_6.jpg
cover: /images/articles/cover_6.jpg
katex: true
description: 在本文中，我们主要研究矩阵的基本概念，行列式的概念和计算，矩阵的逆以及如何在矩阵不可逆的情况下求其伪逆。
---

## 矩阵基本概念

矩阵（Matrix）是线性代数中主要的研究对象，在此，我会给出在本博客中使用的所有矩阵基本符号及定义，后面所有关于线性代数的讨论都将以此作为基础。

用 $m\times n$ 个数排成 $m$ 行的数表

$$\begin{bmatrix}
a_{11}&a_{12}&\cdots&a_{1n}\\
a_{21}&a_{22}&\cdots&a_{2n}\\
\vdots&\vdots&&\vdots\\
a_{m1}&a_{m2}&\cdots&a_{mn}
\end{bmatrix}$$

称作 $m\times n$ 矩阵，记作 $\bm A=(a_{ij})_{m\times n}$ ，其中 $a_{ij}$ 是矩阵第 $i$ 行第 $j$ 列的元素，称作 $(i,j)$ 元，元素为实数的矩阵称作**实矩阵**，元素为复数的矩阵称作**复矩阵**，两个矩阵行数列数相同则称为**同型矩阵**，同型矩阵对应元素相同则称作相等矩阵。

$m\times n$ 个元素全为零的矩阵称作**零矩阵**，记作 $\bm O$ 。

主对角线元素全为1的矩阵称作**单位矩阵**，记作 $\bm I$ 或 $\bm E$ ：

$$\bm I=\begin{bmatrix}
1&0&\cdots&0\\
0&1&\cdots&0\\
\vdots&\vdots&&\vdots\\
0&0&\cdots&1
\end{bmatrix}$$

当 $m=1$ 时，称 $\bm A_{m\times n}$ 为行矩阵或行向量；
当 $n=1$ 时，称 $\bm A_{m\times n}$ 为列矩阵或列向量；
当 $m=n$ 时，称 $\bm A$ 为 $n$ 阶方阵，简记为 $\bm A_n$ 。

### 矩阵基本运算

矩阵加法（仅限于同型矩阵）：

$$\bm A+\bm B=(a_{ij}+b_{ij})$$

负矩阵： $\bm A+(-\bm A)=\bm O$

矩阵加法满足交换律和结合律。

数乘矩阵：

1. $\lambda(\mu\bm A)=(\lambda\mu)\bm A$
2. $(\mu+\lambda)\bm A=\mu\bm A+\lambda\bm A$
3. $\lambda(\bm A+\bm B)=\lambda\bm A+\lambda\bm B$
4. $(-1)\bm A=-\bm A$

矩阵乘法：

$$\bm C=\bm A\bm B$$

只有当左乘矩阵 $\bm A$ 的列数等于右乘矩阵 $\bm B$ 的行数时，矩阵才能相乘，所得矩阵 $\bm C$ 的行数与 $\bm A$ 的行数一致，列数与 $\bm B$ 的列数一致。

对乘加法则： $\bm C$ 的任一元素就等于这个元素所在行对应于 $\bm A$ 的行向量和这个元素所在列对应于 $\bm B$ 的列向量的点乘：

$$c_{ij}=\sum_{k=1}^na_{ik}b_{kj}\quad(i=1,2,\cdots,m;j=1,2,\cdots,p)$$

矩阵乘法满足结合律和分配律，但不满足交换律。

任何矩阵和单位矩阵相乘都等于其本身。

矩阵的幂：

1. $\bm A^k\bm A^l=\bm A^{k+l}$
2. $(\bm A^k)^l=\bm A^{kl}$

$(\bm{AB})^k=\bm A^k\bm B^k$ 不一定成立。

矩阵转置：

矩阵转置就是将矩阵每一元素的行列位置互换：

$$(a_{ij})^T=(a_{ji})$$

1. $(\bm A^T)^T=\bm A$
2. $(\bm A+\bm B)^T=\bm A^T+\bm B^T$
3. $(\lambda\bm A)^T=\lambda\bm A^T$
4. $(\bm A\bm B)^T=\bm B^T\bm A^T$

### 矩阵的分块运算

$$\bm A=\begin{bmatrix}
\bm A_{11}&\bm A_{12}&\cdots&\bm A_{1t}\\
\bm A_{21}&\bm A_{22}&\cdots&\bm A_{2t}\\
\vdots&\vdots&&\vdots\\
\bm A_{s1}&\bm A_{s2}&\cdots&\bm A_{st}
\end{bmatrix}$$

分块加法运算（仅限于分块方法相同的矩阵）：

$$\bm A+\bm B=\begin{bmatrix}
\bm A_{11}+\bm B_{11}&\bm A_{12}+\bm B_{12}&\cdots&\bm A_{1t}+\bm B_{1t}\\
\bm A_{21}+\bm B_{21}&\bm A_{22}+\bm B_{22}&\cdots&\bm A_{2t}+\bm B_{2t}\\
\vdots&\vdots&&\vdots\\
\bm A_{s1}+\bm B_{s1}&\bm A_{s2}+\bm B_{s2}&\cdots&\bm A_{st}+\bm B_{st}
\end{bmatrix}$$

分块数乘运算：

$$\lambda\bm A=\begin{bmatrix}
\lambda\bm A_{11}&\lambda\bm A_{12}&\cdots&\lambda\bm A_{1t}\\
\lambda\bm A_{21}&\lambda\bm A_{22}&\cdots&\lambda\bm A_{2t}\\
\vdots&\vdots&&\vdots\\
\lambda\bm A_{s1}&\lambda\bm A_{s2}&\cdots&\lambda\bm A_{st}
\end{bmatrix}$$

分块乘法运算（对 $\bm A$ 列的分法和对 $\bm B$ 行的分法一致）：

$$\bm A\bm B=\begin{bmatrix}
\bm C_{11}&\bm C_{12}&\cdots&\bm C_{1r}\\
\bm C_{21}&\bm C_{22}&\cdots&\bm C_{2r}\\
\vdots&\vdots&&\vdots\\
\bm C_{s1}&\bm C_{s2}&\cdots&\bm C_{sr}
\end{bmatrix}$$

$$\bm C_{ij}=\sum_{k=1}^t\bm A_{ik}\bm B_{kj}\quad(i=1,2,\cdots,s;j=1,2,\cdots,r)$$

分块矩阵转置：

$$\bm A^T=\begin{bmatrix}
\bm A_{11}^T&\bm A_{21}^T&\cdots&\bm A_{s1}^T\\
\bm A_{12}^T&\bm A_{22}^T&\cdots&\bm A_{s2}^T\\
\vdots&\vdots&&\vdots\\
\bm A_{1t}^T&\bm A_{2t}^T&\cdots&\bm A_{st}^T
\end{bmatrix}$$

### 特殊矩阵

> 以下讨论的特殊矩阵均为方阵。

对角矩阵：

$$\bm\Lambda=\begin{bmatrix}\lambda_1\\&\lambda_2\\&&\ddots&\\&&&\lambda_n\end{bmatrix}$$

简记为 $\bm\Lambda={\rm diag}(\lambda_1,\lambda_2,\cdots,\lambda_n)$

对角矩阵的乘积和幂比较特殊：

$$\bm{AB}=\bm{BA}=\begin{bmatrix}a_1b_1\\&a_2b_2\\&&\ddots&\\&&&a_nb_n\end{bmatrix}$$

$$\bm\Lambda^k=\begin{bmatrix}\lambda_1^k\\&\lambda_2^k\\&&\ddots&\\&&&\lambda_n^k\end{bmatrix}$$

标量矩阵（对角矩阵的特殊情况）：

$$\bm A=\begin{bmatrix}a\\&a\\&&\ddots&\\&&&a\end{bmatrix}$$

上三角形矩阵：

$$\begin{bmatrix}
a_{11}&a_{12}&\cdots&a_{1n}\\
0&a_{22}&\cdots&a_{2n}\\
\vdots&\vdots&&\vdots\\
0&0&\cdots&a_{mn}
\end{bmatrix}$$

下三角形矩阵：

$$\begin{bmatrix}
a_{11}&0&\cdots&0\\
a_{21}&a_{22}&\cdots&0\\
\vdots&\vdots&&\vdots\\
a_{m1}&a_{m2}&\cdots&a_{mn}
\end{bmatrix}$$

上三角矩阵和下三角矩阵可以通过转置互相转换。

对于 $n$ 阶上（下）三角形矩阵 $\bm A,\bm B$ ，矩阵乘积 $\bm{AB}$ （或 $\bm{BA}$ ）的主对角线元素刚好就是 $\bm A,\bm B$ 相应主对角线元素的乘积：

$$\bm{AB}=\begin{bmatrix}a_1b_1&?&?&?\\?&a_2b_2&?&?\\\vdots&\vdots&\ddots&\vdots\\?&?&?&a_nb_n\end{bmatrix}$$

对称矩阵：

对阵矩阵中关于主对角线对称的两个元素相等：

$$a_{ij}=a_{ji}$$

对称矩阵转置，矩阵不发生改变： $\bm A^T=\bm A$

反称矩阵：

反称矩阵中关于主对角线对称的两个元素相反，并且主对角线上的元素均为零：

$$a_{ij}=-a_{ji}$$

反称矩阵转置，矩阵中的元素取其相反数： $\bm A^T=-\bm A$

> 任何方阵均可以表示为一个对称矩阵和一个反称矩阵之和。

分块对角矩阵：

一个分块矩阵，其主对角线上的子块全是方阵（阶数可以不同），其余子块均为零矩阵。

分块对角矩阵的性质和对角矩阵的性质类似。

### 初等变换和初等矩阵

为了解释矩阵的初等变换，我们需要引入**同解方程组**的概念。考虑一个线性方程组，以下三种操作不会影响方程组最后的解：

1. 用一个不等于零的数去乘某个方程。
2. 用一个数去乘某个方程后加到另一个方程上去。
3. 交换两个方程的位置。

这些操作就被称为线性方程组的**初等变换（Elementary transformation）**，经过初等变换后得到的新方程组和原来的方程组互为同解方程组。

同样的，对于矩阵而言，我们有以下三种**初等行变换**：

1. 倍法变换：用一个非零的数乘矩阵的某行。
2. 消法变换：用一个数乘矩阵的某行后再加到另一行上去，
3. 换法变换：交换矩阵的两行。

矩阵的初等行变换和初等列变换，统称为矩阵的初等变换。

如果矩阵 $\bm A$ 经过有限次初等变换变成矩阵 $\bm B$ ，则称矩阵 $\bm A,\bm B$ **等价**，记作 $\bm A\cong\bm B$ 。

矩阵之间的等价关系具有如下性质：

1. 自反性： $\bm A\cong\bm A$
2. 对称性： 若 $\bm A\cong\bm B$ ，则 $\bm B\cong\bm A$
3. 传递性： 若 $\bm A\cong\bm B,\bm B\cong\bm C$ ，则 $\bm A\cong\bm C$

**初等矩阵：**

对单位矩阵 $\bm I$ 施加一次初等变换得到的矩阵称为初等矩阵。

用初等矩阵左乘 $\bm A$ ，相当于对 $\bm A$ 进行对应的初等行变换；用初等矩阵右乘 $\bm A$ ，相当于对 $\bm A$ 进行对应的初等列变换。

初等倍法矩阵：

$$\bm P(i[k])=\begin{bmatrix}1\\&\ddots\\&&1\\&&&k\\&&&&1\\&&&&&\ddots\\&&&&&&1\end{bmatrix}$$

初等消法矩阵：

$$\bm P(i,j[k])=\begin{bmatrix}1\\&\ddots\\&&1&\cdots&k\\&&&\ddots&\vdots\\&&&&1\\&&&&&\ddots\\&&&&&&1\end{bmatrix}$$

初等换法矩阵：

$$\bm P(i,j)=\begin{bmatrix}1\\&\ddots\\&&0&\cdots&1\\&&\vdots&&\vdots\\&&1&\cdots&0\\&&&&&\ddots\\&&&&&&1\end{bmatrix}$$

**标准形矩阵：**

任何一个矩阵 $\bm A_{m\times n}$ 必能经过有限次初等变换化为如下形式：

$$\bm G=\begin{bmatrix}\bm I_r&\bm O\\\bm O&\bm O\end{bmatrix}=\begin{bmatrix}1\\&\ddots\\&&1\\&&&0&\cdots&0\\&&&\vdots&&\vdots\\&&&0&\cdots&0\end{bmatrix}$$

其中 $\bm I_r$ 的行数为 $r$ ，则 $0\leq r\leq\min\{m,n\}$ ， $\bm G$ 称为矩阵 $\bm A$ 在初等变换下的标准形，简称标准形矩阵。

在将矩阵变换为标准形的时候，我们会同时用到初等行变换和初等列变换，但大多数时候我们只会使用初等行变换，将矩阵变换为**行阶梯形矩阵**，它的特点是：

1. 矩阵的所有元素全为0的行（如果存在的话）都集中在矩阵的最下面；
2. 每行左起第一个非零元素（称为首非零元）的下方元素全为0。

形如：

$$\begin{bmatrix}
c_{11}&c_{12}&\cdots&c_{1r}&c_{1r+1}&\cdots&c_{1n}\\
0&c_{22}&\cdots&c_{2r}&c_{2r+1}&\cdots&c_{2n}\\
\vdots&\vdots&&\vdots&\vdots&&\vdots\\
0&0&\cdots&c_{rr}&c_{rr+1}&\cdots&c_{rn}\\
0&0&\cdots&0&0&\cdots&0\\
\vdots&\vdots&&\vdots&\vdots&&\vdots\\
0&0&\cdots&0&0&\cdots&0\\
\end{bmatrix}$$

行阶梯形任能继续化简为**行最简形矩阵**：

$$\begin{bmatrix}
1&\cdots&0&c_{11}&\cdots&c_{1n}\\
\vdots&&\vdots&\vdots&&\vdots\\
0&\cdots&1&c_{r1}&\cdots&c_{rn}\\
0&\cdots&0&0&\cdots&0\\
\vdots&&\vdots&\vdots&&\vdots\\
0&\cdots&0&0&\cdots&0\\
\end{bmatrix}$$

显然，行最简形矩阵只要再作适当的初等列变换，就能化为标准形矩阵。

## 行列式（Determinant）

行列式是一种对于方阵的运算，其运算结果是一个数，设 $n$ 阶方阵 $\bm A=(a_{ij})$ ，称

$$\begin{vmatrix}
a_{11}&a_{12}&\cdots&a_{1n}\\
a_{21}&a_{22}&\cdots&a_{2n}\\
\vdots&\vdots&&\vdots\\
a_{n1}&a_{n2}&\cdots&a_{nn}
\end{vmatrix}$$

为**方阵 $\bm A$ 的行列式**，记作 $|\bm A|$ 或 $\det A$ 。

下面，我们主要研究行列式的计算方式及相关性质。

### 全排列和逆序数

