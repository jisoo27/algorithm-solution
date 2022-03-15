# 2022.03.15 (화요일)
### **1. 미로탐색(DFS)**

Q. 7*7 격자판 미로를 탈출하는 경로의 가지수를 출력하는 프로그램을 작성하세요.      
   출발점은 격 자의 (1, 1) 좌표이고, 탈출 도착점은 (7, 7)좌표이다.      
   격자판의 1은 벽이고, 0은 통로이다. 격 자판의 움직임은 상하좌우로만 움직인다.      
   미로가 아래와 같다면 출발점에서 도착점까지 갈 수 있는 방법의 수는 8가지이다.      
   ![](https://user-images.githubusercontent.com/94853413/158396483-8fe7b038-b4fb-4a2d-8416-65ea183e6efd.png)    


**<풀이 내용>**
```java
import java.util.Scanner;

public class Main {
    static int[] dx = {-1, 0, 1, 0};
    static int[] dy = {0, 1, 0, -1};
    static int[][] board;
    static int answer = 0;

    public static void DFS(int x, int y) {
        if(x == 7 && y == 7) {
            answer++;
        } else {
            for (int i = 0; i < 4; i++) {
                int nx = x + dx[i];
                int ny = y + dy[i];
                if (nx >= 1 && nx <= 7 && ny >= 1 && ny <= 7 && board[nx][ny] == 0) { // 4방향 조건 확인
                    board[nx][ny] = 1; // 지나간 자리 1로 체크
                    DFS(nx, ny);
                    board[nx][ny] = 0; // 뒤로 back 할 경우
                }
            }
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        board = new int[8][8];
        for (int i = 1; i <= 7; i++) {
            for (int j = 1; j <= 7; j++) {
                board[i][j] = sc.nextInt();
            }
        }
        board[1][1] = 1; // 출발점 체크 걸기
        DFS(1, 1);
        System.out.println(answer);
    }
}

```


##  **🔥 새로 배운 내용 정리 & 느낀 점**