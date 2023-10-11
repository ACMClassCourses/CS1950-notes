# Notes 2023/9/28 黄文宾
Arith == Logic  
a + b = a _ b  
\* `_` stands for XOR &amp; AND  
电路中，逻辑门可以使用**三极管**（*特指开关管，即线性空间小的三极管*）来实现  
三极管的结构：  
- 输入端c: **collect**
- 输入端b: **base**
- 输出端e: **emit**
- 开关管的输入 - 输出公式：  
    `Ice = ((Ib >= I0 && Ic > 0) ? I : 0 );`

将三极管进行组合，可以制作出与`AND`、非`NOT`、或`OR`、与非`NAND`、或非`NOR`、异或`XOR`等逻辑门

*c语言是对冯·诺伊曼架构的抽象*  
操作系统对于进程来说就是一个虚拟机  
`Unicode`编码：万国码  
\* `ASCII`是`Unicode`的一个子集  
***
## Chip Fabrication
芯片制造流程：
- 培养高纯单晶硅
- 得到单晶硅圆柱 
- 切片硅晶圆 
- 涂层光敏材料 
- 覆盖光阻 
- 激光照射蚀刻 
- 在凹槽中填入金属线  
    >*化学气相沉积 曾使用铝Al，后使用铜Cu*
  
Q：芯片为什么要做小？  
A：不做小速度、频率就上不去  
*物理学原理：芯片越大，电信号在芯片上传递需要的时间就越长，频率就越低*  
***
## Stored Program Machines  
- 在 *First Draft - Von Neumann* 提出  
- 基本架构：  
`PC`: **Program Counter**  
`IR`: **Instruction Register**  
`AC`: **Accumulator**  

The Manchester Baby: 二战时英国的密码破译机器  
其破译密码的本质算法：高速的查找匹配  

\* Quoted from [Wikipedia](https://zh.wikipedia.org/wiki/%E6%9B%BC%E5%BD%BB%E6%96%AF%E7%89%B9%E4%B8%80%E5%9E%8B "Manchester Mark 1"):  
>曼彻斯特1型（Manchester Mark 1）是最早的存储程序计算机之一，在英国曼彻斯特维多利亚大学研发的别称为“宝贝”的小规模实验机（简称‘SSEM’，1948年6月开始运行）基础上开发完成。  
>Mark 1具有特别的历史意义，因为它在设计上开创性地包含了索引寄存器，这一创新使程序更容易按顺序读取内存中的字组。该机器的开发产生了34项专利，其设计背后的许多理念被纳入随后的商业产品，如IBM 701和702以及费伦蒂1型等。首席设计师弗雷德里克·威廉姆斯[注 4]和汤姆·吉尔本[注 5]从他们对Mark 1的经验得出结论，计算机在科学角色中的使用比在纯数学中更多。1951年以后他们开始研制Mark 1的继任者，也就是包含有一个浮点单元的Meg。
***
## Algorithmic Efficiency 

**Max Flow Problem**: 最大流通量问题  
- 起源：1955年，美国RAND公司的研究员在文章*The Capacity of Soviet's Railway*中首次提出该问题：苏联通过铁路系统向白令海峡输送军备的最大流通量是多少  ？

线性算法：时间复杂度与问题规模成正比 O(n) 如：线性查找  
二分查找的复杂度为 O(logn) *\* 可证明: 查找算法的最低时间复杂度即为O(logn)*