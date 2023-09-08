# 课前须知
> [课程主页](http://staff.ustc.edu.cn/~lszhuang)
http://staff.ustc.edu.cn/~lszhuang
## 关于评分
> - 期末考试（闭卷）+平时作业（按时交作业在原有基础+1分）+出勤（未到不扣分，到了加分）
> - 提交作业在bb系统上面的网页系统（搭建的oj系统）
> - 上机有3个实验，建议提前做
> - 本课程不提供补考，只有重修

# 第一章 算法分析技术
## 算法入门
### 课程学习背景（这节不重要）
#### 算法定义
- ***算法就是问题的程序化解决方案***。它定义了一个良好的计算过程，取一个或者一组值作为输入，并产生出一个或者一组值作为输出。即：算法就是一系列的计算步骤，用来将输入数据转换成输出结果。

```mermaid
graph LR
A((输入)) --> B[计算过程]
B --> C((输出))
B --- D(算法)
```

#### 算法特征

```mermaid
graph LR
A((输入)) --> B[每个算法具有一个或者多个来自指定集合的输入值]
A --- C((输出))
C --> D[每次输入至少具有1个输出值]
C --- E((确定性))
E --> F[算法的每个指令步骤都是明确的]
E --- G((有限性))
G --> H[每次输入都必须在有限步骤内结束]
G --- I((正确性))
I --> J[每次输入都应产生出正确的输出值]
I --- K((通用性))
K --> L[算法的执行过程可应用于所有同类问题求解,不是仅适用于特殊的输入]
```

#### 问题与问题实例
- 问题:规定了输入与输出之间的关系，可用通用语言来描述。
- 问题实例:某一个问题的实例包含了求解该问题所需的输入。
- 问题例子：
  > ① 排序问题：将一系列数按非降顺序进行排序
  ```
  输入: 由n个数组成的一个序列<𝒂𝟏,𝒂𝟐,…,𝒂𝒏 >
  输出: 对输入系列的一个排列(重排) <𝒂𝟏,𝒂𝟐,…,𝒂𝒏>,使得𝒂𝟏≤𝒂𝟐≤ ⋯ ≤𝒂𝒏
  ```
  > ② 一个实例：
  ```
  Input: <31,41,59,26,41,58> —— Output:      <26,31,41,41,58,59>
  ```
- 重要问题类型：排序、字符串匹配、图搜索问题、几何问题、数值问题等。

#### 输入实例与问题规模
- 输入实例：问题的具体计算例子；
- 问题规模：算法的输入实例大小。
如, 排序问题的3个输入实例:
```
① 13,5,6,37,8,92,12
② 43,5,23,76,25
③ 53,67,32,42,22,33,4,39,56
上面排序问题的3个输入实例的规模大小分别为7,5,9
```

#### 正确算法与不正确算法
- 正确的算法 
  > 如果一个算法对问题每一个输入实例，都能输出正确的结果并停止，则称它为正确的。
- 不正确的算法
  > - ✓可能根本不会停止；
  > - ✓停止时给出的不是预期的结果；
  > - ✓如果算法的错误率可以控制，
  > - ***也是有用的***。

### 算法分析基础
#### 问题求解与算法描述
##### 问题求解过程
- 与真实代码差异
  > - ① 对特定算法的描述更加的清晰与精确；
  > - ② 不需要考虑太多技术细节（数据抽象、模块、错误处理等）；
  > - ③ 用伪代码可以体现算法本质；
  > - ④ 永远不会过时。
- 伪代码一些约定
  > - ① 书写上的“缩进”表示程序中的分程序（程序块）结构；
  > - ② 循环结构(while, for, repeat) 和条件结构 (if, then, else) 与Pascal, C语言类似；
  > - ③ “// ” or “►”来表示注释；
  > - ④ 利用i←j←e 来表示多重赋值，等价于 j←e 和i←j；
  > - ⑤ 变量是局部于给定过程的；
  > - ⑥ 数组元素的访问方式: A[i] ; A[1 .. j ] = < A[1], A[2],…, A[i]>
  > - ⑦ 符合数据一般组织成对象，由属性（attribute）或域(field)所组成；域的访问是由域名后跟方括号括住的对象名形式来表示, 如length[A]；
  > - ⑧ 参数采用按值传递方式；
  > - ⑨ 布尔操作 “and” 和“or”具有短路能力: 如 “x and (or) y ”: 无论y的值如何，必须首先计算x的值。

#### 算法分析框架(import)
- [ ] 算法分析：指对一个算法所需要的 ***资源*** 进行预测，通常是对计算 ***时间和空间*** 的预测。
  - [x] 默认情况下，一般是指对算法 ***时间效率*** 的分析；
  - [x] ***目的是从多个候选算法中选择一个最有效的算法或者去掉较差的算法。***
- [ ] 随机存取机模型
  - [x] 指令时逐条执行的，没有并发操作；
  - [x] 只包含常用指令且指令执行时间为常量；
  - [x] 数据类型有整数类型和浮点实数类型；
  - [x] 不对存储器层次进行建模。
- ***算法运行时间是指在特定输入时，所执行的基本操作数。***
- ***输入数据的规模和分布*** 是影响算法运行时间的两个 ***主要因素***。
- ***算法时间效率分析框架：***
  - [x] 算法时间效率用算法输入规模n为参数的函数来度量；
  - [x] 对输入规模相同情况下，有些算法的时间效率会有明显差异。对于这样的算法要区分最坏运行时间、最佳运行时间、平均运行时间；
  - [x] 对于大规模输入，通常只关注运行时间效率函数的增长率，即只关注函数的高阶项，而忽略低阶项和高阶项系数。
- ***最坏运行时间***
  - [x] 对于规模为n的任何输入，一般考察算法的最坏运行时间。
  - [x] 最坏情况运行时间是在任何输入情况下的一个上界；
  - [x] 对于某些算法来说，最坏情况出现还是比较频繁的，如信息检索（信息经常不存在）；
  - [x] 大致上看，“平均情况”通常和最坏情况一样差。
- 平均运行时间（期望运行时间）
- ***函数的增长率***
  - [x] 抽象简化。忽略每条语句的真实代价，用常量ci来表示；进一步忽略了抽象的代价；
  - [x] 增长率或增长量级。只考虑公式中的最高项，忽略最高项系数和低阶项。

#### 示例:插入排序
```
问题描述: 把一系列数据按非递增的顺序排列
输 入: n 个输入数<𝑎1,𝑎2,…,𝑎𝑛>
输 出: 输入系列的一个排序 <𝑎1,𝑎2,…,𝑎𝑛> , 使得𝑎1≤𝑎2≤⋯≤𝑎𝑛
```
```C
NSERTION-SORT(A)                                               cost times
1 for( j = 2; j <=length[A]; j++)                               c1   n
2 { key = A[j]                                                  c2   n-1
3     // Insert A[j] into the sorted sequence A[1 .. j-1]   0   n-1
4     i = j-1          c4  n-1
5     while( i > 0 && A[i] > key)                                c5
6     { A[i+1] = A[i]                                            c6
7         i = i-1                                                c7
8     }
9     A[i+1] = key                                               c8 n-1
10 }
```
