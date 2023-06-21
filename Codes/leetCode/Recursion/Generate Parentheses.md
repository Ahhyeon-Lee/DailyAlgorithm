### Description

Given `n` pairs of parentheses, write a function to *generate all combinations of well-formed parentheses*.

**Example 1:**

```
Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]

```

**Example 2:**

```
Input: n = 1
Output: ["()"]

```

**Constraints:**

- `1 <= n <= 8`

### Solution

- 가능한 모든 조합을 찾으라고 하지만 이 문제는 조합 문제가 아니다. 정해진 갯수의 괄호 한쌍을 만들기 위한 조건을 알면 재귀로 풀 수 있는 문제이다.
- 조건
    1. 괄호 쌍으로 이루어져야 하기 때문에 열고 닫는 괄호의 각 갯수는 n과 동일하다.
    2. 괄호를 추가할 때 `())`, `(()))` 처럼 닫는 괄호의 갯수가 여는 괄호의 갯수보다 많으면 괄호 쌍이 완성될 수 없기 때문에, 닫는 괄호는 여는 괄호의 갯수보다 적을때에만 추가할 수 있다.
    3. 여는 괄호는 최대 n개만 추가할 수 있기 때문에, 여는 괄호는 n개 미만일때에만 추가할 수 있다.
- 위 세개의 조건을 만족하도록 해 시작은 여는 괄호로 해서 각 트리를 뻗어가도록 재귀 함수를 호출하면 각 트리의 마지막 노드에서 list에 쌍이 맞는 괄호 문자열을 추가하게 되고 이를 리턴하면 된다.

```kotlin
class Solution {

    var list = mutableListOf<String>()
    var pairCnt = 0

    fun generateParenthesis(n: Int): List<String> {
        // open == close == n
        // only add close if close < open
        // only add open if open < n
        pairCnt = n
        makeParenthesis("(", 1, 0)
        return list.toList()
    }

    fun makeParenthesis(s: String, open: Int, close: Int) {
        if (open == close && open == pairCnt) {
            list.add(s.toString())
        } else {
            if (open < pairCnt) {
                makeParenthesis("${s}(", open + 1, close)
            }
            if (close < open) {
                makeParenthesis("${s})", open, close + 1)
            }
        }
    }
}
```
