### Description

You are given an array of strings `tokens` that represents an arithmetic expression in a [Reverse Polish Notation](http://en.wikipedia.org/wiki/Reverse_Polish_notation).

Evaluate the expression. Return *an integer that represents the value of the expression*.

**Note** that:

- The valid operators are `'+'`, `'-'`, `'*'`, and `'/'`.
- Each operand may be an integer or another expression.
- The division between two integers always **truncates toward zero**.
- There will not be any division by zero.
- The input represents a valid arithmetic expression in a reverse polish notation.
- The answer and all the intermediate calculations can be represented in a **32-bit** integer.

**Example 1:**

```
Input: tokens = ["2","1","+","3","*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9

```

**Example 2:**

```
Input: tokens = ["4","13","5","/","+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6

```

**Example 3:**

```
Input: tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
Output: 22
Explanation: ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22

```

**Constraints:**

- `1 <= tokens.length <= 104`
- `tokens[i]` is either an operator: `"+"`, `"-"`, `"*"`, or `"/"`, or an integer in the range `[-200, 200]`.

### Solution

- Stack을 이용해 tokens를 돌면서 숫자는 스택에 넣고 연산자를 만나면 쌓여있던 스택 내의 숫자 두개를 이용해 연산 후 해당 숫자들은 스택에서 제거하고 연산 결과를 스택에 넣으면 된다.
- pop()을 하면 제거한 peek()이 반환되므로 pop()으로 연산까지 한 번에 한다.

```kotlin
import java.util.Stack

class Solution {
    fun evalRPN(tokens: Array<String>): Int {
        val stack = Stack<Int>()
        tokens.forEach { token ->
            val result = when(token) {
                "+" -> { stack.pop() + stack.pop() }
                "-" -> { 
                    val snd = stack.pop()
                    val first = stack.pop() 
                    first - snd
                }
                "*" -> { stack.pop() * stack.pop() }
                "/" -> {
                    val bottom = stack.pop()
                    val top = stack.pop() 
                    top / bottom
                }
                else -> { token.toInt() }
            }
            stack.push(result)
        }
        return stack.peek()
    }
}
```
