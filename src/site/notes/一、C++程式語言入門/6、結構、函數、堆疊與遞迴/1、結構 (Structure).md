---
{"dg-publish":true,"permalink":"/一、C++程式語言入門/6、結構、函數、堆疊與遞迴/1、結構 (Structure)/"}
---


- **用於一組變數需要一起宣告時**
- 定義方法 →

```
struct student {
	char name[7]; //姓名
	char id; //學號
	float score; //成績
	int rate; //排名
}student1, student2;
```

- 存取 → 變數名稱 . 結構成員

```
struct student {
	char name[20];
	char id[9];
	float score;
	int rate;
}student1;

int main() {
	cin >> student1.name;
	cin >> student1.id;
	cin >> student1.score;
	cin >> student1.rate;

	cout << student1.name << endl;
	cout << student1.id << endl;
	cout << student1.score << endl;
	cout << student1.rate << endl;
}

輸入 →
John
11110540
60
15

輸出 →
John
11110540
60
15
```

- 使用陣列的宣告方式

```
struct student {
	char name[20];
	char id[7];
	float score;
	int rate;
}student2[2];

int main() {
	for (int i = 0; i < 2; i++) {
		cin >> student2[i].name;
		cin >> student2[i].id;
		cin >> student2[i].score;
		cin >> student2[i].rate;
	}
	cout << student2[1].name << endl;
	cout << student2[1].id << endl;
	cout << student2[1].score << endl;
	cout << student2[1].rate << endl;
}

輸入 →
Jack
11110550
70.5
10
John
11110540
60
15

輸出 →
John
11110540
60
15
```