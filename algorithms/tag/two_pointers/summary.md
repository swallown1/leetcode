# 双指针
---

### 算法思想

1. **双指针：**指的是两个指针指向不同元素，相互协助完成任务。同时也可以延伸至多数组的多指针

2. **滑动窗口：**指的是两个指针同方向移动且不相交，两个指针之间的区域称为滑动窗口。

3. **如果两指针遍历方向相反，则可以用来进行收索，一般都是排序好的序列**

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




###  合并两个有序数组
88. [Merge Sorted Array (Easy)](https://leetcode.com/problems/merge-sorted-array/)
> 题目描述
> 给定两个有序数组，把两个数组合并为一个。
> 输入输出样例
> 输入是两个数组和它们分别的长度 m 和 n。其中第一个数组的长度被延长至 m + n，多出的
> n 位被 0 填补。题目要求把第二个数组归并到第一个数组上，不需要开辟额外空间。

```
Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: nums1 = [1,2,2,3,5,6]
```
这道题的思路采用的是用倒叙的方式，

使用指针i指向m-1，j指向n-1，k指向n+m-1,这样每次只需要比较nums1[i]和nums[j]的大小，大的放在nums[k]即可。

###  快慢指针
142. [Linked List Cycle II (Medium)](https://leetcode.com/problems/linked-list-cycle-ii/)


快慢指针的思想其实是为了寻找数组或者链表中是否存在着环，其关键的代码如下(以链表为例)：
```
quick,slow = head,head
while True:
	if not quick or not quick.next:return  #表示不存在环
	slow = slow.next
	quick = quick.next.next
	if quick == slow:
		break
		#表示链表有环并且这是环的入口节点
```
给定两个指针，
分别命名为 slow 和 fast，起始位置在链表的开头。每次 fast 前进两步，slow 前进一步。如果 fast
可以走到尽头，那么说明没有环路；如果 fast 可以无限走下去，那么说明一定有环路，且一定存
在一个时刻 slow 和 fast 相遇。当 slow 和 fast 第一次相遇时，我们将 fast 重新移动到链表开头，并
让 slow 和 fast 每次都前进一步。当 slow 和 fast 第二次相遇时，相遇的节点即为环路的开始点。

因此此题的解为：
```
class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
		quick,slow = head,head
		while True:
			if not quick or not quick.next:return  #表示不存在环
			slow = slow.next
			quick = quick.next.next
			if quick == slow:
				break  #表示链表有环并且这是环的入口节点
		fast = head
		while fast != slow:  # 第二次遍历寻找环的头节点
			fast, slow = fast.next, slow.next
		return fast

```

###  滑动窗口
滑动窗口指的是采用两个指针，start，end 开始不断的移动end，直到窗口内(start,end)满足题目的要求，其次在移动start，是的窗口不断减小，得到最终符合题意的结果。然后不断重复上述过程，直至start到达最末尾位置


3  [无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

采用start和end双指针，start为窗口的开始位置，然后移动end指针，只要s[end]不存在mask中，加入mask，移动end往后移动
直到end不能移动，此时mask的长度为 end-start，存在res中。

然后将start往后移动一位，并且将mask中的 start-1 位置字符移除。

```
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        res = 0
        mask = []
        end = 0
        for start in range(len(s)):
            if start !=0:
                mask.remove(s[start-1])
            
            while end < len(s) and s[end] not in mask:
                mask.append(s[end])
                end +=1
            res = max(res,end-start)
        return res
```

######  例子
------
209.  [长度最小的子数组](https://leetcode-cn.com/problems/minimum-size-subarray-sum/)：
	本题的思想就是采用两个指针分别从两头进行遍历，j表示子数组开始索引，i表示子数组尾索引。每次i往后移动，当total的值大于
	等于s时，记录子数组长度 ans  然后将j指针往后移动一个。
