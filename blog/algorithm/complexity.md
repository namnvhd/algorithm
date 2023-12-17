# Complexity

## Định nghĩa

Làm thế nào để đánh giá 1 chương trình thực hiện tốt / hiệu quả hay không?

Cần **2 tham số** để đánh giá:

1. **Bộ nhớ (Space complexity)**
2. **Thời gian(Time complexity)**

### _1. Bộ nhớ (Space complexity)_

Là bộ nhớ mà chương trình / thuật toán cần sử dụng khi thực thi / run chương trình đó

**_Note: Thường có độ ưu tiên thấp hơn time complexity_**

- O(1): Nếu chỉ sử dụng 1 bộ nhớ cố định
- O(n), O(n<sup>2</sup>) ... : Thay đổi theo input bài toán

Mục tiêu: tìm ra 1 phương án tối ưu `về mặt bộ nhớ` cho 1 vấn đề nào đó

**Ví dụ**: Cho 1 mảng các chữ số. Dịch chuyển hết các số = 0 về cuối.

Input: [1,0,3,0,4,5,2]

Output: [1, 3, 4, 5, 2, 0, 0]

- O(1):

```python
def sum(arr):
    sum = 0
    for x in arr:
        sum += x
    return sum

Space complexity: O(1)
```
Ở ví dụ trên ta chỉ tạo 1 biến "sum" và biến sum này ko bị phụ thuộc vào số lượng biến của mảng arr.

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int n = nums.length;
        int curIndex = 0;
        if (n ==1) return;
        for (int i = 0; i < n; i++) {
            if (nums[i] != 0) {
                nums[curIndex++] = nums[i];
                if (i != curIndex - 1) {
                    nums[i]=0;
                }
            }
        }
    }
}
```
- O(n)

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int n = nums.length;
        int[] T = new int[n];
        int iT = 0;
        if (n ==1) return;
        for (int i = 0; i < n; i++) {
            if (nums[i] != 0) {
                T[iT++] = nums[i];
            }
        }

        for (int i = 0; i < n; i++) {
            nums[i] = T[i];
        }
    }
}
```

Như vậy ta có thể thấy rằng cách 1 ta ko cần khai báo thêm thông tin bộ nhớ (không mảng phụ) mà sử dụng chính mảng nums còn cách 2 ta thêm 1 mảng phụ T để thực hiện lưu các biến != 0 rồi ghi lại vào mảng nums.

### _2. Thời gian(Time complexity)_

Là định nghĩa 1 khoảng thời gian để thực hiện thuật toán, hàm, chương trình.

**_Note: Thường có độ ưu tiên cao hơn space complexity. Tức là nếu ta tăng thêm biến (tăng space complexity) để giảm thời gian thực hiện thì vẫn tốt hơn để time complexity quá lớn_**

- O(1):

```python
def sum(a, b):
    return a+b

Time complexity: O(1) - constant
```

- O(n)

Với bài tính tổng: ta phải đi qua tất cả các phần tử của mảng arr được truyền vào nên tốn chi phí thời gian = số lượng phần tử của mảng

```python
def sum(arr):
    sum = 0
    for x in arr:
        sum += x
    return sum

Time complexity: O(n) - linear
```
<img src="blog/algorithm/img/complexity0.png" style="display: block; margin-right: auto; margin-left: auto;">

<img src="blog/algorithm/img/complexity.png" style="display: block; margin-right: auto; margin-left: auto;">

<img src="blog/algorithm/img/complexity3.png" style="display: block; margin-right: auto; margin-left: auto;">

## 3. Cách tính complexity

```python
def find_one(arr):
    for x in arr:               # O(n)
        if x == 1:              # O(1)
            return true
    return false

# total = O(n) * O(1) = O(n)
```

```python
for m in range(1, n):                   # O(n)
    for x in range(1, m):               # O(m)
        print(f"Hello {i}-{j}")

# total = O(n) * O(m) = O(n * m)

a = 0
for m in range(1, n):                   # O(n)
    for x in range(m, i, -1):           # O(m)
        a = a + i + j

# total = O(n) * O(m) = O(n * m)
```

- Làm sao để biết 1 chương trình chạy nhanh hay chậm?
- làm sao miêu tả mức ododj nhanh chậm của 1 chương trình?

=> **_Big O notation_**

Định nghĩa: độ phức tạp (về thời gian) là tổng thời gian / số phép tính mà chương trình cần thực hiện.

```python
n=10
x=1
y=2
z=0
t=0
for i in range(n):
    for k in range(n)
        z = x+y
        t = x-y
```

Ở đây số phép tính sẽ là số thời gian thực hiện chương trình. vì mỗi phép tính sẽ tốn 1 lượng circle của CPU nên tương đương

<img src="blog/algorithm/img/complexity4.png" style="display: block; margin-right: auto; margin-left: auto;">

## [Reference youtube video](https://www.youtube.com/watch?v=-JQo4KRZzhE)





<img src="blog/algorithm/img/complexity1.png" style="display: block; margin-right: auto; margin-left: auto;">
<img src="blog/algorithm/img/complexity2.png" style="display: block; margin-right: auto; margin-left: auto;">



https://www.youtube.com/watch?v=BgLTDT03QtU&ab_channel=NeetCode


Ref: https://viblo.asia/p/do-phuc-tap-thuat-toan-anh-huong-cua-o-lon-toi-performance-Ljy5VdjMZra