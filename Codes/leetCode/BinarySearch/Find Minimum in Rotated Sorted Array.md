### Description

Suppose an array of length `n` sorted in ascending order is **rotated** between `1` and `n` times. For example, the array `nums = [0,1,2,4,5,6,7]` might become:

- `[4,5,6,7,0,1,2]` if it was rotated `4` times.
- `[0,1,2,4,5,6,7]` if it was rotated `7` times.

Notice that **rotating** an array `[a[0], a[1], a[2], ..., a[n-1]]` 1 time results in the array `[a[n-1], a[0], a[1], a[2], ..., a[n-2]]`.

Given the sorted rotated array `nums` of **unique** elements, return *the minimum element of this array*.

You must write an algorithm that runs in `O(log n) time.`

**Example 1:**

```
Input: nums = [3,4,5,1,2]
Output: 1
Explanation: The original array was [1,2,3,4,5] rotated 3 times.

```

**Example 2:**

```
Input: nums = [4,5,6,7,0,1,2]
Output: 0
Explanation: The original array was [0,1,2,4,5,6,7] and it was rotated 4 times.

```

**Example 3:**

```
Input: nums = [11,13,15,17]
Output: 11
Explanation: The original array was [11,13,15,17] and it was rotated 4 times.

```

**Constraints:**

- `n == nums.length`
- `1 <= n <= 5000`
- `5000 <= nums[i] <= 5000`
- All the integers of `nums` are **unique**.
- `nums` is sorted and rotated between `1` and `n` times.

Accepted

**1.4M**

Submissions

**2.8M**

Acceptance Rate

### Solution

- In this problem, the fact is that if the left index is smaller than the right index, the nums is sorted and the smallest num is index 0 in nums.

- The first solution could have O(n) time complexity in worst case.
- Because it compares all the elements until meeting the smallest numbers except in case that the smallest number is at index 0.

```kotlin
class Solution {
    fun findMin(nums: IntArray): Int {
        if (nums.size == 1) return nums[0]
        var l = 0
        var r = nums.lastIndex
        var min = 0
        if (nums[l] < nums[r]) {
            min = nums[l]
        } else {
            min = nums[r]
            while (nums[r-1] < nums[r]) {
                min = nums[r-1]
                r--
            }
        }
        return min
    }
}
```

- Second solution is using binary search.
- In sorted array 0 index is the smallest number.
- In rotated array if the m(middle) index is bigger than l (left) index, the left portion is sorted and is bigger than right portion. So we should move l index to m + 1 to find in smaller portion.
- In contrast if the the l index is bigger than m index, the smallest number is in the left portion. So we should move the r(right) index to m - 1.
- Above rules are the point of this solution using binary search and we’ll save the smallest number in `res` and keep comparing it with smaller one.

```kotlin
class Solution {
    fun findMin(nums: IntArray): Int {
        var l = 0
        var r = nums.lastIndex
        var m = (l + r) / 2
        var res = nums[m]
        
        while (l <= r) {
            if (nums[l] <= nums[r]){ 
                res = Math.min(res, nums[l])
                break
            }
            
            if (nums[l] <= nums[m]) {
               l = m + 1
            } else {
               r = m - 1
            }
            m = (l + r) / 2
            res = Math.min(res, nums[m])
        }
        
        return res
    }
}
```
