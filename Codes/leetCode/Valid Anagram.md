### Description

Given two strings `s` and `t`, return `true` *if* `t` *is an anagram of* `s`*, and* `false` *otherwise*.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

```
Input: s = "anagram", t = "nagaram"
Output: true

```

**Example 2:**

```
Input: s = "rat", t = "car"
Output: false

```

**Constraints:**

- `1 <= s.length, t.length <= 5 * 104`
- `s` and `t` consist of lowercase English letters.

### Solution

```kotlin
class Solution {
    fun isAnagram(s: String, t: String): Boolean {
        if (s.length != t.length) {
            return false
        } else {
            val sString = s.split("").sorted().joinToString("")
            val tString = t.split("").sorted().joinToString("")
            if (sString != tString) return false
            else return true
        }      
    }
}
```

- s와 t의 각 Char가 순서만 다르고 모두 같으므로, 반대로 말하면 순서가 같으면 둘은 같은 문자열이라는 것을 알 수 있다.
- 따라서 각 Char를 정렬한 문자열이 같은지 다른지를 비교하면 된다.
