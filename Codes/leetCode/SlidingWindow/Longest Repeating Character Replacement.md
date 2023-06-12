### Description

You are given a string `s` and an integer `k`. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most `k` times.

Return *the length of the longest substring containing the same letter you can get after performing the above operations*.

**Example 1:**

```
Input: s = "ABAB", k = 2
Output: 4
Explanation: Replace the two 'A's with two 'B's or vice versa.

```

**Example 2:**

```
Input: s = "AABABBA", k = 1
Output: 4
Explanation: Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
There may exists other ways to achive this answer too.
```

**Constraints:**

- `1 <= s.length <= 105`
- `s` consists of only uppercase English letters.
- `0 <= k <= s.length`

### Solution

- 난이도 Medium 이라고는 믿을 수 없는 문제였다…
- 이 문제는 우선 s의 0번째 인덱스부터 늘려가면서 접근해, 구간내에 가장 많이 나온 알파벳을 제외한 나머지의 갯수가 k개 이하이면 해당 구간의 길이가 같은 문자열의 최대 길이가 되는 것이다.
- 이 원리를 이용해 Sliding Window 풀이법으로 0번째 인덱스부터 구간을 늘려가고, 해당 구간의 길이에서 가장 많이 나온 알파벳의 수를 뺐을 때 그 수가 k 초과이면 해당 구간은 k 조건에 부합하지 않으므로 start 인덱스를 앞으로 옮겨 다음 구간을 탐색한다.
- 내가 이해되지 않았던 부분은 maxCnt의 값을 줄이지 않고 계속 증가시키기만 한다는 점이었다. start를 오른쪽으로 옮기게 되면 구간 내 maxCnt 값이 바뀌게 될텐데 말이다.
- 하지만 여기에서 포인트는 우리가 구하고자 하는 것은 k 조건에 부합하는 최대 구간 길이라는 점이다.
- maxCnt가 줄어든다는 것은 start가 오른쪽으로 옮겨져 구간 길이가 작아졌음을 뜻한다. 하지만 우리가 구하고자 하는 것은 k 조건에 부합하는 최대 구간 길이를 반환하는 것이다. 따라서 구간 길이가 작아졌을 때는 결국 최대 길이가 아니므로 반환하고자 하는 값과 관련이 없다는 뜻이다. result는 지금껏 구한 구간 길이의 최댓값(result)과 현재 구간 길이(end - start + 1) 중 최대값을 할당하게 되므로 결국 현재 구간 길이가 줄어들었다면 지금까지 구한 최대값이 다시 result에 할당될 것이다.
- 그래서 이 경우를 신경쓰지 않아도 되므로 maxCnt를 줄여주는 일도 할 필요가 없는 것이다.

```kotlin
class Solution {
    fun characterReplacement(s: String, k: Int): Int {
        val frequency = IntArray(26) { 0 }

        var start = 0
        var maxCnt = 0
        var result = 0

        for (end in 0 until s.length) {
            val cnt = ++frequency[s[end]-'A']
            maxCnt = Math.max(maxCnt, cnt)

            if (end - start + 1 - maxCnt > k) {
                frequency[s[start]-'A']--
                start++
            }

            result = Math.max(result, end - start + 1)
        }

        return result
    }
}
```
### 회고
- 이 문제는 풀이를 보고도 이해하기 까지 상당히 시간이 오래 걸렸다. 그래도 많이 풀다보면 익숙해지겠지 생각하며 오늘도 하나 배운다.
