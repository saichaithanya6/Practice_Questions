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

## Question 5:
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

