![image](https://github.com/user-attachments/assets/bf4ddd59-9ef5-4e56-939a-60b1832763a5)

Greedy algorithms are a class of algorithms that make locally optimal choices at each stage with the hope of finding a global optimum

In the above question, we can see that for each index, the maximum number of steps are in the list. We come from the goal itself(From last) to the intital point. If the element(current index) can across the 'goal' then the new goal is set has the current index.
Since, maximum number of skips are present in the list. Just by crossing the goal can meet the requirement.

![image](https://github.com/user-attachments/assets/66dbab8c-9a09-4980-bcd9-a2be3d9539ca)

```
class Solution(object):
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        goal = len(nums) - 1
        for i in range( len(nums) -1, -1, -1):
          if nums[i] + i >= goal:
            goal = i

        return True if goal == 0 else False
```
