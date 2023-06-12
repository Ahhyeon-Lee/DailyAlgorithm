### Description

Given a string `s`, find the length of the **longest**

**substring**

without repeating characters.

**Example 1:**

```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.

```

**Example 2:**

```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

```

**Example 3:**

```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

```

**Constraints:**

- `0 <= s.length <= 5 * 104`
- `s` consists of English letters, digits, symbols and spaces.

### Solution

- 중복되지 않은 문자로만 이루어진 문자열의 최대 길이를 구하는 문제이다.
- string을 돌면서 StringBuilder에 문자를 하나씩 넣다가 중복되는 문자가 나올시 StringBuilder에 저장했던 문자열의 0번째 인덱스 부터 해당 중복 문자열 까지를 잘라낸 후 다시 문자를 더한다.
- 이러한 작업을 하면서 매번 문자열의 길이를 비교하면서 최대값을 구하면 string을 다 돌았을때 중복 없는 최대 문자열의 길이를 구할 수 있다.

```kotlin
fun lengthOfLongestSubstring(string: String): Int {
    if (string.length == 0) return 0
    var max = 0
    var sb = StringBuilder().apply { string[0] }
    string.forEach { s ->
        if (sb.contains(s)) {
            sb.delete(0, sb.indexOf(s)+1)
        }
        sb.append(s)
        max = Math.max(max, sb.length)
    }
    return max
}
```
