## LeetCode分类刷题之二分法(Binary Search)

二分法在面试中是常见的类型，虽然算法思想本身比较简单，但是变化的种类还是比较多的，下面具体看看有那些类别。

### 二分法思想：

#### 1、定义：
		
二分查找又名折半查找(Binary Search)，其时间复杂度是对数级别的 O(log2n)，能进行折半查找必须符合两个条件：1）线性表
必须是顺序存储结构，2）表中元素按照关键字有序排列。

#### 2、主要的思想：

- 假设数据是按升序排序的，对于给定值key，从序列的中间位置k开始比较。
- 若key小于当前位置值arr[k]，则在数列的前半段中查找,arr[low,mid-1]；
- 若key大于当前位置值arr[k]，则在数列的后半段中继续查找arr[mid+1,high]，
- 如果当前位置arr[k]值等于key，则查找成功；


#### 3、常用模板：

```
	left,right = 0,len(nums)-1
	while left <= right:
		mid = (left+right)//2
		if nums[mid] == target:
			//找到目标值
		elif nums[mid] < target:
			//目标值在后半段，缩小范围
		else:
			//目标值在前半段，缩小范围
	return -1
```



### 主要类别：

**一、普通排序数组相关题目：**

此类题型是最常规的二分法，就是在有序数组中查找某个目标值，主要的思路是通过判断中间位置的值和目标是的大小关系，来缩小
目标值可能存在的范围，并最终确定目标值是否在数组中。

如704题，给定一个有序数组查找目标值位于数组中的索引：

```
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left,right = 0,len(nums)-1
        while left <= right:
            mid = (left+right)//2
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                left = mid+1
            else:
                right = mid-1
        return -1
```


**同类型题：**

- [704. 二分查找](https://leetcode-cn.com/problems/binary-search)

- [35. 搜索插入位置](https://leetcode-cn.com/problems/search-insert-position/) 
	
	这道题的思路是找到第一个大于target的数。[【python 详解】](./daily/35_2020-11-12_搜索插入位置.md)

- [剑指 Offer 53 - II. 0～n-1中缺失的数字](https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/) 
	
	这道题主要依据是根据中间值是否等于索引来判断缺失数字所在的范围，根据不断缩小范围找到缺失的数字。[【python 详解】](./daily/剑指Offer53_2020-11-12_0～n-1中缺失的数字.md)

**二、变形排序数组相关题目：**

此类题是基于基础题型变换而来，主要是将有序数组进行旋转得到一个拥有两个有序子序列的数组，在该数组上判断目标是所属的位置范围，然后在不断缩小范围
知道找到目标值。

对于旋转后的数组存在一个特点，即数组中存在两个有序子序列的数组，并且前子序列比后子序列大。因此在数组中间肯定存在一个最小值(当然如果
数组旋转了数组本身长度个单位那个相当于没有旋转)。

之前我们是将mid与target进行比较，但是现在没有了target如何比较？有两种方式，那就是对left比较或者对right比较。根据不同的题
可以采用不同的思路。这两种比较方式最大的区别就是
于是我们可以得到下面的mid与right进行比较的模板：

```
class Solution:
    def func(self, numbers: List[int]) -> int:
        left,right = 0 , len(numbers)-1
        while left <= right:
            mid  = (left+right) // 2
            if numbers[mid] > numbers[right]: 
				# 这种情况表明左边是有序递增的，在[mid:-1]内存在部分递增范围
            elif numbers[mid] < numbers[right]:
                # 这种情况表明右边是有序递增的，在[1：mid]内存在部分递增范围
            else:
                # 这种情况是当数组中存在重复数字的时候，
				# 这时候需要防止numbers[right]==numbers[left]的情况
```

有时候有些情况并不适合与右边比较，此时与左边比较才能符合所有例子。因此还有和左边对比的模板，针对具体问题
具体选择合适的方法。

```
class Solution:
    def func(self, numbers: List[int]) -> int:
        left,right = 0 , len(numbers)-1
        while left <= right:
            mid  = (left+right) // 2
            if numbers[mid] > numbers[left]: 
				# 这种情况表明左边是有序递增的，在[mid:-1]内存在部分递增范围
            elif numbers[mid] < numbers[left]:
                # 这种情况表明右边是有序递增的，在[1：mid]内存在部分递增范围
            else:
                # 这种情况是当数组中存在重复数字的时候，
				# 这时候需要防止numbers[right]==numbers[left]的情况
```


**同类型题：**

- [剑指 Offer 11. 旋转数组的最小数字](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)
	
	这道题的思路是找出最小值，而最小值一般是最左边，为了将最小值保留在最左边，因此适合使用与right比较的方式。然后使用上面的模板即可。[【python 详解】](./daily/剑指offer11旋转数组的最小数字.md)

- [852. 山脉数组的峰顶索引](https://leetcode-cn.com/problems/peak-index-in-a-mountain-array/) 
	
	这道题的思路是根据数组呈现两个子序列来判定最大值的位置，因此关键就是确定最大值所在范围，然后缩小范围即可。 [【python 详解】](./daily/852_2020-11-12_山脉数组的峰顶索引.md)
	
- [面试题 10.03. 搜索旋转数组](https://leetcode-cn.com/problems/search-rotate-array-lcci/)
	
	这道题除了区分范围，并且根据范围是否有序的特点来确定target是否在这个范围，根据这个再去缩小范围。当然还有一种情况就是
	当其中出现重复数字的时候，我们要找到最小的位置，这时候需要判定左边的值是否等于target。   [【python 详解】](./daily/面试题1003_2020-07-20.md)
	
- [33. 搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)
	
	这道题和 **面试题 10.03. 搜索旋转数组** 思路一样。[【python 详解】](./daily/33_2020-04-06搜索旋转排序数组.md)
	
- [81. 搜索旋转排序数组 II](https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/)

	这道题和 **33.搜索旋转排序数组** 思路一样。[【python 详解】](./daily/81_2020-11-12搜索旋转排序数组II.md)
	
	
- [153. 寻找旋转排序数组中的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)
	
	这题需要重点注意的是要和右边比较来确定范围，因为和左边比的时候，如果数组旋转，那么当中间值大于左边值的时候，这时候最小值在右边
	但是如果数组没有旋转，那么那么当中间值大于左边值的时，这时候最小值还是在最左边的那个，因此如果这时候和左边比就会出现错误。[【python 详解】](./daily/153_2020-04-07寻找旋转排序数组中的最小值.md)


- [154. 寻找旋转排序数组中的最小值 II](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/) [hard]
	
	这道题只需要对[153寻找旋转排序数组中的最小值]()进行调整就行，通过模板可以看出，我们只需要对else里面的内容进行
	改动即可，因为else里面 nums[mid] == nums[right] ，所以right - 1 即可，因为如果这是最小值，mid还在范围内。  [【python 详解】](./daily/154_2020-11-12寻找旋转排序数组中的最小值II.md)


**总结：**

这里上面出现两种类型题：

1、搜索旋转排序数组：这里有target，和左侧比较可以符合target的查找范围
2、寻找旋转排序数组中的最小值：这里应该和右侧比较，因为这样不会出现最小值在左边，被跳过的情况。

难度提升主要是数组中是否有重复值，总的来说其实还是按照模板进行扩展的。


**三、排序矩阵相关题目：**

- [74  搜索二维矩阵  ](https://leetcode-cn.com/problems/search-a-2d-matrix)

	形式上以二维矩阵存储，搜索上以一维数组进行二分查找[【python 详解】](./daily/74_2020-11-13_搜索二维矩阵.md)

- [240.搜索二维矩阵 II](https://leetcode-cn.com/problems/search-a-2d-matrix-ii/)
	
	与74题不同的是，下一行的第一个数不一定大于山一行最后一个数，因此需要行和列分别进行二分查找。[【python 详解】](./daily/240_2020-11-13_搜索二维矩阵II.md)
	
- [面试题 10.09.排序矩阵查找](https://leetcode-cn.com/problems/sorted-matrix-search-lcci/)
	
	与**240.搜索二维矩阵 II**是同一道题，[【python 详解】](./daily/240_2020-11-13_搜索二维矩阵II.md)

- [1351. 统计有序矩阵中的负数](https://leetcode-cn.com/problems/count-negative-numbers-in-a-sorted-matrix/)



- [378. 有序矩阵中第K小的元素](https://leetcode-cn.com/problems/kth-smallest-element-in-a-sorted-matrix/)



- [1292. 元素和小于等于阈值的正方形的最大边长](https://leetcode-cn.com/problems/maximum-side-length-of-a-square-with-sum-less-than-or-equal-to-threshold/)



- [436. 寻找右区间](https://leetcode-cn.com/problems/find-right-interval/)


**四、实例应用相关题目：**

- [69. x 的平方根](https://leetcode-cn.com/problems/sqrtx/)
- [658. 找到 K 个最接近的元素](https://leetcode-cn.com/problems/find-k-closest-elements/)
- [441. 排列硬币](https://leetcode-cn.com/problems/arranging-coins/)
- [744. 寻找比目标字母大的最小字母](https://leetcode-cn.com/problems/find-smallest-letter-greater-than-target/)
- [34. 在排序数组中查找元素的第一个和最后一个位置](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)
- [287. 寻找重复数](https://leetcode-cn.com/problems/find-the-duplicate-number/)
- [1574. 删除最短的子数组使剩余数组有序](https://leetcode-cn.com/problems/shortest-subarray-to-be-removed-to-make-array-sorted/)

**五、系列题：**

1、两个数的交集：

- [349. 两个数组的交集](https://leetcode-cn.com/problems/intersection-of-two-arrays/)
- [350. 两个数组的交集 II](https://leetcode-cn.com/problems/intersection-of-two-arrays-ii/)

2、H指数

- [275. H 指数 II](https://leetcode-cn.com/problems/h-index-ii/)
- [274. H 指数](https://leetcode-cn.com/problems/h-index/)


3、两数之和

- [1. 两数之和](https://leetcode-cn.com/problems/two-sum/solution/liang-shu-zhi-he-by-leetcode-solution/) [非二分法问题]
- [167. 两数之和 II - 输入有序数组](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/)

4、丑数
- [剑指 Offer 49	丑数](https://leetcode-cn.com/problems/chou-shu-lcof)

	同[264_丑数 II](./daily/264_2020-11-13_丑数II.md) 

- [263	丑数](https://leetcode-cn.com/problems/ugly-number) [【python 详解】](./daily/263_2020-11-13_丑数.md)
	
- [264	丑数 II](https://leetcode-cn.com/problems/ugly-number-ii) 
		
	通过利用动态规划的思想，记录2,3,5累乘的结果，将所有丑数排序[【python 详解】](./daily/264_2020-11-13_丑数II.md)
	
- [1201	丑数 III](https://leetcode-cn.com/problems/ugly-number-iii)