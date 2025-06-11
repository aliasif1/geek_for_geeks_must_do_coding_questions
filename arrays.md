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

##### 6. Rearrange arrays alternately
```
SKIPPED: As a mathematical formula needs to be known in order to solve this optimally
```

##### 7. Number of pairs
```
import bisect
class Solution:    
    def countPairs(self,arr,brr):
        brr.sort()
        freq = [0] * 5
        for val in brr:
            if val < 5: freq[val] +=1
        count = 0
        for x in arr:
            if x == 1: continue
            count+=(len(brr) - bisect.bisect_right(brr, x))
            count +=freq[1]
            if x == 2:
                count -=(freq[3] + freq[4])
            if x == 3:
                count +=freq[2]
        return count
```

##### 8. Inversion of array
```
# 8. Inversion of Array
class Solution:
    def inversionCount(self, arr):
        (sortedArr, inversions) = self.divide(arr)
        return inversions
    
    def divide(self, arr):
        n = len(arr)
        if n == 1:
            return (arr, 0)
        (leftSortedArr, leftInversions) = self.divide(arr[:n//2])
        (rightSortedArr, rightInversions) = self.divide(arr[n//2:])
        (sortedArr, mergeInversions) =  self.merge(leftSortedArr, rightSortedArr)
        return (sortedArr, leftInversions + rightInversions + mergeInversions)
    
    def merge(self, arr1, arr2):
        n,m = len(arr1), len(arr2)
        arr = []
        i,j = 0, 0
        inversions = 0
        while i < n and j < m:
            if arr1[i] <= arr2[j]:
                arr.append(arr1[i])
                i+=1
            else:
                inversions += (n - i)
                arr.append(arr2[j])
                j+=1
        while i < n:
            arr.append(arr1[i])
            i+=1
        while j < m:
            arr.append(arr2[j])
            j+=1
        return (arr, inversions)
```

##### 9. Sort an array of 0s, 1s and 2s
```
class Solution:
    def sort012(self, arr):
        n = len(arr)
        left = 0
        right = n-1
        i = 0
        while i <= right:
            if arr[i] == 1:
                i+=1
                continue
            if arr[i] == 0:
                arr[i], arr[left] = arr[left], arr[i]
                left+=1
                i+=1
                continue
            if arr[i] == 2:
                arr[i], arr[right] = arr[right], arr[i]
                right -=1
```

##### 10. Equilibrium point
```
class Solution:
    def findEquilibrium(self, arr):
        s = sum(arr)
        s_before = 0
        for i in range(len(arr)):
            s -=arr[i]
            if s == s_before: return i
            s_before +=arr[i]
        return -1
```

##### 11. Leaders in an array
```
class Solution:
    def leaders(self, arr):
        n = len(arr)
        if n == 0: return 0
        res = []
        maxRight = float('-inf')
        for i in range(n-1 , -1, -1):
            if arr[i] >= maxRight: res.append(arr[i])
            maxRight = max(maxRight, arr[i])
        res.reverse()
        return res
```

##### 12. Minimum platforms 

```
class Solution:    
    def minimumPlatform(self,arr,dep):
        n = len(arr)
        if n == 0: return 0
        arr.sort()
        dep.sort()
        minPlatforms = 0
        currentPlatforms = 0
        i = 0
        j = 0
        while i < n:
            if arr[i] <= dep[j]:
                currentPlatforms +=1
                minPlatforms = max(minPlatforms, currentPlatforms)
                i+=1
            else:
                currentPlatforms -=1
                j+=1
        return minPlatforms
```

##### 13. Reverse array in group
```
class Solution:
    def reverseInGroups(self, arr, k):
        def reverse(arr,start,end):
            i = start
            j = end
            while i < j:
                arr[i], arr[j] = arr[j], arr[i]
                i+=1
                j-=1
        i = 0
        while i <= len(arr)-1:
            start = i
            end = min((start + k - 1), (len(arr) - 1))
            reverse(arr, start, end)
            i = end + 1
        return arr
```

##### 14. Kth smallest element
```
import heapq
class Solution:
    def kthSmallest(self, arr, k):
        heapq.heapify(arr)
        for i in range(k - 1):
            heapq.heappop(arr)
        return heapq.heappop(arr)
```

##### 15. Trapping Rain water
```
class Solution:
    def maxWater(self, arr):
        leftMax = 0
        rightMax = 0
        i = 0
        j = len(arr) - 1
        water = 0
        while i <= j:
            if leftMax <= rightMax:
                water+=max(0, leftMax - arr[i])
                leftMax = max(leftMax, arr[i])
                i+=1
            else:
                water+=max(0, rightMax - arr[j])
                rightMax = max(rightMax, arr[j])
                j-=1
        return water
```

##### 16. pythagorean triplets
```
class Solution:
    def pythagoreanTriplet(self, arr):
        n = len(arr)
        if n < 3: return True
        arr = [x ** 2 for x in arr]
        arr.sort(reverse=True)
        for i in range(n - 2):
            j = i+1
            k = n-1
            while j < k:
                if arr[i] == arr[j] + arr[k]: return True
                elif arr[i] < arr[j] + arr[k]: j+=1
                else: k-=1
        return False
```

###### 17. Chocolate distributin problem
```
class Solution:
    def findMinDiff(self, arr, M):
        n = len(arr)
        arr.sort()
        minDiff = float('inf')
        for i in range(n - M + 1):
            diff = arr[i + M - 1] - arr[i]
            minDiff = min(minDiff, diff)
        return minDiff
```

##### 18. Stock buy and sell
```
class Solution:
    def stockBuySell(self, arr):
        n = len(arr)
        if n <= 1: return 0
        profit = 0
        buyDate = 0
        while True:
            while buyDate <= n-2 and arr[buyDate+1] <= arr[buyDate]:
                buyDate+=1
            sellDate = buyDate + 1
            if sellDate == n : return profit
            while sellDate <= n-2 and arr[sellDate + 1] >= arr[sellDate]:
                sellDate+=1
            profit+=(arr[sellDate] - arr[buyDate])
            buyDate = sellDate + 1
            if buyDate >= n-1: return profit
```

##### 19. Element with left side smaller or equal and right side greater or equal
```
class Solution:
    def findElement(self, arr):
        n = len(arr)
        leftMaxArr = [0] * n
        rightMinArr = [0] * n
        leftMaxArr[0] = float("-inf")
        rightMinArr[-1] = float("inf")
        for i in range(1, n):
            leftMaxArr[i] = max(leftMaxArr[i-1], arr[i-1])
        for i in range(n-2, -1, -1):
            rightMinArr[i] = min(rightMinArr[i+1], arr[i+1])
        for i in range(1,n-1):
            if leftMaxArr[i] <= arr[i] <= rightMinArr[i]: return arr[i]
        return -1
            
```

##### 20. Convert array to zig zag fashion
```
from typing import List
class Solution:
    def zigZag(self,arr : List[int]) -> None:
        for i in range(len(arr) - 1):
            if i % 2 == 0:
                if arr[i+1] < arr[i]: arr[i], arr[i+1] = arr[i+1], arr[i]
            else:
                if arr[i+1] > arr[i]: arr[i], arr[i+1] = arr[i+1], arr[i]
        return arr
```