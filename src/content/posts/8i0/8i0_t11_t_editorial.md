---
title: Lời giải đề thi tháng 11 lớp 8I0 - Tách
published: 2026-01-04
description: ''
image: ''
tags: [Editorials]
category: 8I0
draft: false 
lang: 'vi'
---

Chấm bài tại đây: [OJ](https://inconsonantly-heliocentric-arnav.ngrok-free.dev/contest/8i0_t11_t_mirror)

# Bài 1: Tích cực trị

## Tóm tắt đề bài

Cho mảng $a$ gồm $n$ phần tử. Tính $\max(a) \times \min(a)$ sau khi xoá đi phần tử $a_{n}$.

**Ràng buộc:** $2 \le n \le 10^5; \ |a_i| \le 10^6$.

## Lời giải

Làm y những gì đề bài bảo.

Độ phức tạp: $O(n)$ hoặc $O(n \log n)$.

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
int n;
ll a[N], maxx = -1e6, minn = 1e6;

int main() {
   ios_base::sync_with_stdio(false);
   cin.tie(nullptr);
   cout.tie(nullptr);
   cin >> n;
   for (int i = 1; i < n; i++) {
       cin >> a[i];
       maxx = max(maxx, a[i]);
       minn = min(minn, a[i]);
   }
   cout << maxx * minn;
   return 0;
}

```
</details>

---

# Bài 2: Xoá phần tử trùng nhau

## Tóm tắt đề bài

Cho mảng $a$ gồm $n$ phần tử. In ra các phần tử sau khi xoá đi các phần tử trùng lặp và đã giữ bản sao cuối cùng.

**Ràng buộc:** $1 \le n \le 10^5; \ -10^6 \le a_i \le 10^6$.

## Lời giải

Chúng ta có thể duyệt mảng đó theo chiều ngược, kiểm tra xem phần tử đó đã xuất hiện hay chưa, từ đó ta có hai trường hợp:

* **Trường hợp 1:** Nếu phần tử đó xuất hiện lần đầu thì chúng ta thêm vào mảng kết quả.
* **Trường hợp 2:** Nếu phần tử đó xuất hiện từ lần thứ hai trở đi, chúng ta di chuyển đến phần tử tiếp theo luôn.

Sau đó, chúng ta chỉ cần đảo lại mảng kết quả rồi in nó ra là xong.

Độ phức tạp: $O(n)$.

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
int n, a[N];
unordered_set <int> s; // cấu trúc dữ liệu giữ lại 1 bản sao của 1 phần tử khác nhau
vector<int> r;

int main() {
   ios_base::sync_with_stdio(false);
   cin.tie(nullptr);
   cout.tie(nullptr);
   cin >> n;
   for (int i = 1; i <= n; i++) {
       cin >> a[i];
   }
   for (int i = n; i >= 1; i--) {
       auto it = s.find(a[i]);
       if (it == s.end()) {
           s.insert(a[i]);
           r.push_back(a[i]);
       }
   }
   reverse(r.begin(), r.end());
   for (auto i:r) {
       cout << i << " ";
   }
   return 0;
}

```
</details>

---

# Bài 3: Khu trưng bày

## Tóm tắt đề bài

Cho mảng $a$ gồm $n$ phần tử. Tính khoảng cách từ phần tử đầu tiên đến vị trí đầu tiên sao cho số lượng phần tử khác nhau tính đến thời điểm đó bằng $m$.

**Ràng buộc:** $1 \le n \le 10^5; \ 1 \le m \le n; \ 1 \le a_i \le 10^9;$ mảng $a$ có ít nhất $m$ giá trị khác nhau.

## Lời giải

Chúng ta chỉ cần đếm số lượng phần tử khác nhau để kiểm tra xem phần tử đó có tồn tại không, rồi kiểm tra xem số lượng phần tử của nó có bằng $m$ không, nếu có thì in ra $(i - 1) \times 5$ (vì bạn Nam chỉ cần đi $(i-1)$ lần).

Độ phức tạp: $O(n)$.

<details>
<summary>Code mẫu</summary>

```cpp
#include <bits/stdc++.h>
#pragma GCC optimize("O3, unroll-loops")
#define ll long long
#define ld long double
#define st string

using namespace std;

int n, m, a;
unordered_set <int> s; // cấu trúc dữ liệu giữ lại 1 bản sao của 1 phần tử khác nhau

int main() {
   ios_base::sync_with_stdio(false);
   cin.tie(nullptr);
   cout.tie(nullptr);
   cin >> n >> m;
   for (int i = 1; i <= n; i++) {
       cin >> a;
       if (s.find(a) == s.end()) {
           s.insert(a);
       }
       if (s.size() == m) {
           cout << (i - 1) * 5;
           return 0;
       }
   }
   return 0;
}

```
</details>

---

# Bài 4: Đếm giá trị

## Tóm tắt đề bài

Cho mảng $a$ gồm $n$ phần tử. Đếm số lượng phần tử mà xuất hiện từ $2$ lần trở lên.

**Ràng buộc:** $1 \le n \le 10^5; \ |a_i| \le 10^6$.

## Lời giải

Chúng ta chỉ cần dùng một mảng đếm để đếm số lượng các phần tử, sau đó xem trong mảng đếm đó, nếu số lượng phần tử lớn hơn hoặc bằng $2$ thì chúng ta thêm vào biến đếm kết quả.

Độ phức tạp: $O(n)$.

<details>
<summary>Code mẫu</summary>

```cpp
#include <bits/stdc++.h>
#pragma GCC optimize("O3, unroll-loops")
#define ll long long
#define ld long double
#define st string

using namespace std;

int n, s, cnt = 0;
unordered_map <int, int> mp; // cấu trúc dữ liệu dùng làm mảng đếm

int main() {
   ios_base::sync_with_stdio(false);
   cin.tie(nullptr);
   cout.tie(nullptr);
   cin >> n;
   for (int i = 1; i <= n; i++) {
       cin >> s;
       mp[s]++;
   }
   for (auto i:mp) {
       if (i.second >= 2) {
           cnt++;
       }
   }
   cout << cnt << "\n";
   return 0;
}

```
</details>