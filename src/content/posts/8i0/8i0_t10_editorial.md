---
title: Lời giải đề thi tháng 10 lớp 8I0 - Chính
published: 2026-01-03
description: ''
image: ''
tags: [Editorials]
category: 8I0
draft: false
lang: 'vi'
---

# Bài 1: Đồng hồ

## Tóm tắt đề bài

Cho ba số $h, p, s$ thể hiện giờ, phút, giây của một đồng hồ điện tử. Tính $h, p, s$ hiển thị trên màn hình sau $1$ giây.

**Ràng buộc:** $0 \le h \le 23; \ 0 \le p, s \le 59$.

## Lời giải

Chúng ta chỉ cần in ra $h, \ p, \ s+1$. Tuy nhiên, vẫn cần phải xét nhưng trường hợp đặc biệt khi $s=60, \ p = 60, \ h = 24$.

Độ phức tạp: $O(1)$.

<details>
<summary>Code mẫu</summary>

```cpp
#include <bits/stdc++.h>
#pragma GCC optimize("O3, unroll-loops")
#define ll long long
#define ld long double
#define st string

using namespace std;

int h, p, s;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    cin >> h >> p >> s;
    s++;
    if (s == 60) {
        s = 0;
        p++;
    }
    if (p == 60) {
        p = 0;
        h++;
    }
    if (h == 24) {
        h = 0;
    }
    cout << h << " " << p << " " << s;
    return 0;
}

```
</details>

---

# Bài 2: Người vắng mặt

## Tóm tắt đề bài

Cho mảng $a$ gồm $m$ phần tử phân biệt trong khoảng $[1, n]$. In ra những số trong khoảng $[1, n]$ mà không xuất hiện trong mảng theo tứ tự từ bé đến lớn. Nếu không có số như vậy, in ra "HAPPY".

**Ràng buộc:** $1 \le m \le n \le 10^6; \ 1 \le a_i \le n$.

## Lời giải

Chúng ta có thể dễ dàng thấy được nếu $m=n$ thì tất cả các số trong khoảng $[1, n]$ sẽ xuất hiện trong mảng. Từ đó, nếu điều kiện này đúng, chúng ta chỉ cần in ra "HAPPY".

Nếu $m \lt n,$ chúng ta duyệt qua mảng $a$ và dùng mảng đếm để theo dõi những phần tử đã xuất hiện. Sau đó, chúng ta chỉ cần duyệt mảng đếm trong khoảng $[1, n]$ để tìm những số không xuất hiện trong $a,$ rồi sau đó in ra kết quả.

Độ phức tạp: $O(m + n)$.

<details>
<summary>Code mẫu</summary>

```cpp
#include <bits/stdc++.h>
#pragma GCC optimize("O3, unroll-loops")
#define ll long long
#define ld long double
#define st string

using namespace std;

const int N = 1e6 + 1;
int n, m, a, cnt[N];

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    cin >> n >> m;
    if (n - m == 0) {
        cout << "HAPPY";
        return 0;
    }
    while (m--) {
        cin >> a;
        cnt[a]++;
    }
    for (int i = 1; i <= n; i++) {
        if (cnt[i] == 0) {
            cout << i << " ";
        }
    }
    return 0;
}

```
</details>

---

# Bài 3: Dịch cửa sổ

## Tóm tắt đề bài

Cho mảng $a$ gồm $n$ phần tử. Tìm:

$$
\max_{1 \le i \le n-m+1}(\sum_{k=i}^{i+m-1} {(a_k)})
$$

**Ràng buộc:** $1 \le n \le 10^4; \ 1 \le m \le 10^3; \ m \le n; \ |a_i| \le 10^9$.

## Lời giải

### Cách 1:

Chúng ta có thể duyệt hết các chỉ sổ $i$ thoả mãn điều kiện $1 \le i \le n - m + 1$ rồi tính $res=\sum_{k=i}^{i+m-1} {(a_k)}$ rồi cập nhật $ans=\max(ans, \ res)$.

Độ phức tạp: $O(n^2)$ (nếu tính tổng trực tiếp) hoặc $O(n)$ (nếu dùng prefix sum).

<details>
<summary>Code mẫu</summary>

```cpp
#include <bits/stdc++.h>
#pragma GCC optimize("O3, unroll-loops")
#define ll long long
#define ld long double
#define st string

using namespace std;

int n, m;
ll a[10001], s[10001], ans = -1e18;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    cin >> n >> m;
    for (int i = 1; i <= n; i++) {
        cin >> a[i];
        s[i] = s[i - 1] + a[i];
    }
    for (int i = 1; i <= n - m + 1; i++) {
        ans = max(ans, s[i + m - 1] - s[i - 1]);
    }
    cout << ans;
    return 0;
}

```
</details>

### Cách 2:

Chúng ta có thể dùng kỹ thuật cửa sổ trượt (sliding window) để tìm $\max$.

:::note
Kỹ thuật cửa số trượt (sliding window) được áp dụng khi chúng ta tính $res=\sum_{i=1}^{m} {(a_i)}$, rồi với mỗi lần duyệt $i$ thoả mãn điều kiện $2 \le i \le n - m + 1$ (tức là di chuyển cửa sổ từ đoạn $[i-1, \ i+m-2]$ sang đoạn $[i, \ i+m-1]$), chúng ta sẽ lấy $res=res-a_{i-1}$ và $res=res+a_{i+m-1}$.
:::

Độ phức tạp: $O(n)$.

:::important
To-do: Làm sol.
:::

---

# Bài 4: Kẻ làm loạn

## Tóm tắt đề bài

Cho $T$ bộ xâu kí tự $a, b, c$ gồm chữ cái viết hoa. Trong mỗi bộ $a, b, c$, xác định xem mỗi chữ cái trong xâu kí tự $a+b$ có xuất hiện đúng cùng số lần trong xâu kí tự $c$ hay không. Nếu có, in ra "YES", ngược lại, in ra "NO".

Gọi $|s|$ là độ dài xâu của một xâu kí tự.

**Ràng buộc:** $1 \le T \le 100; \ |a|, |b|, |c| \le 100$.

## Lời giải

### Cách 1:

Làm y những gì đề bài bảo (sử dụng mảng đếm).

Độ phức tạp: $O(|a+b|+|c|)$ mỗi test.

:::important
Làm sol.
:::

### Cách 2:

Chúng ta chỉ cần sắp xếp lại các xâu kí tự rồi kiểm tra xem chúng có bằng nhau không.

<details>
<summary>Code mẫu</summary>

```cpp
#include <bits/stdc++.h>
#pragma GCC optimize("O3, unroll-loops")
#define ll long long
#define ld long double
#define st string

using namespace std;

int tt;
st a, b, s, res;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    cin >> tt;
    while (tt--) {
        cin >> a >> b >> s;
        res = a + b;
        sort(s.begin(), s.end());
        sort(res.begin(), res.end());
        if (res == s) {
            cout << "YES\n";
        }
        else {
            cout << "NO\n";
        }
    }
    return 0;
}

```
</details>

Độ phức tạp: $O((|a+b| \log |a+b|) + |c| \log |c|)$ mỗi test.

---

# Bài 5: Tìm số

## Tóm tắt đề bài

Cho số tự nhiên $a$, tìm số $x$ lớn nhất thoả mãn $x \le a$ sao cho các chữ số trong biểu diễn thập phân của $x$ tăng ngặt từ trái sang phải (các số $x \le 9$ được coi là thoả mãn điều kiện).

**Ràng buộc:** $T \le 10^6; \ 0 \le a \le 10^9$.

## Lời giải

**Nhận xét:** Vì các chữ số tăng ngặt nên mỗi chữ số chỉ được xuất hiện nhiều nhất một lần. Từ đó, số lượng số $x$ thoả mãn và nằm trong khoảng $[1, 10^9]$ là:

$$
\sum_{k=1}^{9} \binom{9}{k}=2^9-1=511
$$

Vì số $x$ thoả mãn rất nhỏ, chúng ta có thể dùng hàm đệ quy để sinh ra các số này trước, sắp xếp mảng kết quả rồi dùng tìm kiếm nhị phân để tìm kết quả mỗi test.

Độ phức tạp:

* Tiền xử lý: $2^{10}=1024$ lần duyệt.
* Truy vấn: $\log 511$ mỗi test.

$\implies$ Tổng thể: $O(1)$ mỗi test.

<details>
<summary>Code mẫu</summary>

```cpp
#include <bits/stdc++.h>
#pragma GCC optimize("O3, unroll-loops")
#define ll long long
#define ld long double
#define st string

using namespace std;

int tt;
ll a;
vector <ll> v;

void gen(st s, int t) {
    if (!s.empty()) {
        v.push_back(stoll(s));
    }
    for (int i = t + 1; i <= 9; i++) {
        gen(s + char('0' + i), i);
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    v.push_back(0);
    gen("", 0);
    sort(v.begin(), v.end());
    cin >> tt;
    while (tt--) {
        cin >> a;
        auto it = lower_bound(v.begin(), v.end(), a);
        if (*it == a) {
            cout << a << "\n";
        }
        else {
            cout << *(it - 1) << "\n";
        }
    }
    return 0;
}

```
</details>