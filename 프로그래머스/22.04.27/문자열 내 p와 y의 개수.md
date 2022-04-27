# 2022.04.27 (수요일)

### **1. 문자열 내 p와 y의 개수**

Q. 대문자와 소문자가 섞여있는 문자열 s가 주어집니다. s에 'p'의 개수와 'y'의 개수를 비교해 같으면 True,   
   다르면 False를 return 하는 solution를 완성하세요. 'p', 'y' 모두 하나도 없는 경우는 항상 True를 리턴합니다.   
   단, 개수를 비교할 때 대문자와 소문자는 구별하지 않습니다.   
   예를 들어 s가 "pPoooyY"면 true를 return하고 "Pyy"라면 false를 return합니다.   

    제한사항
    - 문자열 s의 길이 : 50 이하의 자연수
    - 문자열 s는 알파벳으로만 이루어져 있습니다.


**<풀이 방법>**
```java
import java.util.*;

public class Solution {
    public static boolean solution(String s) {
        boolean answer;
        int count = 0;
        int count2 = 0;
        String str = s.toLowerCase();
        for (char c : str.toCharArray()) {
            if (c == 'p') {
                count++;
            } else if (c == 'y') {
                count2++;
            }
        }
        if (count == count2) {
            answer = true;
        } else {
            answer = false;
        }

        return answer;
    }

     public static void main(String[] args) {
         Scanner sc = new Scanner(System.in);
         String str = sc.next();
         System.out.println(solution(str));
     }
 }
```

**<다른 풀이>**
```java
import java.util.*;

public class Solution {
    public static boolean solution(String s) {
        s = s.toLowerCase();
        return s.chars().filter(value -> 'p' == value).count() == s.chars().filter(value -> 'y' == value).count();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String str = sc.next();
        System.out.println(solution(str));
    }
}
```
##  **🔥 새로 배운 내용 정리 & 느낀 점**

      1. 람다식을 이용하여 간단하게 풀 수도 있다는 것을 배웠다.
      