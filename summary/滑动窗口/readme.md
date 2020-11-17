## LeetCode分类刷题之滑动窗口(Sliding window)

滑动窗口经常是用来执行数组或是链表上某个区间（窗口）上的操作。
比如找最长的全为1的子数组长度。滑动窗口一般从第一个元素开始，一直往右边一个一个元素挪动。

### 滑动窗口思想：

- 滑动窗口其实是双指针构成的，一个左指针left，一个右指针right，
	然后[left,right]表示的索引范围是一个窗口了。
	
- 右指针right是用来扩大窗口:当窗口内的条件没有达到要求时，我们需要不断扩大窗口的大小(right右移)
	直到满足条件为止。
	
- 左指针left是用来缩小窗口:当窗口内的条件已满足题目条件或多于题目条件时（窗口溢出），
	我们缩小窗口，也就是左指针left需要右移直到窗口条件不满足为止。这时候我们需要记录当前
	窗口的大小，并更新以当前窗口满足条件的结果。然后再次向右移动指针，再次使之满足条件。
 
**注：滑动窗口用来处理连续满足一定条件的连续区间的性质（长度等）问题的，两个指针都起始于原点，并一前一后向终点前进。**

### 常用伪代码：

滑动窗口主要分为两种，一种是窗口的大小是固定的，另一种是窗口的大小是变化的，

- 如果窗口的大小是固定的，我们只需要在一个指针即可，并且在固定大小的窗口里判定是否满足条件。

- 如果窗口的大小是动态变化的，就需要两个指针来控制窗口的大小，同时，我们需要根据窗口是否满足条件
	进行动态的变化窗口大小。

除此之外，还有不同的写法就是我们可以将left或right指针其中一个作为主要的控制变量。因为双指针法一般都只会对
数组进行一次遍历，因此我们只需要考虑left或right其中遍历完整个链表即可，因此这里有两个不同的模板，
针对不同的问题具体使用哪个可以自行判断。

以left为主的伪代码：

```
def function(self, s: int, nums: List[int]) -> List[int]:
	n = len(nums)
	right,totle = -1,0
	for left in range(n): # 以left为主遍历整个nums
		if left !=0:
			# 对left指针进行处理
		while totle < s and right+1 < n:  #判断滑动窗口是否满足条件
			# 将滑动窗口进行右移
		if totle >= s: ans = min(ans,right-left+1)  #更新结果
	return ans
```

以right为主的伪代码：

```
def function(self, s: int, nums: List[int]) -> List[int]:
	ans = []
	ns1= len(p)
	right = ns1-1
	while right < len(s): #控制right遍历整个nums
	    # 考虑移动后新的元素对当前状态的影响
	    if # 判断新的窗口是否满足条件：
			满足条件则更新当前的结果，
			然后去除left带来的状态影响，并将left进行右移
	    else:
	        不满足条件则将right进行右移
	    right +=1
	return ans
```


### 经典题目：

- [3. 无重复字符的最长子串【难度：中等】](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

	借用Set来做窗口，遍历整个字符串中若没有遇到重复字符，right继续扩展，同时更新ans；
	若遇到重复字符，我们需要缩小窗口，也就是left右移。[【python 详解】](./daily/3_2020-11-14_无重复字符的最长子串.md)

- [209. 长度最小的子数组【难度：中等】](https://leetcode-cn.com/problems/minimum-size-subarray-sum/)

	借用left，right来记录窗口的位置，遍历整个数组，若窗口内的值小于s，right继续扩展，直到大于s时候，更新ans；
	然后left右移来缩小窗口。[【python 详解】](./daily/209_2020-11-14_长度最小的子数组.md)

- [424. 替换后的最长重复字符](https://leetcode-cn.com/problems/longest-repeating-character-replacement/)

	使用动态窗口来寻找最长字符，通过使用字典记录窗口内字符的个数，进而判断缩小还是扩散窗口。
	进而找到最长重复字符的长度。[【python 详解】](./daily/424_2020-11-14_替换后的最长重复字符.md)

 [438. 找到字符串中所有字母异位词【难度：中等】](https://leetcode-cn.com/problems/find-all-anagrams-in-a-string/)

	本题求的是模式串p在总串s中的所有字母异位词，所以我们所建立的窗口windows大小维持在与模式串p生成
	的字符表pCount的大小相等即可。[【python 详解】](./daily/438_2020-11-14_找到字符串中所有字母异位词.md)

- [567. 字符串的排列【难度：中等】](https://leetcode-cn.com/problems/permutation-in-string/)

	本题属于**438.找到字符串中的所有字母异位词的子题**，前者是找到所有异位词并添加异位词出现的下标，
	而本题比前者简单多了，若在总串找到模式串的异位词，直接返回ture就行了；
	若遍历完整个总串也没找到模式串的异位词，返回false就行。[【python 详解】](./daily/567_2020-11-14_字符串的排列.md)

- [1052.爱生气的书店老板【难度：中等】](https://leetcode-cn.com/problems/grumpy-bookstore-owner/)

	先计算不生气的人数，然后将问题转化成在全部生气的时候找出在所有窗口中最多的生气人数，最后将
	两部分人数相加就得到最多感到满意的客户数量。[【python 详解】](./daily/1052_2020-11-16_爱生气的书店老板.md)

- [978.最长湍流子数组【难度：中等】](https://leetcode-cn.com/problems/longest-turbulent-subarray/)
	
	当窗口到达数组末尾或者湍流不成立，我们需要重新开始扩展空间。[【python 详解】](./daily/978_2020-11-16_最长湍流子数组.md)

- [1208.尽可能使字符串相等【难度：中等】](https://leetcode-cn.com/problems/get-equal-substrings-within-budget/)
		
	常规的滑动窗口思路，这里通过判定窗口内，像个数组对应为ascii差值的绝对值总和与maxCost的大小关系
	作为窗口是否符合的条件[【python 详解】](./daily/1208_2020-11-17_尽可能使字符串相等.md)

- [1423.可获得的最大点数【难度：中等】](https://leetcode-cn.com/problems/maximum-points-you-can-obtain-from-cards/)
		
	常规的滑动窗口思路，这里需要根据题意理解出，滑动窗口的范围不再是遍历
	整个数组，而是在[-k,k]的范围内进行窗口的滑动【python 详解】](./daily/1423_2020-11-17_可获得的最大点数.md)

- [面试题 17.18 最短超串【难度：中等】](https://leetcode-cn.com/problems/shortest-supersequence-lcci/)
- [1004 最大连续1的个数 III【难度：中等】](https://leetcode-cn.com/problems/max-consecutive-ones-iii/)	
- [1040 移动石子直到连续 II【难度：中等】](https://leetcode-cn.com/problems/moving-stones-until-consecutive-ii/)
- [1438 绝对差不超过限制的最长连续子数组](https://leetcode-cn.com/problems/longest-continuous-subarray-with-absolute-diff-less-than-or-equal-to-limit/)

- [76. 最小覆盖子串 【难度：困难】](https://leetcode-cn.com/problems/minimum-window-substring/)

	这道题最重要的是使用的存储方式，通过dict的存储，对出现过的-1，对未出现的+1，
	进而判断窗口中是否包含t。【python 详解】](./daily/76_2020-11-17_最小覆盖子串.md)

- [159. 至多包含两个不同字符的最长子串【难度：中等】【会员】](https://leetcode-cn.com/problems/longest-substring-with-at-most-two-distinct-characters/)
- [30. 串联所有单词的子串 【难度：困难】](https://leetcode-cn.com/problems/substring-with-concatenation-of-all-words/)
- [239. 滑动窗口最大值【难度：困难】](https://leetcode-cn.com/problems/sliding-window-maximum/)
- [480. 滑动窗口中位数【难度：困难】](https://leetcode-cn.com/problems/sliding-window-median/)
- [992.K个不同整数的子数组【难度：困难】](https://leetcode-cn.com/problems/subarrays-with-k-different-integers/)
- [995.K连续位的最小翻转次数【难度：困难】](https://leetcode-cn.com/problems/minimum-number-of-k-consecutive-bit-flips/)

- [727. 最小窗口子序列【会员】](https://leetcode-cn.com/problems/minimum-window-subsequence/)
- [1074.元素和为目标值的子矩阵数量【难度：困难】](https://leetcode-cn.com/problems/number-of-submatrices-that-sum-to-target/)
- Maximum Sum Subarray of Size K
- Smallest Subarray with a given sum (easy)
- Longest Substring with K Distinct Characters (medium)
- Fruits into Baskets (medium)No-repeat Substring (hard)
- Longest Substring with Same Letters after Replacement (hard)
- Longest Subarray with Ones after Replacement (hard)
