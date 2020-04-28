# LeetCode之树结构(Tree)

---

### 贪心算法的思想：
>树是一种抽象数据类型（ADT）或是实现这种抽象数据类型的数据结构，用来模拟具有树状结构性质的数据集合。它是由 n(n>0)n(n>0) 个有限节点组成一个具有层次关系的集合。

把它叫做「树」是因为它看起来像一棵倒挂的树，也就是说它是根朝上，而叶朝下的。

它具有以下的特点：

 - 每个节点都只有有限个子节点或无子节点；
 - 没有父节点的节点称为根节点；
 - 每一个非根节点有且只有一个父节点；
 - 除了根节点外，每个子节点可以分为多个不相交的子树；
 - 树里面没有环路
 

### LeetCode Algorithm

(Notes: "&hearts;" Make small but daily progress)

**Easy**

| # | Title | Solution | Difficulty |
|---| ----- | -------- | ---------- |
|404|[左叶子之和](https://leetcode-cn.com/problems/sum-of-left-leaves) | [python](./daily/404_2020-04-14.md)|Easy|
|437|[左叶子之和](https://leetcode-cn.com/problems/is-subsequence/) | [python](./daily/437_2020-04-14.md)|Easy|
|572|[另一个树的子树](https://leetcode-cn.com/problems/subtree-of-another-tree/) | [python](./daily/572_2020-04-14.md)|Easy|
|501|[左叶子之和](https://leetcode-cn.com/problems/is-subsequence/) | [python](./daily/501_2020-04-14.md)|Easy|
|530|[左叶子之和](https://leetcode-cn.com/problems/is-subsequence/) | [python](./daily/530_2020-04-14.md)|Easy|
|538|[把二叉搜索树转换为累加树](https://leetcode-cn.com/problems/convert-bst-to-greater-tree/) | [python](./daily/538_2020-04-15.md)|Easy|
|606|[根据二叉树创建字符串](https://leetcode-cn.com/problems/construct-string-from-binary-tree/) | [python](./daily/606_2020-04-16.md)|Easy|
|653|[两数之和 IV - 输入 BST](https://leetcode-cn.com/problems/two-sum-iv-input-is-a-bst/submissions/)| [python](./daily/653_2020-04-17.md)|Easy|
|563|[二叉树的坡度](https://leetcode-cn.com/problems/binary-tree-tilt/)| [python](./daily/563_2020-04-18.md)|Easy|
|617|[合并二叉树](https://leetcode-cn.com/problems/merge-two-binary-trees/)| [python](./daily/617_2020-04-18.md)|Easy|
|637|[二叉树的层平均值](https://leetcode-cn.com/problems/average-of-levels-in-binary-tree/)| [python](./daily/637_2020-04-19.md)|Easy|
|669|[修剪二叉搜索树](https://leetcode-cn.com/problems/trim-a-binary-search-tree/)| [python](./daily/669_2020-04-19.md)|Easy|
|671|[二叉树中第二小的节点](https://leetcode-cn.com/problems/second-minimum-node-in-a-binary-tree/)| [python](./daily/671_2020-04-19.md)|Easy|
|559|[N叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-n-ary-tree/comments/)|[python](./daily/559_2020-04-20.md)|Easy|
|589|[N叉树的前序遍历](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/)|[python](./daily/589_2020-04-20.md)|Easy|
|590|[N叉树的后序遍历](https://leetcode-cn.com/problems/n-ary-tree-postorder-traversal/)| |Easy|
|700|[二叉搜索树中的搜索](https://leetcode-cn.com/problems/search-in-a-binary-search-tree/)|[python](./daily/700_2020-04-21.md)|Easy|
|783|[二叉搜索树结点最小距离](https://leetcode-cn.com/problems/minimum-distance-between-bst-nodes/)|[python](./daily/783_2020-04-21.md)|Easy|
|530|[ 二叉搜索树的最小绝对差](https://leetcode-cn.com/problems/minimum-absolute-difference-in-bst/)|[python](./daily/530_2020-04-27.md)|Easy|
|872
|897
|938
|965
|993
|1022



**Medium**

| # | Title | Solution | Difficulty |
|---| ----- | -------- | ---------- |
|814|[二叉树剪枝](https://leetcode-cn.com/problems/binary-tree-pruning/)|[python](./daily/814_2020-04-25.md)|Medium|
|701|[二叉搜索树中的插入操作](https://leetcode-cn.com/problems/insert-into-a-binary-search-tree/)|[python](./daily/701_2020-04-26.md)|Medium|
|889|[根据前序和后序遍历构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/)|[python](./daily/889_2020-04-26.md)|Medium|
|889|[根据前序和后序遍历构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/)|[python](./daily/889_2020-04-26.md)|Medium|
|285二叉搜索树中的顺序后继	
|298二叉树最长连续序列
|333最大 BST 子树	
|337打家劫舍 III	
|366寻找二叉树的叶子节点	
|510二叉搜索树中的中序后继 II	
|449序列化和反序列化二叉搜索树	
|450删除二叉搜索树中的节点	
|515在每个树行中找最大值|[在每个树行中找最大值](https://leetcode-cn.com/problems/find-largest-value-in-each-tree-row/)|[python](./daily/515_2020-04-22.md)|Easy|
|508|[出现次数最多的子树元素和](https://leetcode-cn.com/problems/most-frequent-subtree-sum/)|[python](./daily/508_2020-04-22.md)|Medium|
|652|[寻找重复的子树](https://leetcode-cn.com/problems/find-duplicate-subtrees/)|[python](./daily/652_2020-04-23.md)|Medium|
|513|[找树左下角的值	](https://leetcode-cn.com/problems/find-bottom-left-tree-value/)|[python](./daily/513_2020-04-24.md)|Medium|
|549|[二叉树中最长的连续序列](vip的题)|[python](./daily/549_2020-04-24.md)|Medium|
|666|路径和 IV	
|623|[在二叉树中增加一行](https://leetcode-cn.com/problems/add-one-row-to-tree/)|[python](./daily/623_2020-04-24.md)|Medium|
|622|[二叉树最大宽度](https://leetcode-cn.com/problems/maximum-width-of-binary-tree/)|[python](./daily/622_2020-04-25.md)|Medium|
|654|[最大二叉树](https://leetcode-cn.com/problems/maximum-binary-tree/)|[python](./daily/654_2020-04-25.md)|Medium|
|105|[从前序与中序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)|[python](./daily/105_2020-04-27.md)|Medium|