---
layout: post
title:  "线性代数精品制作小组 - 秩"
---

## 基本性质

以下为对秩基本结论的总结

（1～3 分块阵基础、4～6 相乘阵的秩、7～10 相加阵的秩、11～14 转置 伴随 幂等 对合阵的性质）

**1.（不重合的分块）**

$$
\text{rank}
\begin{pmatrix}
	A & O\\
	O & B
\end{pmatrix}
=
\text{rank}(A) + \text{rank}(B)
$$

**2.（三角状的分块）**

$$
\text{rank}
\begin{pmatrix}
	A & O\\
	C & B
\end{pmatrix}
\geq
\text{rank}(A) + \text{rank}(B)
$$

**3.（子矩阵）**

$$
A_1 \subset A \text{ (submatrix)} 
\Rightarrow
\text{rank}(A) \geq \text{rank}(A_1)
$$

**4. (秩的乘法)**

$$
\text{rank}AB
\leq
    \text{min}\{
        \text{rank}A,
        \text{rank}B
    \}
$$

**5. (Sylvester不等式)**

$$
\text{rank}AB
\geq
    \text{rank}A+
    \text{rank}B-
        n
$$

**6. (Frobenius不等式)**

$$
    \text{rank}ABC+
    \text{rank}B
\geq
    \text{rank}AB+
    \text{rank}BC
$$

**7. (秩的加法)**

$$
\text{rank}\left(
        A+B
    \right)
\leq
    \text{rank}A+
    \text{rank}B
$$

**8.（等号成立的一个充分条件）** 

$$
AB=BA=O,
    \text{rank}A^2=
    \text{rank}A
\quad\Rightarrow\quad
    \text{rank}\left(
        A+B
    \right)=
    \text{rank}A+
    \text{rank}B
$$

**9.（秩加法的推广）**

$$
\text{rank}\left(
        P_1AQ_1+P_2BQ_2
    \right)
\leq
    \text{rank}A+
    \text{rank}B
$$

**10.（9的特例之一）**

$$
\text{rank}(I-AB)
\leq
\text{rank}(I-A)
+ \text{rank}(I-B)
$$

**11. （行秩等于列秩）**

$$
    \text{rank}A
=   \text{rank}A^T
$$

**12.（证明最小二乘法中的一个结论）**

$$
\text{rank}A
=   \text{rank}A^TA
$$

**13.（关于伴随矩阵）**

$$
\text{rank}(A^*)=
\begin{cases}
	n,	& \text{rank}(A) = n\\
	1,  & \text{rank}(A) = n-1\\
	0,  & \text{rank}(A) \leq n-2
\end{cases}
$$

**14.（关于幂等和对合矩阵）**

$$
A^2 = I \Leftrightarrow
\text{rank}(I+A)+\text{rank}(I+B) = n\\
A^2 = A \Leftrightarrow
\text{rank}(A)+\text{rank}(I-A) = n
$$

**15.（ $$I-AB​$$ 的可交换性）**

$$
m + \text{rank}(I_n-AB) = n + \text{rank}(I_m-BA)
$$

## 工具方法

##### 1.初等变换

$$
\text{rank}(PAQ)=\text{rank}(A)
$$

##### 2. 相抵分解

$$
\text{rank}(A) = r,\quad A = P I_r Q
$$

##### 3. 满秩分解

$$
\text{rank}(A) = r,\; \exist P \in F^{m \times r} \; Q\in F^{r \times n}(\text{P、Q满秩}),A=PQ
$$

##### 4. 线性空间

$$
\text{rank}(A) = \text{dim}({\text{Im}}{\scr A})=n - \text{dim}(\text{Ker}{\scr A})
$$

##### 5. 极大无关组

##### 6. 广义逆与M-P逆

## 练习思考

**1. ** 已知矩阵 $$A,B$$，且满足 $$AB=BA=O$$  ，试证明：存在正整数 $$m$$，使得

$$
rank(A^m+B^m)=rank(A^m)+rank(B^m)
$$

**2. **已知 $$A_{s\times n}$$ ，$$B_{n\times s}$$ ，试证明：

$$
rank(A-ABA)=rank(A)+rank(I_n-BA)-n
$$

**3.** 已知 $$A_{m\times n}$$ ，$$B_{n\times m}$$ ,证明：

$$
-\frac{n}{2} \leq 
\text{rank}(AB) - \text{rank}(BA)
\leq - \frac{m}{2}
$$

**4.** （关于基本结论不等式中等号成立充分必要条件）

$$
\text{rank}(AB) = \text{rank}(A) \Leftrightarrow
\exist X,ABX=A\\
\text{rank}
\begin{pmatrix}
	A & O\\
	C & B
\end{pmatrix}
\geq
\text{rank}(A) + \text{rank}(B)\Leftrightarrow
\exist X,Y,AX+BY=C\\
\text{rank}(A)+\text{rank}(B)=\text{rank}(A+B) \Leftrightarrow
\exist P,Q,
A=P\begin{pmatrix}
	I & O\\
	O & O
\end{pmatrix}Q 
\;\text{  and  }\;
B=P\begin{pmatrix}
	O & O\\
	O & I
\end{pmatrix}Q 
$$

## 参考

[常见的矩阵秩(不)等式及其各种证明](https://zhuanlan.zhihu.com/p/55206421)

[线性代数课程讲义 王新茂](https://drive.wps.cn/view/l/svf35ku)

