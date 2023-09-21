<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
<script type="text/x-mathjax-config">
    MathJax.Hub.Config({ tex2jax: {inlineMath: [['$', '$']]}, messageStyle: "none" });
</script>
# Week2 LectureNotes Difference Machine

## Core Thought

利用差分将非线性运算转变为线性运算

***

## Possible Answers to the Questions in the Preview PPT

Q1：如何使用并行计算来优化？以为$f(x)=x^7+x$例进行思考

A1：这里我们选择不一项一项加 而是每两项进行相加 即并行运算 这样的运算是互相独立的 可同时进行 避免了其余部件的闲置（详见后文）

Q2：对于一般的连续函数比如 (步长0.01),差分机如何解决？

A2：使用泰勒展开 将$e^x$转化为$1+x+x^2/2!+x^3/3!$……

Q3：一个开放式问题:$f(x)=[x^2]$(步长0.01,[]为取小数部分)适合用差分机打表吗？思考⼀种较优的策略

A3：个人觉得不太合适 直接的话小数位数太多 应加一个额外的寄存器记录小数位数 其余正常计算

***

## Overview
**Difference Engine**, an early calculating machine, verging on being the first computer, designed and partially built during the 1820s and ’30s by Charles Babbage. Its purpose is to automate mathematical calculations, especially for generating numerical tables of polynomials. The difference engine is a physical implementation of the mathematical principles used by Babbage in the analysis and calculation of polynomials.

差分机，一种早期的计算机，几乎可以算作是第一台计算机，由查尔斯·巴贝奇在19世纪20年代和30年代设计并部分建造。它的目的是自动进行数学计算，特别是用于生成多项式的数值表。差分机是巴贝奇在分析和计算多项式时所使用的数学原理的物理实现。

<img src="https://p.sda1.dev/13/f8c556fca978efc6de47e194ceb74518/image.png" width="300" height="400" >
<img src="https://p.sda1.dev/13/0afcade493582c912598bed3ef4d6ed8/image.png" width="300" height="400" >

***

The name difference engine is derived from the method of divided differences, a way to interpolate or tabulate functions by using a small set of polynomial coefficients. Some of the most common mathematical functions used in engineering, science and navigation, are built from logarithmic and trigonometric functions, which can be approximated by polynomials, so a difference engine can compute many useful tables. (from WIKIPEDIA)

差分机的名称源自差分法，这是一种通过使用一小组多项式系数来插值或制表函数的方法。在工程、科学和导航中使用的一些最常见的数学函数是由对数函数和三角函数构建的，这些函数可以通过多项式来近似，因此差分机可以计算出许多有用的表格。（来自维基百科）

## Theory

### 差分法(calculus of differences)：$f(X)=2X^2+3X+1$

| X      | $f(X)$ | $Δ_1$      |$Δ_2$            |
| ----------- | ----------- | ----------- | ----------- |
| 1 | 6|
| 2 | 15|$15-6=9$|
| 3 | 28|$28-15=13$|$13-9=4$
| 4 | 45|$45-28=17$|$17-13=4$
| 5 | 66|$66-45=21$|$21-17=4$

### Improvement: parallel computing

#### [并行计算](https://blog.csdn.net/qq_25985027/article/details/103351550)

可以划分成时间并行和空间并行。时间并行即流水线技术，空间并行使用多个处理器执行并发计算，当前研究的主要是空间的并行问题。

并行计算是相对于串行计算来说的。要理解并行计算，首先需要了解*串行计算*。串行计算是不将任务进行拆分，一个任务占用一块处理资源。

![串行运算](https://p.sda1.dev/13/c774d2c157a4de4c21c1ec548f133d4c/20191202164303923.png)

并行计算则不同。首先，并行计算可以划分成时间并行和空间并行。时间并行就是流水线技术，空间并行使用多个处理器执行并发计算。目前以研究空间并行为主。从空间并行的角度来说，并行计算将一个大任务分割成多个子任务，每个子任务占用一定处理资源。并行计算中不同子任务占用的不同的处理资源来源于同一块大的处理资源。 换一个说法，就是将一块大的处理资源分为几块小的处理资源，将一个大任务分割成多个子任务，用这些小的处理资源来单独处理这些子任务。 并行计算中各个子任务之间是有很大的联系的，每个子任务都是必要的，其结果相互影响。

![并行计算](https://p.sda1.dev/13/824be56f5f715935b8cc2cfa68856ad0/20191203172200703.png)

***

#### Example: $f(X)=X^7+X$

**原理**：这里我们选择不一项一项加 而是每两项进行相加 这样的运算是互相独立的 并且可以提高运行效率

<table style="border-collapse: collapse; width: 100%; height: 216px;" border="1">
<tbody>
<tr style="height: 24px;">
<td style="width: 10%; height: 24px;">x</td>
<td style="width: 10%; height: 24px;">f(x)</td>
<td style="width: 10.7862%; height: 24px;">DT1</td>
<td style="width: 9.05661%; height: 24px;">DT2</td>
<td style="width: 10.1572%; height: 24px;">DT3</td>
<td style="width: 10%; height: 24px;">DT4</td>
<td style="width: 10%; height: 24px;">DT5</td>
<td style="width: 10%; height: 24px;">DT6</td>
<td style="width: 10%; height: 24px;">DT7</td>
</tr>
<tr style="height: 24px;">
<td style="width: 10%; height: 24px;">1</td>
<td style="width: 10%; height: 24px;">2</td>
<td style="width: 10.7862%; height: 24px;">128</td>
<td style="width: 9.05661%; height: 24px;">1932</td>
<td style="width: 10.1572%; height: 24px;">10206</td>
<td style="width: 10%; height: 24px;">25200</td>
<td style="width: 10%; height: 24px;">31920</td>
<td style="width: 10%; height: 24px;">20160</td>
<td style="width: 10%; height: 24px;">5040</td>
</tr>
<tr style="height: 24px;">
<td style="width: 10%; height: 24px;">2</td>
<td style="width: 10%; height: 24px;">130</td>
<td style="width: 10.7862%; height: 24px;">2060</td>
<td style="width: 9.05661%; height: 24px;">12138</td>
<td style="width: 10.1572%; height: 24px;">35406</td>
<td style="width: 10%; height: 24px;">57120</td>
<td style="width: 10%; height: 24px;">52080</td>
<td style="width: 10%; height: 24px;"><span style="background-color: #ffff00;">25200</span></td>
<td style="width: 10%; height: 24px;"><span style="background-color: #ffff00;">5040</span></td>
</tr>
<tr style="height: 24px;">
<td style="width: 10%; height: 24px;">3</td>
<td style="width: 10%; height: 24px;">2190</td>
<td style="width: 10.7862%; height: 24px;">14198</td>
<td style="width: 9.05661%; height: 24px;">47544</td>
<td style="width: 10.1572%; height: 24px;">92526</td>
<td style="width: 10%; height: 24px;"><span style="background-color: #ffff00;">109200</span></td>
<td style="width: 10%; height: 24px;"><span style="background-color: #ffff00;">77280</span></td>
<td style="width: 10%; height: 24px;"><span style="background-color: #ffcc00;">30240</span></td>
<td style="width: 10%; height: 24px;"></td>
</tr>
<tr style="height: 24px;">
<td style="width: 10%; height: 24px;">4</td>
<td style="width: 10%; height: 24px;">16388</td>
<td style="width: 10.7862%; height: 24px;">61742</td>
<td style="width: 9.05661%; height: 24px;"><span style="background-color: #ffff00;">140070</span></td>
<td style="width: 10.1572%; height: 24px;"><span style="background-color: #ffff00;">201726</span></td>
<td style="width: 10%; height: 24px;"><span style="background-color: #ffcc00;">186480</span></td>
<td style="width: 10%; height: 24px;"></td>
<td style="width: 10%; height: 24px;"></td>
<td style="width: 10%; height: 24px;"></td>
</tr>
<tr style="height: 24px;">
<td style="width: 10%; height: 24px;">5</td>
<td style="width: 10%; height: 24px;"><span style="background-color: #ffff00;">78130</span></td>
<td style="width: 10.7862%; height: 24px;"><span style="background-color: #ffff00;">201812</span></td>
<td style="width: 9.05661%; height: 24px;"><span style="background-color: #ffcc00;">341796</span></td>
<td style="width: 10.1572%; height: 24px;"></td>
<td style="width: 10%; height: 24px;"></td>
<td style="width: 10%; height: 24px;"></td>
<td style="width: 10%; height: 24px;"></td>
<td style="width: 10%; height: 24px;"></td>
</tr>
<tr style="height: 24px;">
<td style="width: 10%; height: 24px;">6</td>
<td style="width: 10%; height: 24px;"><span style="background-color: #ffcc00;">279942</span></td>
<td style="width: 10.7862%; height: 24px;">543608</td>
<td style="width: 9.05661%; height: 24px;"></td>
<td style="width: 10.1572%; height: 24px;"></td>
<td style="width: 10%; height: 24px;"></td>
<td style="width: 10%; height: 24px;"></td>
<td style="width: 10%; height: 24px;"></td>
<td style="width: 10%; height: 24px;"></td>
</tr>
<tr style="height: 24px;">
<td style="width: 10%; height: 24px;">7</td>
<td style="width: 10%; height: 24px;">823550</td>
<td style="width: 10.7862%; height: 24px;">1273610</td>
<td style="width: 9.05661%; height: 24px;"></td>
<td style="width: 10.1572%; height: 24px;"></td>
<td style="width: 10%; height: 24px;"></td>
<td style="width: 10%; height: 24px;"></td>
<td style="width: 10%; height: 24px;"></td>
<td style="width: 10%; height: 24px;"></td>
</tr>
<tr style="height: 24px;">
<td style="width: 10%; height: 24px;">8</td>
<td style="width: 10%; height: 24px;">2037160</td>
<td style="width: 10.7862%; height: 24px;"></td>
<td style="width: 9.05661%; height: 24px;"></td>
<td style="width: 10.1572%; height: 24px;"></td>
<td style="width: 10%; height: 24px;"></td>
<td style="width: 10%; height: 24px;"></td>
<td style="width: 10%; height: 24px;"></td>
<td style="width: 10%; height: 24px;"></td>
</tr>
</tbody>
</table>

(由两个黄色的数块相加得到橙色部分)
***

## 第一个程序员

![](https://p.sda1.dev/13/afd65eac32725e81443ae3705542666b/image.png)

**Ada Byron**，全名 Augusta Ada King-Noel, Countess of Lovelace，是19世纪英国的一位数学家和编程先驱。她是英国数学家查尔斯·巴贝奇（Charles Babbage）的合作者，被认为是世界上第一位计算机程序员。Ada Byron生于1815年12月10日，是英国诗人拜伦勋爵（Lord Byron）的独生女。她从小接受了私人教育，学习了数学和科学知识。在她的教育中，她接触到了巴贝奇的分析机（Analytical Engine）的设计，并对其产生了浓厚的兴趣。
Ada Byron与巴贝奇成为了合作伙伴，她对分析机的运作原理进行了深入研究，并撰写了一份详细的笔记。这些笔记中包含了一些被认为是世界上第一份计算机程序的内容，其中包括了一种算法，可以用来计算分析机上的贝塞尔函数。尽管分析机从未被建造出来，但Ada Byron的笔记对计算机科学的发展产生了重要影响。她的工作在20世纪被重新发现，并被广泛认可为计算机程序设计的先驱。

## 补充：ByteCode
加法器的指令很简单 只有几个字符 与如今Java中的ByteCode相似

![](https://p.sda1.dev/13/65689d3ab2090000bfacae72ecd353a9/image.png)

网络的传输基本单位Byte，你不能保证网络一定是连续两个Byte一定能连续或者不间断地传输，所以你要用两个时间或3个时间表达一个指令。那就不能保证指定的原子性，所以一定要想出，一个简短体系，我知道这个指令终归要表达什么和什么相加，放到什么地方光这个操作数表达。必须要占很宽的比特，一个自己很难表达出来，但是他们表达出你们都能看懂，就可以同样说明，我们一定找到了一个Solution。

## 补充："操作系统就是一个虚拟机"

将操作系统比喻为一个虚拟机可以帮助我们理解操作系统的作用和功能。虚拟机是一种软件或硬件实现，它可以在物理计算机上创建和运行多个虚拟操作系统实例。每个虚拟机都提供了一个独立的运行环境，包括处理器、内存、存储和网络等资源。

类似地，操作系统也提供了一个虚拟的运行环境，使得应用程序可以在上面运行。操作系统作为一个中间层，隐藏了底层硬件的复杂性，为应用程序提供了一个统一的接口和抽象。它管理和分配计算机的硬件资源，包括处理器、内存、存储和输入输出设备等，以便应用程序可以在这些资源上运行。操作系统提供了各种服务和功能，例如进程管理、内存管理、文件系统、设备驱动程序等，这些功能使得应用程序可以在虚拟的运行环境中协调和执行。类似于虚拟机为虚拟操作系统提供了一个隔离的运行环境，操作系统为应用程序提供了一个隔离和抽象的运行环境。因此，将操作系统比喻为一个虚拟机，强调了操作系统提供的虚拟的运行环境和抽象层。它帮助我们理解操作系统的作用是为应用程序提供一个统一的接口和资源管理，隐藏底层硬件的复杂性，使得应用程序可以在一个独立、安全和可控的环境中运行。
