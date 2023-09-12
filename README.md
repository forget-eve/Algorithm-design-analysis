# 课前须知
> [课程主页](http://staff.ustc.edu.cn/~lszhuang)
http://staff.ustc.edu.cn/~lszhuang
## 关于评分
> - 期末考试（闭卷）+平时作业（按时交作业在原有基础+1分，作业也有考研算法部分 ~~，做了加分~~）+出勤（未到不扣分，到了加分）
> - 提交作业在bb系统上面的网页系统（搭建的oj系统(http://202.38.88.88:45008/)）
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
##### 问题描述
```
问题描述: 把一系列数据按非递增的顺序排列
输 入: n 个输入数<𝑎1,𝑎2,…,𝑎𝑛>
输 出: 输入系列的一个排序 <𝑎1,𝑎2,…,𝑎𝑛> , 使得𝑎1≤𝑎2≤⋯≤𝑎𝑛
```
##### 算法效率分析
```C
NSERTION-SORT(A)                                               cost times
1 for( j = 2; j <=length[A]; j++)                               c1   n
2 { key = A[j]                                                  c2   n-1
3     // Insert A[j] into the sorted sequence A[1 .. j-1]       0    n-1
4     i = j-1                                                   c4   n-1
5     while( i > 0 && A[i] > key)                               c5
6     { A[i+1] = A[i]                                           c6
7         i = i-1                                               c7
8     }
9     A[i+1] = key                                              c8   n-1
10 }
```
- 总时间效率
  > 注: $t_j$ 为当第j轮执行for循环时，while语句需要执行的次数(重排前面排过序列的次数)
$$T(n)=c_1 n+c_2 (n-1)+c_4 (n-1)+c_5 \sum\limits_{j=2}^n t_j +c_6 \sum\limits_{j=2}^n (t_j -1)+c_7 \sum\limits_{j=2}^n (t_j -1) +c_8 (n-1)
$$
- 如果数组是排好序的，则会出现最好情况：
$$T(n)=c_1 n+c_2 (n-1)+c_4 (n-1)+c_5 (n-1) +c_8 (n-1)=(c_1 +c_2 +c_4 +c_5 +c_8)n–(c_2 +c_4 +c_5 +c_8))=an+b
$$
- 如果数组是逆序排序的，则会出现最坏情况：
$$T(n)=c_1 n+c_2 (n-1)+c_4 (n-1)+c_5 \left(\frac{n(n+1)}{2}-1\right)+c_6 \left(\frac{n(n-1)}{2}\right)+c_7 \left(\frac{n(n-1)}{2}\right)+c_8 (n-1)=an^3 +bn+3
$$
  > 此时必须将每个元素A[j]与整个已排序的子数组A[1..j-1]中的每一个元素进行比较，对j=2,3,…,n,有 $t_j=j$ ,则有：
$$\sum\limits_{j=2}^n j=\frac{n(n+1)}{2}-1，\sum\limits_{j=2}^n (j-1)=\frac{n(n-1)}{2}
$$

### 算法设计策略——分治法
#### 概述
- 核心思想： 分而治之，各个击破。
- 分治策略：
  > ① 将原问题划分为n个规模较小而结构与原问题相似的子问题；

  > ② 递归地解决这些子问题，然后再合并其结果，得到原问题解。

- 三个步骤
  > ① 分解（Divide)：将原问题分成一系列子问题；

  > ② 解决（Conquer)：递归求解各子问题。若子问题足够小，则直接求解；

  > ③ 合并（Combine)：将子问题的结果合并成原问题的解。

#### 示例：归并排序
##### 归并排序算法(Merge sort algorithm)
> ① 分解：把n个元素分成各含n/2个元素的子序列；

> ② 解决：用归并排序算法对两个子序列递归地排序；

> ③ 合并：合并两个已排序的子序列以得到排序结果。

```mermaid
graph TB
A[2 3 8 1 4 5 7 6] <--> B[2 3 8 1]
A <--> C[4 5 7 6]
B <--> D[2 3]
B <--> E[8 1]
C <--> F[4 5]
C <--> G[7 6]
D <--> H[2]
D <--> I[3]
E <--> J[8]
E <--> K[1]
F <--> L[4]
F <--> M[5]
G <--> N[7]
G <--> O[6]
```
> 对子序列排序时，其长度为1时递归结束。单个元素被视为是已排好序的。

##### 关键步骤
MERGE(A, p, q, r)是关键步骤。
- [x] A是个数组，p, q, r 数组中元素的下标，且p ≤ q < r.
- [x] 假设子数组 A[p .. q] 和 A[q+1 .. r]是有序的，将它们合并成一个已排好序的子数组代替当前子数组 A[p .. r]。
- [x] 合并过程:
```mermaid
graph TB
A[        ?       ]
B[2 3 8 1] -->A
C[4 5 7 6] -->A
```
  > 合并其实是同层(在此层下层处已经按照该步骤，将该层数组内元素的顺序排好了)合并至上层(父层)，先比较同层的2个子数组中第一个位置元素大小(分别为a，b)，按照排序规则放入上层第一个位置，假设为a，然后比较a所在子数组内的元素和b的大小，再进行放入第二个位置，以此类推排好上层元素顺序。
- [x] MERGE(A, p, q, r)算法伪代码
```C
MERGE(A, p, q, r)                                       cost  times
1 n1 ← q-p+1                                             c    1
2 n2 ← r-q                                               c    1
3 create arrays L[1 .. n1+1] and R[1 .. n2+1]               c    1
4 for i←1 to n1                                          c    n1+1
5     do L[i]←A[p+i-1]                                    c    n1
6 for j←1 to n2                                          c    n2+1
7     do R[j]←A[q+j]                                     c    n2
8 L[n1+1]←∞          //设置哨兵元素                         c    1
9 R[n2+1]←∞          //设置哨兵元素                         c    1
10 i←1                                                  c    1
11 j←1                                                  c    1
12 for k←p to r                                          c    r-p+2
13    do if L[i]≤R[j]                                    c    r-p+1
14        then A[k]←L[i]                                 c    x
15            i←i+1                                      c    x        
16        else A[k]←R[j]                                c    r-p+1-x
17            j←j+1                                     c    r-p+1-x
```
  - 时间复杂度：
$$𝜃(𝑛_1 + 𝑛_2)= 𝜃(𝑛)$$
- [x] 递归算法
```C
MERGE-SORT(A, p, r)
1 if p < r
2     Then 𝑞 ← (𝑝 + 𝑟)/2
3         MERGE-SORT(A, p, q)
4         MERGE-SORT(A, q+1, r)
5 MERGE(A, p, q, r)
```
```mermaid
graph TB
B[2 3 8 1] --> D[2 3]
B --> E[8 1]
D <--> H[2]
D <--> I[3]
E <--> J[8]
E <--> K[1]
A[2 3 8 1]
C[2 3] --> A
F[1 8] --> A
G[2] --> C
L[3]--> C
M[8] --> F
N[1] --> F
```

##### 分支法分析
###### 分治法时间复杂度

$$ 
T(n)=
\begin{cases}
  Θ(1), & \text{if } n \geq c \\
  aT(n/b)+D(n)+C(n), & \text{otherwise } 
\end{cases}
$$

➢ D(n)是把原问题分解为子问题所花的时间；

➢ C(n)是把子问题的解合并为原问题的解所花的时间；

➢ T(n)是一个规模为n的问题的运行时间，a和b可认为将规模n分解为a个规模为n/b的问题。
> 为简化算法分析，通常假设n为2的幂次，使得每次分解产生的子序列长度恰为n/2。这一假设并不影响递归式解的增长量级。

###### 合并排序最坏运行时间
- ① 当n=1时，合并排序一个元素的时间是个常量；
- ② 当n>1时，运行时间分解如下：
  > ➢ 分解：仅仅是计算出子数组的中间位置，需要常量时间，D(n)=Θ(1)；
  > 
  > ➢ 解决：递归地求解两个规模为n/2的子问题，时间为2T(n/2)；
  > 
  > ➢ 合并：MERGE过程的运行时间为C(n)=Θ(n)。

$$
T(n)=
\begin{cases}
  Θ(1), & \text{if } n =1 \\
  2T(n/2)+Θ(n), & \text{if } n >1
\end{cases}
$$
##### 归并排序时间复杂度求解
- 递归式重写

$$
T(n)=
\begin{cases}
  Θ(1), & \text{if } n =1 \\
  2T(n/2)+Θ(n), & \text{if } n >1
\end{cases}
 →
T(n)=
\begin{cases}
  Θ(1), & \text{if } n =1 \\
  2T(n/2)+cn, & \text{if } n >1
\end{cases}
$$
- 递归式求解
$$cn(\lg n+1)=cn\lg n+cn=Θ(n\lg n)$$
其中：
  - [x] 每一层总代价: $2^i c(n/2^i)=cn$
    > 即为一个树状图，每层有 $2^i$ 个，每个的运行时间为 $c(n/2^i)$ 。
  - [x] 树的总层数: $\lg n+1$
    > 推导：假设树的总层数为d，则根据等比数列1,2,4,..., $2^d$ 的求和所得 $2^{d+1}-1$ ,则有不等式 $2^{d}-1 \leq n \leq2^{d}-1$ ,求解不等式后可得 $d\approx\lg n+1$

## 函数增长
### 渐进记号
#### 渐进记号
- 函数的增长量级
  > 用于简单地刻画算法效率，舍弃了低阶项和高阶项的系数。
- 函数的渐近效率
  > 当输入规模无限增加时，描述了算法的运行时间如何随着输入规模的变大而增加。也就是，描述函数的渐近增长行为。
- 渐近记号
  > 用来描述算法渐近运行时间的渐近界，主要用于简化算法的渐近分析。本质上，渐近记号作用于定义域为自然数集N={0,1,2,…}的函数上，代表了一个函数集合。
$$o\approx <;O\approx \leq; \Theta\approx =;\Omega\approx \geq;\omega\approx >$$

#### Θ记号：渐近紧界（asymptotically tight bound）
##### 定义
- 𝜽(𝒈(𝒏))定义：
  > 对给定函数 $𝑔(𝑛)，𝜃(𝑔(𝑛))$ 表示以下函数的集合：
  $$𝜃(𝑔(𝑛))= \lbrace 𝑓(𝑛):∃正常数𝑐_1,𝑐_2,𝑛_0,∀𝑛 ≥ 𝑛_0,有0 ≤ 𝑐_1𝑔(𝑛)≤𝑓(𝑛)≤𝑐_2𝑔(𝑛)\rbrace$$
  > 类似 `夹逼定理` 。
- 说明：
  > ① 𝑔(𝑛)是𝑓(𝑛)的一个渐近紧确界；
  > 
  > ② 𝜃(𝑔(𝑛))定义要求每个成员𝑓(𝑛)均渐近非负，𝑔(𝑛)本身也渐近非负。本课程后面应用于渐近记号的函数均认为满足该假设；
  > 
  > ③ 𝑓(𝑛)∈ 𝜃(𝑔(𝑛))表示𝑓(𝑛)是𝜃(𝑔(𝑛))的成员，可以简写为𝑓(𝑛)= 𝜃(𝑔(𝑛)) 。

##### 举例

例子1：证明 $\frac{n^2}{2}-3n=\omega(n^2)$

证明：假设 $∃c_1,c_2和n_0$ ,使得 $∀𝑛 ≥ 𝑛_0$ ,有 $c_1 n^2 \leq\frac{n^2}{2}-3n \leq c_2n^2$

⟹ $c_1 \leq\frac{1}{2}-\frac{3}{n}\leq c_2$ 当𝑛 → ∞时，可以得到 $c_1 \leq\frac{1}{2},c_2\geq\frac{1}{2}$ 。

取 $c_1=\frac{1}{14},c_2=\frac{1}{2}$ ,以及 $n_0=7$ ,可以证明 $\frac{n^2}{2}-3n=\omega(n^2)$

例子2：证明 $6n^3\neq\omega(n^2)$
证明：(反证法)
假设 $∃c_2 >0,n_0 >0$ 使得所有的 $n>n_0$ ,由 $6n^3\leq\omega(n^2)$ 。

也就是说,对于所有 $n\geq n_0$ 都有 $n\leq c_2/6$ 成立,而不等式的右边是个常数，显然不可能对任意大的𝑛成立。

##### 关于渐进紧界
- 通常情况下，可以把一个函数的低阶项和高阶项系数忽略，从而得到函数的渐近紧界。
  > 比如: $f(n)=an^2+bn+c$ ,其中，a>0,b,c为常量，则有 $f(n)=\theta (n^2)$ 。
- 一般情况下，对任意的多项式 **$p(n)=\sum\limits_{i=0}^d a_in^i$** ,其中 $a_i$ 是常数且 $a_d>0$ , 我们有 $𝒑(𝒏)=\theta (𝒏_d)$ 。
- 任意常数函数都可以用渐近符号 $\theta (𝒏_𝟎)$ 或 $\theta (𝟏)$ 来表示，通常利用 $\theta (𝟏)$ 来表示常数或者常数函数。

#### 𝑂记号：渐近上界（asymptotically upper bound）
##### 𝑂(𝒈(𝒏))定义
- 对给定函数𝑔(𝑛)，𝑂(𝒈(𝒏))表示以下函数的集合：
  $$𝑂(𝑔(𝑛)) = \lbrace 𝑓(𝑛) :∃正常数𝑐,  𝑛_0 > 0，∀𝑛 ≥ 𝑛_0,有0 ≤ 𝑓(𝑛) ≤ 𝑐𝑔(𝑛)\rbrace$$
> 理解为𝑓(n)一直向上趋近于𝑔(𝑛)
##### 关于渐进上界的说明
###### 𝑓(𝑛)=𝑂(𝑔(𝑛))说明
1. 𝑔(𝑛)是𝑓(𝑛)的一个 `渐近上界` ；
2. 每个成员𝑓(𝑛)均渐近非负，𝑔(𝑛)本身也渐近非负；
3. 𝑓(𝑛)= 𝑂(𝑔(𝑛)) 等价于𝑓(𝑛)∈ 𝑂(𝑔(𝑛))，意味着𝑓(𝑛)是集合𝑂(𝑔(𝑛))的成员;
4. 如果𝑓(𝑛)=𝜃(𝑔(𝑛)) ，则𝑓(𝑛)=𝑂(𝑔(𝑛))，𝜃(𝑔(𝑛))=𝑂(𝑔(𝑛))，反之不成立。
###### $𝑂(n^2)$ 函数举例
$an^2+bn+c$ , $an$ , $n^{1.9999}$ , $n^2 / \lg \lg \lg n$

#### 𝜴记号：渐近下界(asymptotically lower bound)
##### 𝜴(𝒈(𝒏))定义
- 对给定函数𝑔(𝑛)，𝛺(𝑔(𝑛))表示以下函数的集合：
  $$𝛺(𝑔(𝑛))=\lbrace 𝑓(𝑛):∃正常数𝑐, 𝑛_0 > 0，∀𝑛 ≥ 𝑛_0,有0 ≤ 𝑐𝑔(𝑛)≤𝑓(𝑛)\rbrace$$
> 理解为𝑓(n)一直向下趋近于𝑔(𝑛)
##### 关于渐进下界的说明
###### 𝑓(𝑛)=𝛺(𝑔(𝑛))说明
1. 𝑔(𝑛)是𝑓(𝑛)的一个 `渐近下界` ；
2. 每个成员𝑓(𝑛)均渐近非负，𝑔(𝑛)本身也渐近非负；
3. 𝑓(𝑛)= 𝛺(𝑔(𝑛)) 等价于𝑓(𝑛)∈ 𝛺(𝑔(𝑛))，意味着𝑓(𝑛)是集合𝛺(𝑔(𝑛))的成员;
4. 如果𝑓(𝑛)=𝜃(𝑔(𝑛)) ，则𝑓(𝑛)=𝛺(𝑔(𝑛))，𝜃(𝑔(𝑛))=𝛺(𝑔(𝑛))，反之不成立。
###### $𝛺(n^2)$ 函数举例
$an^2+bn+c$ , $n^3$ , $n^{2.000001}$ , $n^2 \lg \lg \lg n$
##### 定理3.1 
- 对任意两个函数𝒇(𝒏)和𝒈(𝒏)，有𝒇(𝒏)=𝜽(𝒈(𝒏))当且仅当𝒇(𝒏)=𝑶(𝒈(𝒏))且𝒇(𝒏)=𝜴(𝒈(𝒏))同时成立。
  > 证明:
  > 
  > → $𝒇(𝒏)=𝜽(𝒈(𝒏)),then \ ∃c_2>0,c_2>0,n_0>0,$
  > 
  >   $s.t. \ n \geq n_0,0 \leq c_1𝒈(𝒏) \leq 𝒇(𝒏) \leq c_2𝒈(𝒏)$
  > 
  >   $then \ n \geq n_0,0 \leq 𝒇(𝒏) \leq c_2𝒈(𝒏)⟹ 𝒇(𝒏)=𝑶(𝒈(𝒏))$
  >
  >   $then \ n \geq n_0,0 \leq c_1𝒈(𝒏) \leq 𝒇(𝒏)⟹ 𝒇(𝒏)=𝜴(𝒈(𝒏))$
  > 
  > ← $𝒇(𝒏)=𝑶(𝒈(𝒏)),then \ ∃c_2>0,c_{20}>0,n_{20}>0,$
  >
  >   $s.t. n \geq n_{20},0 \leq 𝒇(𝒏) \leq c_{20}𝒈(𝒏)$
  > 
  >   $𝒇(𝒏)=𝜴(𝒈(𝒏)),then \ ∃c_2>0,c_{10}>0,n_{10}>0,$
  > 
  >   $s.t. n \geq n_{10},0 \leq c_{20}𝒈(𝒏) \leq 𝒇(𝒏)$
  >
  >   $let \ n_0=max\lbrace n_{10},n_{20}\rbrace,then \ n \geq n_0$
  > 
  >   $0\leq c_{10}𝒈(𝒏) \leq 𝒇(𝒏)\leq c_{20}𝒈(𝒏),that \ is \ 𝒇(𝒏)=𝜽(𝒈(𝒏))$

#### 关于渐进上界和下界某些说明
- [x] 算法的运行时间为𝑂(𝑔(𝑛))意味着：当𝑛足够大时，对输入规模为𝑛的任意输入，其运算时间至多是𝑔(𝑛)的一个常数倍；
- [x] 算法的运行时间为𝜴(𝑔(𝑛))意味着：当𝑛足够大时，对输入规模为𝑛的任意输入，其运算时间至少是𝑔(𝑛)的一个常数倍；
- [x] 部分问题：
  > ✓ 插入排序的算法运行时间为 $𝑂(𝑛^2)$ ？还是 $𝜴(𝑛^2)$ ？还是 $𝜃(𝑛^2)$ ？
  > > 这个问题的答案应该是要分开回答的，一般最坏情况运行时间为 $𝑂(𝑛^2)$ ，平均运行时间认为是 $𝜃(𝑛^2)$ ，最好情况运行时间为 $𝜴(𝑛^2)$ 。
  > ✓ 插入排序的算法最坏运行时间为 $𝑂(𝑛^2)$ ？还是 $𝜴(𝑛^2)$ ？还是 $𝜃(𝑛^2)$ ？
  > > $𝑂(𝑛^2)$ ,表示在最坏情况下，它的运行时间是二次多项式级别的。
  > ✓ 我们如果说一个算法的运行时间不超过 $𝜴(𝑛^2)$ ，这是否有矛盾？为什么？
  > > 说一个算法的运行时间不超过 $𝜴(𝑛^2)$ 没有矛盾，因为这也是一个上界条件。

#### 等式和不等式中的渐近记号
- 如何解释：“𝒏 = $𝑶(𝒏^2)$ ”,” $𝟐𝒏^𝟐 + 𝟑𝒏 + 𝟏 = 𝟐𝒏^2+ 𝜽(𝒏)$ ”, …
  - [ ] 渐近记号单独在等式的右侧，比如𝑛 = $𝑂(𝑛^2)$ ，这表示左侧函数属于右侧集合的一个
成员，即 $𝑛 ∈ 𝑂(𝑛^2)$;
  - [ ] 渐近记号出现在一个公式的内部，比如” $2𝑛^2 + 3𝑛 + 1 = 2𝑛^2 + 𝜃(𝑛)$ ”表示存在某个匿名函数𝑓(𝑛)使得” $2𝑛^2 + 3𝑛 + 1 = 2𝑛^2 + 𝑓(𝑛)$ ”成立，其中𝑓(𝑛)∈ 𝜃(𝑛)；
  - [ ] 渐近记号出现在等式的左侧，可以被解释为无论怎样从左侧渐近记号表示的集合中选择成员，总是可以从右侧的渐近记号表示的集合中选择某个成员使得等式成立。例如“ $2𝑛^2 + 𝜃(𝑛)= 𝜃(𝑛^2)$” 可解释为任给𝑓(𝑛)∈ 𝜃(𝑛)，存在𝑔(𝑛)∈ $𝜃(𝑛^2)$ ，使等式成立。
- [x] **因此，我们可以列出等式” $𝟐𝒏^𝟐 + 𝟑𝒏 + 𝟏 = 𝟐𝒏^𝟐 + 𝜽 𝒏 = 𝜽(𝒏^𝟐)$ ”.**

#### o记号：非渐近紧确上界
- [x] 𝑂(𝑔(𝑛))的局限性：
  > 如：2𝑛 = 𝑂(𝑛)是渐近紧确的，但是 $2𝑛 = 𝑂(𝑛^2)$ 不是渐近紧确的。
- [x] 𝒐(𝒈(𝒏))表示一个非渐近紧确上界：
  > 对给定函数𝑔(𝑛)，𝑜(𝑔(𝑛))表示以下函数的集合：
  >
  > $𝑜(𝑔(𝑛))=\lbrace 𝑓(𝑛):对于任意正常数𝑐, ∃𝑛_0> 0，∀𝑛 ≥ 𝑛_0,有0 ≤ 𝑓(𝑛) < 𝑐𝑔(𝑛) \rbrace$
  > > 例， $2𝑛 = 𝑜(𝑛^2)$ ，但是 $2𝑛^2 ≠ 𝑜(𝑛^2)$ 。

#### ω记号：非渐近紧确下界
- [x] Ω(𝑔(𝑛))的局限性：
  > 如： $2𝑛^2 = 𝛺(𝑛^2)$ 是渐近紧确的，但是 $2𝑛^2 = 𝛺(𝑛)$ 不是渐近紧确的。
- [x] 𝝎(𝒈(𝒏))表示一个非渐近紧确下界：
  > 对给定函数𝑔(𝑛)，𝜔(𝑔(𝑛))表示以下函数的集合：
  > 
  > $𝜔(𝑔(𝑛))=\lbrace𝑓(𝑛):对于任意正常数𝑐, ∃𝑛_0> 0，∀𝑛 ≥ 𝑛_0,有0 ≤ 𝑐𝑔(𝑛) < 𝑓(𝑛)\rbrace$
  > >例， $2𝑛^2 = ω(𝑛)$ ，但是 $2𝑛^2 ≠ ω(𝑛^2)$ 。
- [x] 𝒇(𝒏)= 𝝎(𝒈(𝒏)) 当且仅当𝑔(𝑛)=𝑜(𝑓(𝑛))成立，存在极限： $\lim\limits_{n \to \infty} \frac{𝑓(𝑛)}{𝑔(𝑛)} = \infty$

#### 函数比较
- [x] 传递性
  > $𝒇(𝒏)=\theta (𝑔(𝑛)) \ and \ 𝑔(𝑛)=\theta (h(𝑛)) \ imply \ 𝒇(𝒏)=\theta (h(𝑛))$
  >
  > $𝒇(𝒏)=O(𝑔(𝑛)) \ and \ 𝑔(𝑛)=O(h(𝑛)) \ imply \ 𝒇(𝒏)=O(h(𝑛))$
  >
  > $𝒇(𝒏)=\Omega(𝑔(𝑛)) \ and \ 𝑔(𝑛)=\Omega (h(𝑛)) \ imply \ 𝒇(𝒏)=\Omega (h(𝑛))$
  >
  > $𝒇(𝒏)=o(𝑔(𝑛)) \ and \ 𝑔(𝑛)=o(h(𝑛)) \ imply \ 𝒇(𝒏)=o(h(𝑛))$
  >
  > $𝒇(𝒏)=w(𝑔(𝑛)) \ and \ 𝑔(𝑛)=w(h(𝑛)) \ imply \ 𝒇(𝒏)=w(h(𝑛))$

- [x] 对称性
  > $𝒇(𝒏)=\theta (𝑔(𝑛)) \ if \ and \ only \ if \ 𝑔(𝑛)=\theta (𝒇(𝒏))$

- [x] 反对称性
  > $𝒇(𝒏)=O(𝑔(𝑛)) \ if \ and \ only \ if \ 𝑔(𝑛)=\Omega (𝑔(𝒏))$
  >
  > $𝒇(𝒏)=\Omega (𝑔(𝑛)) \ if \ and \ only \ if \ 𝑔(𝑛)=O(𝑔(𝒏))$

- [x] 自反性
  > $𝒇(𝒏)=\theta (𝒇(𝒏))$
  >
  > $𝒇(𝒏)=O(𝒇(𝒏))$
  >
  > $𝒇(𝒏)=\Omega(𝒇(𝒏))$

- [x] 与实数比较进行类比
  > $𝒇(𝒏)=o(𝑔(𝑛)) \approx a < b$
  >
  > $𝒇(𝒏)==O(𝑔(𝑛)) \approx a \leq b$
  > 
  > $𝒇(𝒏)=\theta (𝑔(𝑛)) \approx a=b$
  > 
  > $𝒇(𝒏)=\Omega(𝑔(𝑛)) \approx a \geq b$
  > 
  > $𝒇(𝒏)=w(𝑔(𝑛)) \approx a > b$

- [x] 实数的三分性定理
  > 任意两个实数 𝑎 和 𝑏, 它们的大小关系必然满足三种关系的其中之一: 𝑎 < 𝑏, 𝑎 = 𝑏 或𝑎 > 𝑏。
- [x] 不是所有的函数都是渐近可比较的，比如：
  > 函数 $𝑓(𝑛)= 𝑛^{1+𝑠𝑖𝑛𝑛}$ 和 函数 $𝑔(𝑛)=𝑛$ 就无法用渐近记号相互比较！
  > > $-1 \leq sinn \leq 1⟹n^0 \leq n^{1+𝑠𝑖𝑛𝑛} \leq n^2$
  > >
  > > $n^{1+𝑠𝑖𝑛𝑛} \leq n \leq n^{1+𝑠𝑖𝑛𝑛} ,矛盾$

### 常用函数
#### 标准记号与常用函数
- [x] 下取整与上取整(Floors and ceilings)
$$x-1 < \lfloor x \rfloor \leq x \leq \lceil x \rceil < x+1$$
- [x] 模运算(Modular arithmetic)
$$a \ mod \ n=a- \lfloor a/n \rfloor n$$
- [x] 多项式(Polynomials)
$$p(n)=\sum\limits_{i=0}^d a_in^i$$
- [x] 指数(Exponentials)
- [x] 对数(Logarithms)
- [x] 阶乘(Factorials)
> ***斯特林近似公式*** ，考试会给出来，不用特地记

$$n!=\sqrt{2\pi n}\left(\frac{n}{e}\right)^n\left(1+\theta\left(\frac{1}{n}\right)\right)$$
$$⟹n!=o(n^n),n!=w(2^n),\lg (n!)=\theta (n\lg n)$$
- [x] 迭代函数(Functional iteration)
  > 使用记号 $𝑓^{(𝑖)}(𝑛)$ 来表示函数𝑓(𝑛)使用初始值𝑛进行迭代𝑖次后的结果。对非负的𝑖，递归地定义

$$
𝑓^{(𝑖)}(𝑛)=
\begin{cases}
  n, & \text{if } i =0 \\
  𝑓(𝑓^{(i-1)}(n)), & \text{if } i >0
\end{cases}
$$
  > 假设𝑓(𝑛)= 2𝑛，那么

$$𝑓^{(2)}(𝑛)=𝑓(𝑓(𝑛))=𝑓(2𝑛)=2(2n)=2^2n$$

$$...$$

$$𝑓^{(𝑖)}(𝑛)=2^in$$
- [x] 多重对数函数（The iterated logarithm function）
  > 使用记号lg*n来表示。令 $\lg ^{(𝑖)} 𝑛$ 为之前定义的迭代函数,其中𝑓(𝑛)=𝑙𝑔𝑛,即 $\lg ^{(𝑖)} 𝑛 = \lg(\lg ^{(𝑖−1)}(𝑛))$ 。 $\lg ^{(𝑖)} 𝑛$ 有定义仅当 $\lg ^{(𝑖−1)} 𝑛 > 0$ 。注意区分 $\lg^{(𝑖)} 𝑛$ 与 $\lg ^𝑖 𝑛$ 。

$$\lg^\*n 被定义为：\lg^\*n=min\lbrace i \leq 0:\lg^{(i)}n \leq 1\rbrace$$

> 多重对数函数是一个增长十分缓慢的函数：

$$\lg^\*2=1,\lg^\*4=2,\lg^\*16=3,\lg^\*65536=4,\lg^\*2^65536=5$$

> $2^{65536}>>10^{80}$ ,极少会遇到使 $\lg ^\* n>5$
- [x] 斐波那契数（Fibonacci numbers）

### 级数求和
#### 级数求和
- [x] 定义：有限和、无限和、级数收敛、级数发散的、绝对收敛级数
- [x] 等差级数： $\sum\limits\_{k=1}^n k=1+2+...+n=\frac{1}{2}n(n+1)=\theta (n^2)$
- [x] 平方和与立方和： $\sum\limits\_{k=0}^n k^2=\frac{n(n+1)(2n+1)}{6}$ , $\sum\limits\_{k=0}^n k^3=\frac{n^2(n+1)^2}{4}$
- [x] 几何级数： $\sum\limits\_{k=0}^n x^k=1+x+x^2+...+x^n=\frac{x^{n+1}-1}{x-1}$
- [x] 调和级数： $H_n=1+\frac{1}{2}+\frac{1}{3}+...+\frac{1}{n}=\sum\limits\_{k=1}^n \frac{1}{k}=\ln n+O(1)$
- [x] 级数的积分和微分： $\sum\limits_{k=0}^{\infty}kx^k=\frac{x}{(1-x)^2}$

#### 确定求和时间的界
- [x] 数学归纳法
1. 计算级数的准确值
2. 计算和式的界，如：证明几何级数 $\sum\limits_{k=1}^n3^k$ 的界是 $O(3^n)$
3. 一个容易犯的错误，如：证明 $\sum\limits_{k=1}^nk=O(n)$
- [x] 确定级数各项的界
1. 一个级数的理想上界可以通过对级数中的每个项求界来获得；
2. 一个级数实际上以一个几何级数为界时，可以选择级数的最大项作为每项的界（注意防止犯错！）
- [x] 分割求和：可以将级数表示为两个或多个级数，按下标的范围进行划分，然后再对每个级数分别求界。

## 递归式求解
### 代换法
#### 引言
- [x] 递归式: 是一组等式或不等式，用更小输入下该函数的值来定义自身。

$$
T(n)=
\begin{cases}
  1, & \text{if } n =1 \\
  2T\left(\frac{n}{2}\right)+n, & \text{if } n >1
\end{cases}
$$

- [x] 一些细节：
1. 假设函数自变量为整数，忽略上取整和下取整，如：

$$
T(n)=
\begin{cases}
  \theta (1), & \text{if } n =1 \\
  T\left(\lceil\frac{n}{2}\rceil\right)+T\left(\lfloor\frac{n}{2}\rfloor\right)+\theta (n), & \text{if } n >1
\end{cases}
$$

2. 忽略递归式的边界条件，并假设对于小的n值，T(n)是常量。

$$
T(n)=2T\left(\frac{n}{2}\right)+\theta (n)
$$

- [x] 递归式求解方法：
  > A. 代 换 法：先猜有某个解存在，用数学归纳法证明猜测的正确性；
  >
  > B. 迭 代 法：把递归式转化为求和表达式，然后求和式的界；
  >
  > C. 递归树法：直观地表达了迭代法；
  >
  > D. 主 方 法：给出求解𝑇(𝑛)=𝑎𝑇(𝑛/𝑏)+𝑓(𝑛)这种形式递归式的简单方法。
#### 代换法
- [x] 代换法求解步骤：
  > ① 先猜测解的基本形式
  >
  > ② 用数学归纳法证明猜测的正确性
  > > A. 先证明一般情况成立
  > >
  > > B. 再考虑边界条件

##### 示例
> 求解T(n)的表达式

$$
T(n)=
\begin{cases}
  1, & \text{if } n =1 \\
  2T\left(\frac{n}{2}\right)+n, & \text{if } n >1
\end{cases}
$$

> 答案1
> 
> ① 猜测问题的解是 𝑇(𝑛) = 𝑛lgn + 𝑛 。
> 
> ② 归纳证明：
> > A. 当𝑛 = 1时， 𝑇(1)= 𝑛lg𝑛 + 𝑛 = 1 成立；
> > 
> > B. 假设 ∀𝑘 < 𝑛 时，有 𝑇 𝑘 = 𝑘lg𝑘 + 𝑘 。当𝑘 ≥ 𝑛时，有：
> > 
> > $T(n)=2T\left(\frac{n}{2}\right)+n$
> > $=2[\left(\frac{n}{2}\right)+\lg \left(\frac{n}{2}\right)+\frac{n}{2}]+n$ ( ***归纳假设*** )
> > $=n\lg \left(\frac{n}{2}\right)+n+n$
> > $=n(\lg n-\lg 2)+2n$
> > $=𝑛lg𝑛 + 𝑛$

> 答案2
> 
> ① 猜测问题的解是 𝑇(𝑛) = 𝑶(𝑛lgn) 。
>
> ② 证明𝑇(𝑛)≤ 𝑐𝑛lg𝑛 对某正常量𝑐, $𝑛_0$ 成立。
> > A. 假设该不等式关系对𝑘 < 𝑛 成立，则有 $$T\left(\frac{n}{2}\right)\leq \frac{cn}{2}\lg \frac{n}{2}$$
> > B.当𝑘 ≥ 𝑛时，有：
> >
> > $T(n)=2T\left(\frac{n}{2}\right)+n \leq cn\lg \frac{n}{2}+n$
> > $=cn\lg n-cn\lg 2+n$
> > $≤ 𝑐𝑛\lg 𝑛 ， ∀𝑐 \geq 1$
> > ***C. 当𝒏 = 𝟏时，𝑻(𝟏) ≤ 𝟎, 与边界条件矛盾！！！***
> > **D. 取 $n_0=2$ ,c=1时，上述结论成立，证毕**

> ***注：总结：*** `如果归纳假设与边界条件不一致，可以设立新的边界条件使得归纳证明成立。`

##### 如何做一个好的猜测？
$$
T(n)=T\left(\lceil\frac{n}{2}\rceil\right)+T\left(\lfloor\frac{n}{2}\rfloor\right)+1
$$

> 解：首先，猜测解为T(n)=𝑂(𝑛) ；
>
> 然后，证明𝑇(𝑛)≤𝑐𝑛对某正常数𝑐, $𝑛_0$ 成立。
>
> A. 假设该结论对𝑘 < 𝑛成立，则有
>
> $T\left(\lceil\frac{n}{2}\rceil\right)\leq c\lceil\frac{n}{2}\rceil$ , $T\left(\lfloor\frac{n}{2}\rfloor\right)\leq c\lfloor\frac{n}{2}\rfloor$
>
> B. 当𝑘 ≥ 𝑛时，则有
> 
> $T(n) \leq c\lceil\frac{n}{2}\rceil+c\lfloor\frac{n}{2}\rfloor+1 \leq cn+1$
>
> `这对任意𝒄都不意味着 𝑇(𝑛)≤𝑐𝑛 ,怎么处理？`

```math
预证结论：𝑇(𝑛)≤ 𝑐𝑛
推导结果：𝑇(𝑛)≤ 𝑐𝑛 + 1
```

<p align="center">↓<span></span></p>

```math
解决方案：可以通过对更小的值假设更强的条件，对于一个给定值证明更强的结论。
```

<p align="center">↓<span></span></p>

> 解：首先，猜测解为T(n)=𝑂(𝑛) ；
>
> 然后，证明𝑇(𝑛)≤𝑐𝑛-a对某正常数𝑐, $𝑛_0$ 成立。
>
> A. 假设该结论对𝑘 < 𝑛成立，则有
>
> $T\left(\lceil\frac{n}{2}\rceil\right)\leq c\lceil\frac{n}{2}\rceil -a$ , $T\left(\lfloor\frac{n}{2}\rfloor\right)\leq c\lfloor\frac{n}{2}\rfloor -a$
>
> B. 当𝑘 ≥ 𝑛时，则有
> 
> $T(n) \leq c\lceil\frac{n}{2}\rceil -a+c\lfloor\frac{n}{2}\rfloor -a+1 \leq cn+1$
>
> $\leq cn-2a+1$
>
> $\leq  cn-a,((∀𝑎 \geq 1都成立)$
>
> $\leq cn$
>
> $因此，当𝒄 = 𝟏, 𝒏_𝟎 = 𝟏可证明𝑻(𝒏) ≤ 𝒄𝒏成立。$

##### 关于部分陷阱
- [x] 避免陷阱：
  > $T(n)=2T\left(\lfloor\frac{n}{2}\rfloor\right)+1$
  > 
  > 解：首先，猜测解为T(n)=𝑂(𝑛) ；
  >
  > 然后，证明𝑇(𝑛)≤𝑐𝑛对某正常数𝑐, $𝑛_0$ 成立。
  >
  > A. 假设该结论对𝑘 < 𝑛成立，则有
  >
  > $T\left(\lfloor\frac{n}{2}\rfloor\right)\leq c\lfloor\frac{n}{2}\rfloor$
  >
  > B. 当𝑘 ≥ 𝑛时，有
  >
  > $T(n) \leq 2c\lfloor\frac{n}{2}\rfloor+n \leq cn+n=O(n)$
  >
  > 证毕。
  
  >  ***`错误！因为没有证明出与归纳假设严格一致的形式！`***

##### 改变变量
$$T(n)=2T(\lfloor\squr n\rfloor)+\lg n$$
> 解：令m=lgn，则有 $T(2^m)=2T(2^{\frac{m}{2}})+m$
>
> 令 $S(m)T(2^m)$ ,则原递归式可以转为： $S(m)=2S(\frac{m}{2})+m$
>
> 上面递归式与之前例题相似有相同的解: $S(m)=O(mlgm)$
>
> 最后将变量变换回去得到： $T(n)=T(2^m)=O(mlgm)=O(lgnlglgn)$

### 迭代法
- [x] 核心思路： 扩展（迭代）原递归式并将其表示成更小的项以及初始条件的累和的形式。
#### 举例
$T(n)=3T(\lfloor\frac{n}{4}\rfloor)+n=n+3T(\lfloor\frac{n}{4}\rfloor)$
$=n+3(\lfloor\frac{n}{4}\rfloor+3T(\lfloor\frac{n}{4^2}\rfloor))$
$=n+3\lfloor\frac{n}{4}\rfloor+3^2(\lfloor\frac{n}{4^2}\rfloor+3T(\lfloor\frac{n}{4^3}\rfloor))$
$=n+3\lfloor\frac{n}{4}\rfloor+3^2\lfloor\frac{n}{4^2}\rfloor+3^3(\lfloor\frac{n}{4^3}\rfloor+3T(\lfloor\frac{n}{4^4}\rfloor))$
$=...$
$=n+\sum\limits_{i=1}^k (3^i\lfloor\frac{n}{4^i}\rfloor)$
$=？$

> - [ ] 展开终止条件：当子问题规模达到边界条件时, $\lfloor\frac{n}{4^i}\rfloor$ =1时迭代终止。
> - [ ] 考虑到 $\lfloor\frac{n}{4^i}\rfloor \leq \frac{n}{4^i}$ ，可以得到下面递减的等比级数：
> > $T(n)=3T(\lfloor\frac{n}{4}\rfloor)+n=n+\sum\limits_{i=1}^k (3^i\lfloor\frac{n}{4^i}\rfloor)$
> >
> > $\leq n+\sum\limits_{i=1}^k (3^i\*\frac{n}{4^i})=n\sum\limits_{i=1}^k\left(\frac{3}{4}\right)^i$
> >
> > $\leq n\sum\limits_{i=1}^{\infty}\left(\frac{3}{4}\right)^i=4n$
> >
> > $=O(n)$
