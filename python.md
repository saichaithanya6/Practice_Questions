Question1:
Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer 
range [-231, 231 - 1], then return 0.


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

Note: reversed_x = str(x)[::-1] 
str(x) → Converts x into a string.
[::-1] → Uses Python slicing to reverse the string.
The slicing format is [start:stop:step], and [::-1] means:
start: (default) → Start from the end.
stop: (default) → Go until the beginning.
step = -1 → Move backwards, effectively reversing the string.
