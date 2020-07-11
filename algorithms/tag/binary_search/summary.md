# 二分法
---

二分法其实是双指针的一种特殊情况，但是区别一般双指针指的是一步一步的移动，二分法每次移动
的是半个区间的长度。

对于二分法主要存在3中题型：

1. **双指针：**指的是两个指针指向不同元素，相互协助完成任务。同时也可以延伸至多数组的多指针

2. **查找区间：** 指的是在一个递增区间中查找一个目标元素，同时应该注意左开右闭和左闭右闭的情况。

3. **旋转数组查找数字：** 指的是该区间是一个递增区间经过一次旋转再查找一个目标元素，此时分析的情况就会多一些需要注意。

### two sum
167. Two Sum II - Input array is sorted (Easy)
> 题目描述
> 在一个增序的整数数组里找到两个数，使它们的和为给定值。已知有且只有一对解。
> 输入输出样例
> 输入是一个数组（numbers）和一个给定值（target）。输出是两个数的位置，从 1 开始计数。
```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
```

这道题采用的就是思想3，在给定一个排序好的列表，通常采用两指针反方向遍历的方式进行解题，**对于排好序且有解的数组，双指针一定能遍历到最优解。**

######  例子
------
1.  [633 平方数之和](https://leetcode-cn.com/problems/sum-of-square-numbers)：
	本题的思想就是采用两个指针分别从两头进行遍历，直到两指针指向同一位置，关键点在于右边的指针从 c**0.5 开始即可。

2. [680 验证回文字符串 Ⅱ](https://leetcode-cn.com/problems/valid-palindrome-ii/):
	本题的思路依旧是两指针的思路，不过这道题的关键在于去除一个字符后验证是否回文，具体思路参考[python](./daily/680_2020-07-02.md)




###  查找区间
34. [在排序数组中查找元素的第一个和最后一个位置](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)
> 题目描述
> 给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。
> 你的算法时间复杂度必须是 O(log n) 级别。
> 如果数组中不存在目标值，返回 [-1, -1]。
 

```
输入: nums = [5,7,7,8,8,10], target = 8
输出: [3,4]

输入: nums = [5,7,7,8,8,10], target = 6
输出: [-1,-1]
```
因为时间复杂度的要求是　o(log n) 因此只能用二分法，所以这里关键就是用两次二分查找找到target位置

第一次：
	用的就是二分法的常用思路。由于nums是递增序列，因此当nums[mid] >= target时 此时 right = mid 因为mid有可能就是target

此处应 排除nums为空情况， 防止target不在nums中情况，因此判断nums[left] != target即可

第二次：
	此次查找target最大下标，此时这里只会存在nums[mid] ＝= target　或　nums[mid] ＞ target的　情况，所以＜＝　换成　＝＝也是对的。
	因此当nums[mid] ＝= target，令left=mid，直至找到最大下标。
	
关键一点：
	因为第一次找最左边的下标，因此此时 mid = (left+right) // 2 ，举个例子，(0+5)//2 为 2 这样就保证了不会因取余漏掉下标为2 的值
	反之 第二次的时候应该 mid = (left+right+1) // 2 
```
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
		#找出最小下标
        left,right=0,len(nums)-1
        while left < right:
            mid = (left+right) // 2
            if nums[mid] >= target:
                right = mid
            else:
                left = mid +1
				
		## 排除nums为空情况， 防止target不在nums中情况
        if not nums or nums[left] != target:
            return [-1,-1]
			
		
        ans = left
		
		#此时left直接从最小表开始寻找
        right = len(nums)-1
        while left < right:
            mid = (left+right+1) // 2
			#此时这里只会存在nums[mid] ＝= target　或　nums[mid] ＞ target的　情况，所以＜＝　换成　＝＝也是对的
            if nums[mid] <= target:
                left = mid
            else:
                right = mid-1
        return [ans,left]
```

######  例子
------
 
###  旋转数组查找数字
81. [搜索旋转排序数组II](https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/)
> 题目描述
> 假设按照升序排序的数组在预先未知的某个点上进行了旋转。( 例如，数组 [0,0,1,2,2,5,6] 可能变为 [2,5,6,0,0,1,2] )。
> 编写一个函数来判断给定的目标值是否存在于数组中。若存在返回 true，否则返回 false。
 
```
输入: nums = [2,5,6,0,0,1,2], target = 0
输出: true

输入: nums = [2,5,6,0,0,1,2], target = 3
输出: false
```

对于二分法常常是借用数组的递增序列的特点，旋转数组之后其实任然是可以运用这一特点。

**对于当前的中间节点指向的值小于等于最右边的值，说明右边区间是一个有序递增序列。
反之说明左边区间是一个有序递增序列。** 如果目标值在有序区间内，可以对这个区间继续二分查找；反之，我们对于另一半区
间继续二分查找。

此题还要注意区间中有重复数字，如果是按照上面讲mid值和最右边的值比较，那么 出现mid的值等于 right的值时，将right-=1
(如果mid值和最左边的值比较，则将left+=1)

```
class Solution:
    def search(self, nums: List[int], target: int) -> bool:
        left,right = 0,len(nums)-1
        while left <= right:
            mid = (left +right) // 2
            if nums[mid] == target:return True
            if nums[mid] < nums[right]:
                if nums[mid] < target<=nums[right]:
                    left = mid+1
                else:
                    right = mid-1
            elif nums[mid] > nums[right]:
                if nums[left] <= target<nums[mid]:
                    right=mid - 1
                else:
                    left = mid+1
            else:right -=1
        return False
```


######  例子
------
1.  [154 寻找旋转排序数组中的最小值 II](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/)
	本题的就是旋转数组查找最小值，相比于81题还是简单的，关键是，最小值的下标是r。因为nums[mid] < nums[r]时 r=mid，所以
	r始终保持当前最小值下标。 具体思路参考[python](./daily/154_2020-07-10.md)
	
 