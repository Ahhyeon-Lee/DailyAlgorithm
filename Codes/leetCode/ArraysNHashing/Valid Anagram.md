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

- s와 t의 각 Char가 순서만 다르고 모두 같으므로, 반대로 말하면 순서가 같으면 둘은 같은 문자열이라는 것을 알 수 있다.
- 따라서 각 Char를 정렬한 문자열이 같은지 다른지를 비교하면 된다.
- 하지만 정렬 알고리즘은 O(n logn)의 시간 복잡도를 가지므로 이 다음에는 map을 이용해 풀어볼 것이다.

```kotlin
// 첫번째 풀이
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

- 두번째 풀이는 HashMap을 이용해 문자열의 각 Char와 Char 횟수를 저장해놓고 두 맵을 비교한다.
- s와 t의 문자열의 길이가 같은 경우에만 맵에 각 Char와 횟수를 넣으므로 각 문자열의 맵을 비교할 때 하나의 맵만 반복문을 돌리면 된다.
    - 나는 처음엔 sMap과 tMap 각각을 반복문을 돌려 비교해야 한다고 생각했었다. 하지만 두 문자열의 길이가 같으므로 하나의 맵으로만 반복문을 돌리면 어차피 하나의 맵에 있는 Char가 없는 경우는 다른 맵에 다른 Char가 있다는 뜻이 되므로 false를 반환하면 된다.
- 이 방법을 사용하면 문자열 한바퀴, 맵 한바퀴만 돌면 되므로 시간 복잡도는 O(n)이 된다.

```kotlin
// 두번째 풀이
class Solution {
    fun isAnagram(s: String, t: String): Boolean {
        if (s.length != t.length) {
            return false
        } else {
            val sMap = HashMap<Char, Int>()
            val tMap = HashMap<Char, Int>()
            for (i in (0 until s.length)) {
                sMap[s[i]] = sMap[s[i]]?.let { it + 1 } ?: 1
                tMap[t[i]] = tMap[t[i]]?.let { it + 1 } ?: 1
            }
            
            sMap.forEach {
                if (it.value != tMap[it.key]) return false
            }
            return true
        }      
    }
}
```

- 정렬 알고리즘을 푼 풀이와 HashMap을 이용한 풀이의 런타임 시간을 비교해보니 2배 이상의 차이가 났다.
