# 2022.02.10 (목요일)
### **1. Tree 말단 노드까지의 가장 짧은 경로(DFS)**

Q. 아래 그림과 같은 이진트리에서 루트 노드 1에서 말단노드까지의 길이 중 가장 짧은 길이를 구하는 프로그램을 작성하세요.   
   각 경로의 길이는 루트노드에서 말단노드까지 가는데 이동하는 횟수를 즉 간선(에지)의 개수를 길이로 하겠습니다.   
      
   ![](https://user-images.githubusercontent.com/94853413/153325275-b5495442-9f84-4dcc-ad7b-4632cfae100b.png)
   )

**<풀이 내용>**
```java
package p4;

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
    int L = 0;
    public int DFS(int L, Node root) {
        if (root.left == null && root.right == null) {
            return L;
        }else {
            return Math.min(DFS(L+1, root.left), DFS(L+1, root.right));
        }
    }

    public static void main(String[] args) {
        Main tree = new Main();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        System.out.println(tree.DFS(0, tree.root));
    }
}

```


##  **🔥 새로 배운 내용 정리 & 느낀 점**

      