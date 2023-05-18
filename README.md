# _Đệ quy_ và thuật toán _đệ quy (Recursion)_

## Đệ quy

### Bài toán

Chứng minh đẳng thức sau đúng $\forall n \in N^*$:
$1 + 3 + 5 + ... + (2n - 1) = n^2$
**Bài giải**
Để chứng minh bài toán này ta sử dụng phương pháp quy nạp toán học.

  <details>
  <summary>Chứng minh</summary>

- Bước 1: Chứng minh đẳng thức đúng với $n=1$
  Ta thấy: $1=1^2 \Rightarrow$ đẳng thức đúng với $n=1$
- Bước 2: Giả sử đẳng thức đúng với $n=k$ $(k\geqslant1)$
  $\Rightarrow 1 + 3 + 5 + ... + (2k - 1) = k^2$
- Bước 3: Chứng minh đẳng thức đúng với $n=k+1$
Ta có:
$1 + 3 + 5 + ... + [2(k+1) - 3] + [2(k + 1) - 1]$
$= 1 + 3 + 5 + ... + (2k + 2 - 3) + (2k + 2 - 1)$
$= 1 + 3 + 5 + ... + (2k -1) + (2k +1)$
$=k^2 + 2k +1$
$= (k+1)^2 \Rightarrow đpcm$.
$\rightarrow$ Phương pháp này đã sử dụng tính chất **đệ quy** để giải quyết bài toán.
</details>

### Thế đệ quy là gì?

_Định nghĩa:_ Đệ quy (recursion) là phương pháp dùng trong các chương trình máy tính trong đó có một hàm tự gọi chính nó.
Một bài toán $P$ được gọi là có tính chất đệ quy khi lời giải của nó có thể đưa về bài toán nhỏ hơn là $P'$ có dạng giống nó, đồng thời lời giải của $P'$ không liên quan tới $P$. Bản chất của đệ quy là phân tách bài toán lớn thành những bài toán nhỏ hơn nó và kết hợp nó lại để giải bài toán lớn ban đầu.

### Công thức truy hồi

Để giải quyết một bài toán đệ quy cần phải thực hiện 2 nhiệm vụ là:

- Tìm lời giải cho bài toán cơ sở
- Kết hợp lời giải của những bài toán cơ sở để giải quyết bài toán lớn
  Ví dụ: - Dãy số $u_{n}$ với công thức truy hồi:
  $u_{n} = 2 \times u_{n-1}$ $(n\geqslant1)$
  với cơ sở $u_{1} = 1$ - _Dãy số Fibonacci_ có công thức truy hồi:
  $f_{n}=f_{n-1} + f_{n-2}$ $(n\geqslant1)$
  với hai cơ sở: $f_{0} =0, f_{1} = 1$

## Thuật toán _đệ quy_

### Hàm đệ quy

Hàm đê quy giống như một vòng lặp, nó lặp đi lặp lại cho đến khi ra kết quả hoặc là lặp vô hạn.
Một hàm đệ quy gồm _2 phần_:

- Phần cơ sở: Điều kiện thoát khỏi đệ quy, nếu không có thì đệ quy sẽ lặp đi lặp lại vô hạn gây tr n _bộ nhớ stack_.
- Phần đệ quy: Thân hàm chứa phần gọi đệ quy cho đến khi thỏa mãn điều kiện của phần cơ sở.
  Ví dụ:

```
<tên_hàm>(<danh_sách_tham_số>) {
    if (<điều kiện thoát>) {
        return <giá_trị>;
    } else {
        // thực hiện đệ quy
        <tên_hàm>(<danh_sách_tham_số>);
    }
}
```

### Ví dụ 1: Dãy Fibonacci

- Công thức: $f_{n}=f_{n-1} + f_{n-2}$
- <details>
  <summary>Mã giả</summary>

  ```
  fib(n) {
    if (n <= 2) return 1;
    else return fib(n-1) + fib(n-2);
  }
  ```

  </details>

- <details>
  <summary>Cài đặt <i>(C++)</i>:</summary>

  ```
  long long fib(long long n) {
    if (n <= 2) {
      return 1;
    }
    return fib(n-1) + fib(n-2);
  }
  ```

  </details>

- Bất biến của thuật toán trên là nếu đầu vào của hàm fib(n) là một số nguyên không âm n, thuật toán sẽ luôn trả về kết quả là số Fibonacci thứ n. Tuy nhiên, nếu đầu vào là một số nguyên âm, kết quả trả về từ thuật toán sẽ không tương ứng với số Fibonacci thực sự tại vị trí đó, và bất biến này không còn đúng nữa.
- Độ phức tạp của thuật toán trên là O(2^n): Mỗi lần đệ quy sẽ tạo ra hai nhánh đệ quy mới, và các nhánh đệ quy này sẽ tiếp tục tạo ra những nhánh đệ quy mới cho đến khi n đạt đến điều kiện dừng. Vì vậy, số lần đệ quy được gọi sẽ là 2^n.
- <details>
  <summary>Cải tiến bằng thuật toán khác</summary>

  ```
  long long fib(int n) {
    long long f[n+1];
    f[0] = f[1] = f[2] = 1;
    for (int i = 3; i <= n; i++) {
      f[i] = f[i-1] + f[i-2];
    }

  return f[n];
  }
  ```

  Độ phức tạp của thuật toán là O(n)
  </details>

### Ví dụ 2: Tính ước chung lớn nhất

- <details>
    <summary>Mã giả</summary>

  ```
  gcd(a, b) {
    if (b == 0) return a;
    else return gcd(b, a mod b);
  }
  ```

  </details>

- <details>
    <summary>Cài đặt <i>(C++)</i>:</summary>
    
    ```
    long long gcd(long long a, long long b) {
      return (b == 0) ? a : gcd(b, a % b);
    }
    ```
  </details>

- Bất biến của thuật toán trên là nếu ta gọi d là ước chung lớn nhất của a và b, thì d cũng là ước chung lớn nhất của b và a % b.
- Độ phức tạp của thuật toán là O(log min(a, b))

### Bài toán 1: Tháp Hà Nội (Hanoi Tower)

**Đề bài**: Tháp Hà Nội bao gồm ba thanh dọc (hoặc chốt hoặc tháp) và một số đĩa có kích thước khác nhau có thể trượt lên bất kỳ thanh nào.
Câu đố bắt đầu với các đĩa trên một thanh theo thứ tự tăng dần về kích thước, nhỏ nhất ở trên cùng, do đó tạo thành hình nón.
<img src="https://genk.mediacdn.vn/2017/photo-1-1488855314632.png" alt="Hình ảnh minh họa bài toán tháp hà nội">
Mục tiêu của câu đố là di chuyển toàn bộ ngăn xếp sang một thanh khác, thỏa mãn các quy tắc sau:
Mỗi lần chỉ có thể di chuyển một đĩa.
Mỗi bước di chuyển bao gồm việc lấy đĩa trên từ một trong các thanh và đặt nó lên một thanh khác, lên trên các đĩa khác có thể đã có trên thanh đó.
Không có đĩa nào có thể được đặt trên đĩa nhỏ hơn.

**Ý tưởng:**

- Di chuyển n - 1 đĩa trên cùng từ Nguồn đến tháp Phụ
- Di chuyển đĩa thứ n từ Nguồn đến tháp Đích
- Di chuyển n - 1 đĩa từ tháp Phụ đến tháp Đích.
- Việc chuyển n-1 đĩa trên cùng từ Nguồn sang Tháp phụ một lần nữa có thể được coi là một vấn đề mới và có thể được giải quyết theo cách tương tự. Khi chúng ta giải được bài toán bằng ba đĩa, chúng ta có thể giải nó với bất kỳ số đĩa nào bằng thuật toán trên.

<details>
  <summary>Mã giả</summary>

```
  solve(n, source, destination, extra) {
    if (n==1) {
      print move from source to destination
    }
    solve(n-1, source, extra, destination);
    print move from source to destination;
    solve(n-1, extra, destination, source);
  }

```

</details>

<details>
  <summary>Cài đặt <i>(C++)</i>:</summary>

```
  void solve(int n, char source, char destination, char extra){
    if (n == 1) {
      cout << "Move from " << source << " to " << destination << endl;
    }
    solve(n-1, source, extra, destination);
    cout << "Move from " << source << " to " << destination << endl;

    solve(n-1, extra, destination, source);
  }

```

</details>
