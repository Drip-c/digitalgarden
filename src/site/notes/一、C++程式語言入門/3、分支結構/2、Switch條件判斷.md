---
{"dg-publish":true,"permalink":"/一、C++程式語言入門/3、分支結構/2、Switch條件判斷/"}
---


- 僅能比較特定變數是否為某一數值或字元

```
switch (a) {
	case 1:
		cout << "a = 1";
		break;
	case 2:
		cout << "a = 2";
		break;
	default:
		cout << "a != 1 && a != 2";
		break;
}

輸入 →2
輸出 →a = 2
```

- 若case內沒有相符的則會執行default內的內容 (default與else差不多)
- 每一個case結束時都要加上break;
- **case可以設定範圍**

```
int score;
cin >> score;
switch(score) {
	case 0 ... 59: //範圍為 [0, 59]
		cout << "F";
		break;
	case 60 ... 69:
		cout << "C";
		break;
	case 70 ... 79:
		cout << "B";
		break;
	case 80 ... 89:
		cout << "A";
		break;
	case 90 ... 99:
		cout << "A+";
		break;
	case 100:
		cout << "A++";
		break;
}
```