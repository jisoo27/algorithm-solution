# 2022.04.14 (목요일)
### **1. x만큼 간격이 있는 n개의 숫자**

Q. 함수 solution은 정수 x와 자연수 n을 입력 받아, x 부터 시작해 x씩 증가하는 숫자를          
   n개 지니는 리스트를 리턴해야 한다.    
   다음 제한 조건을 보고, 조건을 만족하는 함수, solution을 완성해라.   


**<나의 풀이>**
```java
class Solution {
    public long[] solution(int x, int n) {
        long[] answer = new long[n];
        answer[0] = x;
        for (int i = 1; i < n; i++) {
            answer[i] += answer[i-1] + x;
        }
        return answer;
    }
}
```

##  **🔥 새로 배운 내용 정리 & 느낀 점**
   
      1. 한번에 통과해서 기뻤다 ^-^