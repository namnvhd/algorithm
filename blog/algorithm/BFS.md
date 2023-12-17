# Thuật toán BFS - Breadth first search

Là thuật toán tìm kiếm theo chiều rộng: Ưu tiên duyệt rộng các đỉnh kề với đỉnh hiện tại trước khi đi duyệt các đỉnh kề với đỉnh tiếp theo

<img src="blog/algorithm/img/BFS.png" style="display: block; margin-right: auto; margin-left: auto;">

## Pseudocode:

Tư tưởng là sử dụng queue. Nguyên tắc của queue là FIFO (First in, first out). Nên khi ta thăm 1 điểm (đẩy điểm đó vào queue) ngay sau đó ta sẽ thăm các điểm kề từ điểm được thêm đầu tiên (lẩy từ queue)

<img src="blog/algorithm/img/BFS1.png" style="display: block; margin-right: auto; margin-left: auto;">


```java
BFS(s) {
    // Khởi tạo queue
    Queue<Integer> queue = new LinkedList<Integer>(); 
    // Thêm đỉnh đầu vào queue
    queue.add(s);
    // Đánh dấu thăm đỉnh s
    visited[s] = true;

    // tiếp tục duyệt nếu còn đỉnh đến khi hết
    while(queue.size() != 0) {

        // lấy phần tử front trong queue ra
        v = queue.poll();

        // duyệt tất cả các phần từ kề vs đỉnh v
        Iterator<Integer> i = adj[s].listIterator();
        while (i.hasNext()) {
            int n = i.next();
            // Nếu đỉnh chưa được thăm thì đánh dấu đã thăm và đẩy vào queue
            if (!visited[n]) {
                visited[n] = true;
                queue.add(n);
            }
        }
    }
}
```

## Độ phức tạp

Đồ thị G =<V, E> V đỉnh và E cạnh
- Biểu diễn bằng ma trận kề: O(V*V)
- Biểu diễn bằng danh sách cạnh: O(V*E)
- Biểu diễn bằng danh sách kề: O(V+E)

### Note: với `ma trận không trọng số` thì thuật toán BFS sẽ tìm ra `đường đi ngắn nhất`

