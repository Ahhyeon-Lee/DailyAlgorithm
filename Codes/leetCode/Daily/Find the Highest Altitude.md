### Description

There is a biker going on a road trip. The road trip consists of `n + 1` points at different altitudes. The biker starts his trip on point `0` with altitude equal `0`.

You are given an integer array `gain` of length `n` where `gain[i]` is the **net gain in altitude** between points `i` and `i + 1` for all (`0 <= i < n)`. Return *the **highest altitude** of a point.*

**Example 1:**

```
Input: gain = [-5,1,5,0,-7]
Output: 1
Explanation: The altitudes are [0,-5,-4,1,1,-6]. The highest is 1.

```

**Example 2:**

```
Input: gain = [-4,-3,-2,-1,4,3,2]
Output: 0
Explanation: The altitudes are [0,-4,-7,-9,-10,-6,-3,-1]. The highest is 0.

```

**Constraints:**

- `n == gain.length`
- `1 <= n <= 100`
- `100 <= gain[i] <= 100`

### Solution

- 고도 0 에서부터 시작해 gain이 이전 봉우리부터 현재 봉우리까지의 격차이다.
- 따라서 가장 높은 봉우리를 구하려면 gain을 돌면서 현재 봉우리의 고도를 구하고, 이를 구하면서 최대값을 비교하면 된다.

```kotlin
class Solution {
    fun largestAltitude(gain: IntArray): Int {
        var highest = 0
        var current = 0
        gain.forEach {
            current += it
            highest = Math.max(highest, current)
        }
        return highest
    }
}
```
