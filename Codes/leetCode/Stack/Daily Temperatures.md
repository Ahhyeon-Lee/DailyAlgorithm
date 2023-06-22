### Description

Given an array of integers `temperatures` represents the daily temperatures, return *an array* `answer` *such that* `answer[i]` *is the number of days you have to wait after the* `ith` *day to get a warmer temperature*. If there is no future day for which this is possible, keep `answer[i] == 0` instead.

**Example 1:**

```
Input: temperatures = [73,74,75,71,69,72,76,73]
Output: [1,1,4,2,1,1,0,0]

```

**Example 2:**

```
Input: temperatures = [30,40,50,60]
Output: [1,1,1,0]

```

**Example 3:**

```
Input: temperatures = [30,60,90]
Output: [1,1,0]

```

**Constraints:**

- `1 <= temperatures.length <= 105`
- `30 <= temperatures[i] <= 100`

### Solution

- 첫번째 풀이는 temperatures의 각 인덱스를 돌 때 마다 ***이후** 인덱스를 탐색*하여 현 인덱스보다 큰 수를 찾아 인덱스 차를 도출해냈다.
- 이렇게 하면 매 인덱스마다 이후에 탐색한적 있는 인덱스라도 다시 탐색하게 되므로 테스트 케이스에 따라 시간복잡도가 O(n^2)가 될 수도 있다.
- 아니나다를까 temperatures가 매우 길고 현 인덱스보다 큰 수가 멀리에 있는 케이스가 많을 때 타임아웃 오류가 났다.

```kotlin
// 첫번째 풀이 (Time out 오류)
class Solution {
    fun dailyTemperatures(temperatures: IntArray): IntArray {
        val answer = IntArray(temperatures.size) { 0 }
        temperatures.forEachIndexed { index, value ->
            if (index == temperatures.lastIndex) return answer
            var compare = index + 1
            var day = 0
            while (temperatures.getOrNull(compare) ?: value + 1 <= value) {
                day++
                compare++
            }
            answer[index] = if (temperatures.lastIndex - index < ++day) 0 
                else day
        }
        return answer
    }
}
```

- 관건은 한 번 탐색한 인덱스를 다시 탐색하는 횟수를 최대한 줄이는 것이다.
- 두번째 풀이의 접근 방식은 temp의 각 인덱스를 돌 때 현 인덱스 ***이전 값들을 비교***하는 것이다. (첫번째 풀이에서는 현 인덱스 이후 값들을 비교했다. 두번째 풀이는 반대의 접근방식이다.)
- temp의 각 값을 Stack에 넣으면서 현 인덱스의 값보다 작은 값이 있을 경우 이를 pop 하면서 인덱스 간의 차를 구하면 temp를 한 번만 돌면서 재탐색 횟수를 최대한 줄일 수 있다.
- 정답을 구하기 위해서는 인덱스 간의 차를 구해야 하므로 Stack에는 temp 각 값의 인덱스를 넣었다.
- temp를 돌면서 지금까지 돈 인덱스를 저장해놓은 Stack의 peek 값과 현 인덱스의 값을 비교해, 현 인덱스의 값이 더 크면 stack에서 peek 값을 지우고 정답의 peek 인덱스에 두 인덱스 간의 차를 넣는다. (answer은 temp와 동일한 인덱스를 가지고 있고, 스택에는 temp의 인덱스를 넣었으므로, 스택의 peek을 지울때 해당 값이 answer의 인덱스가 된다.)
- 이렇게 하면 스택에는 우리가 차를 구해야 할 현 인덱스보다 큰 값만 남게되므로(현 인덱스보다 작은 값은 pop 해왔기 때문에) temp를 돌면서 효율적으로 정답을 구할 수 있다.

```kotlin
// 두번째 풀이 (정답)
import java.util.*

class Solution {
    fun dailyTemperatures(temp: IntArray): IntArray {
        val answer = IntArray(temp.size) { 0 }
        val stack = Stack<Int>()
        for (i in 0..temp.lastIndex) {
            while (stack.isNotEmpty() && temp[stack.peek()] < temp[i]) {
                answer[stack.peek()] = i - stack.pop()
            }
            stack.push(i)
        }
        return answer
    }
}
```
