
# 量子计算

## Lecture Note 2023.11.23

## 量子计算起源

### 物理史

- 1900.4.27 开尔文演讲：两朵乌云（误）
- 1900 普朗克：能量量子化假说
- 1905 爱因斯坦：光电效应 验证光量子的概念 能量不连续
- 1924 德布罗意：物质波假说（前有康普顿散射，后有电子双缝干涉）
- 1930 狄拉克《量子力学原理》：叠加态 $\frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$
- 1932 冯诺依曼 《量子力学的数学基础》
- 1935 爱因斯坦、波多尔斯基和罗森：量子纠缠（参考：EPR佯谬）$\frac{1}{\sqrt{2}}(|01\rangle + |10\rangle)$

### 一点数学（有私货）

用光子的偏振态举例，一束光的光子的偏振状态存在两种稳定状态——x方向和y方向——可以用$|0\rangle$和$|1\rangle$表示，那么一束光沿某一方向的偏振态可以表示为态矢量：（=1qubit）

$|\psi\rangle = \alpha|0\rangle + \beta|1\rangle$

其中$\alpha$和$\beta$是复数。由于光子偏振态是归一化的，有

$\langle\psi|\psi\rangle = |\alpha|^2 + |\beta|^2 = 1$

其中$\langle\psi|$是$|\psi\rangle$的**共轭**转置，$\langle\phi|\psi\rangle$是两个态矢量的内积。

（至于为什么在量子力学中要引入复数，这个我也不太会，有兴趣可以参考[量子力学中引入虚数 i 的深层意义是什么？ - 知乎](https://www.zhihu.com/question/28557223/answer/41348676)）

由于两个偏振态正交归一，两个态矢量$|0\rangle$和$|1\rangle$是二维复线性空间$\mathbb{C}^2$的单位正交基。用$|0\rangle = \begin{bmatrix}1\\0\end{bmatrix}$，$|1\rangle = \begin{bmatrix}0\\1\end{bmatrix}$，可以将$|\psi\rangle$表示为$\begin{bmatrix}\alpha\\\beta\end{bmatrix}$。由此，可以将量子门表示为$2\times2$的矩阵，见[门电路](#jump)。

## 量子计算的发展历程

- 1981 lecture at MIT: Richard Feynman **经典计算机难以模拟量子系统的演化**
- 1985 David Deutsch: 量子计算机的理论基础、量子图灵机
- 1992 Deutsch-Jozsa算法：判断一个函数是常函数还是平衡函数的量子算法，证明了量子算法相对于经典算法有指数级别的加速能力
- 1994 Peter Shor质因数分解: 量子计算机的第一个重要算法
- 2017 IBM: 50q比特原型机
- 2019 Google: 53比特超导量子芯片（quantum supremacy）
- 2021.5 潘建伟团队: 66比特可编程超导量子处理器“祖冲之号”2.0 在随机线路采样问题上实现突破
- 2023.3 Google: 创新量子纠错系统
- IBM仍然在往上堆qubit数

和传统计算机不同，量子计算算力的提高主要在于提高qubit数量、提高qubit之间实现量子纠缠的性能和提高量子操作精度（见[量子纠错](#jump1)）。

<span id="jump"><span>

## 量子门电路

### 量子逻辑门的本质

量子门电路的本质是复向量空间上模长不变的线性变换。由于变换前后的$|\psi\rangle$的模均为1，有下式

$(U|\psi\rangle)^\dagger(U|\psi\rangle) = \langle\psi|U^\dagger U|\psi\rangle = \langle\psi|\psi\rangle = 1$

由二次型的性质得到

$U^\dagger U = I$

对应的矩阵都是2阶酉矩阵，即$U^\dagger U = I$，其中$U^\dagger$是$U$的共轭转置矩阵，$I$是单位矩阵。

量子线路 $|\psi_0\rangle$ --[H]--[X]--[Y]--[H]-->$|\psi\rangle$

### 几种常见的单qubit量子门

- $X$: Pauli-X gate，又称NOT gate，将$|0\rangle$变为$|1\rangle$，将$|1\rangle$变为$|0\rangle$，$\sigma_x=\begin{bmatrix}0&1\\1&0\end{bmatrix}$
- $Y$: Pauli-Y gate，将$|0\rangle$变为$i|1\rangle$，将$|1\rangle$变为$-i|0\rangle$，$\sigma_y=\begin{bmatrix}0&-i\\i&0\end{bmatrix}$
- $Z$: Pauli-Z gate，将$|0\rangle$变为$|0\rangle$，将$|1\rangle$变为$-|1\rangle$，$\sigma_z=\begin{bmatrix}1&0\\0&-1\end{bmatrix}$
- $H$: Hadamard gate，$H=\frac{1}{\sqrt{2}}\begin{bmatrix}1&1\\1&-1\end{bmatrix}$

### 几种常见的多qubit量子门

#### $CX$ $(CNOT)$

    q0-->--·-->--q0'
           |
    q1-->--○-->--q1'

若q0为0，则q1不变；若q0为1，则q1取反。相当于q0起到了**控制**的作用。

q0和q1组成2qubit的量子态，可以表示为$|00\rangle$、$|01\rangle$、$|10\rangle$、$|11\rangle$，对应的矩阵为

$CNOT = \begin{bmatrix}1&0&0&0\\0&1&0&0\\0&0&0&1\\0&0&1&0\end{bmatrix}$

#### 课堂问题

经典：所有逻辑运算能用not and or实现。

（实际上，not and or 都能用 nand （或 nor）实现，是不是说明仅用nand门（或 nor 门）能表示所有逻辑运算？）

量子：单qubit量子门无限个（$\alpha$和$\beta$取值连续），多qubit量子门也是无限个，所有这些量子逻辑门能用有限个量子逻辑门表示吗？

<span id="jump1"></span>

## 实现技术

光量子、离子阱、超导电路、半导体量子点、拓扑量子计算

## 量子纠错

当一个qubit的量子态可能受到外界影响时，我们不能用测量的方法去纠错，因为测量一次就会使叠加态坍缩，如果该qubit还和其他qubit纠缠在一起，那么其他qubit的量子态也会坍缩。

Peter Shor编码： 8个qubit保护1个qubit（参考[现在的量子计算机发展到什么地步了？ - Vincent的回答 - 知乎](https://www.zhihu.com/question/409714881/answer/1372095339)讲到了一点细节）

## 量子机器学习

4种模式：

- 经典算法+经典数据
- 经典算法+量子数据
- 量子算法+经典数据
- 量子算法+量子数据

优势：

能够提取非典型模式，效率高

## 变分量子算法

$H$：哈密顿算符，描述量子体系的能量

$E$：系统哈密顿算符的本征值，表示测量能量的结果

定态Schrödinger方程：

$H|\psi\rangle = E|\psi\rangle$

变分原理：Schrödinger方程的任何近似解都比体系基态能量高

$E_0 = \min_{|\psi\rangle} \frac{\langle\psi|H|\psi\rangle}{\langle\psi|\psi\rangle}$

目标：找到$|\psi\rangle$，使得$E=\frac{\langle\psi|H|\psi\rangle}{\langle\psi|\psi\rangle}$最小。$|\psi\rangle$可以是离散的，也可以是连续的（即函数，这里用到变分）

该算法相当于模拟一个黑箱，不清楚经典系统的细节时，那么可以用量子体系模拟，改变量子系统的状态，测量能量（本征值），得到最优解

两个最重要的应用方向：

- 计算化学：室温超导/迈斯纳效应/计算电子分布等具体问题->写出哈密顿算符，近似解Schrödinger方程->分子基态能量、键长预测
- 组合数学：最大割问题为例

## 总结

### 局限性

- 编程方法：直接在量子门层面编程，通过设计量子电路图（汇编）的方式直接得到算法，由输入数据直接得到输出结果
- 能够解决的问题具有特定形式
- 经典逻辑门是**非线性、不可逆、非单射**的（如and门），经典神经网络中的部分神经元也需要引入**非线性的激活函数**（如sigmoid函数、tanh函数）来避免trivial的分类。然而，你是否注意到，所有量子逻辑门都是**可逆的线性变换**？这是量子机器学习算法潜在的的局限性之一。

### 优越性

- 经典模式下摩尔定律失效：晶体管不断变小的同时，量子隧穿影响计算精度
- 并行计算，当然对于特定问题非常“powerful”
- 机器学习和量子计算互补，可以在经典机器学习的部分步骤中引入量子计算，从而提升算法的性能。
