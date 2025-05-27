## Arrays

##### 1. Subarray with a given sum
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

##### 2. Count the triplets - The question description says count only unique solutions but the solution it accepts wants all solutions - including duplicates
```
class Solution:
    def countTriplet(self, arr):
        arr.sort(reverse=True)
        triplets = 0
        for i in range(len(arr) - 2):
            j = i + 1
            k = len(arr) - 1
            while j < k:
                if arr[i] == arr[j] + arr[k]:
                    triplets+=1
                    j+=1
                    k-=1
                elif arr[i] < arr[j] + arr[k]:
                    j+=1
                else:
                    k-=1
        return triplets
```

##### 2. Count the triplets - correct Solution - verified with leetcode 3Sum problem
```
class Solution:
    def countTriplet(self, arr):
        arr.sort(reverse=True)
        triplets = 0
        lastValue = None
        for i in range(len(arr) - 2):
            if arr[i] == lastValue: continue
            j, k = i + 1, len(arr) - 1
            while j < k:
                if arr[i] == arr[j] + arr[k]:
                    triplets +=1
                    j+=1
                    k-=1
                    while j < k and arr[j] == arr[j-1]: j+=1
                    while j < k and arr[k] == arr[k+1]: k-=1
                elif arr[i] < arr[j] + arr[k]:
                    j+=1
                else:
                    k-=1
                lastValue = arr[i]
        return triplets
```

##### 3. Kadane's Algorithm
```
class Solution:
    def maxSubArraySum(self, arr):
        n = len(arr)
        if n == 0: return 0
        currentsum = arr[0]
        maxSum = arr[0]
        for i in range(1, n):
            currentsum = max(currentsum + arr[i], arr[i])
            maxSum = max(maxSum, currentsum)
        return maxSum
```

##### 4. Missing number in array
```
# 4. Missing number in array
class Solution:
    def missingNum(self, arr):
        val = 0
        for i in range(len(arr)):
            val +=(i+1)
            val -=arr[i]
        val+=len(arr) + 1
        return val
```

##### 5. Merge 2 sorted arrays
```
class Solution:
    def mergeArrays(self, a, b):
        j = len(a) - 1
        k = 0
        while j >= 0 and k < len(b) and a[j] > b[k]:
            a[j], b[k] = b[k], a[j]
            j-=1
            k+=1
        a.sort()
        b.sort()
```
