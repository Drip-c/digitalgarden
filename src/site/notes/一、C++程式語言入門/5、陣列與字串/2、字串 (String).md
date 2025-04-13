---
{"dg-publish":true,"permalink":"/一、C++程式語言入門/5、陣列與字串/2、字串 (String)/"}
---


- **輸入一串英文字**

### Char 陣列

```
int main() {
	char input[100];

	cin >> input;
	cout << input;

	return 0;
}

輸入 →
hello!

輸出 →
hello!
```

- 讀取第n位置的字元

```
cout << input[0] << endl;
input[0] = 'h';

cout << input[1] << endl;
input[1] = 'e';

輸出 →
h
e
```

### String 變數型態

- C++內建string變數

```
#include <iostream>
#include <string> //必須加標頭檔
using namespace std;

int main() {
	string s; //沒有長度限制

	cin >> s;
	cout << s << endl;

	return 0;
}
```

- 補充用法

```
int len = s.length(); // 字串s的長度（若s為"Hello"，則回傳5）

string s1 = s; //指派s的內容給s1

string s2 = s + s; //字串相加（若s為"Hello"，則s2為"HelloHello"）

if (s == "Hello") { //若字串s等於Hello，則...
	...
}

char char_array[100];
cin >> char_array;
string s3(char_array); //可以在s3宣告的時候，把char_array儲存的字串寫入s3
					   //此做法可以視為 char陣列 轉 string的做法
```