### Description

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `ith` line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return *the maximum amount of water a container can store*.

**Notice** that you may not slant the container.

**Example 1:**

![https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

```

**Example 2:**

```
Input: height = [1,1]
Output: 1

```

**Constraints:**

- `n == height.length`
- `2 <= n <= 105`
- `0 <= height[i] <= 104`

### Solution

- 이 문제는 [ 두 엔드 포인터의 인덱스 사이 * 두 엔드 포인터 중 짧은 포인터의 높이 ] 중 가장 큰 값을 구하는 것이다.
- 양 끝의 엔드 포인터를 좁혀오는 과정에서 주의해야할 점은 결국 두 포인터 중 높이가 짧은쪽이 곱하는 수가 되므로 짧은 쪽이 최대한 커야 한다는 점이다.
- 이를 유의하면서 포인터 간격을 좁히면, 두 포인터 중 짧은 쪽의 포인터를 옮겨야 한다는 것이다.
- 이렇게 해야 두 포인터 중 짧은 쪽을 계속 옮겨가면서 최대한 넓은 인덱스 거리에 최대한 높은 포인터의 높이를 곱해 max 값을 구할 수 있다.
- 이 풀이는 height 어레이를 한번만 순회 하므로 시간 복잡도 O(n)을 가지고, max, l, r 을 담을 변수만 가지면 되므로 공간 복잡도는 O(1)이 된다.

```kotlin
class Solution {
    fun maxArea(height: IntArray): Int {
        var max = 0
        var l = 0
        var r = height.size - 1
        while (l < r) {
            val size = (r - l) * Math.min(height[l], height[r])
            if (size > max) max = size
            if (height[l] > height[r]) r--
            else l++
        }
        return max
    }
}
```
