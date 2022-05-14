# 2022.05.14 (토요일)

### **1. K번째 수**

Q. 배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.   
   예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면   
        1. array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.   
        2. 1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.   
        3. 2에서 나온 배열의 3번째 숫자는 5입니다.   

   배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때,   
   commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.       
   
   [제한사항]
   
    - array의 길이는 1 이상 100 이하입니다.
    - array의 각 원소는 1 이상 100 이하입니다.
    - commands의 길이는 1 이상 50 이하입니다.
    - commands의 각 원소는 길이가 3입니다.




**<나의 풀이>**
```java
import java.util.*;

public class Solution {
    public static int[] solution(int[] array, int[][] commands) {
        List<Integer> answer = new ArrayList<>();
        for (int i = 0; i < commands.length; i++) {
            int tmp = commands[i][2];
            int[] ints = Arrays.copyOfRange(array, commands[i][0] - 1, commands[i][1]);
            Arrays.sort(ints);
            answer.add(ints[tmp-1]);
        }
        return answer.stream().mapToInt(Integer::intValue).toArray();
    }


    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }
        int[][] commands = new int[3][3];
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                commands[i][j] = sc.nextInt();
            }
        }
        System.out.println(solution(arr, commands));
    }
}
```

**<다른 풀이>**
```java
import java.util.*;

public class Solution {
    public static String solution(int[] array, int[][] commands) {
        int[] answer = {};
        answer = new int[commands.length];
        for (int i = 0; i < commands.length; i++) {
            List<Integer> arrInt = new ArrayList<Integer>();
            for (int j = commands[i][0] - 1; j < commands[i][1]; j++) {
                arrInt.add(array[j]);
            }
            Collections.sort(arrInt);
            answer[i] = arrInt.get(commands[i][2] - 1);
        }
        return Arrays.toString(answer);
    }


    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }

        int[][] commands = new int[3][3];
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                commands[i][j] = sc.nextInt();
            }
        }
        System.out.println(solution(arr, commands));
    }
}
```

##  **🔥 새로 배운 내용 정리 & 느낀 점**

    1. Arrays.copyOfRange(복사하고자하는 배열, 시작위치, 끝 위치)
    =>  특정 배열의 원하는 범위만큼 복사하여 새로운 배열을 만든다.
        값에 의한 복사이므로 복사된 배열에서 값을 바꿔도 원본 배열의 값이 바뀌지 않는다.