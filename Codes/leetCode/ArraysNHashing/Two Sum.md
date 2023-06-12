### Description

Given an array of integers `nums` and an integer `target`, return *indices of the two numbers such that they add up to `target`*.

You may assume that each input would have ***exactly* one solution**, and you may not use the *same* element twice.

You can return the answer in any order.

**Example 1:**

```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

```

**Example 2:**

```
Input: nums = [3,2,4], target = 6
Output: [1,2]

```

**Example 3:**

```
Input: nums = [3,3], target = 6
Output: [0,1]

```

**Constraints:**

- `2 <= nums.length <= 104`
- `109 <= nums[i] <= 109`
- `109 <= target <= 109`
- **Only one valid answer exists.**

**Follow-up:** Can you come up with an algorithm that is less than `O(n2)` time complexity?

### Solution

- 첫번째 풀이는 nums의 모든 요소에 대해 타겟을 구할 수 있는 끝 인덱스를 찾을 때까지 순회하는 방법이다.
- nums = [2, 7, 11, 15], target = 9
    - 2 → 7, 11, 15
    - 7 → 11, 15
    - 이런식으로 각 요소를 시작점으로 타겟을 구할 끝 인덱스를 찾을 때까지 리스트를 두 번 순회하므로 시간 복잡도는 O(n2)가 된다.

```kotlin
// 첫번째 풀이
class Solution {
    fun twoSum(nums: IntArray, target: Int): IntArray {
        var isContinue = true
        var firstIndex = 0
        var sndIndex = 1
        while (isContinue) {
            if (nums[firstIndex] + nums[sndIndex] == target){
                isContinue = false
            } else {
                sndIndex++
            }

            if (sndIndex == nums.size) {
                firstIndex++
                sndIndex = firstIndex+1
            }
        }
        return intArrayOf(firstIndex, sndIndex)
    }
}
```

- 두번째 풀이는 target = num + (target - num) 이라는 점을 활용한 방법이다.
- 각 요소는 한 번만 사용할 수 있으므로 target에서 뺀 num의 인덱스를 제외한 나머지 요소에서 합의 수를 구하려면, 1. num과 인덱스를 가지고 있는 HashMap을 만들어 2. nums를 순회할 때 이전 인덱스까지의 num만 HashMap에 넣고 3. target-num이 HashMap에 있는지 확인해 있으면 그 num의 인덱스를 현재 num의 인덱스와 함께 반환하고, 없으면 현재 num과 인덱스를 HashMap에 저장해 다음 요소를 돌때 num을 찾을 수 있도록 하는 것이다.
- 이렇게 하면 nums를 한 번만 순회하면서 target - num의 인덱스를 찾으면 되므로 시간 복잡도는 O(n)이 되며, num과 인덱스를 저장하는 HashMap을 사용하므로 공간 복잡도도 O(n)이 된다.

```kotlin
// 두번째 풀이
class Solution {
    fun twoSum(nums: IntArray, target: Int): IntArray {
        val map = HashMap<Int, Int>()
        nums.forEachIndexed { index, value ->
            val gap = target - value
            if (map.get(gap) != null) {
                return intArrayOf(index, map[gap]!!)
            } else {
                map[value] = index
            }
        }
        return intArrayOf()
    }
}
```
