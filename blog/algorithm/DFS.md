# Thuật toán DFS - Depth first search

Là thuật toán tìm kiếm theo chiều sâu: Ưu tiên duyệt xuống nhất có thể trước khi quay lại.

<img src="blog/algorithm/img/DFS.png" style="display: block; margin-right: auto; margin-left: auto;">

## Pseudocode:

### Sử dụng đệ quy
```java
DFS(s) {
    // Đánh dấu thăm đỉnh s - start
    visited[s] = true;
    // duyệt các đỉnh kề với đỉnh s
    for(v: adj[s]) {
        // Nếu đỉnh chưa được thăm thì thăm và duyệt tiếp từ đỉnh này xuống
        if(!visited[v]) {
            DFS(v);
        }
    }
}
```
### Không sử dụng đệ quy

Đây là cách sử dụng stack. Nguyên tắc của stack là LIFO (Last in, first out). Nên khi ta thăm 1 điểm (đẩy điểm đó vào stack) ngay sau đó ta sẽ thăm các điểm kề từ điểm được thêm sau cùng (lẩy từ stack)

<img src="blog/algorithm/img/DFS1.png" style="display: block; margin-right: auto; margin-left: auto;">


```java
DFS(s) {
    // Đánh dấu thăm đỉnh s
    visited[s] = true;
    Stack<Integer> stack = new Stack();
    // đẩy đỉnh `s` vào stack để bắt đầu duyệt
    stack.push(s);

    // tiếp tục duyệt nếu còn đỉnh đến khi hết
    while(!stack.isEmpty()) {

        // Get giá trị của phần tử mới thêm gần nhất của stack (top) để tìm các đỉnh liền kề
        v = stack.peek();
        // Bỏ phần tử này ra khỏi stack
        stack.pop();
        
        if (visited[v] == false) {
            // nếu điểm chưa thăm thì đánh dấu là đã thăm
            visited[v] = true;
        }

        // duyệt tất cả các phần từ kề vs đỉnh v
        Iterator<Integer> itr = adj[s].iterator();
        while (itr.hasNext()) 
        {
            int t = itr.next();
            // nếu phần tử t này chưa được thăm thì sẽ đẩy vào stack và quay lại hàm while để thực hiện bước tiếp theo
            if(!visited.get(t))
                stack.push(t);
        }
    }
}
```

## Độ phức tạp

Đồ thị G =<V, E> V đỉnh và E cạnh
- Biểu diễn bằng ma trận kề: O(V*V)
- Biểu diễn bằng danh sách cạnh: O(V*E)
- Biểu diễn bằng danh sách kề: O(V+E)

### Note: với `ma trận không trọng số` thì thuật toán DFS sẽ tìm ra `đường đi dài nhất`
