# Hàng đợi (Queue)
## 1. Khái niệm

Stack là một danh sách được bổ sung 2 thao tác: thêm một phần tử vào cuối danh sách, và loại bỏ một phần tử ở đầu danh sách.

Queue hoạt động theo nguyên tắc FIFO (First In - First Out, hay vào trước - ra trước).

# Note: Hay đc sử dụng trong bài toán BFS (Breadth first search)

<img src="blog/algorithm/img/queue.png" style="display: block; margin-right: auto; margin-left: auto;">


## 2. Cài đặt

### 2.1 Cài đặt thủ công

```
C++
    queue<int> st;
    st.push(5); // thêm 5 vào stack
    st.push(10); // thêm 10 vào stack
    cout << st.top() << endl; // In ra 10
    st.pop(); // loại bỏ phần tử ở cuối
    cout << st.top() << endl; // In ra 5
    return 0;

Java
    Queue<Integer> queue = new Queue<Integer>();
    queue.add(2);
    queue.put(10);
    queue.remove(); // Lấy ra 2
    queue.peek(); // In ra đỉnh của queue - in ra 10
    queue.add(5);
    queue.peek(); // In ra đỉnh của queue - in ra 10
    queue.remove(); // Lấy ra 10
    queue.peek(); // In ra đỉnh của queue - in ra 5
```

### 2.3 Độ phức tạp

- Time complexity: O(1)
- Space complextity: O(N) - do có N phần tử đưa vào queue

