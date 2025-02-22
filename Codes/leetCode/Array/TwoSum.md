# Two Sum
## Description
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.

Example 1:
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

Example 2:
Input: nums = [3,2,4], target = 6
Output: [1,2]

Example 3:
Input: nums = [3,3], target = 6
Output: [0,1]
 
Constraints:
2 <= nums.length <= 104
-109 <= nums[i] <= 109
-109 <= target <= 109
Only one valid answer exists.
 
Follow-up: Can you come up with an algorithm that is less than O(n2) time complexity?

## Solution
```
class Solution {
    fun twoSum2(nums: IntArray, target: Int): IntArray {
        val map = hashMapOf<Int, Int>()
        nums.forEachIndexed { index, cur ->
            val num = map[target-cur]
            if (num != null) {
                return intArrayOf(index, num)
            } else {
                map.put(cur, index)
            }
        }
        return intArrayOf()
    }

    fun twoSum1(nums: IntArray, target: Int): IntArray {
        nums.forEachIndexed { index, num ->
            var next = index+1
            while (next < nums.size) {
                if (num + nums[next] == target) {
                    return intArrayOf(index, next)
                }
                next++
            }
        }
        return intArrayOf()
    }
}
```
- twoSum1 : 시간복잡도 O(n^2), 공간복잡도 O(1)
  - target을 만드는 두 수를 찾기 위해 이중 반복문을 돌린 방법이다.
  - 공간은 살 수 있지만 시간은 살 수 없으므로 알고리즘에서는 시간 복잡도를 줄이는 것이 관건이다. 따라서 두번째 방법으로 넘어간다.
- twoSum2 : 시간복잡도 O(n), 공간복잡도 O(n)
  - Map을 이용해 target - cur 한 원소를 찾는 방법이다. 배열을 돌면서 맵에 target - cur 가 있는지 확인하고, 없으면 cur과 index를 배열에 저장한다.
  - 이 방법으로 배열을 한 번만 돌면서 맵에 배열의 원소들을 넣어 target - cur에 해당하는 값이 있으면 키로 한 번에 찾을 수 있으므로 시간복잡도 O(n), 공간복잡도 O(n)의 솔루션을 도출할 수 있다.
