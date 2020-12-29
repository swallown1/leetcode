## LeetCode分类刷题之动态规划(DP)

动态规划

### 滑动窗口思想：

 
 
**注： 

### 常用伪代码：

 


### 经典题目：

- [300. 最长递增子序列【难度：中等】](https://leetcode-cn.com/problems/longest-increasing-subsequence/)
     这道题的思路是利用dp来存储以第i个位置结尾的最长递增子序列，其中对两种状态进行遍历，即第一层循环遍历整个
     数组 i，第二个遍历是考虑以i之后的j可以构成的递增子序列。状态转移条件nums[i] >  nums[j] ，此时状态转移方程为
     dp[i] = max(dp[i],dp[j]+1)。[【python 详解】](./daily/300_2020-12-23_最长递增子序列.md)


- [978. 最长湍流子数组【难度：中等】](https://leetcode-cn.com/problems/longest-turbulent-subarray/)
     这道题的思路通过将大小关系转化成1，-1关系，题意是找到湍急数组，等价于中间的数小于或大于
	 两边的数。转化成1，-1就是中间数和两边数的关系相乘等于1。然后接下来就是找最长的子数组长度，则子问题为到前一位为止
	 最大的湍急数组长度为多少，状态转移为 ans = max()[【python 详解】](./daily/978_2020-12-24_最长湍流子数组.md)


- [787. K站中转内最便宜的航班【难度：中等】](https://leetcode-cn.com/problems/cheapest-flights-within-k-stops/)
     这道题的思路通过采用二维数组表示经过第k次到地点v所需的最少钱数。并且状态转移比较三个状态
	 dp[k][v] = min(dp[k-1][v],dp[k-1][s]+Wsv,dp[k][v])[【python 详解】](./daily/787_2020-12-24_K站中转内最便宜的航班.md)


- [1641. 统计字典序元音字符串的数目【难度：中等】](https://leetcode-cn.com/problems/count-sorted-vowel-strings/)
     这道题的难点在于不容易找到状态转移方程。对于n=3时，如何通过n=2的结果进行递推。
	 考虑一下对于n=3时，以u结尾的个数有多少呢？其实是等于n=2时，以小于u结尾的个数总和，
	 因为可以在这些子串的末尾加上u，是成立的。因此理解了这个递推关系就不难了。[【python 详解】](./daily/1641_2020-12-24_统计字典序元音字符串的数目.md)


- [1292. 元素和小于等于阈值的正方形的最大边长【难度：中等】](https://leetcode-cn.com/problems/maximum-side-length-of-a-square-with-sum-less-than-or-equal-to-threshold/)
     这道题的主要的思路是采用二维数组前缀和的方式，计算从[0,0]开始到点[i,j]
	 范围的和dp[i,j]，在通过dp求出任意点开始到[i,j]点范围的和。其中要注意的是
	 边界条件，i-k<0 或j-k<0的情况.这道题k是未知，且要求是正方形范围的面积，所以注意
	 遍历k的变化范围。[【python 详解】](./daily/1292_2020-12-24_元素和小于等于阈值的正方形的最大边长.md)


- [1314. 矩阵区域和【难度：中等】](https://leetcode-cn.com/problems/matrix-block-sum/)
     这道题的主要的思路是采用二维数组前缀和的方式，计算从[0,0]开始到点[i,j]
	 范围的和dp[i,j]，在通过dp求出任意点开始到[i,j]点范围的和。其中要注意的是
	 边界条件，主要就是两个点([i-k,j-k]、[i+k+1,j+k+1])的范围问题。[【python 详解】](./daily/1314_2020-12-24_矩阵区域和.md)


- [357. 计算各个位数不同的数字个数【难度：中等】](https://leetcode-cn.com/problems/count-numbers-with-unique-digits/)
     这道题的难点在每位数字不能重复，其实就是没加一位，该位置的候选数字减1。例如三位数不重复的个数是  9*9*8 ，对于4为数那么不重复的4位数有  9*9*8*7.
     所以这里其实不完全算是动态规划，只是用到了前一次的结果。最终的结果只需要将所有不同
     位数中不重复的数加和即可。[【python 详解】](./daily/357_2020-12-24_计算各个位数不同的数字个数.md)


- [343. 整数拆分【难度：中等】](https://leetcode-cn.com/problems/integer-break/)
     本题的关键思路在于  对dp[i] 来说最大的乘积和等于 dp[j]*dp[i-j]。
     这样保证每一个i都是最大的乘积和，这样最终的结果就是最大的乘积和。
     [【python 详解】](./daily/343_2020-12-25_整数拆分.md)


- [1664. 生成平衡数组的方案数【难度：中等】](https://leetcode-cn.com/problems/ways-to-make-a-fair-array/)
     本题需要注意的一个地方是，对于删除i位置的数之后，后面的奇偶下标切换。i前面的
     奇偶下标不变。也就是说：奇数和 = A[i]左边的奇数和+A[i]右边的偶数和;
	 偶数和 = A[i]左边的偶数和+A[i]右边的奇数和 [【python 详解】](./daily/1664_2020-12-25_生成平衡数组的方案数.md)

- [62. 不同路径【难度：中等】](https://leetcode-cn.com/problems/unique-paths/)
     本题使用dp(i, j)表示从左上角走到(i,j) 的路径数量，并且对于每个位置(i,j)只会从上和左方
	  过来，因此动态规划转移方程: dp(i,j)=dp(i−1,j)+dp(i,j−1)[【python 详解】](./daily/62_2020-12-25_不同路径.md)

- [63. 不同路径II【难度：中等】](https://leetcode-cn.com/problems/unique-paths-ii/)
     本题和上一题思路没什么区别，状态转移的时候需要考虑是否存在障碍，
	 同时初始化的时候也存在不同。[【python 详解】](./daily/63_2020-12-25_不同路径II.md)


下面这三道题是属于一类问题，都是基于所在区域内的正方形的相关问题。

- [221. 最大正方形【难度：中等】](https://leetcode-cn.com/problems/maximal-square/)
     本题的关键在于找到最大边长的正方形，其中关键的一个迭代关系
	 dp[i][j] = min(dp[i-1][j],dp[i][j-1],dp[i-1][j-1])+1[【python 详解】](./daily/221_2020-12-28_最大正方形.md)

- [1277. 统计全为 1 的正方形子矩阵【难度：中等】](https://leetcode-cn.com/problems/count-square-submatrices-with-all-ones/)
     本题的关键在于找到最大边长的正方形，其中关键的一个迭代关系
	 dp[i][j] = min(dp[i-1][j],dp[i][j-1],dp[i-1][j-1])+1[【python 详解】](./daily/1277_2020-12-28_统计全为1的正方形子矩阵.md)

- [1504. 统计全 1 子矩形【难度：中等】](https://leetcode-cn.com/problems/count-submatrices-with-all-ones/)
     本题的关键在于想到，只要连续的就是矩形，通过二维数组，记录以位置[i,j]
	 为右下角的矩形的个数，在通过列从上往下的统计每个位置[i,j]在行列位置上
	 能够构成的矩形个数。[【python 详解】](./daily/1504_2020-12-28_统计全1子矩形.md)

- [85. 最大矩形【难度：困难】](https://leetcode-cn.com/problems/count-submatrices-with-all-ones/)
     本题和上题解法类似，也是通过记录每个位置的i,j作为右下角的最大宽度，
	 在通过在列的方向上寻找最大的矩形面积，得到最终结果。除此之外
	 还有一个单调栈的解法类似于84题的解法。[【python 详解】](./daily/85_2020-12-28_最大矩形.md)
















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
