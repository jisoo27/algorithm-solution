# 2022.03.31 (목요일)
### **2. 친구인가(Disjoint-Set : Union & Find)**

Q. 오늘은 새 학기 새로운 반에서 처음 시작하는 날이다. 현수네 반 학생은 N명이다.   
   현수는 각 학생들의 친구관계를 알고 싶다. 모든학생은 1부터 N까지 번호가 부여되어있고   
   현수에게는 각각 두명의 학생은 친구관계가 번호로 표현된 숫자쌍이 주어진다.    
   만약 (1, 2), (2, 3), (3, 4)의 숫자쌍이 주어지면 1번 학 생과 2번 학생이 친구이고, 2번 학생과 3번 학생이 친구,   
   3번 학생과 4번 학생이 친구이다. 그리고 1번 학생과 4번 학생은 2번과 3번을 통해서 친구관계가 된다.   
   학생의 친구관계를 나타내는 숫자쌍이 주어지면 특정 두 명이 친구인지를 판별하는 프로그램을 작성하여라.    
   두 학생이 친구이면 “YES"이고, 아니면 ”NO"를 출력한다.   

**<풀이 내용>**
```java
import java.util.*;
class Main {
    
    static int[] unf;
    
    public static int Find(int v){
        if (v == unf[v]) {
            return v;
        } else {
            return unf[v] = Find(unf[v]);
        }
    }
    
    public static void Union(int a, int b){
        int fa = Find(a);
        int fb = Find(b);
        if (fa != fb) {
            unf[fa]=fb;
        }
    }
    
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int m = sc.nextInt();
        unf = new int[n+1];
        for (int i = 1; i <= n; i++) {
            unf[i] = i;
        }
        for (int i = 1; i <= m; i++){
            int a = sc.nextInt();
            int b = sc.nextInt();
            Union(a, b);
        }
        int a = sc.nextInt();
        int b = sc.nextInt();
        int fa = Find(a);
        int fb = Find(b);
        if (fa == fb) {
            System.out.println("YES");
        }
        else {
            System.out.println("NO");
        }
    }
}
```


##  **🔥 새로 배운 내용 정리 & 느낀 점**
      
      1. Disjoint-Set 이란?
      => 서로소 집합구조를 의미한다.
      
      2. Union & Find 구조로 많이 풀기 때문에 방식 자체를 외우는 것이 좋다.
      

