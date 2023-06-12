### Description

Given two strings `s1` and `s2`, return `true` *if* `s2` *contains a permutation of* `s1`*, or* `false` *otherwise*.

In other words, return `true` if one of `s1`'s permutations is the substring of `s2`.

**Example 1:**

```
Input: s1 = "ab", s2 = "eidbaooo"
Output: true
Explanation: s2 contains one permutation of s1 ("ba").

```

**Example 2:**

```
Input: s1 = "ab", s2 = "eidboaoo"
Output: false

```

**Constraints:**

- `1 <= s1.length, s2.length <= 104`
- `s1` and `s2` consist of lowercase English letters.

### Solution

- s1의 조합을 s2가 가지고 있는지를 판단하는 문제이다.
- s1의 조합은 s1의 anagram이므로 s2를 s1 길이만큼 자른 문자열의 Char의 갯수를 map에 저장해두고 s1의 Char의 갯수를 저장한 map과 비교했다.

```kotlin
class Solution {
  fun checkInclusion(s1: String, s2: String): Boolean {
      val map1 = HashMap<Char, Int>()
      s1.forEach { s ->
          map1[s] = (map1[s] ?: 0) + 1 
      }

      var l = 0
      var r = l + s1.lastIndex
      while (r <= s2.lastIndex) {
          val map2 = HashMap<Char, Int>()
          s2.slice(l .. r).forEach { s ->
              map2[s] = (map2[s] ?: 0) + 1
          }
          if (map1 == map2) return true
          l++
          r++
      }

      return false
  }
}
```
