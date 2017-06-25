# LeetCode Solutions

[TOC]



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


### 557.Reverse Words in a String III

*Given a string, you need to reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.*

```
Input: "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"
```

思路：很简单利用字符串方法以及列表切片

```python
class Solution(object):
    def reverseWords(self, s):
        """
        :type s: str
        :rtype: str
        """
        return " ".join(x[::-1] for x in s.split(' '))
```



### 344.Reverse String

*Write a function that takes a string as input and returns the string reversed.*

***Example:***
*Given s = "hello", return "olleh".*

思路：slice or built-in function

```python
class Solution(object):
    def reverseString(self, s):
        """
        :type s: str
        :rtype: str
        """
        return s[::-1]
```



### 575.Distribute Candies

*Given an integer array with **even** length, where different numbers in this array represent different **kinds** of candies. Each number means one candy of the corresponding kind. You need to distribute these candies **equally** in number to brother and sister. Return the maximum number of **kinds** of candies the sister could gain.*

```
Input: candies = [1,1,2,2,3,3]
Output: 3
Explanation:
There are three different kinds of candies (1, 2 and 3), and two candies for each kind.
Optimal distribution: The sister has candies [1,2,3] and the brother has candies [1,2,3], too. 
The sister has three different kinds of candies. 
```

思路：这里的意思是，用一个列表表示一堆糖，不同的数字代表种类不一样的糖，有兄妹二人分糖，试问妹妹最多可以分到几种糖。这里的话，我们先得到这一堆糖里有多少种糖，可以用集合得到，然后再算平分，也就是该列表长度的一半就是妹妹最终能拿到的糖数。再对得到的两个数进行比较，较小的也就是妹妹最终能得到的糖的种类。

```python
class Solution(object):
    def distributeCandies(self, candies):
        """
        :type candies: List[int]
        :rtype: int
        """
        return min(len(set(candies)),len(candies)/2)
```



### 136.Single Number

*Given an array of integers, every element appears *twice* except for one. Find that single one.

***Note:***
*Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?*

思路：位运算。

```python
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        rec = 0
        for n in nums:
            rec ^= n
        return rec
    	#or
        #return reduce(lambada:x,y x^y,nums)
```



### 485.Max Consecutive Ones

*Given a binary array, find the maximum number of consecutive 1s in this array.*

```
Input: [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s.
    The maximum number of consecutive 1s is 3.
```

*Note*

**The input array will only contain 0 and 1.**
**The length of input array is a positive integer and will not exceed 10,000**

思路：利用`split()`函数。

```python
class Solution(object):
    def findMaxConsecutiveOnes(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        
        return max(map(len,''.join([str(n) for n in nums]).split('0')))
```



### 292.Nim Game

*You are playing the following Nim Game with your friend: There is a heap of stones on the table, each time one of you take turns to remove 1 to 3 stones. The one who removes the last stone will be the winner. You will take the first turn to remove the stones.*

*Both of you are very clever and have optimal strategies for the game. Write a function to determine whether you can win the game given the number of stones in the heap.*

*For example, if there are 4 stones in the heap, then you will never win the game: no matter 1, 2, or 3 stones you remove, the last stone will always be removed by your friend.*

思路：判断是否是4的倍数即可.

```python
class Solution(object):
    def canWinNim(self, n):
        """
        :type n: int
        :rtype: bool
        """
        return (n%4 != 0)
```



### 521.Longest Uncommon Subsequence I

*Given a group of two strings, you need to find the longest uncommon subsequence of this group of two strings. The longest uncommon subsequence is defined as the longest subsequence of one of these strings and this subsequence should not be **any** subsequence of the other strings.*

*A **subsequence** is a sequence that can be derived from one sequence by deleting some characters without changing the order of the remaining elements. Trivially, any string is a subsequence of itself and an empty string is a subsequence of any string.*

*The input will be two strings, and the output needs to be the length of the longest uncommon subsequence. If the longest uncommon subsequence doesn't exist, return -1.*

```
Input: "aba", "cdc"
Output: 3
Explanation: The longest uncommon subsequence is "aba" (or "cdc"), 
because "aba" is a subsequence of "aba", 
but not a subsequence of any other strings in the group of two strings. 
```

思路：这道题很无聊。。。

```python
class Solution(object):
    def findLUSlength(self, a, b):
        """
        :type a: str
        :type b: str
        :rtype: int
        """
        return -1 if a==b else max(len(a),len(b))
```



### 226.Invert Binary Tree

思路：翻转二叉树。

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def invertTree(self, root):
        """
        :type root: TreeNode
        :rtype: TreeNode
        """
        if root:
            root.left,root.right = self.invertTree(root.right),self.invertTree(root.left)
            return root
```



### 349.Intersection of Two Arrays

*Given two arrays, write a function to compute their intersection.*

*Example:*
*Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2].*

*Note:*
*Each element in the result must be unique.*
*The result can be in any order.*

思路：变成集合再用集合运算

```python
class Solution(object):
    def intersection(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        return list(set(nums1)&set(nums2))
```



### 283.Move Zeroes

*Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.*

*For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].*

*Note:*
*You must do this in-place without making a copy of the array.*
*Minimize the total number of operations.*

思路：先查找列表中为0的元素，再删去一个0后增加一个。

```python
class Solution(object):
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        for i in range(len(nums)):
            if nums[i] == 0:
                nums.remove(0)
                nums.append(0)

```

