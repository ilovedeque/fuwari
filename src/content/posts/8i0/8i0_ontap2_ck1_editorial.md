---
title: Lời giải đề ôn tập số 2 cuối kì 1 lớp 8I0 (25-12-2025) - Chính
published: 2026-05-04
description: ''
image: ''
tags: [Editorials]
category: 8I0
draft: false 
lang: 'vi'
---

# Bài 1: Cuộc đua của ốc sên

## Tóm tắt đề bài

Cho $n$ con ốc sên cùng bò lên đỉnh của cây có độ cao $V$ mét. Với mỗi con ốc, nó sẽ leo lên $a$ mét vào ban ngày và tụt $b$ mét vào ban đêm. Hãy xác định số ngày ít nhất để mỗi con ốc sên bò lên đỉnh cây. Nếu con nào không thể leo lên được thì in ra $-1$.

**Ràng buộc:**

* $1 \le n \le 10^5$
* $1 \le V \le 10^{18}$
* $1 \le a_i, b_i \le 10^9 \ \forall i \in \{1, 2, \dots, n\}$

## Lời giải

Ta có thể chia bài này thành ba trường hợp như sau:

### Trường hợp 1: $a \ge V$

Khi đó thì con ốc sên có thể lên được đỉnh trong một ngày, vì vậy đáp án của trường hợp này là $1$.

### Trường hợp 2: $a \le b, a < V$

Khi đó thì sau mỗi ngày hoàn chỉnh, ta có $a - b \le 0$. Suy ra, ốc sên sẽ không thể tăng được chiều cao, mà vì ngày đầu không thể đạt $V$ do $a < V$, nên con ốc sên đó sẽ không thể bao giờ lên đỉnh được. Vì vậy, đáp án của trường hợp này là $-1$.

### Trường hợp 3:

Gọi $k$ là số ngày để một con ốc sên leo lên đỉnh, $d = a - b$.

Khi đó, ta có điều kiện để đạt đỉnh là bất phương trình như sau:

$$
\begin{aligned}
(k - 1) \cdot d + a &\ge V \\
k \cdot d &\ge V - a + d \\
k \cdot d &\ge V - a + a - b \\
k \cdot d &\ge V - b \\
\implies k &\ge \frac{V - b}{d} \\
\end{aligned}
$$

Vì ta cần đáp án $k$ là số nguyên dương nhỏ nhất, nên ta có:

$$
k = \left\lceil \frac{V - b}{a - b} \right\rceil
$$

Trong đó, $\lceil x \rceil$ là số nguyên nhỏ nhất lớn hơn hoặc bằng $x$.

**Độ phức tạp:** $O(n)$

<details>
<summary>Code tham khảo</summary>

```cpp
#include <bits/stdc++.h>
#pragma GCC optimize("O3, unroll-loops")
#define ll long long
#define ld long double
#define st string

using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    if (fopen("SNAILS.inp", "r")) {
        freopen("SNAILS.inp", "r", stdin);
        freopen("SNAILS.out", "w", stdout);
    }
    int n;
    ll v;
    cin >> n >> v;
    while (n--) {
        ll a, b, d;
        cin >> a >> b;
        if (a - b <= 0 && a < v) {
            cout << "-1\n";
            continue;
        }
        if (a >= v) {
            cout << "1\n";
            continue;
        }
        d = (v - b + (a - b - 1)) / (a - b);
        cout << d << "\n";
    }
    return 0;
}

```
</details>