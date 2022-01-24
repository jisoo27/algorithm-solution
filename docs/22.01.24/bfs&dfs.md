# 2022.01.24 (월요일)
### **1. 자료구조 bfs & dfs 직접 구현해 보기**

**<풀이 내용>**
```java
import java.util.LinkedList;
import java.util.NoSuchElementException;
import java.util.Stack;

class Queue<T> {
    class Node<T> {
        private T data;
        private Node<T> next;

        public Node(T data) {
            this.data = data;
        }
    }
    private Node<T> first;
    private Node<T> last;

    public void enqueue(T item) {
        Node<T> t = new Node<T>(item);
        if (last != null) {
            last.next = t;
        }
        last = t;
        if (first == null) {
            first = last;
        }
    }

    public T dequeue() {
        if (first == null) {
            throw new NoSuchElementException();
        }
        T data = first.data; // 데이터를 백업하고
        first = first.next; // 다음애를 first로 만들어 준다.

        if (first == null) {
            last = null;
        }
        return data;
    }

    public T peek() {
        if (first == null) {
            throw new NoSuchElementException();
        }
        return first.data;
    }

    public boolean isEmpty() {
        return first == null;
    }
}

class Graph {
    class Node {
        int data;
        LinkedList<Node> adjacent; // 인접한 노드들 간의 관계는 링크드 리스트처럼 표현
        boolean marked;
        Node (int data) { // 노드의 생성자에서는
            this.data = data; // 데이터를 받고
            this.marked  = false; // 마킹플래그를 false로 초기화
            adjacent = new LinkedList<Node>(); // 링크드 리스트를 준비시킨다.
        }
    }
    Node[] nodes;
    Graph(int size) {
        nodes = new Node[size];
        for (int i = 0; i < size; i++) {
            nodes[i] = new Node(i); // 편의를 위해 데이터와 방의 번호를 동일하게 만들어주었다.
        }
    }

    void addEdge(int i1, int i2) { // 두 노드의 관계를 저장하는 함수 , 데이터가 인덱스와 같으니
        Node n1 = nodes[i1];
        Node n2 = nodes[i2];
        // 2개의 노드에 인접한 노드를 저장하는 linked list에 상대방이 없다면 추가를 해준다.
        if (!n1.adjacent.contains(n2)) {
            n1.adjacent.add(n2);
        }
        if (!n2.adjacent.contains(n1)) {
            n2.adjacent.add(n1);
        }
    }

    void dfs() { // 그냥 dfs 를 호출하게 되면 0부터 시작하는걸로 설정한다.
        dfs(0);
    }

    void dfs(int index) { // 시작 인덱스를 받아 dfs 순회결과를 출력하는 함수
        Node root = nodes[index]; // 해당 인덱스로 노드를 가져오고
        Stack<Node> stack = new Stack<Node>(); // stack 을 하나 생성한다
        stack.push(root); // 현재 노드를 스택에 추가한다.
        root.marked = true; // 스택에 들어갔다고 표시를 해준.
        while (!stack.isEmpty()) { // 스택에 들어있는 것이 다 사라질때까지 반복
            Node r = stack.pop();
            for (Node n : r.adjacent) { // 가져온 노드의 자식들을 스택에 추가하고
                if (n.marked == false) { // 스택에 추가되지 않은 노드들만 골라
                    n.marked = true;
                    stack.push(n); // 다시 추가한다.
                }
            }
            visit(r); // 출력
        }
    }
    void bfs() { // 마찬가지로 bfs 가 인자없이 추출되면 0부터 시작
        bfs(0);
    }

    void bfs(int index) {
        Node root = nodes[index];
        Queue<Node> queue = new Queue<Node>();
        queue.enqueue(root);
        root.marked = true;
        while (!queue.isEmpty()) { // 이때 위와 같이 추가되지 않은 노드들만 추가해준다. queue 에 데이터가 없을때까지 반복한다
            Node r = queue.dequeue();
            for (Node n : r.adjacent) {
                if (n.marked == false) {
                    n.marked = true;
                    queue.enqueue(n);
                }
            }
            visit(r);
        }
    }
    // 재귀 호출을 이용한 dfs 구현
    void dfsR(Node r) { // 재귀호출을 할 때에는 linked list가 노드에 주소를 가지고 있기 때문에 , 재귀함수는 노드를 갖는 형태가 되어야 한다.
        if (r == null) { // 받은 노드가 null일 경우 그냥 나가고
            return;
        }
        r.marked = true; // 호출되었다고 마킹을 한다.
        visit(r);
        for (Node n : r.adjacent) {
            if (n.marked == false) {
                dfsR(n);
            }
        }
    }

    void dfsR(int index) {
        Node r = nodes[index];
        dfsR(r);
    }

    void dfsR() {
        dfsR(0);
    }



    void visit(Node n) {
        System.out.print(n.data + " ");
    }
}

public class Test {
    public static void main(String[] args) {
        Graph g = new Graph(9); // 생성시 9개의 노드와 함께 그래프를 만든다.
        g.addEdge(0, 1);
        g.addEdge(1, 2);
        g.addEdge(1, 3);
        g.addEdge(2, 4);
        g.addEdge(2, 3);
        g.addEdge(3, 4);
        g.addEdge(3, 5);
        g.addEdge(5, 6);
        g.addEdge(5, 7);
        g.addEdge(6, 8);
        g.dfsR();
    }
}

```

##  **🔥 새로 배운 내용 정리 & 느낀 점**

        1. 아직 완벽히 코드를 이해하지 못했기 때문에 여러번 더 반복해야 할 것 같다.
        