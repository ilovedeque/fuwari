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
    freopen("UOCSO.inp", "r", stdin);
    freopen("UOCSO.out", "w", stdout);
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
    freopen("UOCSO.inp", "r", stdin);
    freopen("UOCSO.out", "w", stdout);
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

Chúng ta dùng sàng nguyên tố biến đổi để tìm số ước từ $1$ đến $\max(a_i)$, rồi chúng ta duyệt qua từng phần tử trong mảng $a$ để lấy số ước của từng số và so sánh kết quả đó để ra được đáp án cần tìm.

**Độ phức tạp:** $O(n + \max(a_i) \log \log \max(a_i))$.

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

---

# Bài 3

---

# Bài 4