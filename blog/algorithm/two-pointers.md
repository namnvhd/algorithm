# Hai con trỏ

## Bài toán 1: lặp trên 1 đối tượng

1. 1 con trỏ bắt đầu ở chỉ số đầu, con trỏ còn lại ở chỉ số cuối
2. Sử dụng vòng lặp while cho đến khi 2 con trỏ dừng ở cùng 1 chỉ số
3. Di chuyển con trỏ này tới con trỏ kia trong mỗi vòng lặp


<img src="blog/algorithm/img/twoPointer.png" style="display: block; margin-right: auto; margin-left: auto;">

**Mã giả:**

```python
function fn(arr):
    left = 0
    right = arr.length - 1

    while left < right:
        do some logic here depending on the problem
        do some more logic here to decide on 1 of following:
            1. left++
            2. right--
            3. both left++ and right--
```

### **Ví dụ: Bài toán palindrome: Viết hàm trả về true nếu chuỗi là palindrome còn không trả về false**
```text
Example: tekket => true

tekkea => false

abccab => false

azr => false
```

```java
public boolean isPalindrome(String s) {
    
    int left = 0;
    s = s.replaceAll("[^a-zA-Z0-9]", "");
    System.out.println("test: " + s);
    System.out.println("length string: " + s.length());
    if (s.length() == 0) return true;

    int right = s.length() - 1;

    while (left<=right) {
        if (Character.toLowerCase(s.charAt(left)) == Character.toLowerCase(s.charAt(right))) {
            left ++;
            right--;
        } else {
            return false;
        }
    }
    return true;
}
```

Ref: https://leetcode.com/problems/valid-palindrome/


## Phương pháp cửa sổ trượt

1. Xác định cọn trỏ trái và con trỏ phải
2. Lặp lại mảng với con trỏ phải để thêm phần tử vào cửa sổ
3. Trong vòng lặp nếu điều kiện bị phá vỡ thì ta tăng con trỏ trái

<img src="blog/algorithm/img/twoPointer1.png" style="display: block; margin-right: auto; margin-left: auto;">


**Mã giả: **

```python
function fn(arr):
    
    left = 0
    for right in range(0, arr.lenth -1):
        do some logic here to "add" element at arr[right] to window

        while (left < right) AND (conditon from problem not met):
            do some logic to "remove" element at arr[left] from window
            left++
            
        Do some logic to update thi answer
```

### **Ví dụ 1: Bài toán tìm chuỗi dài nhất: cho 1 số nguyên k sao cho tổng <= k**

```text
k=10;
nums = [1, 1, 4, 9, 3, 6, 6, 8]
```

```java
int findMaxLength(List<int> nums, int k) {
    int left = 0;
    int sum = 0;
    int ans = 0;

    for (int right = 0; right < nums.size(); right++) {
        sum += nums[right];
        while (sum > k) {
            sum -= nums[left];
            left++;
        }
        ans = max(ans, right - left + 1);
    }
    return ans;
}
```
### Ví dụ 2: cho 1 chuỗi nhị phân s. độ dài chuỗi con dài nhất chỉ chứa ký tự 1 là bao nhiêu?

```
Example: 
1000111101101
100011
```


```java
int findMaxLength(String s) {
    int left = 0;
    int curr = 0; // tổng số phần tử = 0
    int ans = 0;

    for (int right = 0; right < s.size(); right++) {
        if (s.charAt(right) == '0') {
            curr++;
        }
        while(curr > 1) { // nếu số phân tử 0 liên tiếp lớn hơn 1 thì sẽ dịch chuyển left sang 1 đơn vị
            if (s.charAt(left) == '0') {
                curr--;
            }
            left++;
        }
        ans = max(ans, right - left + 1);
    }
    return ans;
}
```

### Ví dụ 3: Cho 1 mảng nums và 1 số nguyên k. Tìm số lượng mảng con chứa các phần tử mà tích các phân từ < k

```
Example: 
nums = [1, 6, 4, 5, 2]
k = 45

đáp án: 11
[1]
[1, 6]
[1, 6, 4]
[6]
[6, 4]
[4]
[4, 5]
[4, 5, 2]
[5]
[5, 2]
[2]
```


```java
int findMaxArrays(List<Integer> nums, Integer k) {
    int left = 0;
    int curr = 1; // tích của các phần tử tạm tính
    int ans = 0;

    for (int right = 0; right < nums.size(); right++) {
        curr *= nums.get(right);
        while(curr > k) {
            curr /= nums.get(left);
            left++;
        }
        ans += right - left + 1;
    }
    return ans;
}
```



### Ví dụ 4: Cho 1 mảng nums và 1 số nguyên k. Tìm số lượng mảng con có tổng lớn nhất có độ dài k

```
Example: 
nums = [3, 6, 4, -5, 9, -1, 2]
k = 4

đáp án: 4 [3, 6, -5, 9]
```


```java
int findMaxArrays(List<Integer> nums, Integer k) {
    int left = 0;
    int curr = 0; // tổng tạm tính
    int ans = 0;

    for (int right = 0; right < nums.size(); right++) {
        if (right - left + 1 <= k) {
            curr += nums.get(right);
        } else {
            ans = Math.max(ans, curr);
            curr -= nums.get(left);
            left++;
        }
    }
    return ans;
}
```