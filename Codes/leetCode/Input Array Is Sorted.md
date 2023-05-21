### Description

Given a **1-indexed** array of integers `numbers` that is already ***sorted in non-decreasing order***, find two numbers such that they add up to a specific `target` number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where `1 <= index1 < index2 <= numbers.length`.

Return *the indices of the two numbers,* `index1` *and* `index2`*, **added by one** as an integer array* `[index1, index2]` *of length 2.*

The tests are generated such that there is **exactly one solution**. You **may not** use the same element twice.

Your solution must use only constant extra space.

**Example 1:**

```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].

```

**Example 2:**

```
Input: numbers = [2,3,4], target = 6
Output: [1,3]
Explanation: The sum of 2 and 4 is 6. Therefore index1 = 1, index2 = 3. We return [1, 3].

```

**Example 3:**

```
Input: numbers = [-1,0], target = -1
Output: [1,2]
Explanation: The sum of -1 and 0 is -1. Therefore index1 = 1, index2 = 2. We return [1, 2].

```

**Constraints:**

- `2 <= numbers.length <= 3 * 104`
- `1000 <= numbers[i] <= 1000`
- `numbers` is sorted in **non-decreasing order**.
- `1000 <= target <= 1000`
- The tests are generated such that there is **exactly one solution**.

### Solution

- 첫번째 풀이는 지난번 Two Sum 문제에서  taget과 num 사이의 차와 HashMap을 이용한 방법으로 풀었다.

```kotlin
// 첫번째 풀이
fun twoSum(numbers: IntArray, target: Int): IntArray {
    val map = HashMap<Int, Int>()
    numbers.forEachIndexed { index, num ->
        val gap = target - num
        if (map[gap] != null) {
            return intArrayOf(Math.min(index+1, map[gap]!!+1), Math.max(index+1, map[gap]!!+1))
        } else {
            map[num] = index
        }
    }
    return IntArray(0)
}
```

- Two Sum 문제와 이 문제의 차이는 nums의 정렬 여부이다. 이번 문제는 nums가 정렬되어 있으므로 왼쪽 끝과 오른쪽 끝의 포인터를 옮겨가며 정답을 찾는 방법을 사용할 수 있다.
- nums가 정렬되어 있으므로 끝 인덱스들을 더하면서 더한 수가 target 보다 크거나 작을 경우 포인터를 한칸씩 옮겨서 계산할 수 있다.
    ![image](https://github.com/Ahhyeon-Lee/DailyAlgorithme/assets/68845653/c455fcc7-3bae-4118-917e-82ffbc9d1732)
    
- 더한 수가 target 보다 크면 작은 수로 옮겨가야 하므로 오른쪽 끝인 r 포인터를 왼쪽으로 옮겨 더한다.
- 더한 수가 target 보다 작으면 큰 수로 옮겨가야 하므로 왼쪽 끝인 l 포인터를 오른쪽으로 옮겨 더한다.
- 그렇게 옮겨가면 nums 안에는 정답이 무조건 있으므로 target과 같은 값을 구할 수 있다.

```kotlin
// 두번째 풀이
fun twoSum(nums: IntArray, target: Int): IntArray {
    var l = 0
    var r = nums.size - 1
    while (true) {
        if(nums[l] + nums[r] > target) r--
        if(nums[l] + nums[r] < target) l++
        if(nums[l] + nums[r] == target) {
            return intArrayOf(l+1, r+1)
        }
    }
    return IntArray(0)
}
```

- Valid Pandindrome 문제 처럼 정답이 있는지 여부를 반환하는 문제였다면 l과 r 포인터를 더하고 빼면서 끝까지 찾지 못했을 경우를 판단하는 조건을 하나 추가해야 했겠지만, 이번 문제는 nums 사이에 정답이 꼭 있으므로 포인터의 대소 관계를 판별하는 조건은 필요 없게 되었다.
