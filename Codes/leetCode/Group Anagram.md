### Description

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

```
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]

```

**Example 2:**

```
Input: strs = [""]
Output: [[""]]

```

**Example 3:**

```
Input: strs = ["a"]
Output: [["a"]]

```

**Constraints:**

- `1 <= strs.length <= 104`
- `0 <= strs[i].length <= 100`
- `strs[i]` consists of lowercase English letters.

### Solution

1. strs 내의 각 원소들을 anagram 기준이 되는 문자열로 변환해 이를 키로 가지고, 해당 anagram에 맞는 str 리스트를 밸류로 가진 HashMap을 사용한다.
    1. str을 각 Char로 재정렬해 키로 사용
    2. str의 각 Char의 횟수를 저장한 어레이를 문자열로 바꿔 키로 사용

```kotlin
class Solution {
    fun groupAnagrams(strs: Array<String>): List<List<String>> {
        val map = HashMap<String, MutableList<String>>()
        strs.forEach { str ->
            val charArray = Array(26) { 0 }
            str.forEach { char ->
                val index = char - 'a'
                charArray[index] += 1
            }
            val key = charArray.joinToString()
            map[key] = map[key]?.apply { add(str) } ?: mutableListOf(str)
        }
        return map.values.toList()
    }
}
```
