### Description

Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4

```

**Example 2:**

```
Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1

```

**Constraints:**

- `1 <= nums.length <= 104`
- `104 < nums[i], target < 104`
- All the integers in `nums` are **unique**.
- `nums` is sorted in ascending order.

### Solution

- 시간복잡도 O(log n)으로 풀려면 이진 탐색으로 찾아야 한다. 코틀린에는 binarySearch 함수가 있으므로 간단히 풀어보았다.

```kotlin
class Solution {
    fun search(nums: IntArray, target: Int): Int {
        return nums.binarySearch(target, 0, nums.size)?.takeIf { it >= 0 } ?: -1
    }
}
```

![image](https://github.com/Ahhyeon-Lee/DailyAlgorithm/assets/68845653/a032581f-5c6a-44d6-8341-bd5a67a83dc9)

- 하지만 직접 BinarySearch를 구현하는 것이 더 의미있기에 다시 풀어본다.
- 이진 탐색도 Two Pointers 관점에서 접근하면 더 방법을 도출해내기 쉽다.
- 왼쪽 끝과 오른쪽 끝 포인터를 두고, 가운데 인덱스의 값과 target을 비교하면서 가운데 값이 target 보다 크면 오른쪽 포인터를 옮기고, 가운데 값이 target 보다 작으면 왼쪽 포인터를 옮긴다.

```kotlin
class Solution {
    fun search(nums: IntArray, target: Int): Int {
        var l = 0
        var r = nums.lastIndex
        var m = (l + r) / 2
        while (l <= r) {
            when {
                target < nums[m] -> r = m - 1
                nums[m] < target -> l = m + 1
                else -> return m
            }
            m = (l + r) / 2
        }
        return -1
    }
}
```

![image](https://github.com/Ahhyeon-Lee/DailyAlgorithm/assets/68845653/ad41f615-9303-49bb-a35e-6adad47627cb)

- 이진 탐색이 왜 O(log n)의 시간복잡도를 가지는지 알아보자.
- $log(n)$은 $log_2(n)$과 같은 말로 2를 X 제곱 했을때 n(이 문제에서는 nums.size)을 구하는 방법이다.
- 예를 들어 nums에 16개의 원소가 있었다고 하면, 이진 탐색 기법을 쓰면 매번 양 끝의 가운데 값을 찾아 target과 비교후 절반씩 줄어들므로 16 → 8 → 4 → 2 → 1 이렇게 마지막 target 값 한 개가 남을때 까지 절반씩 줄여 4번만 찾으면 된다.
- 따라서 이진탐색으로  $log_2(n) = 16$ → n = 4 회만 검사하면 되는 풀이가 된다.
