# 2022.04.07 (목요일)
### **2. 가장 높은 탑 쌓기(LIS 응용)**

Q. 밑면이 정사각형인 직육면체 벽돌들을 사용하여 탑을 쌓고자 한다.   
   탑은 벽돌을 한 개씩 아래 에서 위로 쌓으면서 만들어 간다.     
   아래의 조건을 만족하면서 가장 높은 탑을 쌓을 수 있는 프 로그램을 작성하시오.   
   (조건1) 벽돌은 회전시킬 수 없다. 즉, 옆면을 밑면으로 사용할 수 없다.   
   (조건2) 밑면의 넓이가 같은 벽돌은 없으며, 또한 무게가 같은 벽돌도 없다.    
   (조건3) 벽돌들의 높이는 같을 수도 있다.   
   (조건4) 탑을 쌓을 때 밑면이 좁은 벽돌 위에 밑면이 넓은 벽돌은 놓을 수 없다.    
   (조건5) 무게가 무거운 벽돌을 무게가 가벼운 벽돌 위에 놓을 수 없다.    

**<풀이 내용>**
```java
import java.util.*;

class Brick implements Comparable<Brick> {
    public int s, h, w;
    Brick(int s, int h, int w) {
        this.s = s;
        this.h = h;
        this.w = w;
    }
    @Override
    public int compareTo(Brick o) {
        return o.s - this.s;
    }
}

class Main {
    static int[] dy;
    public static int solution(ArrayList<Brick> arr) {
        int answer = 0;
        Collections.sort(arr);
        dy[0] = arr.get(0).h;
        answer = dy[0];
        for (int i = 1; i < arr.size(); i++) {
            int max_h = 0;
            for (int j = i-1; j >= 0; j--) {
                if (arr.get(j).w > arr.get(i).w && dy[j]>max_h) {
                    max_h = dy[j];
                }
            }
            dy[i] = max_h + arr.get(i).h;
            answer = Math.max(answer, dy[i]);
        }
        return answer;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        ArrayList<Brick> arr = new ArrayList<>();
        dy = new int[n];
        for (int i = 0; i < n; i++) {
            int a = sc.nextInt();
            int b = sc.nextInt();
            int c = sc.nextInt();
            arr.add(new Brick(a, b, c));
        }
        System.out.print(solution(arr));
    }
}
```


##  **🔥 새로 배운 내용 정리 & 느낀 점**

     

