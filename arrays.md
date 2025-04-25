# Arrays

#### 1. Subarray with a given sum
```
class Solution:
    def subarraySum(self, arr, target):
        if len(arr) == 0: return [-1]
        left = 0
        accumulatedSum = 0
        for i in range(len(arr)):
            accumulatedSum +=arr[i]
            while accumulatedSum > target and left < i:
                accumulatedSum -= arr[left]
                left+=1
            if accumulatedSum == target: return [left+1, i+1]
        return [-1]
```