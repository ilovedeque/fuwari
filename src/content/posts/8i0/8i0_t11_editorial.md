---
title: Lời giải đề thi tháng 11 lớp 8I0 - Chính
published: 2026-01-05
description: ''
image: ''
tags: [Editorials]
category: 8I0
draft: false 
lang: 'vi'
---

# Bài 1: Chấm điểm

## Tóm tắt đề bài

Cho $N$ bộ số $a, b, c$. Trong mỗi bộ số đó, xác định xem $\max(a, b, c) - \min(a, b, c) \le 25$ không. Nếu có, in ra $median(a, b, c)$, trong đó $median$ là trung vị. Nếu không, in ra "check again".

**Ràng buộc:** $N \le 10^5; \ 0 \le a, b, c \le 100$.

## Lời giải

Làm y những gì đề bài bảo.

**Độ phức tạp:** $O(1)$ mỗi test.

<details>
<summary>Code mẫu</summary>

```cpp
#include <bits/stdc++.h>
#pragma GCC optimize("O3, unroll-loops")
#define ll long long
#define ld long double
#define st string

using namespace std;

int n, abc[4];

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    cin >> n;
    while (n--) {
        for (int i = 1; i <= 3; i++) {
            cin >> abc[i];
        }
        sort(abc + 1, abc + 4);
        if (abc[3] - abc[1] > 25) {
            cout << "check again\n";
            continue;
        }
        cout << abc[2] << "\n";
    }
    return 0;
}

```
</details>

---

# Bài 2: Tìm đoạn con

## Tóm tắt đề bài

Cho mảng $A$ gồm $n$ phần tử nguyên dương và số $k$. Tìm độ dài đoạn con liên tiếp dài nhất có tổng không vượt quá $k$.

**Ràng buộc:**

* **Subtask 1:** $1 \le n \le 10^2; \ k \le 10^{12}; \ 0 \le a_i \le 10^6$.
* **Subtask 2:** $1 \le n \le 5000; \ k \le 10^{12}; \ 0 \le a_i \le 10^6$.
* **Subtask 3:** $1 \le n \le 10^5; \ k \le 10^{12}; \ 0 \le a_i \le 10^6$.

## Lời giải

### Subtask 1, 2:

Chúng ta chỉ cần duyệt qua tất cả dãy con $(i, j)$ $(1 \le i \le j \le n)$ rồi kiểm tra xem $\sum_{x=i}^{j} {(a_x)} \le k$ không. Nếu có thì $ans=\max(ans, j - i + 1)$.

**Độ phức tạp:** $O(n^2)$.

<details>
<summary>Code mẫu</summary>

```cpp
#include <bits/stdc++.h>
#pragma GCC optimize("O3, unroll-loops")
#define ll long long
#define ld long double
#define st string

using namespace std;

const int N = 1e5 + 1;
int n, ans = 0;
ll a[N], k, s;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    cin >> n >> k;
    for (int i = 1; i <= n; i++) {
        cin >> a[i];
    }
    for (int i = 1; i <= n; i++) {
        s = 0;
        for (int j = i; j <= n; j++) {
            s += a[j];
            if (s <= k) {
                ans = max(ans, j - i + 1);
            }
            else {
                break;
            }
        }
    }
    cout << ans;
    return 0;
}

```
</details>

### Subtask 3:

**Nhận xét:**

* Chúng ta có thể thấy được các phần tử trong mảng đều dương.
* Với một đoạn $(i, j)$ bất kì thì tổng đoạn $[a_i, a_j]$ sẽ tăng lên nếu tăng $j$ và sẽ giảm nếu tăng $i$.

Vì vậy, chúng ta sẽ dùng kỹ thuật hai con trỏ (two pointers) để duyệt qua mảng $A$. Cụ thể hơn, gọi $(l, r)$ là dãy con thoả mãn tổng các phần tử không quá $k$ $(1 \le l \le r \le n)$. Với mỗi lần xét $r+1$, nếu tổng đoạn $[a_l, a_{r+1}]$ vượt quá $k$ thì chúng ta sẽ dịch chuyển biến $l$ lên $1$ đơn vị cho đến khi tổng đoạn đó không vượt quá $k$. Sau đó, chúng ta chỉ cần cập nhật $ans=\max(ans, r - l + 1)$.

**Độ phức tạp:** $O(n)$.

<details>
<summary>Code mẫu</summary>

```cpp
#include <bits/stdc++.h>
#pragma GCC optimize("O3, unroll-loops")
#define ll long long
#define ld long double
#define st string

using namespace std;

const int N = 1e5 + 1;
int n, l = 1, r = 1, ans = 0;
ll a[N], k, s;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    cin >> n >> k;
    for (int i = 1; i <= n; i++) {
        cin >> a[i];
    }
    s = a[1];
    while (r <= n) {
        while (s > k && l < r) {
            s -= a[l];
            l++;
        }
        if (s <= k) {
            ans = max(ans, r - l + 1);
        }
        r++;
        s += a[r];
    }
    cout << ans;
    return 0;
}

```
</details>

---

# Bài 3: Numdle

## Tóm tắt đề bài

Cho một xâu kí tự $s$ gồm $n$ chữ số trong khoảng $[1, 9]$ và $q$ truy vấn. Với mỗi truy vấn, cho một xâu kí tự $t$ gồm $n$ chữ số trong khoảng $[1, 9]$, tính số chữ số ở $t$ mà ở đúng vị trí (kí hiệu là $C$), sai vị trị (kí hiệu là $P$) và không tồn tại (kí hiệu là $I$) trong $s$.

**Ràng buộc:** 

Gọi $|x|$ là độ dài xâu của một xâu kí tự.

* **Subtask 1:** $1 \le n \le 10^2; \ 1 \le q \le 10^5; \ n \times (q + 1) \le 5 \times 10^5$.
* **Subtask 2:** $1 \le n \le 10^5; \ 1 \le q \le 10^5; \ n \times (q + 1) \le 5 \times 10^5; \ s_i \in \{\text{‘0’, ‘1’}\} \  \forall \ 1 \le i \le n$.
* **Subtask 3:** $1 \le n \le 10^5; \ 1 \le q \le 10^5; \ n \times (q + 1) \le 5 \times 10^5$.

## Lời giải

Với mỗi truy vấn, chúng ta duyệt qua kí tự $i$ $(0 \le i \le n-1)$ của $s$ và $t$. Từ đó, chúng ta có $2$ trường hợp:

* **Trường hợp 1:** Nếu $s[i]=t[i]$, chúng ta tăng $C$ lên $1$ đơn vị (vì chữ số đó nằm ở đúng vị trí).
* **Trường hợp 2:** Nếu $s[i] \neq t[i]$, chúng ta lưu lại tần suất của $s[i]$ và $t[i]$ vào hai mảng đếm riêng biệt (lần lượt là $cnts, \ cntt$).

Sau khi duyệt xong, với mỗi chữ số $d$ từ $0$ đến $9$, chúng ta lấy $P=P+min(cnts[d], cntt[d])$.

Khi đó, $I=n-C-P$.

**Độ phức tạp:** $O(n)$ mỗi truy vấn.

<details>
<summary>Code mẫu</summary>

```cpp
#include <bits/stdc++.h>
#pragma GCC optimize("O3, unroll-loops")
#define ll long long
#define ld long double
#define st string

using namespace std;

int n, q, cnt, ss[10], cc[10], I;
st s, c;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    cin >> n >> s >> q;
    while (q--) {
        I = n;
        fill(ss, ss + 10, 0);
        fill(cc, cc + 10, 0);
        cin >> c;
        cnt = 0;
        for (int i = 0; i < n; i++) {
            if (c[i] == s[i]) {
                cnt++;
            }
            else {
                ss[s[i] - '0']++;
                cc[c[i] - '0']++;
            }
        }
        cout << cnt << "C ";
        I -= cnt;
        cnt = 0;
        for (int i = 0; i <= 9; i++) {
            cnt += min(cc[i], ss[i]);
        }
        cout << cnt << "P ";
        I -= cnt;
        cout << I << "I\n";
    }
    return 0;
}

```
</details>

---

# Bài 4: Dãy con có tổng S

## Tóm tắt đề bài

Cho mảng $a$ gồm $n$ phần tử. Xác định một dãy con (không cần liên tiếp) sao cho tổng dãy con đó bằng $k$. Nếu có một dãy con thoả mãn, in ra "YES" rồi in ra chỉ số của các phần tử dãy con đó. Nếu không có dãy con thoả mãn, in ra "NO".

**Ràng buộc:**

* **Subtask 1:** $1 \le n \le 20; \ 1 \le S \le 10^9; \ 1 \le a_i \le 100$.
* **Subtask 2:** $1 \le n \le 100; \ 1 \le S \le 10^9; \ 1 \le a_i \le 100$.

## Lời giải

**Nhận xét:** Chúng ta dễ dàng có thể thấy được nếu tổng các phần tử trong mảng $a$ bé hơn $S$ thì ta sẽ không thể tìm được một dãy thoả mãn. Từ đó, nếu điều kiện đó được thoả mãn, chúng ta sẽ in ra "NO". Đồng thời, giới hạn của $S$ sẽ được giảm xuống tệ nhất là $S \le 10^4$.

### Subtask 1:

Chúng ta có thể duyệt qua tất cả trường hợp của bài toán sử dụng đệ quy (recursion) như sau:

Với vị trí thứ $i \ (1 \le i \le n)$, ta có $2$ cách lựa chọn là: thêm hoặc không thêm $a_i$ vào dãy con. Như vậy, với vị trị thứ $n$, ta sẽ có nhiều nhất $2^{20}=1048576$ trường hợp. Ta có thể thực hiện việc duyệt như sau:

* Với vị trí thứ $i$, ta sẽ xét trường hợp thêm hoặc không thêm $a_i$ vào dãy con, đồng thời duy trì tổng hiện tại của dãy con.
* Đến vị trí thứ $n$, ta kiểm tra xem dãy con đó có tổng bằng $S$ hay không. Nếu có, đây là một dãy thoả mãn và chúng ta sẽ in các chỉ số được chọn đó.
* Thực hiện tìm kiếm với vị trí $i+1$, trong trường hợp đã tính cả $2$ trường hợp được tạo ra, ta quay lại vị trí trước đó để xét các nhánh khác.
* Việc kiểm tra sẽ dừng lại sau khi chúng ta đã duyệt hết các đoạn con hoặc có một dãy con thoả mãn.

**Độ phức tạp:** $O(n \times 2^n)$.

<details>
<summary>Code mẫu</summary>

```cpp
#include <bits/stdc++.h>
#pragma GCC optimize("O3, unroll-loops")
#define ll long long
#define ld long double
#define st string

using namespace std;

int n, S, a[101], res = 0;
vector <int> v;
bool chk = 0;

void gen(int id, int s) {
    if (id > n) {
        return;
    }
    if (s == S && !chk) {
        chk = 1;
        cout << "YES\n";
        for (auto i:v) {
            cout << i << " ";
        }
        return;
    }
    gen(id + 1, s);
    v.push_back(id + 1);
    gen(id + 1, s + a[id + 1]);
    v.pop_back();
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    cin >> n >> S;
    for (int i = 1; i <= n; i++) {
        cin >> a[i];
        res += a[i];
    }
    if (S > res) {
        cout << "NO";
        return 0;
    }
    gen(0, 0);
    if (!chk) {
        cout << "NO";
    }
    return 0;
}

```
</details>

### Subtask 2:

Chúng ta có thể dùng quy hoạch động (Dynamic Programming - DP) để giải bài toán này như sau:

* Gọi $dp[m] = i$ nghĩa là có thể đạt được tổng $m$ bằng cách chọn phần tử $a[i]$ cuối cùng.
* Ta sẽ khởi tạo $dp[0] = 0$ (vì tổng $0$ có thể đạt được bằng cách không chọn phần tử nào).
* Khi đó, chúng ta sẽ duyệt qua từng phần tử, cập nhật $dp$ từ lớn xuống nhỏ để tránh dùng lại phần tử nhiều lần.
* Sau khi duyệt, nếu $dp[S]$ có giá trị hợp lệ, ta sẽ truy vết ngược lại để tìm các chỉ số.

**Độ phức tạp:** $O(n \times \text{sum}(a))$.

<details>
<summary>Code mẫu</summary>

```cpp
#include <bits/stdc++.h>
#pragma GCC optimize("O3, unroll-loops")
#define ll long long
#define ld long double
#define st string

using namespace std;

int n, S, a[101], res = 0, m, id;
vector <int> dp;
vector <int> v;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    cin >> n >> S;
    for (int i = 1; i <= n; i++) {
        cin >> a[i];
        res += a[i];
    }
    if (S > res) {
        cout << "NO";
        return 0;
    }
    dp.resize(res + 1, -1);
    dp[0] = 0;
    for (int i = 1; i <= n; i++) {
        for (m = res; m >= a[i]; m--) {
            if (dp[m - a[i]] != -1 && dp[m] == -1) {
                dp[m] = i;
            }
        }
    }
    if (dp[S] == -1) {
        cout << "NO";
        return 0;
    }
    cout << "YES\n";
    m = S;
    while (m > 0) {
        id = dp[m];
        v.push_back(id);
        m -= a[id];
    }
    sort(v.begin(), v.end());
    for (auto i:v) {
        cout << i << " ";
    }
    return 0;
}

```
</details>