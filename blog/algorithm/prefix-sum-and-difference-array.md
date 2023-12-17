# Mảng cộng dồn và mảng hiệu (prefix sum and difference array)

## 1. Mảng cộng dồn (prefix sum)

Là tạo ra 1 mảng mới có các phần tử là cộng dồn của các phần tử trước đó từ mảng gốc đến vị trí hiện tại

Cho mảng A

Thông thường nếu S<sub>0</sub> = 0 thì S<sub>i</sub> = S<sub>i-1</sub> + A<sub>i-1</sub>

<img src="blog/algorithm/img/prefix-sum-and-difference-array1.png" style="display: block; margin-right: auto; margin-left: auto;">

### 2. Cài đặt mảng cộng dồn

``` C++
C++

vector<int> buildPrefixSum(const vector<int>& a, int C = 0) {
    int n = (int)a.size();
    vector<int> prefixSum(n + 1);

    prefixSum[0] = C;

    for (int i = 0; i < n; i++)
        prefixSum[i + 1] = prefixSum[i] + a[i];

    return prefixSum;
}

Java

List<Integer> buildPrefixSum(List<Integer> A) {
    int n = (int)a.size();
    List<Integer> prefixSum = new ArrayList();

    prefixSum.add(0);

    for (int i = 0; i < n; i++) {
        prefixSum.add(prefixSum.get(i) + A.get(i));
    }

    return prefixSum;
}
```

Ví dụ: Tìm tổng lớn nhất của chuỗi [-1 3 -2 5 3 -5 2 2]

```C++
int n, a[MAXN];
long long prefSum[MAXN], prefMin[MAXN], ans = 0;

int main() {
    cin >> n;
    for (int i = 1; i <= n; i++) cin >> a[i];
    prefSum[0] = prefMin[0] = 0;
    for (int i = 1; i <= n; i++)
      prefSum[i] = prefSum[i - 1] + a[i], prefMin[i] = min(prefMin[i - 1], prefSum[i]);
    for (int i = 1; i <= n; i++)
        ans = max(ans, prefSum[i] - prefMin[i - 1]);
    cout << ans;
}
```

## 3. Mảng hiệu (difference array)

Là tạo ra 1 mảng mới có các phần tử là hiệu của các phần tử trước đó từ mảng gốc đến vị trí hiện tại

Cho mảng A

Thông thường nếu S<sub>0</sub> = 0 thì S<sub>i</sub> = A<sub>i+1</sub> - A<sub>i</sub>

<img src="blog/algorithm/img/prefix-sum-and-difference-array2.png" style="display: block; margin-right: auto; margin-left: auto;">

### 4. Cài đặt mảng hiệu


```C++
vector<int> buildDifferenceArray(const vector<int>& a) {
    int n = (int)a.size();

    vector<int> differenceArray(n - 1);

    for (int i = 0; i < n - 1; i++)
        differenceArray[i] = a[i + 1] - a[i];

    return differenceArray;
}
```

## 5. Tính chất
### Độ dài mảng
- Đối với mảng cộng do phần tử đầu là 0 nên mảng tổng sẽ nhiều hơn mảng gốc 1 phần tử
- Đối với mảng hiệu thì lại ít hơn mảng gốc 1 phần tử

### Tính riêng biệt

- 1 mảng A bất kỳ ta sinh đc vô hạn mảng cộng dồn (chỉ khác ở hệ số c)
- 1 mảnh A sinh ra chỉ đc 1 mảng hiệu

### Liên hệ mảng cộng dồn và mạng hiệu

Từ mảng cộng dồn và mảng hiệu ta có thể suy ngược lại mảng gốc. Nhưng với mảng hiệu ta cần biết A[0]

- S(A0,D(A))=A
- D(S(c,A))=A với mọi c thực

