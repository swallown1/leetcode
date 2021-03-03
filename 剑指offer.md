
[剑指 Offer 03. 数组中重复的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/submissions/)

在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。
 
思路：采用set来存储，当访问到已经存在字典中的数字的时候，直接返回。(同样适用于返回第一个重复的数字)
这道题的另一个值得思考的问题就是，如果不是返回随意一个，而是将重复的都返回，在只遍历一遍的条件下怎么解决。

```
def findRepeatNumber(self, nums: List[int]) -> int:
	numdict = {}
	for i in nums:
		if i not in numdict:
			numdict[i] = 1
		else:return i
	return None
```

[剑指 Offer 04. 二维数组中的查找](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

思路：从左上角或者右下角网对方向查找
```
def findNumberIn2DArray(self, matrix: List[List[int]], target: int) -> bool:
	if not len(matrix) or not len(matrix[0]):return False
	n,m = len(matrix),len(matrix[0])
	i,j = 0,m-1
	while i<=n-1 and j >=0:
		if matrix[i][j] > target:
			j -=1
		elif matrix[i][j] < target:
			i +=1
		else:return True
	return False
```

[剑指 Offer 05. 替换空格](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)

请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

思路：利用list存储非空格字符，如果是空格存储"%20"。

```
def replaceSpace(self, s: str) -> str:
	res = []
	for i in range(len(s)):
		if s[i] == " ":
			res.append("%20")
		else:res.append(s[i])
	return "".join(res)
```

[剑指 Offer 06. 从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

思路：将值存在list中  最后翻转。可以用递归的方法，但是递归太消耗时间和内存
```
def reversePrint(self, head: ListNode) -> List[int]:
	ans = []
	while head:
		ans.append(head.val)
		head = head.next
	return ans[::-1]
```


[剑指 Offer 07. 重建二叉树](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/)

递归：递归出口是前序或中序为空，然后根据先序序列的第一个值构造根节点，如果先序序列只有一个值，则直接返回即可 
表明是叶子节点，然后找出当前节点在中序序列的索引，接着递归左右子树即可。
```
def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
	if not preorder or not inorder:return None
	root = TreeNode(preorder[0])
	if len(preorder) == 1: return root
	idx = inorder.index(preorder[0])
	root.left = self.buildTree(preorder[1:idx+1],inorder[:idx])
	root.right = self.buildTree(preorder[idx+1:],inorder[idx+1:])
	return root
```
优化版：只对无重复的树有效。
思路是将中序存在哈希表中，然后根据当前节点子先序中的索引构造树结构，然后取出当前节点在中序中的
索引i，根据这个再去递归构建左右子树。之所以比上面的要块是因为这里查找中序节点比index找更快。
```
def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
	def recur(root, left, right):
		if left > right: return                               # 递归终止
		node = TreeNode(preorder[root])                       # 建立根节点
		i = dic[preorder[root]]                               # 划分根节点、左子树、右子树
		node.left = recur(root + 1, left, i - 1)              # 开启左子树递归
		node.right = recur(i - left + root + 1, i + 1, right) # 开启右子树递归
		return node                                           # 回溯返回根节点

	dic, preorder = {}, preorder
	for i in range(len(inorder)):
		dic[inorder[i]] = i
	return recur(0, 0, len(inorder) - 1) 
```

[剑指 Offer 09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)


```
class CQueue:
    def __init__(self):
        self.stack1 = []
        self.stack2 = []

    def appendTail(self, value: int) -> None:
        self.stack1.append(value)

    def deleteHead(self) -> int:
        if self.stack2:return self.stack2.pop()
        if not self.stack1: return -1
        while self.stack1:
            self.stack2.append(self.stack1.pop())
        return self.stack2.pop()
```

[剑指 Offer 10- I. 斐波那契数列](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/)

动态规划
```
class Solution:
    def fib(self, n: int) -> int:
        pre1 = 1
        pre0 = 0
        for _ in range(n):
            pre0,pre1= pre1,pre0 + pre1
        return (pre0) % 1000000007 
```

[剑指 Offer 10- II. 青蛙跳台阶问题](https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/)

注意  初始值问题，从第二个阶梯开始进入DP问题。

```
def numWays(self, n: int) -> int:
        pre1 = 2
        pre0 = 1
        if n < 2:return 1
        for _ in range(2,n):
            pre0,pre1= pre1,pre0 + pre1
        return (pre1) % 1000000007 
```

[剑指 Offer 11. 旋转数组的最小数字](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/submissions/)
思路：和右边比，如果mid大于右边表示最小值在右边，因此left = mid+1
如果mid小于右边表示最小值在做边，因此right = mid
否则  right左移   因此会出现很多值相等情况

```
class Solution:
	def minArray(self, numbers: List[int]) -> int:
		left,right = 0 ,len(numbers)-1
		while left < right:
			mid = (left+right)// 2
			if numbers[mid] < numbers[right]:
				right = mid
			elif numbers[mid] > numbers[right]:
				left = mid + 1
			else: right -=1
		return numbers[left]
```

[剑指 Offer 12. 矩阵中的路径](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/submissions/)

思路：回溯法，对每个点进行一次DFS，通过改变board[i][j]的值，来做已经
访问过的判断。

```
def exist(self, board: List[List[str]], word: str) -> bool:
	n,m=len(board),len(board[0])
	def dfs(i,j,k):
		if not (0<=i<n and 0<=j<m and word[k] == board[i][j]): return False
		if k == len(word)-1:return True
		board[i][j] =' '
		ans = dfs(i+1,j,k+1) or dfs(i-1,j,k+1) or dfs(i,j+1,k+1) or dfs(i,j-1,k+1)
		board[i][j] = word[k]
		return ans
	
	for i in range(n):
		for j in range(m):
			if dfs(i,j,0):
				return True
	return False

```


[剑指 Offer 13. 机器人的运动范围](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

思路：4中情况当前节点不符合条件，i，j越界；si+sj大于k；i，j已访问过
通过字典判断是否访问过，si，sj的变化，如果i或j+1满10 其实其各位数的和
是减少8的反之加1

```
def movingCount(self, m: int, n: int, k: int) -> int:
	def dfs(i,j,si,sj):
		if i >=m or j >=n or (i,j) in visited or si+sj > k:return 0
		visited.add((i,j))
		return 1 + dfs(i+1,j,si+1 if (i+1)%10 else si-8,sj) + dfs(i,j+1,si,sj+1 if (j+1)%10 else sj-8)
	visited = set()
	return dfs(0,0,0,0)
```

[剑指 Offer 14- I. 剪绳子](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/)

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m - 1] 。请问 k[0]*k[1]*...*k[m - 1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

思路：DP方法，dp存储以i为长度的绳子的最大乘积。所以对于长度为i的绳子，切分点为
j，需要从j*dp[i-j]和j\*(i-j)中找最大，同时如果大于现有的dp[i]则更新

```
def cuttingRope(self, n: int) -> int:
	dp = [0]*(n+1)
	for i in range(n+1):
		for j in range(i):
			dp[i] = max(max(j*dp[i-j],j*(i-j)),dp[i])
	return dp[-1]
```

[剑指 Offer 15. 二进制中1的个数](https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/submissions/)

请实现一个函数，输入一个整数（以二进制串形式），输出该数二进制表示中 1 的个数。例如，把 9 表示成二进制是 1001，有 2 位是 1。因此，如果输入 9，则该函数输出 2
 
思路：位运算。  n&1判定最右边是否为1   >> 以为运算  二进制向右移
```
class Solution:
    def hammingWeight(self, n: int) -> int:
        cont = 0
        while n:
            cont += n&1
            n >>=1
        return cont
```

[剑指 Offer 16. 数值的整数次方](https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/)

实现函数double Power(double base, int exponent)，求base的exponent次方。不得使用库函数，同时不需要考虑大数问题。
 
思路：考察的依旧是移位运算，通过计算二进制的方式求整数次方
```
def myPow(self, x: float, n: int) -> float:
	if n <0 : x,n = 1/x,-n
	res = 1
	while n:
		if n&1: res *=x
		x *=x
		n >>=1
	return res
```

[剑指 Offer 17. 打印从1到最大的n位数](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)

```

```

[剑指 Offer 18. 删除链表的节点](https://leetcode-cn.com/problems/shan-chu-lian-biao-de-jie-dian-lcof/)

思路：前后指针，找到后删除。
```
def deleteNode(self, head: ListNode, val: int) -> ListNode:
	if not head:return head
	if head.val == val:return head.next
	pre , curr = head ,head.next
	while curr and curr.val != val:
		pre , curr = curr , curr.next
	pre.next = curr.next
	return head
```

[剑指 Offer 19. 正则表达式匹配](https://leetcode-cn.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof/solution/jian-zhi-offer-19-zheng-ze-biao-da-shi-pi-pei-dong/)

```
```


[剑指 Offer 20. 表示数值的字符串](https://leetcode-cn.com/problems/biao-shi-shu-zhi-de-zi-fu-chuan-lcof/)

```
```

[剑指 Offer 21. 调整数组顺序使奇数位于偶数前面](https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/)

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位于数组的后半部分。

思路，双指针  左边先找到偶数 右边找到奇数 然后交换  然后递归即可
```
def exchange(self, nums: List[int]) -> List[int]:
	left,right = 0,len(nums)-1
	while left < right:
		while left < right and nums[left]&1 == 1:left +=1
		while left < right and nums[right]&1 == 0:right -=1
		nums[left],nums[right] = nums[right],nums[left]
	return nums
```

[剑指 Offer 22. 链表中倒数第k个节点](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)



思路L:双指针，先两个指针相距k个单位 在一起移动
```
def getKthFromEnd(self, head: ListNode, k: int) -> ListNode:
	fast , slow = head,head
	for _ in range(k):
		fast = fast.next
	while fast:
		fast = fast.next
		slow = slow.next
	return slow
```

[剑指 Offer 24. 反转链表](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/)

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

思路:头插法
```
def reverseList(self, head: ListNode) -> ListNode:
	pre,curr = None,head
	while curr:
		tmp = curr.next
		curr.next = pre
		pre = curr
		curr = tmp
	return pre
```

[剑指 Offer 25. 合并两个排序的链表](https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/)

输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

思路：就是比较，然后选择小的加到合并的链表尾部，这其实比leetceode上的链表值做加发简单。

```
def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
	head = p = ListNode(0)
	while l1 and l2 :
		if l1.val > l2.val:
			p.next,l2= l2,l2.next
		else:
			p.next,l1= l1,l1.next
		p = p.next
	if not l1: p.next = l2
	if not l2: p.next = l1
	return head.next
```

[剑指 Offer 26. 树的子结构](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/)
思路：
	首先考虑的是以A,B为根节点  判断是否是相同结构：
		如果B到空，表明以比较完全，A，B相同；如果A为空 或A与B不等，表明不相同；	
		剩下的返回A和B的左右节点是否相等
	然后考虑的是整体，只要满足B是A的子结构 或B是A 的左子树中的子结构 或者B是A 的有子树中的子结构
	一种情况即可
```
def isSubStructure(self, A: TreeNode, B: TreeNode) -> bool:
	def curr(A,B):
		if not B: return True
		if not A or A.val != B.val: return False
		return curr(A.left,B.left) and curr(A.right,B.right)
	return bool(A and B) and (curr(A,B) or self.isSubStructure(A.left,B) or self.isSubStructure(A.right,B))
```


[剑指 Offer 27. 二叉树的镜像](https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/)

请完成一个函数，输入一个二叉树，该函数输出它的镜像。
例如输入：

     4
   /   \
  2     7
 / \   / \
1   3 6   9
镜像输出：

     4
   /   \
  7     2
 / \   / \
9   6 3   1 

思路：交换左右子树，这里注意用变量先保存一下。
```
def mirrorTree(self, root: TreeNode) -> TreeNode:
	def dfs(root):
		if not root: return None
		tmp = root.left
		root.left = self.mirrorTree(root.right)
		root.right = self.mirrorTree(tmp)
		return root
	return dfs(root)
```

[剑指 Offer 28. 对称的二叉树](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/)



思路：递归出口：如果是叶子节点，对称；如果左右子树一个为None 或左右子树不等，不对称
然后返回结果  查看左子树的左子树与右子树的右子树是否一样，左子树的右子树与右子树的左子树是否一样，

```
def isSymmetric(self, root: TreeNode) -> bool:
	def dfs(r1,r2):
		if not r1 and not r2:return True
		if not r1 or not r2 or r1.val != r2.val:return False
		return dfs(r1.left,r2.right) and dfs(r1.right,r2.left)
	return dfs(root.left,root.right) if root else True
```


[剑指 Offer 29. 顺时针打印矩阵](https://leetcode-cn.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/)

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

思路：设定上下左右四个边界，依次循环遍历即可
```
def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
	if not matrix:return []
	l,r,t,b = 0,len(matrix[0])-1,0,len(matrix)-1
	res = []
	while True:
		for i in range(l,r+1):res.append(matrix[t][i])
		t +=1
		if t > b:break
		for i in range(t,b+1):res.append(matrix[i][r])
		r -=1
		if r < l:break
		for i in range(r,l-1,-1):res.append(matrix[b][i])
		b -=1
		if t > b: break
		for i in range(b,t-1,-1):res.append(matrix[i][l])
		l +=1
		if l > r:break
	return res
```

[剑指 Offer 30. 包含min函数的栈](https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/)

思路：维护一个栈，和一个是当前栈内的最小值minstack：
对于入栈，如果minstack为空，或minstack[-1]>=x 则也需要将x入minstack中
对于弹出，如果stack弹出的值为minstack[-1] 则也需要将minstack最后一个值弹出。
```
class MinStack:
    def __init__(self):
        self.stack , self.minstack = [],[]
    def push(self, x: int) -> None:
        self.stack.append(x)
        if not self.minstack or self.minstack[-1] >=x:
            self.minstack.append(x)
    def pop(self) -> None:
        if self.stack.pop() == self.minstack[-1]:
            self.minstack.pop()
    def top(self) -> int:
        return self.stack[-1]
    def min(self) -> int:
        return self.minstack[-1]
```


[剑指 Offer 31. 栈的压入、弹出序列](https://leetcode-cn.com/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof/)

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如，序列 {1,2,3,4,5} 是某栈的压栈序列，序列 {4,5,3,2,1} 是该压栈序列对应的一个弹出序列，但 {4,3,5,1,2} 就不可能是该压栈序列的弹出序列。
 
思路：遍历入栈顺序进行入栈，如果栈的最后一位等于出栈的第i位则将栈弹出
并将i加1，直到栈为空，返回True
```
def validateStackSequences(self, pushed: List[int], popped: List[int]) -> bool:
	stack = []
	i = 0
	for num in pushed:
		stack.append(num)
		while stack and stack[-1] == popped[i]:
			stack.pop()
			i +=1
	return not stack 
```

[剑指 Offer 32 - I. 从上到下打印二叉树](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/)



思路：层次遍历，使用队列
```
def levelOrder(self, root: TreeNode) -> List[int]:
	if not root: return []
	queue = collections.deque()
	res = []
	queue.append(root)
	while queue:
		root = queue.popleft()
		res.append(root.val)
		if root.left:queue.append(root.left)
		if root.right:queue.append(root.right)
	return res
```

[剑指 Offer 32 - II. 从上到下打印二叉树 II](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/)
思路：
```
def levelOrder(self, root: TreeNode) -> List[List[int]]:
	if not root: return []
	queue = collections.deque()
	res = []
	queue.append(root)
	while queue:
		tmp = []
		for _ in range(len(queue)):
			root = queue.popleft()
			tmp.append(root.val)
			if root.left:queue.append(root.left)
			if root.right:queue.append(root.right)
		res.append(tmp)
	return res
```

[剑指 Offer 32 - III. 从上到下打印二叉树 III](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)
思路：tmp的时候使用双向队列，根据res的长度来判断当前是从头插还是从尾插。
```
def levelOrder(self, root: TreeNode) -> List[List[int]]:
	if not root: return []
	queue = collections.deque([root])
	res = []
	while queue:
		tmp = collections.deque()
		for _ in range(len(queue)):
			root = queue.popleft()
			if len(res) % 2 == 1:tmp.appendleft(root.val)
			else: tmp.append(root.val)
			if root.left:queue.append(root.left)
			if root.right:queue.append(root.right)
		res.append(list(tmp))
	return res
```

[剑指 Offer 33. 二叉搜索树的后序遍历序列](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)
思路：倒叙后续遍历  就是 根 右 左，又是二叉搜索树，因此通过栈就能找到右 根
这是一个递增序列，当遇到不是递增的情况，说明这个数是某棵树的左节点，然后依次弹出
栈中的节点，看当前节点是哪个节点的左节点。如果出现倒叙中出现大于根节点的
节点，则一定存在问题  不会是一个二叉搜索树的后续遍历序列。
```
def verifyPostorder(self, postorder: List[int]) -> bool:
        stack = []
        root = float("inf")
        for i in range(len(postorder)-1,-1,-1):
            if postorder[i] > root:return False
            while stack and postorder[i] < stack[-1]:
                root = stack.pop()
            stack.append(postorder[i])
        return True
```

[剑指 Offer 34. 二叉树中和为某一值的路径](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/)
思路：深度优先，判断当target等于0且当前为叶子节点，保存结果。然后就是遍历左右
子树。当前得先计算path和target才能判断是否符合条件，不然序列的最后一个数值
不能被保存。

```
def pathSum(self, root: TreeNode, sum: int) -> List[List[int]]:
	res = []
	path=[]
	def dfs(root,target):
		if not root: return False
		path.append(root.val)
		target -=root.val
		if target == 0 and not root.left and not root.right:  
			res.append(list(path))
		dfs(root.left,target)
		dfs(root.right,target)
		path.pop()
	dfs(root,sum)
	return res
```
或
```
def pathSum(self, root: TreeNode, sum: int) -> List[List[int]]:
	res = []
	def dfs(root,currsum,tmp):
		if not root: return False
		tmp.append(root.val)
		if sum == currsum+root.val and not root.left and not root.right:  
			res.append(list(tmp))
		dfs(root.left,currsum+root.val,tmp)
		dfs(root.right,currsum+root.val,tmp)
		tmp.pop()
	dfs(root,0,[])
	return res
```

[剑指 Offer 35. 复杂链表的复制](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/)


思路：这道题和树的深度拷贝是一样的，使用深度优先思想，用字典来判断是否
复制过该节点，已复制的直接返回，否则进行构造，并将构造好的保存到字典中。
```
def copyRandomList(self, head: 'Node') -> 'Node':
	def dfs(root):
		if not root :return root
		if root in visited:
			return visited[root]
		copy = Node(root.val, None, None)
		visited[root] = copy
		copy.next = dfs(root.next)
		copy.random = dfs(root.random)
		return copy
	visited = {}
	return dfs(head)
```

[剑指 Offer 36. 二叉搜索树与双向链表](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/)


输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的循环双向链表。要求不能创建任何新的节点，只能调整树中节点指针的指向。

思路，递归的中序遍历进行改进，类似于判断是否是二叉搜索树那题
通过pre 和curr指针，将pre和curr进行连接。最后在吧链表尾部和头部连接。
```
def treeToDoublyList(self, root: 'Node') -> 'Node':
	if not root: return 
	def dfs(curr):
		if not curr: return 
		dfs(curr.left)
		if self.pre:
			self.pre.right,curr.left = curr, self.pre
		else:
			self.head = curr
		self.pre = curr
		dfs(curr.right)
	self.pre = None
	dfs(root)
	self.pre.right,self.head.left = self.head,self.pre
	return self.head
```
 
[剑指 Offer 38. 字符串的排列](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/)

输入一个字符串，打印出该字符串中字符的所有排列。你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。

思路：回溯法，主要的思路是通过交换位置，达到组合变幻，对于
可能出现重复字母，这里的做法是通过集合的方式，排除两个相同的字符相互交换。

```
def permutation(self, s: str) -> List[str]:
	c,res = list(s),[]
	def dfs(x):
		if x == len(c)-1:
			res.append("".join(c))
		dic = set()
		for i in range(x,len(c)):
			if c[i] in dic:continue  # 排除两个相同的相互交换
			dic.add(c[i])
			c[x],c[i] = c[i],c[x]
			dfs(x+1)
			c[i],c[x] = c[x],c[i] 
	dfs(0)
	return res
```
 
 
 [剑指 Offer 39. 数组中出现次数超过一半的数字](https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)
 
 数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。你可以假设数组是非空的，并且给定的数组总是存在多数元素。
 
 思路：投票法来找出众数，然后利用众数来计算出现过的次数是否大于一半的数
 空间复杂度  O(1)  时间复杂度  O(N)
 ```
 def majorityElement(self, nums: List[int]) -> int:
	 vote,cont = 0,0
	 for n in nums:
		 if vote == 0: x = n 
		 vote +=1 if n == x else -1
	 for n in nums:
		 if x == n:cont +=1
	 return x if cont > len(nums)//2 else 0
 ```

 
[剑指 Offer 68 - I. 二叉搜索树的最近公共祖先](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/)

给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉搜索树:  root = [6,2,8,0,4,7,9,null,null,3,5]
 

思路：比较根节点的值和p q的关系，如果p，q的值都大于或小于root 的值
那么p，q必然在root的右子树或左子树。迭代下去，知道不满足这两种情况则是最深的
共同祖先
 ```
 def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
 	while root:
 		if root.val < p.val and root.val < q.val:
 			root = root.right
 		elif root.val > p.val and root.val > q.val:
 			root = root.left
 		else: break
 	return root
 ```
 
[剑指 Offer 68 - II. 二叉树的最近公共祖先](https://leetcode-cn.com/problems/er-cha-shu-de-zui-jin-gong-gong-zu-xian-lcof/)

给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉树:  root = [3,5,1,6,2,0,8,null,null,7,4] 

思路：如果根节点等于p或q，返回该节点即可，然后遍历左右子树
如果左子树为空表示不再左子树  所以有可能在右子树 返回右子树
如果右子树为空表示不再右子树  所以有可能在自左子树 返回左子树
 ```
 def lowestCommonAncestor(self, root: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode:
 	if not root or root == p or root == q:return root
 	left = self.lowestCommonAncestor(root.left,p,q)
 	right = self.lowestCommonAncestor(root.right,p,q)
 	if not left : return right
 	if not right: return left
 	return root
 ```
 
 
[剑指 Offer 40. 最小的k个数](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)

快排：
 ```
 def quick_sort(arr,l,r):
	 if l >= r:return
	 i,j = l,r
	 while i < j:
		 while i<j and arr[l] <= arr[j]: j -=1
		 while i<j and arr[l] >= arr[i]: i +=1
		 arr[i],arr[j] = arr[j],arr[i]
	 arr[l],arr[i]=arr[i],arr[l]
	 quick_sort(arr,l,i-1)
	 quick_sort(arr,i+1,r)
 quick_sort(arr,0,len(arr)-1)
 ```
 
思路：由于不需要有序的，因此只需要找到以k为基数的所有左边的值即为最小的k个数
因此就不需要想快拍一样左右两边递归进行排序。
 
 ```
def getLeastNumbers(self, arr: List[int], k: int) -> List[int]:
	def quick_sort(arr,l,r):
		if l >= r:return
		i,j = l,r
		while i < j:
		 while i<j and arr[l] <= arr[j]: j -=1
		 while i<j and arr[l] >= arr[i]: i +=1
		 arr[i],arr[j] = arr[j],arr[i]
		arr[l],arr[i]=arr[i],arr[l]
		if k < i: quick_sort(arr,l,i-1)
		if k > i: quick_sort(arr,i+1,r)
		return arr[:k]
	return  quick_sort(arr,0,len(arr)-1)
 ```
 
 
[剑指 Offer 42. 连续子数组的最大和](https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/)
思路：动态规划题，可以直接用nums来存储中间状态，关键就是如果前i-1的状态
的和小于0 那么直接就用nums[i]原值做最大和。即状态转移：nums[i] += max(nums[i-1],0)
 ```
def maxSubArray(self, nums: List[int]) -> int:
	if len(nums) == 0:return 0
	for i in range(1,len(nums)):
		nums[i] += max(nums[i-1],0)
	return max(nums)
 ```
 
[剑指 Offer 44. 数字序列中某一位的数字](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)
思路：通过start * digital * 9 计算以digital为位数的数的总数
然后通过 start + (n-1)//digital 找到这个数
最后通过str(nums)[(n-1)%digital] 定位到时这个数中的那个数字。
 ```
def findNthDigit(self, n: int) -> int:
	start,digital,cont = 1,1,9
	while n > cont:
		n -=cont
		start *=10
		digital +=1
		cont = start * digital * 9
	nums = start + (n-1)//digital
	return  int(str(nums)[(n-1)%digital])
 ```
 
 
[剑指 Offer 45. 把数组排成最小的数](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。

思路：如果 3,30组成330 大于30,3组成303，那么其实3应该放在30 的后面组成的str
所对应的值更小。那么我们需要对数组进行排序，使得两两数之间组成的数是最小的情况。
因此可以修改快排的排序规则，重排数组，然后将数组组成字符串。注意
这里可以使用字符相加比较  于是对于数组需要转化成str。
 ```
def minNumber(self, nums: List[int]) -> str:
	def fast_sort(l,r):
		if l >= r:return
		i,j = l,r
		while i<j:
			while i<j and strs[j]+strs[l] >=strs[l]+strs[j]: j-=1
			while i<j and strs[i]+strs[l] <=strs[l]+strs[i]: i+=1
			strs[i],strs[j] = strs[j],strs[i]
		strs[l],strs[i] = strs[i],strs[l]
		fast_sort(l,i-1)
		fast_sort(i+1,r)
	strs = [str(num) for num in nums]
	fast_sort(0,len(strs)-1)
	return "".join(strs)
 ```
 
 
[剑指 Offer 46. 把数字翻译成字符串](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

思路：DP。由于若xi和 xi−1组成的两位数字是在10-25之内的话，
则 dp[i]=dp[i−1]+dp[i−2] 否则 dp[i]=dp[i−1] 。由于之和两个状态
相关于是用a，b分别表示dp[i−1]和dp[i−2]

```
def translateNum(self, num: int) -> int:
	s = str(num)
	a = b =1
	for i in range(2,len(s)+1):
		curr = s[i-2:i]
		c = (a+b) if '10'<=curr<="25" else a 
		b,a = a,c
	return a    

```
还有一个，利用//和%的方式从后往前的方法，和上一个方法反过来
只不过不用将num转化成str，优化空间
```
def translateNum(self, num: int) -> int:
        a = b = 1
        y = num % 10
        while num != 0:
            num //= 10
            x = num % 10
            tmp = 10 * x + y
            c = a + b if 10 <= tmp <= 25 else a
            a, b = c, a
            y = x
        return a 
```

[剑指 Offer 47. 礼物的最大价值](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/)

在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？
  
思路：二维数组的DP问题
```
def maxValue(self, grid: List[List[int]]) -> int:
	row,col = len(grid),len(grid[0])
	for i in range(1,row):
		grid[i][0] +=grid[i-1][0]
	for i in range(1,col):
		grid[0][i] +=grid[0][i-1]
	
	for i in range(1,row):
		for j in range(1,col):
			grid[i][j] += max(grid[i-1][j],grid[i][j-1])
	return grid[-1][-1]
```

[剑指 Offer 48. 最长不含重复字符的子字符串](https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)


思路：利用互动窗口，如果窗口内出现重复字母，则更新窗口左条件
否则更新字典，然后记录当前的窗口距离是否是最大的。
```
def lengthOfLongestSubstring(self, s: str) -> int:
	res, dic,i= 0,{},-1
	for j in range(len(s)):
		if s[j] in dic:
			i = max(i,dic[s[j]])
		dic[s[j]] = j
		res = max(res,j-i)
	return res
```
或者
```
def lengthOfLongestSubstring(self, s: str) -> int:
	if not s:return 0
	n = len(s)
	substr = set()
	right,ans =-1,0
	for left in range(n):
		if left != 0:
			substr.remove(s[left-1])
		while right+1 < n and s[right+1] not in substr:
			substr.add(s[right+1])
			right +=1
		ans= max(ans,right - left + 1)
	return ans
```


[剑指 Offer 49. 丑数](https://leetcode-cn.com/problems/chou-shu-lcof/)

我们把只包含质因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。

思路：递推关系式 dp[i] = min(dp[a]*2,dp[b]\*3,dp[c]\*5),
```
def nthUglyNumber(self, n: int) -> int:
	dp=[1]*n
	a,b,c = 0,0,0
	for i in range(1,n):
		a1,b1,c1 = dp[a]*2,dp[b]*3,dp[c]*5
		dp[i] = min(a1,b1,c1)
		if dp[i] == a1: a+=1
		if dp[i] == b1: b+=1
		if dp[i] == c1: c+=1
	return dp[-1]
```

[剑指 Offer 50. 第一个只出现一次的字符](https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/)

在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

思路：遍历s，用哈希表来存储是否存在大于1 的状态，然后遍历哈希表，返回第一个是
value是true的 key值。
```
def firstUniqChar(self, s: str) -> str:
	dic = {}
	for i in s:
		dic[i] = not i in dic
	for k,v in dic.items():
		if v: return k
	return " "
```

[剑指 Offer 52. 两个链表的第一个公共节点](https://leetcode-cn.com/problems/liang-ge-lian-biao-de-di-yi-ge-gong-gong-jie-dian-lcof/)

输入两个链表，找出它们的第一个公共节点。

思路：A,B同时后移，A到结尾在从headB开始，B到结尾从headA开始
直到遇见相同节点  即A==B
```
def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
	A , B = headA,headB
	while A!=B:
		A = A.next if A else headB
		B = B.next if B else headA
	return A
```

[剑指 Offer 53 - I. 在排序数组中查找数字 I](https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/)

统计一个数字在排序数组中出现的次数。

思路：找到最右侧的索引，这样找target和target-1的最右侧索引，两者的差就是
数组中的个数。
```
def search(self, nums: List[int], target: int) -> int:
        def helper(tar):
            left,right = 0,len(nums)-1
            while left <= right:
                mid = (left+right) // 2
                if nums[mid] <= tar: left = mid + 1
                else: right = mid-1
            return left
        return helper(target) - helper(target-1)
```

[剑指 Offer 53 - II. 0～n-1中缺失的数字](https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/)

一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。
 
思路：如果nums[mid] == mid 表明左边不缺少值，否则说明缺失值在左边部分
```
def missingNumber(self, nums: List[int]) -> int:
	left,right = 0,len(nums)-1
	while left <= right:
		mid = (left+right)//2
		if nums[mid] == mid:
			left = mid + 1
		else:
			right = mid - 1
	return left
```

[剑指 Offer 54. 二叉搜索树的第k大节点](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)

给定一棵二叉搜索树，请找出其中第k大的节点。

思路：二叉搜索树的中序遍历是递增的，那么反过来遍历  即 右 根 左
那么就是降序，则只需要找到第k个数即可。那么只需要在遍历是控制变量k
直到k==0  范围当前节点值 则为最大的第k个值。
```
def kthLargest(self, root: TreeNode, k: int) -> int:
	def midorder(root):
		if not root :return 
		midorder(root.right)
		if self.k == 0:return
		self.k -=1
		if self.k == 0: self.res = root.val
		midorder(root.left)
	self.k = k
	midorder(root)
	return self.res
```

[剑指 Offer 55 - I. 二叉树的深度](https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof)

输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。

```
def maxDepth(self, root: TreeNode) -> int:
	def dfs(root):
		if not root:return 0
		return max(dfs(root.left),dfs(root.right))+1
	return dfs(root)
```

[剑指 Offer 55 - II. 平衡二叉树](https://leetcode-cn.com/problems/ping-heng-er-cha-shu-lcof/)

输入一棵二叉树的根节点，判断该树是不是平衡二叉树。如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。

思路：后续遍历，先判断左右的情况，在判断根节点的情况。这里还可以使用剪枝
如果左子树不是平衡二叉树，那直接就返回。否则判断右子树。-1为不符合平衡二叉树的
情况。
```
def isBalanced(self, root: TreeNode) -> bool:
	def dfs(root):
		if not root:return 0
		left = dfs(root.left)
		if left == -1:return -1
		right = dfs(root.right)
		if right == -1: return -1
		return -1 if abs(left - right) > 1 else max(left,right)+1
	return dfs(root) != -1
```

思路：深度优先，先计算根节点的左右子树的深度，并判断根节点的左右子树高度差是否
不大于1，然后在继续讨论左右子树是否符合。这其实消耗的时间更多一下。
```
def isBalanced(self, root: TreeNode) -> bool:
		if not root:return True
        def dfs(root):
            if not root:return 0
            return max(dfs(root.left),dfs(root.right)) + 1
	    return abs(dfs(root.left)-dfs(root.right)) <=1 and \
		self.isBalanced(root.left) and self.isBalanced(root.right)
```

[剑指 Offer 57. 和为s的两个数字](https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/)

输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。

思路：双指针法
```
def twoSum(self, nums: List[int], target: int) -> List[int]:
	left,right = 0,len(nums)-1
	while left <right:
		if nums[left] + nums[right] < target:
			left +=1
		elif nums[left] + nums[right] > target: right -=1
		else: return [nums[left],nums[right]]
	return []
```

[剑指 Offer 57 - II. 和为s的连续正数序列](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/)

输入一个正整数 target ，输出所有和为 target 的连续正整数序列（至少含有两个数）。
序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。 

思路：滑动窗口  动态的判断窗口内的值和target的大小关系
```
def findContinuousSequence(self, target: int) -> List[List[int]]:
	i,j,s,res = 1,2,3,[]
	while i<j:
		if s == target:
			res.append(list(range(i,j+1)))
		if s >=target:
			s -=i
			i +=1
		else:
			j +=1
			s +=j
	return res
```

[剑指 Offer 58 - I. 翻转单词顺序](https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/)

输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student. "，则输出"student. a am I"。
  
思路：双指针，从后往前i找到首个空格，j用户指向最后一个字母，这样窗口内
就是一个单词，然后放入数组，最后将数组转化成字符串。
```
def reverseWords(self, s: str) -> str:
	s = s.strip()
	i = j = len(s)-1
	res = []
	while i >= 0:
		while i>=0 and s[i] != ' ':  i-=1
		res.append(s[i+1:j+1])
		while s[i] == ' ': i -=1
		j = i
	return ' '.join(res)
```

[剑指 Offer 58 - II. 左旋转字符串](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。
 
思路：用取余的方法实现了索引的问题。当然用切片的方法最快。
```
def reverseLeftWords(self, s: str, n: int) -> str:
	res = ""
	for i in range(n,n+len(s)):
		res += s[i % len(s)]
	return res
```

[剑指 Offer 59 - I. 滑动窗口的最大值](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)

给定一个数组 nums 和滑动窗口的大小 k，请找出所有滑动窗口里的最大值。

思路：通过单调栈的方式，记录当前窗口的最大值，也就是说如果nums[i]
大于最后一个值，则需要弹出，如果窗口满了的话，需要判定当前最大值是否是
窗口的最左侧，即queue[0] == nums[i-k].

```
def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
	if not nums or k==0: return []
	queue,res  = collections.deque(),[]
	for i in range(k):  #未形成窗口
		while queue and queue[-1] < nums[i]:
			queue.pop()
		queue.append(nums[i])
	res.append(queue[0])
	for i in range(k,len(nums)):
		if queue[0] == nums[i-k]:
			queue.popleft()
		while queue and queue[-1] < nums[i]:
			queue.pop()
		queue.append(nums[i])
		res.append(queue[0])
	return res
```

[剑指 Offer 59 - II. 队列的最大值](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/)

请定义一个队列并实现函数 max\_value 得到队列里的最大值，要求函数max\_value、push\_back 和 pop\_front 的均摊时间复杂度都是O(1)。
若队列为空，pop\_front 和 max\_value 需要返回 -1
  
思路：和那个有min的栈思路是一样的，就是维护一个单调栈，目的就是存储当前
队列中的最大值的栈  stack，这个用法个上面的滑动窗口最大值是一样的。
这里主要有两点：当入队列的时候，要判断当前值和stack的末尾值的大小，当大于时
需要将栈的末尾弹出；其次就是出队列的时候，要注意出队列的是否是当前最大值
即 stack[0]
```
class MaxQueue:
    def __init__(self):
        self.queue,self.stack = [],[]
    def max_value(self) -> int:
        return self.stack[0] if self.stack else -1

    def push_back(self, value: int) -> None:
        self.queue.append(value)
        while self.stack and self.stack[-1] < value:
            self.stack.pop()
        self.stack.append(value)

    def pop_front(self) -> int:
        if not len(self.stack): return -1
        val = self.queue.pop(0)
        if val == self.stack[0]:
            self.stack.pop(0)
        return val
```
 
[剑指 Offer 61. 扑克牌中的顺子](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)

从扑克牌中随机抽5张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0 ，可以看成任意数字。A 不能视为 14。

思路：这道题的充要条件：除去大小王，1、无重复数字；2、最大值和最小值的差小于5
因此可以用set来验证重复，或者用排序然后判断前后是否存在相等。
```
def isStraight(self, nums: List[int]) -> bool:
	minval,maxval,repeat = 100,-100,set()
	for num in nums:
		if num == 0:continue
		minval = min(minval,num)
		maxval = max(maxval,num)
		if num in repeat:return False
		repeat.add(num)
	return  maxval-minval < 5
```

[剑指 Offer 62. 圆圈中最后剩下的数字](https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/)
0,1,···,n-1这n个数字排成一个圆圈，从数字0开始，每次从这个圆圈里删除第m个数字（删除后从下一个数字开始计数）。求出这个圆圈里剩下的最后一个数字。

例如，0、1、2、3、4这5个数字组成一个圆圈，从数字0开始每次删除第3个数字，则删除的前4个数字依次是2、0、4、1，因此最后剩下的数字是3。


思路：约瑟夫环” 问题，存在递推公式：
初始 i = 1,f(0) = 0
i = 2   f(1) = (f(0)+m) % n
i = 3   f(2) = (f(1)+m) % n
...
i = n-1   f(n-2) = (f(n-3)+m) % n
返回的就是需要删除的下标。由于这里是1，...，n-1，所以下标等于改值。

这里存在一个动态的一个状态转移  dp[i] = (dp[i-1]+m) % i    dp[0]=0 
```
def lastRemaining(self, n: int, m: int) -> int:
	x = 0
	for i in range(2,n+1):
		x = (x+m) % n
	return x
```

[剑指 Offer 63. 股票的最大利润](https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof)

思路：一次购买  无代价  五冷冻期
```
def maxProfit(self, prices: List[int]) -> int:
	have = -float("inf")
	nothave = 0
	for curr in prices:
		nothave = max(nothave,have+curr)
		have = max(have,-curr)
	return nothave
```

[剑指 Offer 64. 求1+2+…+n](https://leetcode-cn.com/problems/qiu-12n-lcof)

求 1+2+...+n ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

思路：通过逻辑短路判断递归的出口。
```
class Solution:
    def __init__(self):
        self.res = 0

    def sumNums(self, n: int) -> int:
        n >1 and self.sumNums(n-1)
        self.res +=n
        return self.res
```

[剑指 Offer 65. 不用加减乘除做加法](https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/)

```
class Solution:
    def add(self, a: int, b: int) -> int:
        x = 0xffffffff
        a, b = a & x, b & x
        while b != 0:
            a, b = (a ^ b), (a & b) << 1 & x
        return a if a <= 0x7fffffff else ~(a ^ x)
 
```


[剑指 Offer 66. 构建乘积数组](https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/)

```
def constructArr(self, a: List[int]) -> List[int]:
	B = [1]*len(a)
	tmp = 1
	for i in range(1,len(a)):
		B[i] = B[i-1] * a[i-1]
	for i in range(len(a)-2,-1,-1):
		tmp *=a[i+1]
		B[i] *=tmp 
	return B
```




#### 排序算法

1、冒泡排序： 思路是比较前后两个，将大的数往后移动  O(n^2)

```
for i in range(len(nums)):
	flag = False #判断当前是否还有移动，如果没有表明已经有序了  
	for j in range(len(nums)-1-i):
		if nums[j] > nums[j+1]:
			nums[j],nums[j+1]=nums[j+1],nums[j]
			flag = True
	if flag: break
```

2、选择排序：思路是每次找到最小的放到开头
```
def selectSort(self,nums):
	for i in range(len(nums)):
		minidx = i
		for j in range(i+1,len(nums)):
			if nums[minidx] > nums[j]:
				minidx = j
		if minidx != i: nums[minidx],nums[i] = nums[i],nums[minidx]
```

3、快速排序：分治的思想   O(NlogN)

```
def quick_sort(self,nums):
	def helper(nums,left,right):
		if left > right : return 
		i,j=left,right
		while i<j:
			while i<j and nums[j] >nums[left]: j -=1
			while i<j and nums[i] <nums[left]: i +=1
			nums[i],nums[j]=nums[j],nums[i]
		nums[i],nums[left]=nums[left],nums[i]
		helper(left,i-1)
		helper(i+1,right)
	helper(nums,0,len(nums)-1)
```

4、希尔排序：主要是采用分组的方式进行插入排序的方式，当增量减小，组数变多，最后成为一个整组，排序结束。
```
def shellSort(arr):
	length  = len(arr)-1
	gap = length//2
	while gap>0: #gap=1是最后的增量
		for i in range(gap,length): #从第gap个分组开始
			j = i
			while j-gap>=0 and nums[j-gap] > nums[j]:
				nums[j-gap],nums[j] = nums[j] > nums[j-gap]
				j -=gap #判断下一个分组需不需要继续互换
		gap//2 #增量减少，
```

5、归并排序：先采用分治的思想，进行递归的划分，然后根据两个小分组进行排序成一个有序的组
```
def mergeSort(nums):
	if len(nums) <= 1:return nums
	mid = len(nums)//2
	left = mergeSort(nums[:mid])
	right = mergeSort(nums[mid:])
	return merge(left,right)

def merge(left,right):
	i,j = 0,0
	res = []
	while i < len(left) and j < len(right):
		if left[i] <= right[j]:
			res.append(left[i])
			i +=1
		else:
			res.append(right[j])
			j -=1
	if i<len(left): res += left[i:]
	if j<len(right): res += right[j:]
	return res
```

6、堆排序

7、