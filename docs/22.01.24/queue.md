# 2022.01.20 (목요일)
### **1. 자료구조 queue 직접 구현해 보기**

**<풀이 내용>**
```java
import jdk.swing.interop.SwingInterOpUtils;

import java.util.NoSuchElementException;

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

    public void add(T item) {
        Node<T> t = new Node<T>(item);
        if (last != null) {
            last.next = t;
        }
        last = t;
        if (first == null) {
            first = last;
        }
    }

    public T remove() {
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


public class Test {
    public static void main(String[] args) {
        Queue<Integer> q = new Queue<Integer>();
        q.add(1);
        q.add(2);
        q.add(3);
        q.add(4);
        System.out.println(q.remove()); // 1
        System.out.println(q.remove()); // 2
        System.out.println(q.peek());   // 3
        System.out.println(q.isEmpty()); // false
        System.out.println(q.remove()); // 3
        System.out.println(q.remove()); // 4
        System.out.println(q.isEmpty()); // true
    }
}

```

##  **🔥 새로 배운 내용 정리 & 느낀 점**

        1. 내부클래스를 처음 사용해보아서 구현에 어려움이 있었지만 2번 3번 반복해주었더니
           이해에 많은 도움이 되었다.
        