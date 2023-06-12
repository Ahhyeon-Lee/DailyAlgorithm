### Description

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

**Example 1:**

```
Input: s = "()"
Output: true

```

**Example 2:**

```
Input: s = "()[]{}"
Output: true

```

**Example 3:**

```
Input: s = "(]"
Output: false

```

**Constraints:**

- `1 <= s.length <= 104`
- `s` consists of parentheses only `'()[]{}'`.

### Solution

```kotlin
import java.util.Stack

class Solution {
    fun isValid(s: String): Boolean {
        val map = HashMap<Char, Char>().apply {
            put(')', '(')
            put(']', '[')
            put('}', '{')
        }
        val stack = Stack<Char>()
        s.forEach {
            when (it) {
                '(', '[', '{' -> stack.push(it)
                else -> {
                    if (stack.isEmpty()) return false
                    if (stack.peek() == map[it]!!) stack.pop()
                    else stack.push(it)
                }
            }
        }

        return stack.isEmpty()
    }
}
```
