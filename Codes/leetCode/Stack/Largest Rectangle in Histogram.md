### Description

Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return *the area of the largest rectangle in the histogram*.

**Example 1:**

![Untitled](https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg)

```
Input: heights = [2,1,5,6,2,3]
Output: 10
Explanation: The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.

```

**Example 2:**

![Untitled](https://assets.leetcode.com/uploads/2021/01/04/histogram-1.jpg)

```
Input: heights = [2,4]
Output: 4

```

**Constraints:**

- `1 <= heights.length <= 105`
- `0 <= heights[i] <= 104`

### Solution

```kotlin
import java.util.*

class Solution {
    fun largestRectangleArea(heights: IntArray): Int {
        val stack = Stack<Pair<Int, Int>>()
        stack.push(Pair(-1, 0))
        var max = 0

        for (i in heights.indices) {
            var start = i

            while (!stack.isEmpty() && stack.peek().second > heights[i]) {
                val curr = stack.pop()
                val height = curr.second
                start = curr.first
                max = Math.max(max, height * (i - start))
            }

            stack.push(Pair(start, heights[i]))
        }

        while (!stack.isEmpty()) {
            val curr = stack.pop()
            max = Math.max(max, curr.second * (heights.size - curr.first))
        }

        return max
    }
}
```
