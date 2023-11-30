## 为什么机械实现的基数排序必须从低位到高位排序

理论上，基数排序可以从高位开始，也可以从低位开始。但是，从高位开始的基数排序是一种递归的结构。在排好某一位后，为了让这一位的顺序保持，需要借助递归去排低一位。这对于机械过于打杂，难以实现。

从低位开始的基数排序虽然看起来不是很直观，但实现起来有很多便利。因为基数排序是稳定的，所以如果先排低位再排高位，只要高位相同，低位必定已经按顺序排列。所以不需要借助递归的结构实现，只需把某一位排好的几堆按顺序放在一起就可以了。这对于机械结构的实现比较简单。

## 基于比较的排序算法的时间复杂度下界是$O\left(N\log N\right)$

每一次比较至多过滤掉一半的可能性，经过$k$次比较，得到唯一的答案。可得：$\left(\frac{1}{2}\right)^k N!<1$，即$k>\log_2\left(N!\right)$

因此时间复杂度下界是$O\left(\log_2\left(N!\right)\right)$

$$\log_2\left(N!\right)<\log_2\left(N^N\right)=N\log_2 N=O\left(N\log N\right)$$

$$\log_2\left(N!\right)>\log_2\left(\left[\frac{N}{2}\right]^\left[\frac{N}{2}\right]\right)=\left[\frac{N}{2}\right]\log_2\left[\frac{N}{2}\right]=O\left(N\log N\right)$$

因此$O\left(\log_2\left(N!\right)\right)=O\left(N\log N\right)$

##　傅里叶级数

在函数空间$C\left[0,2\pi\right]$中性质足够好的函数构成的集合上定义内积$\left<f, g\right>=\int_0^{2\pi}f\left(t\right)g\left(t\right)dt$，不难验证，这是一个内积空间，因为积分的性质可以证明内积的对称性、对第一变元的线性性、正定性。

我们先证：$\left(1,\cos t,\cos 2t,\cdots,\cos kt,\sin t,\sin 2t,\cdots,\sin kt\right)$两两正交

$$\left<1,\cos mt\right>=\int_0^{2\pi}\cos mt dt=\left.\frac{1}{m}\sin mt\right|_0^{2\pi}=0$$

$$\left<1,\sin mt\right>=\int_0^{2\pi}\sin mt dt=\left.-\frac{1}{m}\cos mt\right|_0^{2\pi}=0$$

$$\left<\cos mt,\cos nt\right>=\int_0^{2\pi}\cos mt\cos ntdt=\left.\frac{1}{2}\left[\frac{\sin\left(m+n\right)t}{m+n}+\frac{\sin\left(m-n\right)t}{m-n}\right]\right|_0^{2\pi}=0$$

$$\left<\sin mt,\sin nt\right>=\int_0^{2\pi}\sin mt\sin ntdt=\left.\frac{1}{2}\left[\frac{\sin\left(m-n\right)t}{m-n}-\frac{\sin\left(m+n\right)t}{m+n}\right]\right|_0^{2\pi}=0$$

$$\left<\sin mt,\cos nt\right>=\int_0^{2\pi}\sin mt\cos ntdt=\left.-\frac{1}{2}\left[\frac{\cos\left(m+n\right)t}{m+n}+\frac{\cos\left(m-n\right)t}{m-n}\right]\right|_0^{2\pi}=0$$

$f$可近似表达为$f$到这组函数张成的空间上的投影$\tilde{f}$

$$\left<1,1\right>=\int_0^{2\pi}1dt=2\pi$$

$$\left<\cos mt,\cos mt\right>=\int_0^{2\pi}\cos^2 mtdt=\left.\frac{1}{2}\left(t-\frac{\sin 2mt}{2m}\right)\right|_0^{2\pi}=\pi$$

$$\left<\sin mt,\sin mt\right>=\int_0^{2\pi}\sin^2 mtdt=\left.\frac{1}{2}\left(t+\frac{\sin 2mt}{2m}\right)\right|_0^{2\pi}=\pi$$

$$\begin{aligned}\tilde{f}&=\frac{\left<1,f\right>}{\left<1,1\right>}+\sum_{m=1}^n\frac{\left<\cos mt,f\right>}{\left<\cos mt,\cos mt\right>}\cos mt+\sum_{m=1}^n\frac{\left<\sin mt,f\right>}{\left<\sin mt,\sin mt\right>}\\&=\frac{1}{2\pi}\left<1,f\right>+\frac{1}{\pi}\sum_{m=1}^n\left<\cos mt,f\right>\cos mt+\sum_{m=1}^n\left<\sin mt,f\right>\sin mt\end{aligned}$$

设$a_m:=\frac{1}{\pi}\int_0^{2\pi}f\left(t\right)\cos mtdt$，$b_m:=\frac{1}{\pi}\int_0^{2\pi}f\left(t\right)\sin mtdt$

则$\tilde{f}=\frac{a_0}{2}+\sum_{m=1}^n\left(a_m\cos mt+b_m\sin mt\right)$

$n\rightarrow\infty$时，即为傅里叶级数