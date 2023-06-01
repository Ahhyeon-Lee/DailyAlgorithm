### Description

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

**Example 1:**

![https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png )

```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.

```

**Example 2:**

```
Input: height = [4,2,0,3,2,5]
Output: 9

```

**Constraints:**

- `n == height.length`
- `1 <= n <= 2 * 104`
- `0 <= height[i] <= 105`

### Solution

```kotlin
class Solution {
    fun trap(height: IntArray): Int {
        var volume = 0
        var l = 0
        var r = height.lastIndex
        var currentLeftMax = -1
        var currentRightMax = -1

        while (l < r) {
            if (height[l] <= height[r]) {
                currentLeftMax = max(currentLeftMax, height[l])
                l++
                volume += (currentLeftMax - height[l]).coerceAtLeast(0)
            } else {
                currentRightMax = max(currentRightMax, height[r])
                r--
                volume += (currentRightMax - height[r]).coerceAtLeast(0)
            }
        }
        return volume
    }
}
```
