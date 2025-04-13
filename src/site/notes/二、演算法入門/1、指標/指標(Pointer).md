---
{"dg-publish":true,"permalink":"/二、演算法入門/1、指標/指標(Pointer)/"}
---


- 每個變數會有不同的「記憶體地址」
1. **使用&符號來擷取該變數的記憶體位置**

```
#include <iostream>
using namespace std;

int main() {
	int a = 5;

	cout << "變數a的值: " << a << endl;
	cout << "變數a的記憶體位置: " << &a << endl;

	return 0;
}

輸出 →
變數a的值: 5
變數a的記憶體位置: 0x7ffeee673978
```

2. 利用「指標」來將記憶體存起來

```
int a = 1;
char b = 'a';

int *pointer_a = &a; // type *名稱
char *pointer_b = &b;
```

- type代表這個指標要存的記憶體位置存的是**何種型態**的值

3. 存取指標指向的變數用 *

```
#include <iostream>
using namespace std;

int main() {
	int a = 5;
	int *p = &a;

	cout << "變數a的值: " << a << endl;
	cout << "透過pointer讀取變數a的值: " << *p << endl << endl;

	a = 6;
	cout << "變數a的值: " << a << endl;
	cout << "透過pointer讀取變數a的值: " << *p << endl << endl;

	*p = 7;
	cout << "變數a的值: " << a << endl;
	cout << "透過pointer讀取變數a的值: " << *p << endl;

	return 0;
}

輸出 →
變數a的值: 5
透過pointer讀取變數a的值: 5

變數a的值: 6
透過pointer讀取變數a的值: 6

變數a的值: 7
透過pointer讀取變數a的值: 7
```

- 達成兩數字互換

```
#include <iostream>
using namespace std;

void swap(int *a, int *b) {
	int t = *a;
	*a = *b;
	*b = t;
}

int main() {
	int x, y;
	x = 5;
	y = 6;
	swap(&x, &y);
	cout << x << ' ' << y;

	return 0;
}

輸出 →
6 5
```