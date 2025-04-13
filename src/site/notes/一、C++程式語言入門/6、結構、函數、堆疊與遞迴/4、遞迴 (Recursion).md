---
{"dg-publish":true,"permalink":"/一、C++程式語言入門/6、結構、函數、堆疊與遞迴/4、遞迴 (Recursion)/"}
---


- **在函數中呼叫自己的函數**

### 1 + 2 + ... + n

```
#include <iostream>
using namespace std;

int sum(int i) {
	if (i < 1) //如果i不是自然數，則離開函數
		return 0;

	return i + sum (i - 1); //可以視為i + (i - 1) + (i - 2) + ... 1
}

int main() {
	int n;
	cin >> n;
	cout << sum(n);

return 0;
}

輸入 →
100

輸出 →
5050
```

### GCD 最大公因數

```
#include <iostream>
using namespace std;

int gcd(int x, int y) {
	if (y == 0)
		return x;
	return gcd(y, x % y);
} //使用輾轉相除法

int main() {
	int x, y;
	cin >> x >> y;
	cout << gcd(x, y);

	return 0;
}

輸入 →
10 5

輸出 →
5
```

### 費氏數列

```
#include <iostream>
using namespace std;

int Fibonacci(int i) {
	if (i == 1 || i == 2) {
		return 1;
	}
	return Fibonacci(i - 1) + Fibonacci(i - 2);
}
int main() {
	int n;
	cin >> n;
	cout << Fibonacci(n);

	return 0;
}

輸入 →
7

輸出 →
13
```