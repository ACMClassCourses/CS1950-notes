# Quickselect 问题
## 引入
问题：在 n 个数中找出第 k 小的数。        
分治法：每次按照大于等于小于 pivot 三分，只需在 k 所在的部分递归寻找。            
期望复杂度：O(n)，但最坏情况：O(n^2)，甚至慢于直接排序和逐个查找！

## Median of medians 算法
因此，我们需要通过选择合适的初始 pivot 来优化。       
由 BFPRT 五位大佬提出的此算法（[原论文地址](https://people.csail.mit.edu/rivest/pubs/BFPRT73.pdf)）核心思想是将原数组分为五元组，并选出五元组的各中位数的中位数。          
注意到此选择的最重要性质是，至少有30%的元素小于pivot，另外30%的元素大于pivot。           

线性复杂度证明：T(n)≤T(0.2n)+T(0.7n)+O(n).       
其中，T(0.2n)用于递归Quickselect以找出中位数中的中位数；T(0.7n)是剩余部分的最差期望；O(n)用于分组。

# 集卡问题
由抽卡游戏引入。

## Polynomial Identity 问题       
判定多项式与乘式形式的两个多项式是否相同。               
展开系数对比：>= O(d log d).            
代入值，运用代数基本定理比较：乘法过程仍需要 O(d^2).

如果允许一定容错比例？          
随机选择，恰选到根的概率极低；然而，实数上的均匀分布并不存在。如何进行这一随机？

## 概率论
反思：何谓概率？         
Return to Kolmogorov：公理化概率论          
独立：Pairwise Independent & Mutual Independent          
期望：线性性质

## 计算集齐各种卡的期望
结论：E[X]≈n·(ln n+γ).      
可见营销策略的成功性！