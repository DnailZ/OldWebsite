---
layout: post
title:  "矩阵秩性质的证明思路分析"
---

## 一、线性变换的观点


按照线性变换，矩阵有如下定义：

$$
\text{rank}A
    := \text{dim}\text{Im}{\scr{A}}
    =  \text{dim}\text{Ker}^\bot{\scr{A}}
$$

若定义 $${\scr{A}}U$$ 为对 $$U$$ 做线性变换 $${\scr{A}}​$$ 得到的空间，则可以用下面的式子描述维数的变化：

$$
\text{dim}{\scr{A}}U
=   \text{dim}
        U\cap
            \text{Ker}^\bot{\scr{A}}
$$

用上面的式子再加上维数定理，就可以解决不少问题了。

**1. (秩的乘法)** $$
    \text{rank}AB
\leq
    \text{min}\{
        \text{rank}A,
        \text{rank}B
    \}$$

**2. (Sylvester不等式)** $$
    \text{rank}AB
\geq
    \text{rank}A+
    \text{rank}B-
        n$$

**3. (Frobenius不等式)** $$
    \text{rank}ABC+
    \text{rank}B
\geq
    \text{rank}AB+
    \text{rank}BC$$

这三个式子有一个共同点，都非常像集合论(测度?)的公式，特别是第二个式子，看起来有一种容斥原理的感觉。而第三个式子可以用Venn图看出它成立。

![Octocat](https://dnailz.github.io/assets/images/Frobenius.png)

下面以最难(其实更适合用分块矩阵方法)的第三个式子的证明为例。

**证明：**

$$
    \text{rank}ABC
=   \text{dim}\text{Im}{\scr{ABC}}
=   \text{dim}{\scr{ABC}}V
=   \text{dim}{\scr{BC}}V\cap\text{Ker}^\bot{\scr{A}}
$$

由维数定理

$$
    \text{dim}{\scr{BC}}V\cap\text{Ker}^\bot{\scr{A}}
=   \text{rank}A+
    \text{rank}BC-
    \text{dim}\left({\scr{BC}}V+\text{Ker}^\bot{\scr{A}}\right)
$$

由$${\scr{BC}}V \subseteq{\scr{B}}V$$放缩

$$
    \text{rank}ABC
\geq
    \text{rank}A+
    \text{rank}BC-
    \text{dim}\left({\scr{B}}V+\text{Ker}^\bot{\scr{A}}\right)
$$

再用维数定理,即有

$$
    \text{rank}ABC
\geq
    \text{rank}BC-
    \text{rank}B+
    \text{rank}AB
$$

注：以上证明假设 $${\scr{A,B,C}}\in \text{Hom}(V,V)$$，即$$A$$、$$B$$、$$C$$为方阵，若不为方阵，可以把它用0补成方阵，不影响结果。

**4. (秩的加法)** $$
    \text{rank}\left(
        A+B
    \right)
\leq
    \text{rank}A+
    \text{rank}B$$

**5. (等号成立的一个充分条件)** $$
    AB=BA=O,
    \text{rank}A^2=
    \text{rank}A
\quad\Rightarrow\quad
    \text{rank}\left(
        A+B
    \right)=
    \text{rank}A+
    \text{rank}B$$

从线性变换角度解释4还是有点麻烦的，需要两步放缩：

$$
({\scr{A+B}})V\subseteq {\scr{A}}V+{\scr{B}}V,
\text{dim}{\scr{A}}V\cap{\scr{B}}V\geq0
$$

不过这给证明5提供了思路，要证$$
\text{rank}\left(
    A+B
\right)=
\text{rank}A+
\text{rank}B$$只需以下两个条件(第一个条件的等价性容易证明)

$$
({\scr{A+B}})V={\scr{A}}V+{\scr{B}}V
\Leftrightarrow
\text{Ker}A+\text{Ker}B=V,{\scr{A}}V\cap{\scr{B}}V=0
$$

下面给出5的证明。

**证明：**

由$$AB=BA=O,
\text{rank}A^2=
\text{rank}A$$有

$$
\text{Im}{\scr{A}}\subseteq\text{Ker}{\scr{B}},
\text{Im}{\scr{B}}\subseteq\text{Ker}{\scr{A}},
\text{Im}{\scr{A}}\cap\text{Ker}{\scr{A}}=0,
\text{Im}{\scr{A}}=\text{Im}{\scr{A^2}}
$$

1）第一个条件比较复杂（涉及到$$A$$和$$A^2$$的关系），用抽象符号难以分析，这时候，不妨舍弃线性空间的符号。

由$$\text{Im}{\scr{A}}=\text{Im}{\scr{A^2}}$$可设$$Ax=A^2y$$有

$$
A(y-Ax)=0
$$

观察到$$\text{Im}{\scr{A}}\subseteq\text{Ker}{\scr{B}}$$,$$Ax\in\text{Ker}{\scr{B}}$$，可任取 $$y$$ 必有 $$x$$ 使得$$y-Ax\in \text{Ker}{\scr{A}}$$ 即：

$$
V\subseteq\text{Ker}A+\text{Ker}B
$$

则第一个条件成立。

2）由$$\text{Im}{\scr{B}}\subseteq\text{Ker}{\scr{A}},
\text{Im}{\scr{A}}\cap\text{Ker}{\scr{A}}=0$$知第二个条件显然成立。

## 二、向量组与矩阵分解观点

**满秩分解：**

将矩阵表示为向量组的一个线性关系

$$
A=
(a_1,a_2,\ldots,a_n)=
\left(
(b_1,b_2,\ldots,b_r)c_1,
(b_1,b_2,\ldots,b_r)c_2
,\ldots\right)
=BC
$$

若$$A_{m\times n}$$则$$B_{m\times r}$$,$$C_{r\times n}$$($$B、C$$皆满秩)为$$A$$的满秩分解。

有$$r=\text{rank}A$$（若$$B、C$$不都满秩，则秩要小于$$r$$）

把$$B$$、$$C$$分别写成线性无关的向量组，可以写成外积的形式：

$$
A=
\begin{pmatrix}
    b_1 & b_2 &\ldots &b_r \\
\end{pmatrix}
\begin{pmatrix}
     c_1^T\\c_2^T\\ \vdots \\ c_r^T
\end{pmatrix}=
b_1c_1^T+b_2c_2^T+\ldots+b_rc_r^T
$$

这种情况下，想要 $$A$$ 的秩等于 $$r$$，只需要 $${b_1,\ldots,b_r}$$ 和 $${c_1,\ldots,c_r}$$都线性无关即可。

**相抵分解：**

若 $$A \in F^{m \times n}$$,$$r=\text{rank}A$$,有矩阵分解

$$
A=P
\begin{pmatrix}
I_{(r)} & O \\ O & O
\end{pmatrix}
Q
$$

其中$$P$$、$$Q$$为可逆方阵。

若对中间的标准型做满秩分解，

$$
    P\begin{pmatrix}
        I_{(r)} & O \\ O & O
    \end{pmatrix}Q
=   P
    \begin{pmatrix}
        I_{(r)} \\ O
    \end{pmatrix}
    \begin{pmatrix}
        I_{(r)} & O
    \end{pmatrix}
    Q
=   BC
$$

可以得到 $$A$$ 的满秩分解

以上两种相互等价的矩阵分解性质上比较好，可以比较简单地证明秩的一些性质。

**1. (秩的乘法)** $$
    \text{rank}AB
\leq
    \text{min}\{
        \text{rank}A,
        \text{rank}B
    \}$$

**4. (秩的加法)** $$
    \text{rank}\left(
        A+B
    \right)
\leq
    \text{rank}A+
    \text{rank}B$$

以上两个性质可以分别由矩阵的满秩分解和满秩分解的外积形式证得，具体证明略。

**6. (行秩等于列秩)** $$
    \text{rank}A
=   \text{rank}A^T$$

**7.（证明最小二乘法中的一个结论）**  $$
    \text{rank}A
=   \text{rank}A^TA$$

矩阵分解方法可以很好地解决转置矩阵的问题。
下面证明7。

**证明：**

先对 $$A$$ 作满秩分解

$$
    A^TA
=   \begin{pmatrix}
        c_1 & c_2 &\ldots &c_r \\
    \end{pmatrix}
    \begin{pmatrix}
        b_1^T\\b_2^T\\ \vdots \\ b_r^T
    \end{pmatrix}
    \begin{pmatrix}
        b_1 & b_2 &\ldots &b_r \\
    \end{pmatrix}
    \begin{pmatrix}
        c_1^T\\c_2^T\\ \vdots \\ c_r^T
    \end{pmatrix}
$$

注意分解后四个阵的中间两个，如果中间这两个阵从整体上来说是一个可逆方阵，那么7显然成立。

然后发现如果 $$b_1,b_2,\ldots,b_r$$ 相互正交，问题会非常简单。

对 $$
\begin{pmatrix}
    b_1 & b_2 &\ldots &b_r \\
\end{pmatrix}$$ 作施密特正交化，或者QR分解 ([**Thin QR Factorization**](https://en.wikipedia.org/wiki/QR_decomposition#Rectangular_matrix) *Matrix Computations* by Golub & Van Loan)。

$$
    \begin{pmatrix}
        b_1 & b_2 &\ldots &b_r \\
    \end{pmatrix}
=   QR\\
    \begin{pmatrix}
        b_1^T\\b_2^T\\ \vdots \\ b_r^T
    \end{pmatrix}
    \begin{pmatrix}
        b_1 & b_2 &\ldots &b_r \\
    \end{pmatrix}
=   R^TQ^TQR
=   R^TR
$$

$$R$$ 为上三角阵，$$R^TR$$ 可逆。

## 三、分块矩阵的观点

**基本结论：**
$$
    \text{rank}
    \begin{pmatrix}
    A & O \\ 
    O & B \\
    \end{pmatrix}
=   \text{rank}A +
    \text{rank}B
$$

$$
    \text{rank}
    \begin{pmatrix}
    A & O \\ 
    C & B \\
    \end{pmatrix}
\geq
    \text{rank}A +
    \text{rank}B
$$

$$
    A_1{\text{是 }}A{\text{ 的子矩阵}}
\Rightarrow
        \text{rank}A_1
    \leq
        \text{rank}A
$$


**8.** $$
    \text{rank}\left(
        P_1AQ_1+P_2BQ_2
    \right)
\leq
    \text{rank}A+
    \text{rank}B$$，其中$$P_1$$、$$Q_1$$、$$P_2$$、$$Q_2$$任意。

**9.** $$
    \text{rank}(I-AB)
\leq
        \text{rank}(I-A)
    +   \text{rank}(I-B)
$$
9可以由8推出$$\left(I-AB=I-A+A(I-B) \right)$$。

8是显然的。

**证明：**
$$
    \text{rank}A +
    \text{rank}B
=   \text{rank}
        \begin{pmatrix}
            A & O \\
            O & B \\
        \end{pmatrix}\\
\geq 
    \text{rank}
        \begin{pmatrix}
            I & O \\
            O & P_2 \\
        \end{pmatrix}
        \begin{pmatrix}
            A & O \\
            O & B \\
        \end{pmatrix}
        \begin{pmatrix}
            I & O \\
            O & Q_2 \\
        \end{pmatrix}
=   \text{rank}
        \begin{pmatrix}
            A & O \\
            O & P_2BQ_2 \\
        \end{pmatrix}\\
=   \text{rank}
        \begin{pmatrix}
            A & P_1A \\
            AQ_1 & P_2BQ_2+P_1AQ_1 \\
        \end{pmatrix}
\geq
    \text{rank}\left(
        P_1AQ_1+P_2BQ_2
    \right)
$$

## 参考

1.  知乎[一篇文章](https://zhuanlan.zhihu.com/p/55206421)的部分问题。
2.  *Matrix Computations* by Golub & Van Loan
