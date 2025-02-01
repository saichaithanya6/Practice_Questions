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
                num -= conversion[i][1]
        return output
```
