---
title: Lời giải đề ôn tập số 1 cuối kì 1 lớp 8I0 - Chính
published: 2026-02-06
description: ''
image: ''
tags: [Editorials]
category: 8I0
draft: false
lang: 'vi'
---

# Bài 1: Ước số

## Tóm tắt đề bài

Cho mảng $a$ gồm $n$ phần tử nguyên dương. Tìm phần tử có số ước nguyên dương nhiều nhất, nếu có nhiều số thoả mãn thì in ra số xuất hiện đầu tiên trong các số đó.

**Ràng buộc:**

* **Subtask 1:** $n \le 10^3; \ a_i \le 10^3$.
* **Subtask 2:** $n \le 10^5; \ a_i \le 10^5$.

## Lời giải

### Subtask 1:

Chúng ta chỉ cần duyệt qua từng phần tử trong mảng $a$, rồi với mỗi phần tử $a_i$, ta duyệt $j$ từ $1$ đến $a_i$ và đếm số ước của số đó, rồi so sánh kết quả đó để ra được đáp án cần tìm.

**Độ phức tạp:** $O(n \times a_i)$.

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
int n, ans, maxx, s, cnt;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    if (fopen("UOCSO.inp", "r")) {
        freopen("UOCSO.inp", "r", stdin);
        freopen("UOCSO.out", "w", stdout);
    }
    cin >> n;
    while (n--) {
        cin >> s;
        cnt = 0;
        for (ll i = 1; i <= s; i++) {
            if (s % i == 0) {
                cnt++;
            }
        }
        if (cnt > maxx) {
            ans = s;
            maxx = cnt;
        }
    }
    cout << ans;
    return 0;
}

```
</details>

### Subtask 2:

#### Cách 1:

Chúng ta làm như subtask 1, nhưng thay vì duyệt $j$ từ $1$ đến $a_i$ thì ta chỉ cần duyệt $j$ từ $1$ đến $\sqrt {a_i}$ là có số ước của số đó rồi.

**Độ phức tạp:** $O(n \times \sqrt {a_i})$.

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
int n, ans, maxx, s, cnt;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    if (fopen("UOCSO.inp", "r")) {
        freopen("UOCSO.inp", "r", stdin);
        freopen("UOCSO.out", "w", stdout);
    }
    cin >> n;
    while (n--) {
        cin >> s;
        cnt = 0;
        for (ll i = 1; i * i <= s; i++) {
            if (s % i == 0) {
                cnt++;
                if (i != s / i) {
                    cnt++;
                }
            }
        }
        if (cnt > maxx) {
            ans = s;
            maxx = cnt;
        }
    }
    cout << ans;
    return 0;
}

```
</details>

#### Cách 2:

Chúng ta dùng sàng nguyên tố biến đổi để tìm số ước từ $1$ đến $\max(a)$, rồi chúng ta duyệt qua từng phần tử trong mảng $a$ để lấy số ước của từng số và so sánh kết quả đó để ra được đáp án cần tìm.

**Độ phức tạp:** $O(n + \max(a) \log \max(a))$.

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
int a[N], s[N];

void sieve() {
    for (ll i = 1; i < N; i++) {
        for (ll j = i; j < N; j += i) {
            s[j]++;
        }
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    if (fopen("UOCSO.inp", "r")) {
        freopen("UOCSO.inp", "r", stdin);
        freopen("UOCSO.out", "w", stdout);
    }
    sieve();
    int n, ans, maxx = 0;
    cin >> n;
    for (int i = 1; i <= n; i++) {
        cin >> a[i];
        if (s[a[i]] > maxx) {
            maxx = s[a[i]];
            ans = a[i];
        }
    }
    cout << ans;
    return 0;
}

```
</details>

---

# Bài 2: Số lớn nhất

## Tóm tắt đề bài

Cho một xâu kí tự $S$ độ dài $N$ gồm các kí tự chữ cái: $\text{‘a’}~...~\text{‘z’}$, và chữ số: $\text{‘0’}~...~\text{‘9’}$. Tìm số nguyên lớn nhất trong xâu $S$ sau khi xoá bỏ đi các kí tự chữ cái.

**Ràng buộc:**

* **Subtask 1:** $3 \le N \le 10^5; \ $các số xuất hiện trong $S$ có giá trị không vượt quá $9$.
* **Subtask 2:** $3 \le N \le 10^5; \ $các số xuất hiện trong $S$ có giá trị không vượt quá $10^9$.
* **Subtask 3:** $3 \le N \le 10^5$.

**Dữ liệu vào đảm bảo rằng xâu ký tự $S$ có ít nhất $1$ chữ số.**

## Lời giải

### Subtask 1:

Ta duyệt từng kí tự trong $S$, nếu kí tự đó là một chữ số, cập nhật $ans=\max(ans, S_i)$.

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

st s;
int ans = 0;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    freopen("MAXS.inp", "r", stdin);
    freopen("MAXS.out", "w", stdout);
    cin >> s;
    for (auto i:s) {
        if (isdigit(i)) {
            ans = max(ans, i - '0');
        }
    }
    cout << ans;
    return 0;
}

```
</details>

### Subtask 2:

Gọi $res$ là một xâu kí tự chứa các chữ số.

Ta duyệt từng kí tự trong $S$, nếu kí tự đó là một chữ số, cập nhật $res=res+S_i$. Còn nếu kí tự đó không phải là một chữ số, ta dùng hàm ```stoll()``` để chuyển xâu kí tự $res$ thành số nguyên, lấy $ans=\max(ans, res)$, rồi cập nhật ```res = ""```.

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

st s, res;
ll ans = 0;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    if (fopen("MAXS.inp", "r")) {
        freopen("MAXS.inp", "r", stdin);
        freopen("MAXS.out", "w", stdout);
    }
    cin >> s;
    for (int i = 0; i < s.size(); i++) {
        if (s[i] >= '0' && s[i] <= '9') {
            res += s[i];
        }
        else {
            if (res != "") {
                ans = max(ans, stoll(res));
            }
            res = "";
        }
    }
    if (res != "") {
        ans = max(ans, stoll(res));
    }
    cout << ans;
    return 0;
}

```
</details>

### Subtask 3:

Chúng ta làm như subtask 2, nhưng thay vào việc dùng hàm ```stoll()``` thì ta so sánh trực tiếp dùng xâu kí tự. Tuy nhiên, vẫn phải xét trường hợp khi $res$ có các chữ số $0$ ở đầu.

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

st s, res, ans;
int it;

void solve() {
    if (res.empty()) {
        return;
    }
    it = 0;
    while (it < res.size() && res[it] == '0') {
        it++;
    }
    if (res.size() == it) {
        if (ans.empty()) {
            ans = "0";
            return;
        }
    }
    if (res.size() - it > ans.size()) {
        ans = res.substr(it);
        return;
    }
    if (res.size() - it < ans.size()) {
        return;
    }
    for (int i = 0; i < res.size() - it; i++) {
        if (res[i + it] > ans[i]) {
            ans = res.substr(it);
            return;
        }
        if (res[i + it] < ans[i]) {
            return;
        }
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    if (fopen("MAXS.inp", "r")) {
        freopen("MAXS.inp", "r", stdin);
        freopen("MAXS.out", "w", stdout);
    }
    cin >> s;
    for (int i = 0; i < s.size(); i++) {
        if (isdigit(s[i])) {
            res += s[i];
        }
        else {
            if (!res.empty()) {
                solve();
            }
            res = "";
        }
    }
    solve();
    if (ans.empty()) {
        cout << 0;
    }
    else {
        cout << ans;
    }
    return 0;
}

```
</details>

---

# Bài 3: Số đặc biệt

## Tóm tắt đề bài

Cho $M$ cặp số nguyên dương $(a, b)$ thoả mãn $a \le b$, hãy đếm số lượng số có đúng $3$ ước nguyên dương đôi một khác nhau trong vùng $[a, b]$.

**Ràng buộc:**

* **Subtask 1:** $M \le 10^2; \ b \le 10^2$.
* **Subtask 2:** $M \le 10^3; \ b \le 10^3$.
* **Subtask 3:** $M \le 10^5; \ b \le 10^6$.

## Lời giải

### Subtask 1:

Gọi $cnt$ là số lượng số thoả mãn yêu cầu.

Với mỗi số $x$ trong vùng $[a, b]$, chúng ta duyệt từ $1$ đến $x$ để tìm số ước của nó, nếu số đó có $3$ ước khác nhau thì cập nhật $cnt = cnt + 1$.

Cho $n = b - a$.

**Độ phức tạp:** $O(M \times n^2)$.

<details>
<summary>Code mẫu</summary>

```cpp
#include <bits/stdc++.h>
#pragma GCC optimize("O3, unroll-loops")
#define ll long long
#define ld long double
#define st string

using namespace std;

int m, a, b, cnt, r;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    if (fopen("SNUM.inp", "r")) {
        freopen("SNUM.inp", "r", stdin);
        freopen("SNUM.out", "w", stdout);
    }
    cin >> m;
    while (m--) {
        cnt = 0;
        cin >> a >> b;
        for (int i = a; i <= b; i++) {
            r = 0;
            for (int j = 1; j <= i; j++) {
                if (i % j == 0) {
                    r++;
                }
            }
            if (r == 3) {
                cnt++;
            }
        }
        cout << cnt << "\n";
    }
    return 0;
}

```
</details>

### Subtask 2:

Ta làm như subtask 1, nhưng chúng ta chỉ cần duyệt từ $1$ đến $\sqrt x$ là tìm được số ước của nó rồi.

**Độ phức tạp:** $O(M \times n \sqrt n)$.

<details>
<summary>Code mẫu</summary>

```cpp
#include <bits/stdc++.h>
#pragma GCC optimize("O3, unroll-loops")
#define ll long long
#define ld long double
#define st string

using namespace std;

int m, a, b, cnt, r;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    if (fopen("SNUM.inp", "r")) {
        freopen("SNUM.inp", "r", stdin);
        freopen("SNUM.out", "w", stdout);
    }
    cin >> m;
    while (m--) {
        cnt = 0;
        cin >> a >> b;
        for (int i = a; i <= b; i++) {
            r = 0;
            for (int j = 1; j * j <= i; j++) {
                if (i % j == 0) {
                    r++;
                    if (j != i / j) {
                        r++;
                    }
                }
            }
            if (r == 3) {
                cnt++;
            }
        }
        cout << cnt << "\n";
    }
    return 0;
}

```
</details>

### Subtask 3:

**Nhận xét:** Một số $x$ có đúng $3$ ước đôi một khác nhau chỉ và chỉ khi nó là **bình phương của một số nguyên tố**. Từ đó, bài toán trên trở thành tìm số lượng $x$ trong vùng $[a, b]$ sao cho $x=p^2$ với $p$ là số nguyên dương thoả mãn $p$ nguyên tố.

Gọi $N=\max_{1 \le j \le M}(b_j)$.

Ta sẽ sàng nguyên tố từ $1$ đến $\sqrt N$, rồi tiền xử lí mảng công dồn $s$ với $s_i$ $(1 \le i \le n)$ là số lượng số thoả mãn yêu cầu trong vùng $[1, i]$. Sau đó, với mỗi truy vấn, số thoả mãn yêu cầu trong vùng $[a, b]$ là $s_b - s_{a-1}$.

**Độ phức tạp:** $O(N + M)$.

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
bool p[1001];
int s[N], tt, a, b;

bool f(int a) {
    int x = sqrt(a);
    if (x * x == a && p[x]) {
        return 1;
    }
    return 0;
}

void sieve() {
    fill(p, p + 1001, 1);
    p[0] = p[1] = 0;
    for (ll i = 2; i * i <= 1000; i++) {
        if (p[i]) {
            for (ll j = i * i; j <= 1000; j += i) {
                p[j] = 0;
            }
        }
    }
    for (int i = 1; i < N; i++) {
        if (f(i)) {
            s[i] = s[i - 1] + 1;
        }
        else {
            s[i] = s[i - 1];
        }
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    if (fopen("SNUM.inp", "r")) {
        freopen("SNUM.inp", "r", stdin);
        freopen("SNUM.out", "w", stdout);
    }
    sieve();
    cin >> tt;
    while (tt--) {
        cin >> a >> b;
        cout << s[b] - s[a - 1] << "\n";
    }
    return 0;
}

```
</details>

---

# Bài 4: Dãy con không giảm

## Tóm tắt đề bài

## Lời giải

### Subtask 1:

### Subtask 2, 3:

### Subtask 4: