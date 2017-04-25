---
layout: post
title: 矩阵相关知识
categories: journal
author: shiyi
tags:
  - documentation
  - sample
image:
  feature: the_matrix.jpg
---

## 1. 定义(Defination)

由$$m\\times{n}$$个数$$a_{ij}$$排成的$$m$$行$$n$$列的数表称为$$m$$行$$n$$列的矩阵，简称$$m × n$$矩阵。记作： 矩阵 $$ A= \\begin{bmatrix} a_{11} & a_{12} & a_{13}& \\cdots & a_{1n}\\ a_{21} & a_{22} & a_{23} &\\cdots & a_{2n}\\ a_{31} & a_{32} & a_{33} &\\cdots & a_{3n}\\ \\cdots & \\cdots&\\cdots&\\ddots & \\cdots\\ a_{m1} & a_{m2} & a_{m3} & \\cdots & a_{mn}\\ \\end{bmatrix} $$ 这$$m×n$$个数称为矩阵$$A$$的元素，简称为元，数$$a_{ij}$$位于矩阵$$A$$的第$$i$$行第$$j$$列，称为矩阵$$A的(i,j)$$元，以数$$a_{ij}为(i,j)$$元的矩阵可记为$$(a_{ij})$$或$$(a_{ij})_{m × n}$$，$$m×n$$矩阵$$A$$也记作$$A\_{mn}$$。 元素是实数的矩阵称为实矩阵，元素是复数的矩阵称为复矩阵。而行数与列数都等于n的矩阵称为n阶矩阵或n阶方阵

## 2. 矩阵的线性运算

### 2.1 矩阵加法

只有相同维度的矩阵(同型矩阵)之间才能相加 例如: $$ \\begin{bmatrix} 1 & 2 \\ 7 & 5 \\ 1 & 4 \\ \\end{bmatrix} + \\begin{bmatrix} 2 & 1\\ 6 & 4\\ 3 & 3\\ \\end{bmatrix} = \\begin{bmatrix} 3 & 3\\ 13 & 9\\ 4 & 7\\ \\end{bmatrix} $$ 且满足以下规律: $$ A+B=B+A $$ $$ (A+B)+C=A+(B+C) $$

### 2.2 矩阵的数乘(Scalar Multiplication)

即矩阵与实数相乘,等于实数与矩阵里的每个元素相乘 满足以下运算规律: $$ (\\lambda\\mu)A=\\lambda(\\mu{A}) \\ (\\lambda+\\mu)A=\\lambda{A}+\\mu{A} \\ \\lambda(A+B)=\\lambda{A}+\\lambda{B} \\ $$ $$ \\begin{bmatrix} 1 & 5\\ 2 & 7\\ \\end{bmatrix} \\times 3 = \\begin{bmatrix} 3 & 15\\ 6 & 21\\ \\end{bmatrix} $$

## 3. 矩阵的转置

把矩阵$$A$$的行和列互相交换所产生的矩阵称为$$A$$的转置矩阵,记为$$A^T$$ ，这一过程称为矩阵的转置 $$ \\begin{bmatrix} 1 & 5\\ 2 & 7\\ \\end{bmatrix}^T= \\begin{bmatrix} 1 & 2\\ 5 & 7\\ \\end{bmatrix} $$

## 4. 矩阵的乘法

矩阵相乘最重要的方法是一般矩阵乘积。它只有在第一个矩阵的列数（column）和第二个矩阵的行数（row）相同时才有意义。一般单指矩阵乘积时，指的便是一般矩阵乘积。一个m×n的矩阵就是m×n个数排成m行n列的一个数阵。由于它把许多数据紧凑的集中到了一起，所以有时候可以简便地表示一些复杂的模型。 设A为$$m\\times{p}$$的矩阵，B为$$p\\times{n}$$的矩阵，那么称$$m\\times{n}$$的矩阵C为矩阵A与B的乘积，记作$$C=AB$$，其中矩阵C中的第i行第j列元素可以表示为： $$ (AB)_{ij}=\\sum^p_{k=1}a_{ik}b_{kj}=a_{i1}b_{1j}+a_{i2}b_{2j}+\\cdots+a_{ip}b_{pj} $$

**注意事项** 当矩阵A的列数等于矩阵B的行数时，A与B可以相乘。

-   矩阵C的行数等于矩阵A的行数，C的列数等于B的列数。
-   乘积C的第m行第n列的元素等于矩阵A的第m行的元素与矩阵B的第n列对应元素乘积之和。

**基本性质**

-   乘法结合律： $$(AB)C=A(BC)$$
-   乘法左分配律：$$(A+B)C=AC+BC$$
-   乘法右分配律：$$C(A+B)=CA+CB$$
-   对数乘的结合性$$k(AB）=(kA)B=A(kB）$$
-   转置 $$(AB)^T=B^TA^T$$
-   矩阵乘法一般不满足交换律

$$ \\begin{bmatrix} 1 & 5\\ 2 & 7\\ \\end{bmatrix} \\times \\begin{bmatrix} 3 \\ 6 \\ \\end{bmatrix} = \\begin{bmatrix} 3 & 15\\ 6 & 21\\ \\end{bmatrix} $$

## 5. 单位矩阵

$$主对角线上的元素都为1，其余元素全为0的n阶矩阵称为n阶单位矩阵，记为I_n或E_n，通常用I或E来表示。$$ 在线性代数中，大小为n的单位矩阵是在主对角线上均为1，而其他地方都是0的n\*n的正方矩阵。它用I_n表示，或有时阶数可忽略时就直接用I来表示。如下所示： $$ I_1=\\begin{bmatrix} 1 \\end{bmatrix}\\ I_2=\\begin{bmatrix} 1 &0\\ 0&1\\ \\end{bmatrix}\\ I_3=\\begin{bmatrix} 1 &0&0\\ 0&1&0\\ 0&0&1\\ \\end{bmatrix}\\ \\cdots\\cdots\\cdots\\ I_n=\\begin{bmatrix} 1 &0&\\cdots&0\\ 0&1&\\cdots&0\\ \\cdots&\\cdots&\\ddots&\\cdots\\ 0&0&\\cdots&1\\ \\end{bmatrix}\\ $$ 同时单位矩阵也可以简单地记为一个对角线矩阵： $$ I_n=diag(1,1,1,...,1) $$

**性质** 根据矩阵乘法的定义，单位矩阵的重要性质为：$$AI_n=A和I_nB=B$$ 单位矩阵的特征值皆为1，任何向量都是单位矩阵的特征向量。具有重数。因为特征值之积等于行列式，所以单位矩阵的行列式为1。因为特征值之和等于迹数，单位矩阵的迹为$$n$$。

### 矩阵的逆

对于矩阵$$A$$，如果存在一个矩阵$$B$$，使得$$AB=BA=E$$，其中$$E$$为与$$A,B$$同维数的单位阵，就称$$A$$为可逆矩阵（或者称$$A$$可逆），并称$$B$$是$$A$$的逆矩阵，简称逆阵。（此时的逆称为凯利逆） 矩阵A可逆的充分必要条件是$$|A|≠0$$。 伪逆矩阵是逆矩阵的广义形式。由于奇异矩阵或非方阵的矩阵不存在逆矩阵，但可以用函数$$pinv(A)$$求其伪逆矩阵。基本语法为X=pinv(A),X=pinv(A,tol)$$,其中$$tol$$为误差,$$pinv$$为$$pseudo-inverse$$的缩写：$$max(size(A))\_norm(A)\_eps$$。函数返回一个与$$A$$的转置矩阵$$A'$$同型的矩阵$$X$$，并且满足：$$AXA=A,XAX=X$$.此时，称矩阵$$X$$为矩阵$$A$$的伪逆，也称为广义逆矩阵。$$pinv(A)$$具有$$inv(A)$$的部分特性，但不与$$inv(A)$$完全等同。 如果A为非奇异方阵，$$pinv(A)=inv(A)$$，但却会耗费大量的计算时间，相比较而言，$$inv(A)$$花费更少的时间。
