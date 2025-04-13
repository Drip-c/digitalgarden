---
{"dg-publish":true,"permalink":"/一、C++程式語言入門/6、結構、函數、堆疊與遞迴/2、函數 (Function)/"}
---


- **在不同地方執行多次相同程式**

```
void print(int i, int j) {
	if (i > j) {
		cout << i << endl;
	} else {
		cout << j << endl;
	}
	cout << i + j << endl;
	cout << i * j << endl;
	cout << i - j << endl;
}

int main() {
	int a, b;
	cin >> a >> b;
	print(a, b);
	print(b, a);
	return 0;
}

輸入 →
3 9

輸出 →
9
12
27
-6
9
12
27
6
```

- 宣告方式 →

```
[A.回傳變數型態] [B.函數名稱](C.參數1, 2 ... n) {
...
return [D.回傳項目];
}

-----------------------------------------------------------------------------------
int f(int x) { //A → int //B → f //C → int x
	return x * x; //D → x * x
}
int main() {
	cout << f(6);
	return 0;
}

輸出 →
36
```

- 如果回傳型態為 void ，則 return; 代表跳出函數

- **函數裡面更改的值，不會影響到丟進來的參數本身**

```
void f(int x, int y) { 
	x = 1; 
	y = 2; 
} 
int main() { 
	int x, y; 
	x = 5; 
	y = 6; 
	f(x, y); 
	cout << x << ' ' << y; 
	return 0; 
}

輸出 →
5 6
```

