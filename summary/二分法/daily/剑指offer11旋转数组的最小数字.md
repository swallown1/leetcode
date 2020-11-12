## 每日一题 - 剑指 Offer 11. 旋转数组的最小数字

### 信息卡片

- 时间：2020-11-12
- 题目链接：[](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)
- tag：`二分法`
- 难度：简单


### 题目描述

```
把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，

输出旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一个旋转，该数组的最小值为1。  


```
示例 1：

输入：[3,4,5,1,2]
输出：1

示例 2：

输入：[2,2,2,0,1]
输出：0 
 

下面是代码

```
class Solution:
    def minArray(self, numbers: List[int]) -> int:
        left,right = 0 , len(numbers)-1
        while left <= right:
            mid  = (left+right) // 2
            if numbers[mid] > numbers[right]:
                left = mid + 1
            elif numbers[mid] < numbers[right]:
                right = mid 
            else:
                right -=1
        return numbers[left]
```

### 思路



这道题的是为了找最小值，那么我们最好使用与最后一个值进行比较，通过中间值和最后一个值进行判断，根据结果可以判定最小值的位置在哪
并且要注意如果中间值和最后一个值相等，那么这时候最好的办法就是让right-1，因为如果此时中间值最好是最小值，单独移动right
不会让最小值丢失，因为中间值还在范围内，如[222234562]，如果让right = mid-1 那么容易造成最小值丢失。
同时对于 [6666123456]这种情况也不会把最小值丢失。




