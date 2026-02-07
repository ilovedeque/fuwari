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

Ta duyệt từng kí tự trong $S$, nếu kí tự đó là một chữ số, cập nhật $res=res+S_i$. Còn nếu kí tự đó không phải là một chữ số, ta dùng hàm ```stoll()``` để chuyển xâu kí tự $res$ thành số nguyên, lấy $ans=\max(ans, res)$, rồi cập nhật ```res=""```.

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

---

# Bài 3

---

# Bài 4