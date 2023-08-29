
.. _chap_notation:

符号
====


本书中使用的符号概述如下。

数字
----

-  :math:`x`\ ：标量
-  :math:`\mathbf{x}`\ ：向量
-  :math:`\mathbf{X}`\ ：矩阵
-  :math:`\mathsf{X}`\ ：张量
-  :math:`\mathbf{I}`\ ：单位矩阵
-  :math:`x_i`,
   :math:`[\mathbf{x}]_i`\ ：向量\ :math:`\mathbf{x}`\ 第\ :math:`i`\ 个元素
-  :math:`x_{ij}`,
   :math:`[\mathbf{X}]_{ij}`\ ：矩阵\ :math:`\mathbf{X}`\ 第\ :math:`i`\ 行第\ :math:`j`\ 列的元素

集合论
------

-  :math:`\mathcal{X}`: 集合
-  :math:`\mathbb{Z}`: 整数集合
-  :math:`\mathbb{R}`: 实数集合
-  :math:`\mathbb{R}^n`: :math:`n`\ 维实数向量集合
-  :math:`\mathbb{R}^{a\times b}`:
   包含\ :math:`a`\ 行和\ :math:`b`\ 列的实数矩阵集合
-  :math:`\mathcal{A}\cup\mathcal{B}`:
   集合\ :math:`\mathcal{A}`\ 和\ :math:`\mathcal{B}`\ 的并集
-  :math:`\mathcal{A}\cap\mathcal{B}`\ ：集合\ :math:`\mathcal{A}`\ 和\ :math:`\mathcal{B}`\ 的交集
-  :math:`\mathcal{A}\setminus\mathcal{B}`\ ：集合\ :math:`\mathcal{A}`\ 与集合\ :math:`\mathcal{B}`\ 相减，\ :math:`\mathcal{B}`\ 关于\ :math:`\mathcal{A}`\ 的相对补集

函数和运算符
------------

-  :math:`f(\cdot)`\ ：函数
-  :math:`\log(\cdot)`\ ：自然对数
-  :math:`\exp(\cdot)`: 指数函数
-  :math:`\mathbf{1}_\mathcal{X}`: 指示函数
-  :math:`\mathbf{(\cdot)}^\top`: 向量或矩阵的转置
-  :math:`\mathbf{X}^{-1}`: 矩阵的逆
-  :math:`\odot`: 按元素相乘
-  :math:`[\cdot, \cdot]`\ ：连结
-  :math:`\lvert \mathcal{X} \rvert`\ ：集合的基数
-  :math:`\|\cdot\|_p`: ：\ :math:`L_p` 正则
-  :math:`\|\cdot\|`: :math:`L_2` 正则
-  :math:`\langle \mathbf{x}, \mathbf{y} \rangle`\ ：向量\ :math:`\mathbf{x}`\ 和\ :math:`\mathbf{y}`\ 的点积
-  :math:`\sum`: 连加
-  :math:`\prod`: 连乘
-  :math:`\stackrel{\mathrm{def}}{=}`\ ：定义

微积分
------

-  :math:`\frac{dy}{dx}`\ ：\ :math:`y`\ 关于\ :math:`x`\ 的导数
-  :math:`\frac{\partial y}{\partial x}`\ ：\ :math:`y`\ 关于\ :math:`x`\ 的偏导数
-  :math:`\nabla_{\mathbf{x}} y`\ ：\ :math:`y`\ 关于\ :math:`\mathbf{x}`\ 的梯度
-  :math:`\int_a^b f(x) \;dx`:
   :math:`f`\ 在\ :math:`a`\ 到\ :math:`b`\ 区间上关于\ :math:`x`\ 的定积分
-  :math:`\int f(x) \;dx`: :math:`f`\ 关于\ :math:`x`\ 的不定积分

概率与信息论
------------

-  :math:`P(\cdot)`\ ：概率分布
-  :math:`z \sim P`: 随机变量\ :math:`z`\ 具有概率分布\ :math:`P`
-  :math:`P(X \mid Y)`\ ：\ :math:`X\mid Y`\ 的条件概率
-  :math:`p(x)`: 概率密度函数
-  :math:`{E}_{x} [f(x)]`: 函数\ :math:`f`\ 对\ :math:`x`\ 的数学期望
-  :math:`X \perp Y`: 随机变量\ :math:`X`\ 和\ :math:`Y`\ 是独立的
-  :math:`X \perp Y \mid Z`:
   随机变量\ :math:`X`\ 和\ :math:`Y`\ 在给定随机变量\ :math:`Z`\ 的条件下是独立的
-  :math:`\mathrm{Var}(X)`: 随机变量\ :math:`X`\ 的方差
-  :math:`\sigma_X`: 随机变量\ :math:`X`\ 的标准差
-  :math:`\mathrm{Cov}(X, Y)`:
   随机变量\ :math:`X`\ 和\ :math:`Y`\ 的协方差
-  :math:`\rho(X, Y)`: 随机变量\ :math:`X`\ 和\ :math:`Y`\ 的相关性
-  :math:`H(X)`: 随机变量\ :math:`X`\ 的熵
-  :math:`D_{\mathrm{KL}}(P\|Q)`: :math:`P`\ 和\ :math:`Q`\ 的KL-散度

复杂度
------

-  :math:`\mathcal{O}`\ ：大O标记
