
参考博客：https://blog.csdn.net/u013457167/article/details/81989207

一、算法概述

1.1 算法分类

比较类排序：通过比较来决定元素间的相对次序。

    时间复杂度O(nlogn) ~ O(n^2)，主要有：冒泡排序，选择排序，插入排序，归并排序，堆排序，快速排序等。
 
非比较排序：不通过比较来决定元素间的相对次序 

    时间复杂度可以达到O(n)，主要有：计数排序，基数排序，桶排序等。 

分类图如下：
![Image text](https://github.com/RFML/sortofeight/blob/master/images/排序算法分类.png)

1.2 算法复杂度及稳定性
![Image text](https://github.com/RFML/sortofeight/blob/master/images/各类排序算法复杂度.png)

二、详细讲解

2.1 冒泡排序

算法原理:(升序)

	(1)比较相邻的元素。如果第一个比第二个大，就交换他们两个。
	(2)对每一对相邻元素做同样的工作，从开始第一对到结尾的最后一对。在这一步，最后的元素应该会是最大的数。
	(3)针对所有的元素重复以上的步骤，除了最后一个。
	(4)持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。
	
时间复杂度和算法稳定性：

	一共遍历了n-1 + n-2 + … + 2 + 1 = n * (n-1) / 2 = 0.5 * n ^ 2 - 0.5 * n，那么时间复杂度是O(N^2)。
	因为nums[j]==nums[j+1]的时候，我们可以不移动nums[i]和nums[j]，所以冒泡排序是稳定的。

冒泡排序优化：

	初始didswap=false. 当发生一次交换就将didswap置为true，这样如果原始有序，那么一次扫描完一次交换也不会有，
	即didswap=false，此时return，终止排序。此时时间复杂度是O(n),所以最优时间复杂度为O(n)。
	
2.2 选择排序

算法原理:(升序)

	(1)在待排序的一组数中选出最小(或最大)的一个元素，与待排序序列的起始位置(或末尾位置）交换。
	(2)然后在剩下的数中再找最小（或者最大）的与第2个位置的数交换。
	(3)以此类推，知道第n-1个元素（倒数第二个数）和第n个元素（最后一个数）比较为止。
	
时间复杂度和算法稳定性：

	时间复杂度：
	简单选择排序的比较次数与序列的初始排序无关。假设待排序的系列有N个元素，则比较次数总是N（N-1）/2
	而移动次数与系列的初始排序有关，当排序正序时，移动次数最少，为0
	当序列反序时，移动次数最多，为3N（N-1）/2；所以，综上，简单排序的时间复杂度为O（N*N）

	选择排序是不稳定的：
	选择排序是给每个位置选择当前元素最小的，给第一个位置选择最小的，在剩余元素里给第二个元素选择第二小的，
	依次类推，直到第n - 1个元素，第n个元素不用选择了，因为只剩下它一个最大的元素了。
	那么，在一趟选择，如果当前元素比一个元素小，而该小的元素又出现在一个和当前元素相等 的元素后面，
	那么交换后稳定性就被破坏了。比较拗口，举个例子，序列5 8 5 2 9，我们知道第一遍选择第1个元素5会和2交换，
	那么原序列中2个5的相对前后顺序就被破坏了，所以选择排序不是一个稳定的排序算法。

选择排序优化：

	选择排序是一次确定一个元素的位置，而选择排序的优化则是一次确定两个元素的位置，
	比如降序：每次将最小值放在起始位置，最大值放在末尾位置。

2.3 插入排序

2.3.1 直接插入排序：

算法原理:(升序)

	(1)把n个待排序的元素看成为一个有序表和一个无序表。
	(2)开始时有序表中只包含1个元素，无序表中包含有n-1个元素。
	(3)排序过程中每次从无序表中取出第一个元素，将它插入到有序表中的适当位置，使之成为新的有序表。
	(4)重复n-1次可完成排序过程。
	
时间复杂度和算法稳定性：
	
	直接插入排序时间复杂度：
	直接插入排序的时间复杂度是O(N^2)。假设待排序的数列中有N个数。
	遍历一趟的时间复杂度是O(N)，需要遍历N-1；因此，直接插入排序的时间复杂度是O(N^2)。
	如果是排好序的；则时间复杂度是O(n)

	直接插入排序稳定性：
	直接插入排序是稳定的算法，它满足稳定算法的定义。
	假设在数列中存在a[i]=a[j]，若在排序之前，a[i]在a[j]前面；
	并且排序之后，a[i]仍然在a[j]前面。则这个排序算法是稳定的！

2.3.2 折半插入排序：

算法原理:(升序)
	
	折半插入排序（binary insertion sort）是对插入排序算法的一种改进，由于排序算法过程中，
	就是不断的依次将元素插入前面已排好序的序列中。由于前半部分为已排好序的数列，
	这样我们不用按顺序依次寻找插入点，可以采用折半查找的方法来加快寻找插入点的速度。
	
时间复杂度和算法稳定性：
	
	折半插入排序是一种稳定的排序算法，比直接插入排序明显减少了关键字之间比较的次数，
	因此速度比直接插入排序算法快，但记录移动的次数没有变，所以折半插入排序算法的时间复杂度仍然为O(n^2)，
	与直接插入排序算法相同。
	
2.3.3 希尔排序：	
	
	首先它把较大的数据集合分割成若干个小组（逻辑上分组），然后对每一个小组分别进行插入排序，
	此时，插入排序所作用的数据量比较小（每一个小组），插入的效率比较高。
	
算法原理:(升序)
	
	(1)首先它把较大的数据集合分割成若干个小组（逻辑上分组）。
	(2)把每个小组待排序的元素看成为一个有序表和一个无序表。
	(3)开始时有序表中只包含1个元素，无序表中包含有n-1个元素。
	(4)排序过程中每次从无序表中取出第一个元素，将它插入到有序表中的适当位置，使之成为新的有序表。
	(5)重复n-1次可完成排序过程。
	
时间复杂度和算法稳定性：
	
	希尔排序的复杂度和增量序列是相关的
	{1,2,4,8,...}这种序列并不是很好的增量序列，使用这个增量序列的时间复杂度（最坏情形）是O(n^2)
	Hibbard提出了另一个增量序列{1,3,7，...,2^k-1}，这种序列的时间复杂度(最坏情形)为O(n^1.5)
	Sedgewick提出了几种增量序列，其最坏情形运行时间为O（n^1.3）,其中最好的一个序列是{1,5,19,41,109,...}
	
	虽然插入排序是稳定的；但希尔排序不是稳定的。因为希尔排序在插入的时候是跳跃性插入的；可能破坏稳定性。
	
2.4 归并排序

算法原理:(升序)	

	归并排序（MERGE-SORT）是利用归并的思想实现的排序方法，该算法采用经典的分治（divide-and-conquer）
	策略（分治法将问题分(divide)成一些小的问题然后递归求解，而治(conquer)的阶段则将分的阶段得到的
	各答案"修补"在一起，即分而治之)。
	
分而治之：

![Image text](https://github.com/RFML/sortofeight/blob/master/images/分治图片.png)
	
算法步骤

	(1).开辟一块空间，用于存放合并后的序列
	(2).设定两个指针，起始位置分别位于两个已排序序列的起始位置
	(3).比较两个指针所代表的元素，将更小的元素放入合并空间，并将指针后移
	(4).重复步骤3，直至有一个指针到达尾部
	(5).将另一个序列的剩余元素复制到合并序列尾部
	
时间复杂度和算法稳定性：

	每次合并操作的时间复杂度是O(N)，而二叉树的深度是log2N，所以总的时间复杂度是O(N*lgN)。
	因为在合并的时候，如果两个数相等，可以将前面的数先放到辅助数组中，所以归并排序是稳定的。











	
	