### Description

Given an integer array `nums` and an integer `k`, return *the* `k` *most frequent elements*. You may return the answer in **any order**.

**Example 1:**

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]

```

**Example 2:**

```
Input: nums = [1], k = 1
Output: [1]

```

**Constraints:**

- `1 <= nums.length <= 105`
- `104 <= nums[i] <= 104`
- `k` is in the range `[1, the number of unique elements in the array]`.
- It is **guaranteed** that the answer is **unique**.

**Follow up:** Your algorithm's time complexity must be better than `O(n log n)`, where n is the array's size.

### Solution

- 첫번째 풀이는 정렬 알고리즘(시간복잡도 $O(n log n)$)을 이용한 풀이이다.
- 이 방법의 시간 복잡도는 nums를 탐색하고 횟수를 담은 map을 Pair로 다시 변환하며 거친 O(n) + 정렬 알고리즘의 시간복잡도 O(n log n) 이 된다.

```kotlin
// 첫번째 풀이 : 정렬 활용
fun topKFrequent(nums: IntArray, k: Int): IntArray {
    val map = HashMap<Int, Int>()
    nums.forEach { 
        map[it] = map.getOrDefault(it, 0) + 1
    }
    val pairList = map.map { 
        Pair(it.key, it.value)
    }
    
    val answer = pairList
        .sortedByDescending { it.second }
        .slice(0 until k)
        .map { it.first }
    return answer.toIntArray()
}
```

- 두번째 풀이는 버킷 정렬 알고리즘(시간복잡도 $O(n)$ ~ $O(n log n)$)을 이용한 풀이이다.
- nums의 각 값의 횟수를 담은 map을 구하는 것은 동일하나 k개의 최대 횟수인 num을 구하는 과정에서 버킷 정렬 알고리즘이 사용되었다.
- nums의 각 값의 최대 횟수는 nums.size 만큼이 된다. [0 ~ 최대 횟수]의 범위를 갖는 리스트 countList 를 하나 생성해 횟수를 인덱스로 하여 각 횟수에 해당하는 num을 리스트로 넣는 것이다.
- 구해야 하는 것은 k개의 최대 횟수 num 배열이므로 countList의 끝 인덱스부터 해당 인덱스의 num 배열을 answer 배열에 더해 answer 배열의 원소가 k개가 되면 이를 반환하는 것이다.

```kotlin
// 두번째 풀이 : 버킷 정렬 활용
fun topKFrequent(nums: IntArray, k: Int): IntArray {
    val count = HashMap<Int, Int>()
    nums.forEach { 
        count[it] = count.getOrDefault(it, 0) + 1
    }

    val countList = List<MutableList<Int>>(nums.size + 1) { mutableListOf() }
    for ((num, cnt) in count) {
        countList[cnt].add(num)
    }

    val answer = mutableListOf<Int>()
    for (i in countList.size-1 downTo 1) {
        answer.addAll(countList[i])
        if (answer.size == k) {
            return answer.toIntArray()
        }
    }
    return intArrayOf()
}
```

- 버킷 정렬 역시 이름 그대로 리스트 내의 수를 정렬하는 알고리즘이다.
1. 정렬하려는 리스트 A가 주어졌을때 이와 같은 크기의 리스트 B를 만든다.
2. A 리스트 내 값들을 일정 구간으로 나누어 리스트 B의 각 요소에 배열로 입력한다.
    1. 이 문제에서는 횟수를 구해야 했으므로 1을 기준으로 구간을 나누어 리스트 B인 countList에 각 횟수에 해당하는 num을 배열로 넣었다.
3. B 내의 각 비어있지 않은 배열을 정렬한다.
    1. B 내의 각 배열에 담긴 요소가 많으면 결국 버킷 정렬 역시 $O(n log n)$ 의 시간복잡도를 갖게 되므로 데이터를 최대한 고르게 분포하도록 구간을 정하는 것이 좋고, 데이터 역시 최대한 분포도가 고르게 되어 있는 데이터가 좋다.
4. 정렬된 모든 B 내의 각 배열을 더해 최종적으로 정렬된 배열을 얻는다.
- 버킷 정렬 참조
    - [https://hroad.tistory.com/25](https://hroad.tistory.com/25)
    - [https://ratsgo.github.io/data structure&algorithm/2017/10/18/bucketsort/](https://ratsgo.github.io/data%20structure&algorithm/2017/10/18/bucketsort/)
