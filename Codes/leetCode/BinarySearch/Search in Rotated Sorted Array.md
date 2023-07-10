### Description

There is an integer array `nums` sorted in ascending order (with **distinct** values).

Prior to being passed to your function, `nums` is **possibly rotated** at an unknown pivot index `k` (`1 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (**0-indexed**). For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index `3` and become `[4,5,6,7,0,1,2]`.

Given the array `nums` **after** the possible rotation and an integer `target`, return *the index of* `target` *if it is in* `nums`*, or* `-1` *if it is not in* `nums`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4

```

**Example 2:**

```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1

```

**Example 3:**

```
Input: nums = [1], target = 0
Output: -1

```

**Constraints:**

- `1 <= nums.length <= 5000`
- `104 <= nums[i] <= 104`
- All values of `nums` are **unique**.
- `nums` is an ascending array that is possibly rotated.
- `104 <= target <= 104`

### Solution

- To solove this problem in O(log n) time complexity, we should approach by binary search.
- But I think the more important thing is to check all the cases when to move left index or right index.
- At first we can divide in two cases. If left portion is sorted or right portion is sorted. Then if we should search in right portion or in left portion.
    - Left portion is sorted : [4, 5, 6, **7**, 8, 0, 1, 2]
        - Search in right portion (target = 0 || target = 8) : target < nums[l] || nums[m] < target
        - Search in left portion (target = 6) : Else cases except above.
    - Right portion is sorted : [5, 6, 0, **1**, 2, 3 ,4]
        - Search in right portion (target = 2) : nums[m] < target ≤ nums[r]
        - Search in left portion (target = 0) : Else cases except above.

```kotlin
class Solution {
    fun search(nums: IntArray, target: Int): Int {
        var l = 0
        var r = nums.lastIndex
        
        while (l <= r) {
            val m = (l + r) / 2
            if (target == nums[m]) return m
            
            if (nums[l] <= nums[m]) { // left sorted
                if (target < nums[l] || nums[m] < target) { // search right
                    l = m + 1
                } else { // search left
                    r = m - 1
                } 
            } else { // right sorted
                if (nums[m] < target && target <= nums[r]) { // search right
                    l = m + 1
                } else { // search left
                    r = m - 1
                }
            }
        }
        
        return -1
    }
}
```
