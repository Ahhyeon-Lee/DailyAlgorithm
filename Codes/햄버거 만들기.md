## 햄버거 만들기
![image](https://user-images.githubusercontent.com/68845653/212115233-10b68e38-074d-45f9-ac2a-592dcd88329d.png)

## 문제 풀이
인자로 들어오는 IntArray에 1,2,3,1이 연속적으로 있는 경우의 수를 구하는 문제이다.

## 나의 풀이
```kotlin
class Solution {
  fun solution(ingredient: IntArray): Int {
      val string = StringBuilder(ingredient.joinToString(""))
      var index = string.indexOf("1231")
      var answer = 0 

      while (index != -1) {
          string.deleteRange(index, index+4)
          val startIndex = (index-3).takeIf { it > 0 } ?: 0
          index = string.indexOf("1231", startIndex)
          answer++
      }
      return answer
  }
  
  // 시간초과 오류 발생
  fun timeOutSolution(ingredient: IntArray): Int {
      var answer = 0
      var string = ingredient.joinToString("")
      while(string.contains("1231")) {
          if (string.contains("1231")) {
              answer++
              string = string.replaceFirst("1231", "")
          } else break
      }
      return answer
  }
}
```
시간 초과 오류가 문제였다. 오류가 났던 솔루션이 timeOutSolution이다. 시간 초과 오류의 원인은 두가지였다. 1.String을 사용한 것, 2.'1231'를 찾을때마다 문자열을 첫번째 인덱스부터 다시 
탐색을 시작한 것. (StringBuilder와 String의 차이 제대로 알아볼 것.) 두번째 시간초과 원인이었던 인덱스는, 첫번째 '1231' 인덱스를 찾으면 처음부터가 아닌 인덱스-2 번째 인덱스에서 부터만 
다시 탐색을 시작했다. 이미 첫번째 1231 인덱스를 찾고 시작했기 때문에 다시 처음부터 맨 앞으로 돌아가 탐색을 할 필요가 없다. 완성되지 않았을 인덱스부터 탐색하려면 찾으려는 1231 네글자 보다 하나 
작은 인덱스-3부터 탐색을 시작해야 한다.

