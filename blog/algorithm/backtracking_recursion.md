# 1. Thuật toán đệ quy

## 1.1. Khái niệm

Ta gọi một đối tượng là đệ quy (recursion) nếu nó được định nghĩa qua chính nó hoặc một đối tượng cùng dạng với chính nó bằng quy nạp.

Nếu một bài toán P có lời giải được thực hiện bằng một bài toán con `P′` có dạng giống P thì đó là một giải thuật đệ quy.

Một bài toán đệ quy có lời giải gồm 2 phần:

- Phần neo/trường hợp cơ sở (anchor/base case): Đây là phần có thể giải trực tiếp mà không cần phải dựa vào một bài toán con nào, và cũng chính là điểm dừng của lời giải đệ quy. Phần này thường là các trường hợp cụ thể, như x == 0, x == n, …
- Phần đệ quy: Đây chính là phần mà bạn phải gọi ra bài toán con và giải nó, cũng chính là gọi hàm đệ quy. Phần này sẽ được thực hiện đến khi nào bài toán đưa được về trường hợp cơ sở.

## 1.2. Ví dụ

### 1.2.1. Bài toán tính giai thừa

```java
int factorial(int n)
{
    if (n == 0) return 1;    //trường hợp cơ sở
    return factorial(n - 1) * n;    //phần đệ quy
}
```
Ví dụ:
Với n!thì ta có n!=(n−1)!×n

<img src="blog/algorithm/img/backtracking1.png" style="display: block; margin-right: auto; margin-left: auto;">

### 1.2.2. Bài toán fibonaci

```java
void fibo(int n)
{

    if (n == 0) return 0;    //trường hợp cơ sở
    if (n == 1) return 1;    //trường hợp cơ sở
    Integer number = fibo(n - 2) + fibo(n - 1);
    System.out.println("{} ", number);
    return number;    //phần đệ quy
}
```

# 2.Thuật toán quy lui

## 2.1. Khái niệm

Thuật toán quay lui (backtracking) dùng để giải bài toán liệt kê các cấu hình. Mỗi cấu hình được xây dựng bằng cách xây dựng từng phần tử, mỗi phần tử được chọn bằng cách thử tất cả các khả năng.

Tóm gọn lại, chúng ta đang xây dựng một danh sách gồm tất cả các tập hợp (hay dãy, …), mà mỗi phần tử được xét tất cả các trường hợp có thể của nó. Phương pháp này cũng gọi là duyệt vét cạn.

**Thuật toán quy lui (Backtracking) dùng để giải bài toán liệt kê các cấu hình. Mỗi cấu hình được xây dựng bằng cách xây dựng từng phần tử, mỗi phần tử được chọn bằng cách thử tất cả các khả năng**

Giả sử cấu hình cần liệt kê có dạng  (x1, x2, x3, ...., xn) khi đó thuật toán quy lui thực hiện qua các bước:

1. xét tất cả các giá trị x1 có thể nhận thử cho x1 lần lượt nhận các giá trị đó. Với mỗi giá trị thử gán cho x1 ta sẽ tiến hành bước 2
2. xét tất cả các giá trị x2 có thể nhận thử cho x1 lần lượt nhận các giá trị đó. Với mỗi giá trị thử gán cho x2 ta sẽ tiến hành các khả năng của x3 ... cứ tiếp tục đến xn

Mã giả (Mô hình thuật toán tổng quát như sau)

```java
void try(int i) {
    for (v : {tập các giá trị V mà có thể gắn cho x[i]}) {
        x[i] = v;
        if (i==n) {
            return cấu hình tìm đc;
        } else {
            mark[v] = true; //  ghi nhận việc x[i] nhận giá trị v
            try(i+1);
            mark[v] = false; // bỏ việc ghi nhận x[i] nhận giá trị v 
        }
    }
}


void backtrack(int pos)
{	
    // Trường hợp cơ sở
    if (<pos là vị trí cuối cùng>)
    {
        <output/lưu lại tập hợp đã dựng nếu thoả mãn>
        return;
    }
	
    //Phần đệ quy
    for (<tất cả giá trị i có thể ở vị trí pos>)
    {
        <thêm giá trị i vào tập đanh xét>
        backtrack(pos + 1);
        <xoá bỏ giá trị i khỏi tập đang xét>
    }
}
```

## 2.2. Liệt kê các dãy nhị phân độ dài n (bài toán 4 của [Exhaustive search](blog-post-1.html?algorithm=exhaustive_search))

**Ý tưởng**
```C++
C++
int N;
int x[100];

void backtrack(int i) {
    for (int v=0;  v<=1; ++v) {
        x[i] = v;
        if (i==N) {
            print(x);
        } else {
            backtrack(v);
        }
    }
}
```

<img src="blog/algorithm/img/backtracking.png" style="display: block; margin-right: auto; margin-left: auto;">

**Example:**

```C++
C++
int N;
int x[100];
 
void in(int x[]){
    for (int i = 1; i <= N; i++)
        cout << x[i];
    cout << endl;
}
 
void deQuy(int i){
    for (int j = 0; j <= 1; j++){
        x[i] = j;
        if (i == N)
            in(x);
        else
            deQuy(i + 1);
        
    }
}
 
int main(){
    cin >> N;
    deQuy(1);
}
```

```java
private Integer N;
int[] x;

@GetMapping("/test")
public void test(@RequestParam int n) {
    this.N = n;
    x = new int[n]; // x =[0,0,1]
    this.tryFunc(0);
}

// i là số phấn tử của 1 đối tượng cần in ra
private void tryFunc( int i) {
    for (int v=0;  v<=1; v++) {
        x[i] = v;
        if (i==N-1) {
            System.out.println(Arrays.toString(x));
        } else {
            tryFunc(i+1);
        }
    }
}

GET http://localhost:8080/test?k=3

```

## 2.3. Liệt kê các tập con k phần tử tăng dần (bài toán 2 của [Exhaustive search (Vét cạn)](blog-post-1.html?algorithm=exhaustive_search))

Để liệt kê k phần tử của tập {1, 2, 3, ..., n} ta có thể đưa về liệt kê  các cấu hình (x1, x2, x3, ... x(k)) với x1 < x2 < x3 < ... < x(k)

ta có nhận xét:
- x(k) <= n
- x(k-1) < x(k)-1 < n-1
- x(i) < n-k+1
=> x(i-1) +1 <= x(i) < n-k+i (1<=i<=k)

như vậy, x1 từ 1 (`x0+1`) đến `n-k+1`, với mỗi giá trị đó xét tất cả các lựa chọn của x2 từ `x1+1` đế `n-k+2`

**Ý tưởng**

```java
int k;
int[] x;

void backtrack(int i) {
    for (int v=x[i-1]+1; v<=n-k+i; v++) {
        x[i]=v;
        if (i ==k) {
            print(x);
        } else {
            backtrack(i+1);
        }
    }
}
```

**Example:**

```C++
C++
int k;
int n;
int c[100];
int x[100];
 
void in(int x[]){
    for (int i = 1; i <= n; i++)
        cout << x[i];
    cout << endl;
}
 
void deQuy(int i){
    for (int v=x[i-1]+1; v<=n-k+i; v++) {
        x[i] = j;
        if (i == k)
            in(x);
        else
            deQuy(i + 1);
    }
}
```
```java
java
private Integer k;
private Integer n;
int[] x;

@GetMapping("/test")
public void test(@RequestParam int k, @RequestParam int n) {
    this.k = k; // số lượng phần tử trong 1 element kết quả
    this.n = n; // số lượng phần tử cho từ {1, 2, 3, ... n}
    x = new int[k];
    this.tryFunc(0);
}

private void tryFunc(int i) {
    for (int v=x[i-1 < 0 ? 1 : i-1]+1;  v<=n-(k-1)+i; v++) {
        x[i] = v;
        if (i == k-1) {
            System.out.println(Arrays.toString(x));
        } else {
            tryFunc(i + 1);
        }
    }
}

GET http://localhost:8080/test?k=3&n=5

result:
[1, 2, 3]
[1, 2, 4]
[1, 2, 5]
...
[2, 4, 5]
[3, 4, 5]
```

## 2.4. Liệt kê các tập con k phần tử có trùng nhau (mở rộng)

**Example:**

```C++
C++
int k;
int n;
int c[100];
int x[100];
 
void in(int x[]){
    for (int i = 1; i <= k; i++)
        cout << x[i];
    cout << endl;
}
 
void deQuy(int i){
    for (int j = 0; j <= n; j++){
    // for (v : values){
    //   x[i] = v;
        x[i] = j;
        if (i == k)
            in(x);
        else
            deQuy(i + 1);
    }
}
 
int main(){
    cin >> N;
    deQuy(1);
}
```

```java
java
private Integer n;
private Integer k;
int[] x;

@GetMapping("/test")
public void test(@RequestParam int n, @RequestParam int k) {
    this.n = n; // số lượng phần tử trong 1 element kết quả
    this.k = k; // số lượng phần tử cho từ {1, 2, 3, ... n}
    x = new int[k];
    this.tryFunc(0);
}

private void tryFunc(int i) {
    for (int v=1;  v<=n; v++) {
        x[i] = v;
        if (i == k-1) {
            System.out.println(Arrays.toString(x));
        } else {
            tryFunc(i + 1);
        }
    }
}

    GET http://localhost:8080/test?k=3&n=5

result:
[1, 1, 1]
[1, 1, 2]
[1, 1, 3]
[1, 1, 4]
...
[5, 5, 4]
[5, 5, 5]
```

## 2.5. Liệt kê các tập con k phần tử không lặp (bài toán 3 của [Exhaustive search (Vét cạn)](blog-post-1.html?algorithm=exhaustive_search))

Để có thể liệt kê các tập con k phần tử không lặp thì hàm tryFunc(i) có quyền xét tất cả các khả năng chọn từ 1 đến n mà các giá trị này chưa bị các phần tử đứng trước chọn
- ta khai báo 1 mảng `c` kiểu boolean để đánh dấu giá trị i đã bị chọn hay chưa.

**Ý tưởng**

```java
private void tryFunc(int i) {
    for (int v=1;  v<=n; v++) {
        if (Objects.isNull(c[v]) || c[v]) {
            x[i] = v;
            if (i == k-1) {
                System.out.println(Arrays.toString(x));
            } else {
                c[v]= false; // đánh dấu v đã được dùng không sử dụng nữa
                tryFunc(i + 1);
                c[v]= true; // bỏ đánh dấu v đã được dùng để sử dụng lại
            }
        }
    }
}
```


**Example:**

```C++
C++
 
int k;
int n;
int c[100];
int x[100];
 
void in(int x[]){
    for (int i = 1; i <= k; i++)
        cout << x[i];
    cout << endl;
}
 
void deQuy(int i){
    for (int j = 0; j <= n; j++){
        x[i] = j;
        if (i == k)
            in(x);
        else
            deQuy(i + 1);
    }
}
 
int main(){
    cin >> N;
    deQuy(1);
}
```
```java
private Integer k;
private Integer n;
int[] x;
Boolean[] c;

@GetMapping("/test")
public void test(@RequestParam int k, @RequestParam int n) {
    this.k = k; // số lượng phần tử trong 1 element kết quả
    this.n = n; // số lượng phần tử cho từ {1, 2, 3, ... n}
    x = new int[k]; // init
    c = new Boolean[1]; // init
    this.tryFunc(0);
}

private void tryFunc(int i) {
    for (int v=1;  v<=n; v++) {
        if (Objects.isNull(c[v]) || c[v]) {
            x[i] = v;
            if (i == k-1) {
                System.out.println(Arrays.toString(x));
            } else {
                c[v]= false;
                tryFunc(i + 1);
                c[v]= true;
            }
        }
    }
}

    GET http://localhost:8080/test?k=3&n=5

result :
[1, 2, 3]
[1, 2, 4]
[1, 2, 5]
...
[5, 4, 2]
[5, 4, 3]

```

## 2.6. Liệt kê các hoán vị (bài toán 1 của [Exhaustive search (Vét cạn)](blog-post-1.html?algorithm=exhaustive_search))

Bài toán hoán vị chính là bài toán  liệt kê các chỉnh hợp vs n=k. 

**Ý tưởng**

```java
private void tryFunc(int i) {
    for (int v=1;  v<=n; v++) {
        if (Objects.isNull(c[v]) || c[v]) {
            x[i] = v;
            if (i == N-1) {
                System.out.println(Arrays.toString(x));
            } else {
                c[v]= false; // đánh dấu v đã được dùng không sử dụng nữa
                tryFunc(i + 1);
                c[v]= true; // bỏ đánh dấu v đã được dùng để sử dụng lại
            }
        }
    }
}
```

**Example:**

```java
private Integer k;
int[] x;
int[] n = {1,4,5,8,9};
Boolean[] c;

@GetMapping("/test")
public void test(@RequestParam int k) {
    this.k = k; // số lượng phần tử trong 1 element kết quả
    x = new int[k]; // init
    c = new Boolean[6]; // init
    this.tryFunc(0);
}

private void tryFunc(int i) {
    for (int v=0;  v<n.length; v++) {
        if (Objects.isNull(c[v]) || c[v]) {
            x[i] = n[v];
            if (i == k-1) {
                System.out.println(Arrays.toString(x));
            } else {
                c[v]= false;
                tryFunc(i + 1);
                c[v]= true;
            }
        }
    }
}

    GET http://localhost:8080/test?k=3

int[] n = {1,4,5,8,9};

result:

[1, 4, 5]
[1, 4, 8]
[1, 4, 9]
[1, 5, 4]
....
[9, 5, 8]
[9, 8, 1]
[9, 8, 4]
[9, 8, 5]
```


**Ưu điểm**: Việc quay lui là thử tất cả các tổ hợp để tìm được một lời giải. Thế mạnh của phương pháp này là nhiều cài đặt tránh được việc phải thử nhiều trường hợp chưa hoàn chỉnh, nhờ đó giảm thời gian chạy.

**Nhược điểm**: Trong trường hợp xấu nhất độ phức tạp của quay lui vẫn là cấp số mũ. Vì nó mắc phải các nhược điểm sau:

- Rơi vào tình trạng "thrashing": qúa trình tìm kiếm cứ gặp phải bế tắc với cùng một nguyên nhân.
- Thực hiện các công việc dư thừa: Mỗi lần chúng ta quay lui, chúng ta cần phải đánh giá lại lời giải trong khi đôi lúc điều đó không cần thiết.
- Không sớm phát hiện được các khả năng bị bế tắc trong tương lai. Quay lui chuẩn, không có cơ chế nhìn về tương lai để nhận biết đc nhánh tìm kiếm sẽ đi vào bế tắc.


## 2.7. Sinh các dãy nhị phân

Bài toán: Liệt kê tất cả các dãy nhị phân độ dài n, là dãy có tất cả n ký tự và gồm toàn các ký tự 0 và 1. Ví dụ, với n=3 ta có các dãy 000,001,010,011,100,101,110,111.

<img src="blog/algorithm/img/backtracking2.png" style="display: block; margin-right: auto; margin-left: auto;">

Tại hàm `gen(1)`, ta xét từng giá trị của ký tự hiện tại, sau đó gọi `gen(2)` với từng ký tự đó. Tương tự như vậy, ta gọi `gen(3)` từ các ký tự ở `gen(2)` và rồi `gen(4)`. Tới `gen(4)`, ta đã duyệt hết các vị trí và không thể thử thêm nữa, nên có thể in ra xâu.


```C++
int n;
string curString;

void genString(int pos) {
    if (pos > n)
    {
        cout << curString << "\n";
        return;
    }
    for (char i = '0'; i <= '1'; i ++)
    {
        curString.push_back(i);    //thêm ký tự mới vào dãy
        genString(pos + 1);
        curString.pop_back();      //bỏ ký tự này đi
    }
}

int main() {
    cin >> n;
    curString = "";
    genString(1);

    return 0;
}
```


