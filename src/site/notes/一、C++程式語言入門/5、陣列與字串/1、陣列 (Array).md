---
{"dg-publish":true,"permalink":"/一、C++程式語言入門/5、陣列與字串/1、陣列 (Array)/"}
---


- **將同一型態同一作用的變數排在一起**
- **宣告時，變數名稱後面需加上[ n ]，n為陣列的長度**
- **從0開始存取，int a[10] → 從a[0]存取到a[9]**

### 一維陣列

```
int main() {
	int array[4];

	array[0] = 1;
	array[1] = 10;
	array[2] = 12;
	array[3] = 5;

	for (int i = 0; i < 4; i++) {
		cout << array[i] << endl;
	}

	return 0;
}

輸出 →
1
10
12
5
```

### 多維陣列

- 二維陣列 → int array[n]  [n]

```
int main() {
	int n;
	cin >> n;

	int array[n][n];
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			cin >> array[i][j];
		}
	}
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			cout << array[i][j] << ' ';
		}
		cout << endl;
	}

	return 0;
}
```

- 三維、四維等多維陣列差異 →[ ]的數目

