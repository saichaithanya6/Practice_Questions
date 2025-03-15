### Dynamic programming

Breaking the problem into smaller tasks, more manageable sub-problems.

### Question 1
Given an integer array nums, find a subarray that has the largest product, and return the product.

Example 1:

Input: nums = [2,3,-2,4], Output: 6, Explanation: [2,3] has the largest product 6.

```go
class solution:
	def ProductMax(self, nums: List[int]) :
		res = 1
		max_num, min_num = 1, 1
		# The problem can be solved by assigning two variables min, max numbers. We use min_num because if we have -ve numbers this can be helpful.
		for i in nums:
			tem = max_num
			max_num = max( max_num * i, min_num * i, i) 
			min_num = min(tem * i, min_mun * i, i)
			res = max(max_num, res)
		return res
```

### Question 2:
You are climbing a staircase. It takes n steps to reach the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

 
Example 1:

Input: n = 2

Output: 2

Explanation: There are two ways to climb to the top.

1. 1 step + 1 step

2. 2 steps

![image](https://github.com/user-attachments/assets/3db9b77e-57fa-40c4-8d8c-1e9e573ba02c)

For n= 5, we are calculating different possibilities of reaching the end as above. We can observe that the n=2 is done twice. The computation is double since n=2 is repeated. To solve this we use dynamic programming with bottom-up approach.

```go
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        f = 1
        s = 1

	for i in range(n - 1):
		tem = f # Restoring in temporary vaiable
		f += s # finding the next number by adding the previous two numbers
		s = tem
	return f
```
		
### Question 3:

You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

Example 1:

Input: coins = [1,2,5], amount = 11

Output: 3

Explanation: 11 = 5 + 5 + 1

![image](https://github.com/user-attachments/assets/3c50fee6-0fe3-4c80-9606-ae0fd46731b5)

In the above, we store the outputs of each number until the result in 'dp' array so that the dynamic programming is done. 
```go
class Solution(object):
    def coinChange(self, coins, amount):
        """
        :type coins: List[int]
        :type amount: int
        :rtype: int
        """
	dp = [amount + 1] * (amount + 1)
	dp[0] = 0
	for i in range(1, amount+1):
		for c in coins:
			if i - c >= 0:
				dp[i] = min(dp[i], 1+ dp[ i-c])
	return dp[amount + 1] if dp[amount+1] != amount +1 else -1
```

### Question 4:
Given an integer array nums, return the length of the longest strictly increasing subsequence.

Example 1:

Input: nums = [10,9,2,5,3,7,101,18]

Output: 4

Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.
```go
class Solution(object):
    def lengthOfLIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
	lis = [1] * len(nums)
	for i in range(len(nums) -1, -1, -1):
		for j in range(i+1, len(nums)):
			if nums[i] < nums[j]:
				lis[i] = max(lis[i], 1 + lis[j])
	return max(lis)
```

### Question 5:
Given two strings text1 and text2, return the length of their longest common subsequence. If there is no common subsequence, return 0.

A subsequence of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

Example 1:

Input: text1 = "abcde", text2 = "ace"

Output: 3  

Explanation: The longest common subsequence is "ace" and its length is 3.

![image](https://github.com/user-attachments/assets/6dc2d9da-51d0-4554-80c2-db4955c7b4c2)

```do
def longestCommonSubsequence(self, text1, text2):
        """
        :type text1: str
        :type text2: str
        :rtype: int
        """
        matrix = [[0 for i in range(len(text2) + 1)] for i in range(len(text1) + 1)] #We are creating a matrix wiht an additional row, column of all '0'

        for i in range(len(text1)-1, -1, -1):
          for j in range(len(text2)-1, -1, -1):
            if text1[i] == text[j]:
# This problem is dp beacuse if the letter in the text2 and text1 are not equal then we are moving to next iteration. Also this is a bottom-up approach
              matrix[i][j] = 1 + matrix[i+1][j+1] #We add one to the matrix and also add diagonal component (DP)
            else:
              matrix[i][j] = max(matrix[i+1][j], matrix[i][j+1])
        return matrix[0][0]
```
### Question 6:
Given a string s and a dictionary of strings wordDict, return true if s can be segmented into a space-separated sequence of one or more dictionary words.

Note that the same word in the dictionary may be reused multiple times in the segmentation.

Example 1:

Input: s = "leetcode", wordDict = ["leet","code"]
```
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
Example 2:
```
Input: s = "applepenapple", wordDict = ["apple","pen"]
```
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
Note that you are allowed to reuse a dictionary word.
```

![image](https://github.com/user-attachments/assets/ffd54a15-7b02-403e-80e5-566df0c9d708)

In the above example, we have 5 words in wordDict. In normal brut force, we compare each word in the string which makes the compution time more. Every time you are trying to find if the wordDict are in string or not. Using DP, we can minimise the computation time by memorization and segmentation.

![image](https://github.com/user-attachments/assets/4c02c33e-6c9e-4f3d-a46f-f745659f4bb0)

In the above, the 'dog' in the string is matched with the wordDict but to return true in '9' we need to the check if the '6' is true or not to continous segmentation in the string.
```
class Solution(object):
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: List[str]
        :rtype: bool
        """
	res = [False] * (len(s) +1) #Creating a dummy list with all false
	res[len(s)] = True #Assigning the last string element as true
	for i in range(len(s) -1, -1, -1):
		for j in wordDict:
			if i + len(j) <= len(s) AND s[i: len(j) + i] == j:
# Checking from last if the string as any wordDict words. If yes then it would take the result element in res after the len(wordDic] which is assigned true at last for continuation of not breaking the segmentation of the string. (Bottom- up approach)
				res[i] = res[i + len(j)]
			if res[i]:
				break
	return res[0]
```
### Question 7:

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given an integer array nums representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.

Example 1:

Input: nums = [1,2,3,1]

Output: 4

Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3)

Total amount you can rob = 1 + 3 = 4.

![image](https://github.com/user-attachments/assets/04221965-5b74-4c0d-804b-98bea5793aef)

In the above example, Lets assume two numbers rob1, rob2 which are assigned to '0'. We go number by number in the list to assign rob1 and rob2 the numbers where we compare the maximum of the sum.

In the above, rob1 is '1' and  rob2 is '2'. The number max would be max(rob1 + 3, rob2). Then we go to next values till the end.
```
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
	rob1, rob2 = 0, 0

	for n in nums:
		tem = max(n+rob1, rob2)
		rob1 = rob2
		rob2 = tem
	return rob2
```

- What if the houses are in a circle?
#### Example 1:

Input: nums = [2,3,2]

Output: 3

Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2), because they are adjacent houses.

```go
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        return max( self.helper(nums[1:]), self.helper(nums[:-1]), nums[0])

	def helper(self, nums):
		rob1, rob2 = 0, 0
		for i in nums:
			nr = max(rob1 + i, rob2)
			rob1 = rob2
			rob2 = nr
		return rob2
```
