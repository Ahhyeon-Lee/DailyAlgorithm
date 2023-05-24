### Description

Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

**Example 1:**

```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation:
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.

```

**Example 2:**

```
Input: nums = [0,1,1]
Output: []
Explanation: The only possible triplet does not sum up to 0.

```

**Example 3:**

```
Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only possible triplet sums up to 0.

```

**Constraints:**

- `3 <= nums.length <= 3000`
- `105 <= nums[i] <= 105`

### Solution

- 이 문제는 Input Array Is Sorted 문제 처럼 정렬된 숫자 배열에서의 Two Sum과 같다.
- 다만 한가지 추가된 조건은, 주어진 배열을 돌면서 첫번째 숫자를 정하고 나머지 구해야 하는 두 숫자를 Input Array Is Sorted 문제처럼 풀어야 한다는 점이다.
- 그리고 한가지 주의할 점은 반환하는 List 안의 List들은 중복되지 않아야 한다는 점이다. nums 안에 중복 숫자들이 들어갈 수 있으므로 인덱스는 다르나 같은 값을 가진 숫자들로 중복된 리스트를 구하게 될 수도 있다.
    - 예를 들어 nums = [-2,0,0,2,2] 일때 0이 되는 리스트는 [-2, 0, 2], [-2, 0, 2], [-2, 0, 2], [-2, 0, 2] 네 개가 나올 수 있다. 하지만 이럴 경우 리스트가 중복되면 안되므로 [[-2,0,2]]를 반환해야 한다.
- 따라서 이를 피하기 위해 첫번째 숫자를 구하는 반복문을 돌 때에도(i 구할 때) 한 번 체크해야하고, 더한 세 수의 합이 0이 되어 다음 l과 r 값을 구할 때에도 체크해야 한다.(while 문을 돌면서)

```kotlin
class Solution {
    fun threeSum(nums: IntArray): List<List<Int>> {
        if (nums.size == 3) {
            return if (nums.sum() == 0) listOf(nums.toList())
            else listOf<List<Int>>()
        } else {
            nums.sort()
            var answer = mutableListOf<List<Int>>()
            for (i in (0 until nums.size -2)) {
                if (i > 0 && nums[i] == nums[i-1]) continue
                var l = i + 1
                var r = nums.size - 1
                while (l < r) {
                    if (nums[i] + nums[l] + nums[r] > 0) r--
                    else if (nums[i] + nums[l] + nums[r] < 0) l++
                    else if (nums[i] + nums[l] + nums[r] == 0) {
                        println("$i / $l / $r")
                        answer.add(listOf(nums[i], nums[l], nums[r]))
                        r--
                        l++
                        while (l < r && nums[r] == nums[r + 1]) r--
                        while (l < r && nums[l] == nums[l - 1]) l++
                    }
                }
            }
            return answer
        }
    }
}
```
