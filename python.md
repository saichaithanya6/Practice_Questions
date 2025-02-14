## Question1:
Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer 
range [-231, 231 - 1], then return 0.

```go
  class Solution(object):
      def reverse(self, x):
          """
          :type x: int
          :rtype: int
          """
          output = 0
          neg =0
          if x < 0:
              x = x * (-1)
              neg = 1
          while x > 0:
              output = (output * 10) + (x % 10)
              x = x/10
          if neg == 1:
              output = output * -1
          if output < -2**31 or output > 2**31 - 1:
              return 0
          return output
```

- Note: reversed_x = str(x)[::-1]
	- str(x) → Converts x into a string.
	- [::-1] → Uses Python slicing to reverse the string.

- The slicing format is [start:stop:step], and [::-1] means:
	- start: (default) → Start from the end.
	- stop: (default) → Go until the beginning.
	- step = -1 → Move backwards, effectively reversing the string.


## Question2:
Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M. 

- Symbol   : Value
- I         :    1
- V          :   5
- X           :  10
- L          :   50
- C        :     100
- D        :     500
- M        :     1000

For example, 2 is written as II in Roman numeral, just two ones added together. 12 is written as XII, which is simply X + II. The number 27 is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before
the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:
- I can be placed before V (5) and X (10) to make 4 and 9. 
- X can be placed before L (50) and C (100) to make 40 and 90. 
-	C can be placed before D (500) and M (1000) to make 400 and 900.

``` go
class Solution(object):
    def romanToInt(self, s):
        """
        :type s: str
        :rtype: int
        """
        output = 0
        translation = {
            "I": 1,
            "V": 5,
            "X": 10,
            "L": 50,
            "C": 100,
            "D": 500,
            "M": 1000
        }

        s= s.replace("IV", "IIII").replace("IX", "VIIII").replace("XL", "XXXX")
        s = s.replace("XC", "LXXXX").replace("CD", "CCCC").replace("CM", "DCCCC")

        for i in s:
            output += translation[i]
        return output
```

## Question3:
Seven different symbols represent Roman numerals with the following values:

	Symbol	Value
	I	1
	V	5
	X	10
	L	50
	C	100
	D	500
	M	1000
Roman numerals are formed by appending the conversions of decimal place values from highest to lowest. Converting a decimal place value into a Roman numeral has the following rules:
- If the value starts with 4 or 9 use the subtractive form representing one symbol subtracted from the following symbol, for example, 4 is 1 (I) less than 5 (V): IV and 9 is 1 (I) less than 10 (X): IX. Only the following subtractive forms are used: 4 (IV), 9 (IX), 40 (XL), 90 (XC), 400 (CD) and 900 (CM).

```go
	class Solution(object):
    def intToRoman(self, num):
        """
        :type num: int
        :rtype: str
        """
        output = ""
        conversion = [[1000: "M"], [900, "CM"], [500, "D"], [400, "CD"], [100, "C"], [90, "XC"], [50. "L"], [40, "XL"], [10, "X"], [9, "IX"], [5, "V"], [4, "IV"], [1, "I"]]
        for i in range(len(conversion)):
            while num >= conversion[i][0]:
                output += conversion[i][1]
                num -= conversion[i][0]
        return output
```


## Question 4:
Example 1:

- Input: s = "babad"
- Output: "bab"
- Explanation: "aba" is also a valid answer.

```go
class Solution(object):
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        if len(s) <= 1:
            return s
        output = s[0]
        maxlen = 1
        for i in range(len(s)-1):
            for j in range(i+1, len(s)):
                if j-i+1 > maxlen and s[i:j+1] == s[i:j+1][::-1]:
                    output= s[i:j+1]
                    maxlen = j - i + 1
        return output
```

## Question 5:
Convert a string to a 32-bit signed integer.
- Determine the sign by checking if the next character is '-' or '+'
- Ignore any leading whitespace (" ")
- Read the integer by skipping leading zeros until a non-digit character is encountered. Range is [-231, 231 - 1]

Example 1: Input: s = "42". Output: 42.

Example 2: Input: s = " -042" Output: -42.

Example 3: Input: s = "words and 987" Output: 0.

```go
class Solution(object):
    def myAtoi(self, s):
        """
        :type s: str
        :rtype: int
        """
#Removes spaces in the string
        s = s.strip() 
        if not s:
            return 0
        i = 0
        sign = 1
        result = 0
        if s[i] == '-' or s[i] == '+':
#Checks if the first character is + or -
            sign = -1 if s[i] == '-' else 1
            i+= 1
        while i < len(s) and s[i].isdigit():
            digit = int(s[i])
            if (result > (2 ** 31 - 1 - digit) // 10):
#If the result is greater than 2** 31 then return the same
                return 2 ** 31 - 1 if sign == 1 else -2**31
            result = result * 10 + digit
            i += 1
        return sign * result
```

## Question 6:
Write a function to find the longest common prefix string amongst an array of strings. 
Example 1: Input: strs = ["flower","flow","flight"] Output: "fl"

```go
class Solution(object):
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        # First decide a base string from the list
        p = strs[0]

        for i in strs[1:]:
            while not i.startswith(p):
                p = p[:-1]
        return p
```

## Question 7:
Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.
Example 1- Input: nums = [-1,0,1,2,-1,-4] Output: [[-1,-1,2],[-1,0,1]] Explanation: nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
```go
class Solution(object):
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        ans = []
        nums.sort()
        n = len(nums)
        for i in range(n):
            if i > 0 and nums[i-1] == nums[i]:
                continue
            j = i+1
            k = n-1
            while j < k:
                temp = nums[i]+ nums[j]+ nums[k]
                if temp == 0:
                    ans.append([nums[i], nums[j], nums[k]])
                    j += 1
                    while nums[j-1] == nums[j] and j<k:
                        j+= 1
                elif temp > 0:
                    k -= 1
                else:
                    j += 1
        return ans
```

## Question 8: Container With Most Water
You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

```go
class Solution(object):
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        area = 0
        n = len(height)
        i = 0
        j = n -1

        while j > i:
            area = max(area, abs(j - i)*(min(height[i], height[j])))
            if height[i] > height[j]:
                j -= 1
            else:
                i += 1
        return area
```
## Question 9: 
![image](https://github.com/user-attachments/assets/206f4b73-a0b8-44d3-b161-e287e13a245b)
```go
def valid_emails(users: pd.DataFrame) -> pd.DataFrame:
    valid_emails_df = users[users['mail'].str.match(r'^[a-zA-Z][a-zA-Z0-9_.-]*@leetcode\.com$', na= False)]
    
    return valid_emails_df
```
We created a dataframe that has matching strings starting with letters, nums, few special characters. * before @leetcode[.]com allows multiple valid characters before the @.
We can use [.] or \. for retriving exactly the dot. $ states that the @leetcode.com should be the ending string.

## Question 10
Write a solution to find the ids of products that are both low fat and recyclable.
Return the result table in any order.
![image](https://github.com/user-attachments/assets/0fd347e0-a2c0-48b6-a5e4-4d30819c13aa)
```go
def find_products(products: pd.DataFrame) -> pd.DataFrame:
    return products[(products['low_fats']== 'Y') & (products['recyclable']== 'Y')][['product_id']]
```

## Question 11:
Write a solution to report the first name, last name, city, and state of each person in the Person table. If the address of a personId is not present in the Address table, report null instead.

![image](https://github.com/user-attachments/assets/836caea5-f8b6-4722-95af-1688bda4046c)
```go
def combine_two_tables(person: pd.DataFrame, address: pd.DataFrame) -> pd.DataFrame:
    return pd.merge(left= person, right= address, how= 'left', on= 'personId')[['firstName', 'lastName', 'city', 'state']]
```
Used merge operation for joining the tables. In the parameters, mentioned 'left' join and on which column.

What if we have the column names different for the 2 tables?- then mention "left_on" and "right_on" parameters instead of only "on="

## Question 12:
Write a solution to find the second highest distinct salary from the Employee table. If there is no second highest salary, return "null"

![image](https://github.com/user-attachments/assets/9c256a9e-c1e3-40cd-be4d-693fe89aa90a)
```go
def second_highest_salary(employee: pd.DataFrame) -> pd.DataFrame:
    sal = employee['salary'].drop_duplicates().sort_values(ascending= False)

    if len(sal) < 2:
        return pd.DataFrame({'SecondHighestSalary': [None]})

    second = sal.iloc[1]

    return pd.DataFrame({'SecondHighestSalary': [second]})
```
Initially we are dropping duplicates, sort values on descending order. The expression 'iloc[1]' returns the second data point in the table.

## Question 13:
Write a solution to find the nth highest salary from the Employee table. If there is no nth highest salary, return null.

![image](https://github.com/user-attachments/assets/115a9ccc-ca24-4bab-9d19-c880a78afb9f)
```go
def nth_highest_salary(employee: pd.DataFrame, N: int) -> pd.DataFrame:
    employee = employee['salary'].drop_duplicates().sort_values(ascending=False)
    if N > len(employee) or N<= 0:
        return pd.DataFrame({'getNthHighestSalary({})'.format(N): [None]})
    
    return pd.DataFrame({'getNthHighestSalary({})'.format(N): [employee.iloc[N-1]]})
```
To find the nth highest salary, first we need to remove dupllicates, sort it. After sorting we need to return 'N-1' term from the data frame.

## Question 14:

![image](https://github.com/user-attachments/assets/ef1b654d-cad8-4516-a6c3-200468d7e3ef)

```go
def order_scores(scores: pd.DataFrame) -> pd.DataFrame:
	scores["rank"]= scores.score.rank(method = 'rank', ascending = False)
	return scores.sort_values("rank").iloc[:, [1,2]]
```
rank() is a function where it provides ranking based on the quantity or char in the column. iloc[:, [1,2]] This returns the every row in the 1, 2 columns.

## Question 15:
Write a solution to find the employees who earn more than their managers.

![image](https://github.com/user-attachments/assets/8fe72e90-b41a-4d92-95cd-a112a60c1391)
```go
def find_employees(employee: pd.DataFrame) -> pd.DataFrame:
	df = pd.merge(left = 'employees', right = 'employees', left_on = 'manager_Id', right_on = 'id', how = 'left')
 	return pd.DataFrame({"Employee": df[df['salary_x'] > df['salary_y']]['name_x']})
```
## Question 16:
Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let 
these two numbers be numbers[index1] and numbers[index2] where 1 <= index1 < index2 <= numbers.length.
Return the indices of the two numbers, index1 and index2

Example 1:

Input: numbers = [2,7,11,15], target = 9

Output: [1,2]

Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].

```go
class Solution(object):
	def twoSum(self, numbers, target):
		i = 0
		j = len(numbers) - 1

		while numbers[i] + numbers[j] != target:
			if numbers[i] + numbers[j] > target:
				j -=1
			else:
				i += 1
		return [i+1, j+1]
```
## Question 17:
Given an integer array nums of length n and an integer target, find three integers in nums such that the sum is closest to target.

Return the sum of the three integers.

Example 1:

Input: nums = [-1,2,1,-4], target = 1, 
Output: 2

Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

```go
class Solution(object):
    def threeSumClosest(self, nums, target):
	nums = nums.sort() # Sorting the nums array
	diff= float('inf') #Assinging the float value to diff
	for i in range(len(nums)- 2):
		start = i+1 
		end = len(nums) -1
		while start < end:
			sum1 = nums[start] + nums[end] + nums[i] 
			if abs(target - diff) > abs(sum1 - target): #If the 'sum1' difference with 'target' is less than 'diff' difference with 'target' then replace diff with sum1
				diff = sum1
			elif sum1 > target: #Since the array is sorted, if the sum1 is greater than target then select the number 
				end -= 1
			elif sum1 < target:
				start += 1
			else:
				return sum1
	return diff
