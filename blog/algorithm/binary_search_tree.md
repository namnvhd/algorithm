# Cây Tìm Kiếm Nhị Phân (BST - Binary Search Tree)


## 1. Khái niệm

Cây Tìm Kiếm Nhị Phân (BST Binary Search Tree) là một cây nhị phân có tính chất: Với mỗi giá trị trên đỉnh đang xét, giá trị của mọi đỉnh trên cây con trái luôn nhỏ hơn đỉnh đang xét và giá trị của mọi đỉnh trên cây con phải luôn lớn hơn đỉnh đang xét.


Độ phức tạp: **`O(N)`**


Cây tìm kiếm nhị phân là 1 dạng đồ thị nhưng các nút (node) của cây phải có những tính chất sau:

- Mỗi node chỉ có thể có tối đa 2 node con
- Giá trị của node con bên trái phải nhỏ hơn node cha của nó
- Giá trị của node con bên phải lớn hơn node cha của nó

Đặc biệt trong 1 cây tìm kiếm nhị phân không cho phép 2 giá trị trùng nhau. Chính quy luật và cách sắp xếp như trên cấu trúc BST đã giúp sắp xếp dữ liệu theo một cách có trật tự, từ đó giúp người sử dụng dễ dàng hơn trong việc tổ chức dữ liệu cũng như việc tìm kiếm.

<img src="blog/algorithm/img/binary-search-tree1.png" style="display: block; margin-right: auto; margin-left: auto;">

Sau đây là một vài khái niệm trong cây tìm kiếm nhị phân:

- Root node (nút gốc) : node đầu tiên của cây.
- Leaf node (nút lá): node không có con trái và con phải.
- Internal node : những node không phải nút gốc cũng không phải nút lá.
- Level (tầng): như hình minh họa trên chúng ta có 2 cây với 3 tầng.

**Về cơ bản chúng ta có 3 loại cây nhị phân:**

<img src="blog/algorithm/img/binary-search-tree2.png" style="display: block; margin-right: auto; margin-left: auto;">

**Full binary tree**: Những node không phải nút lá đều có 2 con trái và phải.

**Complete binary tree**: Tất cả các tầng đều chứa đầy nodes ngoại trừ tầng cuối có thể đầy hoặc không nhưng các node tầng cuối phải đc xếp lần lượt từ trái đến phải.

**Perfect binary tree**: tất cả nodes đều có 2 con và các nút lá ở cùng một level.

Với cây tìm kiến nhị phân chúng ta có những tác vụ cơ bản sau:

- Search: Tìm kiếm.
- Insert: Thêm 1 node.
- Remove: Xóa 1 node.
- Traversal: Duyệt cây với 3 loại cơ bản: pre-oder traversal, In-order traversal, post-order traversal.

## 2. Tác dụng


Cây tìm kiếm nhị phân cho phép thực hiện các thao tác:

- Thêm 1 phần tử.
- Xóa 1 phần tử.
- Kiểm tra 1 phần tử có tồn tại hay không.
- Tìm phần tử đầu tiên lớn hơn hoặc bằng 1 giá trị x cho trước.
Trong trường hợp dữ liệu ngẫu nhiên, các thao tác trên có độ phức tạp trung bình là `O(logN)`. Tuy nhiên trong trường hợp xấu nhất, cây tìm kiếm nhị phân bị suy biến (thành 1 "đường thẳng"), thì độ phức tạp mỗi thao tác là `O(N)`.

Để khắc phục điều này, có rất nhiều CTDL cải tiến từ cây tìm kiếm nhị phân, thường được gọi là các cây nhị phân cân bằng. Khi đó, các thao tác trên có thể được thực hiện với độ phức tạp `O(logN)`. Ví dụ:

- Cây Đỏ Đen (Red-Black Tree) là một dạng cây tìm kiếm nhị phân (BST) mà sau mỗi truy vấn được thực hiện, cây tự cân bằng theo đúng tính chất của nó với độ phức tạp O(log(N)). CTDL set trong C++ được cài đặt bằng cây đỏ đen.

<img src="blog/algorithm/img/binary-search-tree3.png" style="display: block; margin-right: auto; margin-left: auto;">


```java
import java.util.Scanner;

class BSTNode {
   BSTNode left, right;
   int data;
   public BSTNode(int n) {
      left = null;
      right = null;
      data = n;
   }
}
public class BST {
   static BSTNode root;
   public BST() {
      root = null;
   }
   private BSTNode insert(BSTNode node, int data) {
      if(node == null)
         node = new BSTNode(data);
      else {
         if(data <= node.data)
            node.left = insert(node.left, data);
         else
            node.right = insert(node.right, data);
      }
      return node;
   }


   private boolean search(BSTNode r, int val) {
      boolean found = false;
      while ((r != null) && !found) {
         int rval = r.data;
         if(val < rval)
            r = r.left;
         else if (val > rval)
            r = r.right;
         else {
            found = true;
            break;
         }
         found = search(r, val);
      }
      return found;
   }


   void printTree(BSTNode node, String prefix) {
      if(node == null)
         return;
      printTree(node.left , " " + prefix);
      System.out.println(prefix + "--" + node.data);
      printTree(node.right , prefix + " ");
   }

   public static void main(String args[]) {
      Scanner sc = new Scanner(System.in);
      BST bst = new BST();
      root = bst.insert(root, 55);
      root = bst.insert(root, 20);
      root = bst.insert(root, 90);
      root = bst.insert(root, 80);
      root = bst.insert(root, 50);
      root = bst.insert(root, 35);
      root = bst.insert(root, 15);
      root = bst.insert(root, 65);
      bst.printTree(root, " ");
      System.out.println("Element found = " + bst.search(root, 80));
   }
}
```



