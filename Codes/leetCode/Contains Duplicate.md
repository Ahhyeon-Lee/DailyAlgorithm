### Description

Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.

**Example 1:**

```
Input: nums = [1,2,3,1]
Output: true

```

**Example 2:**

```
Input: nums = [1,2,3,4]
Output: false

```

**Example 3:**

```
Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true

```

**Constraints:**

- `1 <= nums.length <= 105`
- `109 <= nums[i] <= 109`

### Solution

```kotlin
// 첫번째 풀이
fun containsDuplicate(nums: IntArray): Boolean {
    var map = HashMap<Int, Int>()
    var answer = false
    nums.sort()
    nums.forEach {
        if (map.get(it) != null) {
            answer = true
            return@forEach
        } else {
            map[it] = it
        }
    }
    return answer
}
// 두번째 풀이
fun containsDuplicate(nums: IntArray): Boolean {
    val set = HashSet<Int>()
    nums.forEach {
        if (!set.add(it)) return true
    }
    return false
}
```

- 처음에는 배열을 정렬해서 같은 수가 더 빨리 나오도록 한 뒤 map에 값을 넣고 해당 map에 원래 값이 있었으면 함수를 리턴하도록 했다.
- 하지만 set을 쓰면 add 할때부터 해당 값이 set에 있는지 없는지를 반환해준다.
