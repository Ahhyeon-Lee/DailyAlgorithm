### Description

Given an unsorted array of integers `nums`, return *the length of the longest consecutive elements sequence.*

**You must write an algorithm that runs in `O(n)` time.**

**Example 1:**

```
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is[1, 2, 3, 4]. Therefore its length is 4.

```

**Example 2:**

```
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
```

### Solution

- 연이은 수 시퀀스들중 가장 긴 시퀀스의 길이를 반환하는 문제이다.
- 우선 연이은 수들의 시퀀스를 시각적으로 표현해보면 아래와 같다.

![consecutive](https://github.com/Ahhyeon-Lee/DailyAlgorithme/assets/68845653/a9ff2a78-86d4-4b2e-82aa-6c57c7969369)

- 예제 1을 시각화 해보면 3개의 시퀀스가 나온다.
- 시퀀스의 조건은 (시퀀스 시작점 - 1)이 nums에 없어야 한다는 것이다.
- 시작점을 찾으면 그 시작점으로 부터 +1을 해나간 수들이 각 시퀀스를 이룬다.
- 따라서
    1. nums 각 요소 -1이 nums에 있는지 판단해 시퀀스의 시작점을 찾고
    2. 시작점을 찾으면 해당 요소에 +1을 해가면서 이 수가 nums에 있으면 시퀀스를 이루게 되므로 시퀀스 길이에 +1을 한다.
    3. 이렇게 각 시퀀스의 길이를 리스트에 넣어서 이 리스트에서 최대수를 반환한다. 
- 이렇게 하면 nums를 한바퀴만 돌고, nums 길이만큼의 Set과 각 시퀀스 갯수만큼의 리스트만 생성하게 되므로, 시간복잡도 O(n), 공간복잡도 O(n)를 가지는 풀이가 된다.

```kotlin
class Solution {
    fun longestConsecutive(nums: IntArray): Int {
        val numSet = nums.toHashSet()
        val cntList = mutableListOf<Int>()
        numSet.forEach { num ->
            if (!numSet.contains(num-1)) {
                var consecutive = num + 1
                var cnt = 1
                while (numSet.contains(consecutive)) {
                    consecutive++
                    cnt++
                }
                cntList.add(cnt)
            }
        }
        return cntList.max() ?: 0
    }
}
```
