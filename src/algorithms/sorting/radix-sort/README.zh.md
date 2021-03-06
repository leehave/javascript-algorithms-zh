
# 基数排序

基数排序（radix sort）属于“分配式排序”（distribution sort），又称“桶子法”（bucket sort）或 bin sort，顾名思义，它是透过键值的部份资讯，将要排序的元素分配至某些“桶”中，藉以达到排序的作用，基数排序法是属于稳定性的排序，其时间复杂度为`O(nlog(r)m)`，其中`r`为所采取的基数，而`m`为堆数，在某些时候，基数排序法的效率高于其它的稳定性排序法。

## 基本解法

- 第一步

以`LSD`为例，假设原来有一串数值如下所示：
`73, 22, 93, 43, 55, 14, 28, 65, 39, 81`
首先根据个位数的数值，在走访数值时将它们分配至编号0到9的桶子中：


桶子编号 | 数值
---------|----------
0 |
1 | 81
2 | 22
3 | 73 93 43
4 | 14
5 | 55 65
6 |
7 |
8 | 28
9 | 39

- 第二步

接下来将这些桶子中的数值重新串接起来，成为以下的数列：
`81, 22, 73, 93, 43, 14, 55, 65, 28, 39`
接着再进行一次分配，这次是根据十位数来分配：

桶子编号 | 数值
---------|----------
0| 
1 | 14
2 | 22 28
3 | 39
4 | 43
5 | 55
6 | 65
7 | 73
8 | 81
9 | 93

- 第三步

接下来将这些桶子中的数值重新串接起来，成为以下的数列：
`14, 22, 28, 39, 43, 55, 65, 73, 81, 93`

这时候整个数列已经排序完毕；如果排序的对象有三位数以上，则持续进行以上的动作直至最高位数为止。

`LSD`的基数排序适用于位数小的数列，如果位数多的话，使用MSD的效率会比较好。MSD的方式与LSD相反，是由高位数为基底开始进行分配，但在分配之后并不马上合并回一个数组中，而是在每个“桶子”中建立“子桶”，将每个桶子中的数值按照下一数位的值分配到“子桶”中。在进行完最低位数的分配后再合并回单一的数组中。

## 效率分析

时间效率 ：设待排序列为`n`个记录，`d`个关键码，关键码的取值范围为`radix`，则进行链式基数排序的时间复杂度为`O(d(n+radix))`，其中，一趟分配时间复杂度为`O(n)`，一趟收集时间复杂度为`O(radix)`，共进行`d`趟分配和收集。 空间效率：需要`2*radix`个指向队列的辅助空间，以及用于静态链表的`n`个指针。

<!-- ![Radix Sort](https://www.researchgate.net/publication/291086231/figure/fig1/AS:614214452404240@1523451545568/Simplistic-illustration-of-the-steps-performed-in-a-radix-sort-In-this-example-the.png) -->

## 复杂性

| 名称       |   最好   |   平均   |   最差   |   内存  |  稳定 | 注释           |
| -------- | :----: | :----: | :----: | :---: | :-: | :----------- |
| **基数排序** | n \* k | n \* k | n \* k | n + k |  是  | k  - 最长密钥的长度 |

## 参考

-   [Wikipedia](https://en.wikipedia.org/wiki/Radix_sort)
-   [YouTube](https://www.youtube.com/watch?v=XiuSW_mEn7g&index=62&t=0s&list=PLLXdhg_r2hKA7DPDsunoDZ-Z769jWn4R8)
-   [ResearchGate](https://www.researchgate.net/figure/Simplistic-illustration-of-the-steps-performed-in-a-radix-sort-In-this-example-the_fig1_291086231)
- [百度百科](https://baike.baidu.com/item/%E5%9F%BA%E6%95%B0%E6%8E%92%E5%BA%8F)
