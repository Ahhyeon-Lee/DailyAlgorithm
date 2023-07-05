### Description

You are given an `m x n` integer matrix `matrix` with the following two properties:

- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.

Given an integer `target`, return `true` *if* `target` *is in* `matrix` *or* `false` *otherwise*.

You must write a solution in `O(log(m * n))` time complexity.

**Example 1:**

![Untitled](https://assets.leetcode.com/uploads/2020/10/05/mat.jpg)

```
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true

```

**Example 2:**

![Untitled](https://assets.leetcode.com/uploads/2020/10/05/mat2.jpg)

```
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
Output: false

```

**Constraints:**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 100`
- `104 <= matrix[i][j], target <= 104`

### Solution

- `O(log(m * n))` 의 시간복잡도는 결국 matrix의 IntArray의 원소들수를 절반씩 줄여가는 방법으로 target을 찾는 방법을 쓰라는 말이다. 즉, 이진 탐색으로 풀어야 한다.
- 우선 matrix의 어떤 행의 범위에 target이 속하는지 찾고, 그 행 안에서 이진 탐색을 하며 찾으면 된다.

```kotlin
class Solution {
    fun searchMatrix(matrix: Array<IntArray>, target: Int): Boolean {
        val row = matrix.find {
            it.first() <= target && target <= it.last()
        }
        if (row == null) return false
        else {
            var l = 0
            var r = row.lastIndex
            var m = 0

            while (l <= r) {
                m = (l + r) / 2
                when {
                    target < row[m] -> r = m - 1
                    row[m] < target -> l = m + 1
                    else -> return true
                }
            }
            return false
        }
    }
}
```
