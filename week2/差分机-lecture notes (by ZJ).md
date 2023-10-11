# 差分机
> A **difference engine** is an automatic [mechanical calculator](https://en.wikipedia.org/wiki/Mechanical_calculator "Mechanical calculator") designed to tabulate [polynomial](https://en.wikipedia.org/wiki/Polynomial "Polynomial") functions. It was designed in the 1820s, and was first created by [Charles Babbage](https://en.wikipedia.org/wiki/Charles_Babbage "Charles Babbage"). The name _difference engine_ is derived from the method of [divided differences](https://en.wikipedia.org/wiki/Divided_differences "Divided differences"), a way to interpolate or tabulate functions by using a small set of polynomial co-efficients. Some of the most common [mathematical functions](https://en.wikipedia.org/wiki/Mathematical_function "Mathematical function") used in engineering, science and navigation, are built from [logarithmic](https://en.wikipedia.org/wiki/Logarithm "Logarithm") and [trigonometric functions](https://en.wikipedia.org/wiki/Trigonometric_functions "Trigonometric functions"), which can be [approximated](https://en.wikipedia.org/wiki/Taylor_series "Taylor series") by polynomials, so a difference engine can compute many useful [tables](https://en.wikipedia.org/wiki/Mathematical_table "Mathematical table"). [source](https://en.wikipedia.org/wiki/Difference_engine)

在19世纪广泛使用，将非线性的乘法运算转化为线性的加法运算。
最大的**应用**：给出版社提供计算表。
## 原理
### 差分
$$
\Delta P^n(x) = P^{n-1}(x) \implies \Delta^{n}P^{n}(x) = C
$$
因此，有限次数的多项式经过多次差分之后可以转化为常数。
### 泰勒展开
> In [mathematics](https://en.wikipedia.org/wiki/Mathematics "Mathematics"), the **Taylor series** or **Taylor expansion** of a [function](https://en.wikipedia.org/wiki/Function_(mathematics) "Function (mathematics)") is an [infinite sum](https://en.wikipedia.org/wiki/Series_(mathematics) "Series (mathematics)") of terms that are expressed in terms of the function's [derivatives](https://en.wikipedia.org/wiki/Derivative "Derivative") at a single point. For most common functions, the function and the sum of its Taylor series are equal near this point. Taylor series are named after [Brook Taylor](https://en.wikipedia.org/wiki/Brook_Taylor "Brook Taylor"), who introduced them in 1715. A Taylor series is also called a **Maclaurin series** when 0 is the point where the derivatives are considered, after [Colin Maclaurin](https://en.wikipedia.org/wiki/Colin_Maclaurin "Colin Maclaurin"), who made extensive use of this special case of Taylor series in the mid-18th century.
> The [partial sum](https://en.wikipedia.org/wiki/Partial_sum "Partial sum") formed by the first _n_ + 1 terms of a Taylor series is a [polynomial](https://en.wikipedia.org/wiki/Polynomial "Polynomial") of degree n that is called the nth **Taylor polynomial** of the function. Taylor polynomials are approximations of a function, which become generally more accurate as n increases. [Taylor's theorem](https://en.wikipedia.org/wiki/Taylor%27s_theorem "Taylor's theorem") gives quantitative estimates on the error introduced by the use of such approximations. If the Taylor series of a function is [convergent](https://en.wikipedia.org/wiki/Convergence_(mathematics) "Convergence (mathematics)"), its sum is the [limit](https://en.wikipedia.org/wiki/Limit_of_a_sequence "Limit of a sequence") of the [infinite sequence](https://en.wikipedia.org/wiki/Infinite_sequence "Infinite sequence") of the Taylor polynomials. A function may differ from the sum of its Taylor series, even if its Taylor series is convergent. A function is [analytic](https://en.wikipedia.org/wiki/Analytic_function "Analytic function") at a point x if it is equal to the sum of its Taylor series in some [open interval](https://en.wikipedia.org/wiki/Open_interval "Open interval") (or [open disk](https://en.wikipedia.org/wiki/Disk_(mathematics) "Disk (mathematics)") in the [complex plane](https://en.wikipedia.org/wiki/Complex_plane "Complex plane")) containing x. This implies that the function is analytic at every point of the interval (or disk). [source](https://en.wikipedia.org/wiki/Taylor_series)

因此，许多常用函数都可以用多项式近似。
我记得有更好的办法的，但一时间[搜不到](https://sl.bing.net/gedjs4e3Myq)。
## 历史
由巴贝奇发明
## 复现
> During the 1980s, [Allan G. Bromley](https://en.wikipedia.org/wiki/Allan_G._Bromley "Allan G. Bromley"), an associate professor at the [University of Sydney](https://en.wikipedia.org/wiki/University_of_Sydney "University of Sydney"), [Australia](https://en.wikipedia.org/wiki/Australia "Australia"), studied Babbage's original drawings for the Difference and Analytical Engines at the [Science Museum](https://en.wikipedia.org/wiki/Science_Museum_(London) "Science Museum (London)") library in London.[[35]](https://en.wikipedia.org/wiki/Difference_engine#cite_note-35) This work led the Science Museum to construct a working calculating section of difference engine No. 2 from 1985 to 1991, under [Doron Swade](https://en.wikipedia.org/wiki/Doron_Swade "Doron Swade"), the then Curator of Computing. This was to celebrate the 200th anniversary of Babbage's birth in 1991. In 2002, the [printer](https://en.wikipedia.org/wiki/Printer_(computing) "Printer (computing)") which Babbage originally designed for the difference engine was also completed.[[36]](https://en.wikipedia.org/wiki/Difference_engine#cite_note-36) The conversion of the original design drawings into drawings suitable for engineering manufacturers' use revealed some minor errors in Babbage's design (possibly introduced as a protection in case the plans were stolen),[[37]](https://en.wikipedia.org/wiki/Difference_engine#cite_note-37) which had to be corrected. The difference engine and printer were constructed to tolerances achievable with 19th-century technology, resolving a long-standing debate as to whether Babbage's design could have worked using Georgian-era engineering methods. The machine contains 8,000 parts and weighs about 5 tons.

## 课前问题
### Q1：如何使用并行计算来优化？以为$f(x)=x^7+x$例进行思考
这个技巧是用一种方法，交错进行x值的子计算。（对于七次多项式）在第一步中进行四次并行的加法，将第01、23、45、67列加在一起。在第二步中进行三次并行的加法，将第12 34 56列加载一起。更高阶差相加的结果，每一步都在向左传递。
[reference](https://www.youtube.com/channel/UCyx5AKwWRJHT6Z-G_JawKGQ)
### Q2： 对于一般的连续函数比如 (步长0.01),差分机如何解决？
首先，机械的差分机可以通过乘以10的整数次方的方式来计算小数[reference](https://www.youtube.com/channel/UCyx5AKwWRJHT6Z-G_JawKGQ)，因此我们可以用它在一定精度范围内计算连续函数的值。接着，我们可以用泰勒展开将连续函数近似转化为多项式函数，并将系数舍入到小数。然后，我们可以用多项式的方法计算连续函数的值。最后，结合有效数字计算理论，我认为，为了保证较多步长之后的计算精度，差分机的计算精度应当高于计算步长。需要补充的是，对于这个特殊的函数，或许可以通过​这个特殊的性质来重新设计差分机计算。
### Q3：一个开放式问题:$f(x)=[x^2]$(步长0.01,$[]$为取小数部分)适合用差分机打表吗？思考⼀种较优的策略
适合。在打表计算时，只需维护小数部分的数值，而舍弃整数部分。由于差分机只涉及加法运算，因此这样计算可以保证正确性。进一步地，由于此时差分机的状态数有限，因此会出现循环节。只要找到循环节即可停止打表。
## 自己提的问题
1. 在电子计算机成熟的今天，机械的差分机还有意义吗？
2. 差分机的文化和历史价值如何，它是否被视为科技发展的重要里程碑之一？
3. 差分机的历史发展如何，它曾经在哪些领域取得了成功？
## 分析机
没有造出来
指令为前缀表达式
属于**stack machine**，java也在使用，每个指令很短（1字节）
冯诺依曼：指令只有三类（实际上是巴贝奇提的）
## 二进制运算与数字逻辑
- 用二进制表示数据
- 简单的组件可以组成复杂的计算机
- 处理复杂的现代计算机的最好方式是使用一系列不同层级的虚拟机