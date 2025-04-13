---
{"dg-publish":true,"permalink":"/一、C++程式語言入門/4、迴圈控制/1、While迴圈/"}
---

- 用法 →

```
while ( statement ) {
...
}
```

- statementwhile →放置判斷條件，進入while時檢查一次，執行到while底部時也會檢查一次，如果在檢查的時候條件不成立，則跳出迴圈

```
while (input <= 100) {
cin >> input;
}
cout << input;

輸入 →
1
87
100
101
輸出 →
101
```

### 持續輸入

```
int in;
while (cin >> in) {
...
}
```

