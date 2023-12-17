# Ngăn xếp (stack)

## 1. Khái niệm

Stack là một danh sách được bổ sung 2 thao tác: thêm một phần tử vào cuối danh sách, và loại bỏ một phần tử ở cuối danh sách. Ví trí cuối của Stack được gọi là đỉnh (top).

Stack hoạt động theo nguyên tắc LIFO (Last In - First Out, hay vào sau - ra trước).

# Note: Hay đc sử dụng trong bài toán DFS (Depth first search)

<img src="blog/algorithm/img/stack1.png" style="display: block; margin-right: auto; margin-left: auto;">


## 2. Cài đặt

### 2.1 Cài đặt thủ công

```C++
int st[MAXN];
int top = 0;

void push(int x) // thêm x vào cuối Stack
{
    ++top;
    st[top] = x;
}

void pop() // loại bỏ phần tử ở cuối Stack
{
    assert(top); // đảm bảo Stack đang chứa ít nhất 1 phần tử
    --top;
}

int peek() // trả về giá trị của phần tử ở đỉnh Stack
{
    return st[top];
}
```
### 2.2 Sử dụng thư viện

```
C++
    stack<int> st;
    st.push(5); // thêm 5 vào stack
    st.push(10); // thêm 10 vào stack
    cout << st.top() << endl; // In ra 10
    st.pop(); // loại bỏ phần tử ở cuối
    cout << st.top() << endl; // In ra 5
    return 0;

Java
    Stack<Integer> stack = new Stack<Integer>();
    stack.put(2);
    stack.put(10);
    stack.pop(); // Lấy ra 10
    stack.peek(); // In ra đỉnh của stack - in ra 2
    stack.put(5);
    stack.peek(); // In ra đỉnh của stack - in ra 5
    stack.pop(); // Lấy ra 5
    stack.peek(); // In ra đỉnh của stack - in ra 2
```
<img src="blog/algorithm/img/stack2.png" style="display: block; margin-right: auto; margin-left: auto;">

### 2.3 Độ phức tạp

- Time complexity: O(1)
- Space complextity: O(N) - do có N phần tử đưa vào stack


## 3. Ví dụ

Cho xâu S chỉ gồm các số nguyên dương và các dấu +, −, ×, ÷, trong S không có dấu khoảng trống. Bạn cần tính giá trị của biểu thức được biểu diễn bởi xâu đó.


```C++
// xử lý toán tử và cập nhật trực tiếp vào mảng val
void process_op(vector<int>& val, char op)
{
    // l, r là 2 toán hạng, op là dấu giữa chúng
    int r = val.back(); val.pop_back();
    int l = val.back(); val.pop_back();
    switch(op)
    {
    case '+':  val.push_back(l + r); break;
    case '-': val.push_back(l - r); break;
    }
}

// tính giá trị của biểu thức biểu diễn bởi s
int evaluate(string s)
{
    vector<int> val;
    vector<char> op;
    for (int i = 0; i < (int)s.size(); ++i)
    {
        if (isdigit(s[i]))
        {
            int number = 0; // giá trị của toán hạng đang xét
            while (i < (int)s.size() && isdigit(s[i]))
            {
                number = number * 10 + s[i] - '0';
                ++i;
            }
            val.push_back(number);
            --i; // cẩn thận với index!
        }
        else
        {
            if (!op.empty())
            {
                process_op(val, op.back()); // xử lý biểu thức từ trái sang phải
                op.pop_back();
            }
            op.push_back(s[i]);
        }
    }
    
    if (!op.empty())
    {
        process_op(val, op.back());
        op.pop_back();
    }

    return val.back();
}
```





