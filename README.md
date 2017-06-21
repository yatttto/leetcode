# LeetCode Solutions

## Easy

### 412.Fizz Buzz

*Write a program that outputs the string representation of numbers from 1 to n.*

*But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.*

思路：判断是否能被3,5或者同时被3和5整除。简单的写法就是4个判断语句，这里可以用列表解析写出一行的解法。`range()`可以用`xrange()`替代。

```python
class Solution(object):
    def fizzBuzz(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        return ["Fizz"*(not i%3)+ "Buzz"*(not i%5) or str(i) for i in range(1,n+1)]
```



### 104.Maximum Depth of Binary Tree

*Given a binary tree, find its maximum depth.*

*The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.*

思路：先判断是否为空二叉树，这里是一个递归调用自身的`maxDepth`方法

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root:
            return 0
        return 1+max(self.maxDepth(root.left),self.maxDepth(root.right))
```



### 561.Array Partion I

*Given an array of 2n integers, your task is to group these integers into n pairs of integer, say (a1, b1), (a2, b2), ..., (an, bn) which makes sum of min(ai, bi) for all i from 1 to n as large as possible.*

***Example 1:***

```
Input: [1,4,3,2]

Output: 4
Explanation: n is 2, and the maximum sum of pairs is 4 = min(1, 2) + min(3, 4).

```

思路：给我们一个包含偶数个整数的数组，将其两辆分片，然后将每块中最小的数字相加使得得到的结果尽可能大。我们只需要先将这个数组排序，然后利用python的切片进行分片，再讲得到的结果相加。

```python
class Solution(object):
    def arrayPairSum(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        return sum(sorted(nums)[::2])
```