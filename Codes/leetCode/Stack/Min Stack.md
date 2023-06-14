### Description

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

**You must implement a solution with `O(1)` time complexity for each function.**

**Example 1:**

```
Input
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

Output
[null,null,null,null,-3,null,0,-2]

Explanation
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2

```

**Constraints:**

- `231 <= val <= 231 - 1`
- Methods `pop`, `top` and `getMin` operations will always be called on **non-empty** stacks.
- At most `3 * 104` calls will be made to `push`, `pop`, `top`, and `getMin`.

### Solution

- 이 문제의 핵심은 설명의 마지막 부분에 있다. 모든 메소드를 O(1)의 시간복잡도로 구현하는 것. 그러려면 인덱스로 접근해서 바로 가져와야 한다.
- 첫번째 풀이는 그 점에서 제한사항과 맞지 않다. getMin() 메소드에서 min()으로 가져오면 stackList의 모든 원소를 검사 후 가져오는 것이기 때문에 O(n)의 시간복잡도를 갖기 때문이다.

```kotlin
// 첫번째 풀이
class MinStack() {
    
    val stackList = ArrayList<Int>()

    fun push(value: Int) {
        stackList.add(value)
    }

    fun pop() {
        stackList.removeAt(stackList.lastIndex)
    }

    fun top(): Int {
        return stackList[stackList.lastIndex]
    }

    fun getMin(): Int? {
        return stackList.min()
    }

}
```

- 이를 해결한 것이 두번째 풀이이다.
- 최소값을 O(1)의 시간복잡도로 가져오려면 push 할때 최소값을 비교해서 다른 변수에 저장해두어야 하는데, 이걸 그냥 Int 변수에 저장하면 pop()해서 원소를 제거했을시 그 원소가 최소값이었으면 다시 stack에서 최소값을 구해야하는 일이 생긴다.
- 그렇다면 push를 했을때 각 원소의 위치에서 최소값을 가지고 있는 것이 방법이 된다.
- 각 원소의 위치에서의 최소값을 저장할 minStack을 하나 더 만들어서 거기에 push시 들어온 원소와 minStack의 마지막 원소(지금껏 minStack에 쌓인 원소중 최소값일테니)를 비교해 minStack에 추가하고 pop()도 원 stack과 동일하게 해주면 된다.
- 이렇게 하면 getMin() 메소드에서 minStack의 마지막 원소를 가져오면 최소값을 O(1)의 시간복잡도로 가져올 수 있다.

```kotlin
// 두번째 풀이
class MinStack() {
    
    val stack = ArrayList<Int>()
    val minStack = ArrayList<Int>()

    fun push(value: Int) {
        stack.add(value)
        if(minStack.isNotEmpty()) {
            val min = Math.min(minStack.last(), value)
            minStack.add(min)
        } else {
            minStack.add(value)
        }
    }

    fun pop() {
        stack.removeAt(stack.lastIndex)
        minStack.removeAt(minStack.lastIndex)
    }

    fun top(): Int {
        return stack.last()
    }

    fun getMin(): Int? {
        return minStack.last()
    }

}
```
