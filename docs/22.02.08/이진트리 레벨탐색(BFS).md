# 2022.02.08 (화요일)
### **1.이진트리 레벨탐색(BFS)**

Q. 아래 그림과 같은 이진트리를 레벨탐색 연습하세요.
![](https://user-images.githubusercontent.com/94853413/152482572-ce7fa134-6b83-46d4-adef-e2587b98ba78.png)

**<풀이 내용>**
```java
package p2;

import java.util.LinkedList;
import java.util.Queue;

class Node {
    int data;
    Node left;
    Node right;

    public Node(int val) {
        data = val;
        left = right = null;
    }
}

public class Main {
    Node root;
    public void BFS(Node root) {
        Queue<Node> Q = new LinkedList<>();
        Q.offer(root);
        int L = 0; // level
        while (!Q.isEmpty()) {
            int len = Q.size();
            System.out.print(L+ " : ");
            for (int i = 0; i < len; i++) {
                Node cur = Q.poll();
                System.out.print(cur.data+" ");
                if(cur.left != null) {
                    Q.offer(cur.left);
                }
                if(cur.right != null) {
                    Q.offer(cur.right);
                }
            }
            L++;
            System.out.println();
        }
    }

    public static void main(String[] args) {
        Main tree = new Main();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(6);
        tree.root.right.right = new Node(7);
        tree.BFS(tree.root);
    }
}

```

##  **🔥 새로 배운 내용 정리 & 느낀 점**
        1. 저번에 했던 DFS 와 오늘 해본 BFS로 트리구조를 순회하는 연습을 
           계속 반복적으로 해야할 것 같다.
           그래도 조금씩 이해가 가는거 같아서 기분이 좋다!
