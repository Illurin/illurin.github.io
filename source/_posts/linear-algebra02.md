---
title: 矩阵代数（一）：行列式与矩阵求逆
date: 2022-12-2 8:37:00
tags:
	- 大学数学
	- 代数学
categories: 线性代数
top_img: /images/gallery/arcaea_0.jpg
cover: /images/gallery/arcaea_0.jpg
katex: true
description: 在本文中，我们主要研究矩阵的基本概念，行列式的概念和计算，矩阵的逆以及如何在矩阵不可逆的情况下求广义逆矩阵。
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

**对角线计算法则：**

对角线法则适合于计算二阶或三阶这些低阶的行列式：

对于二阶行列式：

$$\begin{vmatrix}a_{11}&a_{12}\\a_{21}&a_{22}\end{vmatrix}=a_{11}a_{22}-a_{12}a_{21}$$

对于三阶行列式：

![](/images/articles/linear-algebra02/image_0.png)

$$\begin{vmatrix}a_{11}&a_{12}&a_{13}\\a_{21}&a_{22}&a_{23}\\a_{31}&a_{32}&a_{33}\end{vmatrix}=\begin{matrix}\ \\\quad a_{11}a_{22}a_{33}+a_{12}a_{23}a_{31}+a_{13}a_{21}a_{32}\\-\ a_{13}a_{22}a_{31}-a_{12}a_{21}a_{33}-a_{11}a_{23}a_{32}\end{matrix}$$

对于高阶行列式而言，我们需要寻找更加通用的解法，这就引出了接下来的内容。

### 全排列与逆序数

$n$ 个自然数 $1,2,\cdots,n$ 按照任何一种次序排成的有序数组 $j_1j_2\cdots j_n$ 称为一个 $n$ 级**排列（Permutation）**，显然，不重复的 $n$ 级排列共有 $n!$ 个。

若规定从小到大为自然数的标准顺序，则当两个数之间不满足这个顺序时，就称作**逆序**，一个 $n$ 级排列所有逆序的总和称为**逆序数（Inversion number）**，记作 $\tau(j_1j_2\cdots j_n)$ 。

逆序数的计算方式：对于排列 $j_1j_2\cdots j_n$ ，自 $j_1$ 开始直到 $j_{n-1}$ ，逐个计算每个元素的右边比它大的元素的个数 $k_1,k_2,\cdots,k_{n-1}$ ，则该排列的逆序数为：

$$\tau(j_1j_2\cdots j_n)=k_1+k_2+\cdots+k_{n-1}$$

我们称逆序数为奇数的排列为**奇排列**，逆序数为偶数的排列为**偶排列**，排列中任何两个数的位置对换必然会改变排列的奇偶性。

借助排列的概念，可以定义 $n$ 行列式 $|\bm A|$ 的通式：

$$D=|\bm A|=\sum_{j_1j_2\cdots j_n}(-1)^{\tau(j_1j_2\cdots j_n)}a_{1j_1}a_{2j_2}\cdots a_{nj_n}$$

或

$$D=|\bm A|=\sum_{i_1i_2\cdots i_n}(-1)^{\tau(i_1i_2\cdots i_n)}a_{i_11}a_{i_22}\cdots a_{i_nn}$$

此处的 $\sum\limits_{j_1j_2\cdots j_n}$ 表示对所有不同的 $n$ 阶排列求和，一共是 $n!$ 项。

乘积项 $a_{1j_1}a_{2j_2}\cdots a_{nj_n}$ 称为行列式的一个**均匀分布项**，简称均布项；
$(-1)^{\tau(j_1j_2\cdots j_n)}$ 称为该均布项的**符号因子**，其正负性取决于排列的奇偶性。

现在我们已经可以计算高阶行列式的值了，但排列法还是过于复杂，之后我们会了解一个更加常用且更易于理解的方法。

### 方阵行列式的性质

1. 分行/列可加性：

$$\begin{vmatrix}
a_{11}&a_{12}&\cdots&a_{1n}\\
\vdots&\vdots&&\vdots\\
b_1+c_1&b_2+c_2&\cdots&b_n+c_n\\
\vdots&\vdots&&\vdots\\
a_{n1}&a_{n2}&\cdots&a_{nn}
\end{vmatrix}\\
=\begin{vmatrix}
a_{11}&a_{12}&\cdots&a_{1n}\\
\vdots&\vdots&&\vdots\\
b_1&b_2&\cdots&b_n\\
\vdots&\vdots&&\vdots\\
a_{n1}&a_{n2}&\cdots&a_{nn}
\end{vmatrix}+\begin{vmatrix}
a_{11}&a_{12}&\cdots&a_{1n}\\
\vdots&\vdots&&\vdots\\
c_1&c_2&\cdots&c_n\\
\vdots&\vdots&&\vdots\\
a_{n1}&a_{n2}&\cdots&a_{nn}
\end{vmatrix}$$

2. 转置不变：$|\bm A|=|\bm A^T|$
<br>

3. 若方阵 $\bm A$ 的第 $i$ 行（第 $j$ 列）乘 $k$ 倍所得得矩阵为 $\bm B$ ，则 $|\bm B|=k|\bm A|$ ：

$$\begin{vmatrix}
a_{11}&a_{12}&\cdots&a_{1n}\\
\vdots&\vdots&&\vdots\\
kb_1&kb_2&\cdots&kb_n\\
\vdots&\vdots&&\vdots\\
a_{n1}&a_{n2}&\cdots&a_{nn}
\end{vmatrix}=k\begin{vmatrix}
a_{11}&a_{12}&\cdots&a_{1n}\\
\vdots&\vdots&&\vdots\\
b_1&b_2&\cdots&b_n\\
\vdots&\vdots&&\vdots\\
a_{n1}&a_{n2}&\cdots&a_{nn}
\end{vmatrix}$$

4. 若方阵 $\bm A$ 经过一次换法变换化为 $\bm B$ ，则 $|\bm B|=-|\bm A|$ 。
推论：若行列式任意两行/列相同，则行列式为0。
推论：若行列式任意两行/列对应元素成比例，则行列式为0。
<br>

5. 消法变换不改变行列式的值，即行列式的任意行/列可以乘一个数加到另外一行/列上。

**方阵行列式运算规律：**

设 $\bm A,\bm B$ 为 $n$ 阶方阵， $\lambda$ 为常数， $m$ 为正整数。

1. $|\lambda\bm A|=\lambda|\bm A|$
2. $|\bm{AB}|=|\bm A||\bm B|$
3. $|\bm A^m|=|\bm A|^m$
4. $|\bm I|=1$

### 拉普拉斯展开（Laplace expansion）

**子式：** 在 $n$ 阶方阵行列式 $|\bm A|$ 中，取部分行列相交形成的阶数 $<n$ 的行列式，称作行列式 $|\bm A|$ 的子式。

**余子式（Minor）：** 把元素 $a_{ij}$ 所在的行列删除后，留下来的 $n-1$ 阶行列式叫做元素 $a_{ij}$ 的余子式，记作 $M_{ij}$ ；把 $k$ 阶子式 $N$ 所在的行列删除后，留下来的 $n-k$ 阶行列式叫做子式 $N$ 的余子式，记作 $M$ 。

**代数余子式（Cofactor）：** 

$$A_{ij}=(-1)^{i+j}M_{ij}$$

叫做元素 $a_{ij}$ 的代数余子式；

$$A=(-1)^{i_1+\cdots+i_k+j_1+\cdots+j_k}M$$

叫做子式 $N$ 的代数余子式。（其中 $i$ 和 $j$ 代表子式所处的行和列的序数）

**定理：** 对于 $|\bm A|$ ，其任意一行/列的所有元素与另一行/列对应元素的代数余子式乘积之和等于零，即当 $i\neq j$ 时，有：

$$a_{i1}A_{j1}+a_{i2}A_{j2}+\cdots+a_{in}A_{jn}=0\\
a_{1i}A_{1j}+a_{2i}A_{2j}+\cdots+a_{ni}A_{nj}=0$$

**拉普拉斯定理：** 设 $D$ 是 $n$ 阶行列式，在 $D$ 中取定某 $k$ 行 $(1\leq k\leq n-1)$ ，则含与此 $k$ 行中的所有 $k$ 阶子式与其代数余子式的乘积之和等于 $D$ 。

运用拉普拉斯定理，可以将行列式按任意行展开：

$$|\bm A|=a_{i1}A_{i1}+a_{i2}A_{i2}+\cdots+a_{in}A_{in}\qquad i=1,2,\cdots,n$$

同理，也可以按任意列展开：

$$|\bm A|=a_{1j}A_{1j}+a_{2j}A_{2j}+\cdots+a_{nj}A_{nj}\qquad j=1,2,\cdots,n$$

**例：** 计算如下行列式

$$D_{2n}=\begin{vmatrix}a&&&&&&&b\\&a&&&&&b\\&&\ddots&&&⋰\\&&&a&b\\&&&c&d\\&&⋰&&&\ddots\\&c&&&&&d\\c&&&&&&&d\end{vmatrix}$$

解：按第一行展开，可以得：

$$D_{2n}=a\begin{vmatrix}a&&&&&b&0\\&\ddots&&&⋰&&\vdots\\&&a&b&&&\vdots\\&&c&d&&&\vdots\\&⋰&&&\ddots&&\vdots\\c&&&&&d&0\\0&\cdots&\cdots&\cdots&\cdots&0&d\end{vmatrix}+b(-1)^{1+2n}\begin{vmatrix}0&a&&&&&b&0\\\vdots&&\ddots&&&⋰&&\vdots\\\vdots&&&a&b&&&\vdots\\\vdots&&&c&d&&&\vdots\\\vdots&&⋰&&&\ddots&&\vdots\\0&c&&&&&d\\c
&0&\cdots&\cdots&\cdots&\cdots&0\end{vmatrix}$$

$$\begin{aligned}D_{2n}&=adD_{2(n-1)}+(-1)^{1+2n}(-1)^{2n-1+1}bcD_{2(n-1)}\\&=(ad-bc)D_{2(n-1)}\end{aligned}$$

以此作为递推公式，可得：

$$\begin{aligned}D_{2n}&=(ad-bc)D_{2(n-1)}\\
&=(ad-bc)^2D_{2(n-2)}\\
&=(ad-bc)^{n-1}D_2\\
&=(ad-bc)^{n-1}\begin{vmatrix}a&b\\c&d\end{vmatrix}\\
&=(ad-bc)^n\end{aligned}$$

**范德蒙（Vandermonde）行列式：**

$$D_n=\begin{vmatrix}1&1&\cdots&1\\x_1&x_2&\cdots&x_n\\x_1^2&x_2^2&\cdots&x_n^2\\\vdots&\vdots&&\vdots\\x_1^{n-1}&x_2^{n-1}&\cdots&x_n^{n-1}\end{vmatrix}=\prod_{1\leq i<j\leq n}(x_j-x_i)$$

其中 $\prod$ 表示满足 $1\leq i<j\leq n$ 的所有可能的 $x_j-x_i$ 进行连乘。

归纳法证明：当 $n=2$ 时

$$D_2=\begin{vmatrix}1&1\\x_1&x_2\end{vmatrix}=x_2-x_1=\prod_{1\leq i<j\leq 2}(x_j-x_i)$$

满足该结论。假设该结论对 $n-1$ 阶范德蒙行列式成立，即

$$D_{n-1}=\begin{vmatrix}1&1&\cdots&1\\x_2&x_3&\cdots&x_n\\x_2^2&x_3^2&\cdots&x_n^2\\\vdots&\vdots&&\vdots\\x_2^{n-2}&x_3^{n-2}&\cdots&x_n^{n-2}\end{vmatrix}=\prod_{2\leq i<j\leq n}(x_j-x_i)$$

> 在 $D_{n-1}$ 中， $i=1$ 的情况被去除了。

证该结论对 $n$ 阶行列式成立，将 $D_n$ 的第 $n-1$ 行的 $-x_1$ 倍加到第 $n$ 行，将第 $n-2$ 行的 $-x_1$ 倍加到第 $n-1$ 行，如此作下去，直到第1行的 $-x_1$ 倍加到第2行，得：

$$D_n=\begin{vmatrix}0&1&\cdots&1\\0&x_2-x_1&\cdots&x_n-x_1\\0&x_2(x_2-x_1)&\cdots&x_n(x_n-x_1)\\\vdots&\vdots&&\vdots\\0&x_2^{n-2}(x_2-x_1)&\cdots&x_n^{n-2}(x_n-x_1)\end{vmatrix}$$

按第一列展开得：

$$D_n=\begin{vmatrix}x_2-x_1&\cdots&x_n-x_1\\x_2(x_2-x_1)&\cdots&x_n(x_n-x_1)\\\vdots&&\vdots\\x_2^{n-2}(x_2-x_1)&\cdots&x_n^{n-2}(x_n-x_1)\end{vmatrix}$$

由行列式的性质可得：

$$\begin{aligned}D_n&=(x_2-x_1)(x_3-x_1)\cdots(x_n-x_1)\begin{vmatrix}1&1&\cdots&1\\x_2&x_3&\cdots&x_n\\\vdots&\vdots&&\vdots\\x_2^{n-2}&x_3^{n-2}&\cdots&x_n^{n-2}\end{vmatrix}\\
&=(x_2-x_1)(x_3-x_1)\cdots(x_n-x_1)\prod_{2\leq i<j\leq n}(x_j-x_i)\\
&=\prod_{1\leq i<j\leq n}(x_j-x_i)\end{aligned}$$

> 此处用 $(x_2-x_1)(x_3-x_1)\cdots(x_n-x_1)$ 连乘补全了 $i=1$ 的情况。

根据数学归纳法，可证得范德蒙行列式结论在 $n\geq 2$ 时成立。

**AB型行列式：**

除了对角线是 $b$ 其余全是 $a$ 的行列式：

$$\begin{vmatrix}
b&a&\cdots&a\\
a&b&\cdots&a\\
\vdots&\vdots&&\vdots\\
a&a&\cdots&b
\end{vmatrix}$$

将除第1行以外每一行都加到第1行上，得：

$$\begin{vmatrix}
b+(n-1)a&b+(n-1)a&\cdots&b+(n-1)a\\
a&b&\cdots&a\\
\vdots&\vdots&&\vdots\\
a&a&\cdots&b
\end{vmatrix}$$

由行列式性质可转化为：

$$[b+(n-1)a]\begin{vmatrix}
1&1&\cdots&1\\
a&b&\cdots&a\\
\vdots&\vdots&&\vdots\\
a&a&\cdots&b
\end{vmatrix}$$

将第1行乘 $(-a)$ 加到下面各行上，得：

$$[b+(n-1)a]\begin{vmatrix}
1&1&\cdots&1\\
0&b-a&\cdots&0\\
\vdots&\vdots&&\vdots\\
0&0&\cdots&b-a
\end{vmatrix}=[b+(n-1)a]\begin{vmatrix}
b-a&\cdots&0\\
\vdots&&\vdots\\
0&\cdots&b-a
\end{vmatrix}$$

可得AB型行列式通式：

$$\begin{vmatrix}
b+(n-1)a&b+(n-1)a&\cdots&b+(n-1)a\\
a&b&\cdots&a\\
\vdots&\vdots&&\vdots\\
a&a&\cdots&b
\end{vmatrix}=[b+(n-1)a](b-a)^{n-1}$$

**加边法：**

加边法是对拉普拉斯展开的逆用，用加边法可以求如下行列式：

$$\begin{vmatrix}
x_1&a_2&\cdots&a_n\\
a_1&x_2&\cdots&a_n\\
\vdots&\vdots&&\vdots\\
a_1&a_2&\cdots&x_n
\end{vmatrix}$$

在行列式左侧加边，可将原式转化为：

$$\begin{vmatrix}
1&-a_1&-a_2&\cdots&-a_n\\
0&x_1&a_2&\cdots&a_n\\
0&a_1&x_2&\cdots&a_n\\
\vdots&\vdots&\vdots&&\vdots\\
0&a_1&a_2&\cdots&x_n
\end{vmatrix}$$

将第1行加到下面各行上，得：

$$\begin{vmatrix}
1&-a_1&-a_2&\cdots&-a_n\\
1&x_1-a_1&0&\cdots&0\\
1&0&x_2-a_2&\cdots&0\\
\vdots&\vdots&\vdots&&\vdots\\
1&0&0&\cdots&x_n-a_n
\end{vmatrix}$$

这种形状的行列式被称作“爪型行列式”，求解爪型行列式：

$$\prod_{i=1}^n(x_i-a_i)\begin{vmatrix}
1&-a_1&-a_2&\cdots&-a_n\\
\dfrac{1}{x_1-a_1}&1&0&\cdots&0\\
\dfrac{1}{x_2-a_2}&0&1&\cdots&0\\
\vdots&\vdots&\vdots&&\vdots\\
\dfrac{1}{x_n-a_n}&0&0&\cdots&1
\end{vmatrix}$$

各行乘 $(-a_i)$ 加到第1行：

$$\prod_{i=1}^n(x_i-a_i)\begin{vmatrix}
1+\sum\limits_{i=1}^n\dfrac{a_i}{x_i-a_i}&0&0&\cdots&0\\
\dfrac{1}{x_1-a_1}&1&0&\cdots&0\\
\dfrac{1}{x_2-a_2}&0&1&\cdots&0\\
\vdots&\vdots&\vdots&&\vdots\\
\dfrac{1}{x_n-a_n}&0&0&\cdots&1
\end{vmatrix}=\prod_{i=1}^n(x_i-a_i)\left(1+\sum_{i=1}^n\frac{a_i}{x_i-a_i}\right)$$

## 矩阵的逆

设 $\bm A$ 为 $n$ 阶方阵，若存在 $n$ 阶方阵 $\bm B$ ，使得

$$\bm{AB}=\bm{BA}=\bm I$$

则称 $\bm A$ 可逆，且 $\bm B$ 是 $\bm A$ 的逆矩阵，简称 $\bm A$ 的**逆（Inverse）**，记作 $\bm B=\bm A^{-1}$ 。

> 一般而言，我们只讨论方阵的逆。

可逆矩阵又称**非奇异矩阵（Nonsingular matrix）**，不可逆矩阵又称**奇异矩阵（Singular matrix）**。

> 易证初等矩阵都是可逆矩阵：
> 1. $\bm P(i[k])^{-1}=\bm P(i[\frac{1}{k}])$
> 2. $\bm P(i,j[k])^{-1}=\bm P(i,j[-k])$
> 3. $\bm P(i,j)^{-1}=\bm P(i,j)$

**可逆矩阵基本性质：**

1. 可逆矩阵的逆是唯一的。
2. 若 $\bm A$ 可逆，则 $(\bm A^{-1})^{-1}=\bm A$ 。
3. 若 $\bm A$ 可逆，数 $\lambda\neq 0$ ，则 $\lambda\bm A$ 可逆，且 $(\lambda\bm A)^{-1}=\frac{1}{\lambda}\bm A^{-1}$ 。
4. 若 $\bm A$ 可逆，则 $\bm A^T$ 可逆，且 $(\bm A^T)^{-1}=(\bm A^{-1})^T$ 。
5. 若 $n$ 阶方阵 $\bm A,\bm B$ 皆可逆，则 $\bm{AB}$ 可逆，且 $(\bm{AB})^{-1}=\bm B^{-1}\bm A^{-1}$ 。
推广：若 $n$ 阶方阵 $\bm A_1,\bm A_2,\cdots,\bm A_s$ 皆可逆，则它们的乘积 $\bm A_1\bm A_2\cdots\bm A_s$ 也可逆，且

$$(\bm A_1\bm A_2\cdots\bm A_s )^{-1}=\bm A_s^{-1}\cdots\bm A_2^{-1}\bm A_1^{-1}$$

6. 规定 $\bm A^{-m}=(\bm A^m)^{-1}=(\bm A^{-1})^m$ 。
7. 可逆矩阵的行列式 $|\bm A^{-1}|=\dfrac{1}{|\bm A|}$

### 伴随矩阵求逆矩阵

对 $n$ 阶方阵每一个元素求其代数余子式 $A_{ij}$ ，填写在原来的位置，然后再进行转置，可以写出如下方阵：

$$\begin{bmatrix}
A_{11}&A_{21}&\cdots&A_{n1}\\
A_{12}&A_{22}&\cdots&A_{n2}\\
\vdots&\vdots&&\vdots\\
A_{1n}&A_{2n}&\cdots&A_{nn}
\end{bmatrix}$$

这个方阵就被称作 $\bm A$ 的**伴随矩阵（Adjugate matrix，the adjoint of a matrix）**，记作 $\bm A^*$ 或 $\text{adj}\ \bm A$。

由代数余子式定理我们可以推出，矩阵与其伴随矩阵乘积的关系：

$$\bm{AA}^*=\bm A^*\bm A=|\bm A|\bm I$$

当 $\bm A$ 可逆时，存在逆矩阵 $\bm A^{-1}$ 使得 $\bm{AA}^{-1}=\bm I$ ，两边取行列式，得

$$|\bm A||\bm A^{-1}|=1$$

因此必然有 $|\bm A|\neq 0$ 。又因为 $\bm{AA}^*=|\bm A|\bm I$ ，可得

$$\bm A^{-1}=\frac{1}{|\bm A|}\bm A^*$$

综上，我们找到了用伴随矩阵求逆矩阵的方法。

**矩阵可逆定理：**

1. 方阵 $\bm A$ 可逆的充要条件是 $|\bm A|\neq 0$ 。
2. 对于 $n$ 阶矩阵 $\bm A,\bm B$ ，只要有 $\bm{AB}=\bm I$ ，则矩阵 $\bm A,\bm B$ 皆可逆且互为逆。
<br>

3. 方阵 $\bm A$ 可逆的充要条件是 $\bm A$ 可以经过有限次初等变换化为单位矩阵。
4. 方阵 $\bm A$ 可逆的充要条件是 $\bm A$ 可以表示为有限个初等矩阵的乘积。
5. 方阵 $\bm A$ 可逆的充要条件是可以只经过初等行变换化为单位矩阵。

借助矩阵的逆和初等变换的关系，可以用初等变换求逆：

$$\begin{bmatrix}\bm A&\bm I\end{bmatrix}\xrightarrow{Elementary}\begin{bmatrix}\bm I&\bm A^{-1}\end{bmatrix}$$

**伴随矩阵基本性质：**

1. $|\bm A^*|=||\bm A|\bm A^{-1}|=\dfrac{|\bm A|^{n}}{|\bm A|}=|\bm A|^{n-1}$
2. $(\bm A^*)^{-1}=(|\bm A|\bm A^{-1})^{-1}=\dfrac{\bm A}{|\bm A|}$
3. $(\bm A^*)^T=(|\bm A|\bm A^{-1})^T=|\bm A^T|(A^T)^{-1}=(\bm A^T)^*$
4. $(k\bm A)^*=|k\bm A|(k\bm A)^{-1}=k^n|\bm A|\dfrac{1}{k}\bm A^{-1}=k^{n-1}\bm A^*$
5. $(\bm A^*)^*=|\bm A^*|(\bm A^*)^{-1}=||\bm A|\bm A^{-1}|(|\bm A|\bm A^{-1})^{-1}=|\bm A|^{n-1}\dfrac{\bm A}{|\bm A|}=|\bm A|^{n-2}\bm A$
6. $(\bm{AB})^*=|\bm{AB}|\bm{AB}^{-1}=|\bm A||\bm B|\bm B^{-1}\bm A^{-1}=|\bm B|\bm B^{-1}|\bm A|\bm A^{-1}=\bm B^*\bm A^*$

### 广义逆矩阵

**左逆和右逆：**

以上我们的求逆都是对于方阵而言的，这种逆被称作两侧逆，而非方阵则不拥有两侧逆，只能分情况讨论其左逆和右逆。

对于 $m\times n(m\neq n)$ 的矩阵：

当 $m>n$ 时，$\bm A^T\bm A$ 是一个 $n\times n$ 的方阵，则可以讨论 $\bm A^T\bm A$ 的逆，此时

$$(\bm A^T\bm A)^{-1}\bm A^T\bm A=\bm I$$

令 $\bm A_{left}^{-1}=(\bm A^T\bm A)^{-1}\bm A^T$ ，则

$$\bm A_{left}^{-1}\bm A=\bm I$$

称 $\bm A_{left}^{-1}$ 为 $\bm A$ 的左逆。

同理，当 $m<n$ 时，$\bm A\bm A^T$ 是一个 $m\times m$ 的方阵，则可以讨论 $\bm A\bm A^T$ 的逆，此时

$$\bm A\bm A^T(\bm A\bm A^T)^{-1}=\bm I$$

令 $\bm A_{right}^{-1}=\bm A^T(\bm A\bm A^T)^{-1}$ ，则

$$\bm A\bm A_{right}^{-1}=\bm I$$

称 $\bm A_{right}^{-1}$ 为 $\bm A$ 的右逆。

**伪逆矩阵：**

对于奇异矩阵，我们无法对其进行常规求逆，此时只能对其求**伪逆（Pseudo-inverse）**，记作 $\bm A^+$ ，此处不讲解其具体来由和定义，只简单提一下其求法。

$\bm A$ 的伪逆是对超定线性方程组 $\bm Ax=b$ 求其最小二乘解，定义为：

$$\bm A^+=\lim_{a\to\infty}(\bm A^T\bm A+a\bm I)^{-1}\bm A^T$$

对于实矩阵，可以用**奇异值分解法（Singular Vector Decomposite，SVD）** 求其伪逆：

$$\bm A=\bm U\bm W\bm V^T$$

![奇异值分解法](/images/articles/linear-algebra02/image_1.png)

其中

$$\bm{AA}^T=\bm U\begin{bmatrix}\bm D&0\\0&0\end{bmatrix}\bm U^T$$

$$\bm A^T\bm A=\bm V\begin{bmatrix}\bm D&0\\0&0\end{bmatrix}\bm V^T\\$$

用以下公式求伪逆：

$$\bm A^+=\bm V\bm D^+\bm U^T$$

伪逆矩阵的性质：

1. $\bm A\bm A^+\bm A=\bm A$
2. $\bm A^+\bm A\bm A^+=\bm A^+$
3. $\bm A\bm A^+=(\bm A\bm A^+)^T$
4. $\bm A^+\bm A=(\bm A^+\bm A)^T$