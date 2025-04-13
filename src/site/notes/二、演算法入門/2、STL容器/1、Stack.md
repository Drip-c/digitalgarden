---
{"dg-publish":true,"permalink":"/二、演算法入門/2、STL容器/1、Stack/"}
---


- 概念於  [[一、C++程式語言入門/6、結構、函數、堆疊與遞迴/3、堆疊 (Stack)\|3、堆疊 (Stack)]]

### 使用方式

#### 標頭檔

```
#include <stack>
```

#### 宣告

```
stack<儲存變數型態> Stack名稱;

ex.
stack<string> stack_string;
stack< stack<int> > stack_stack_int; //在stack裡面儲存stack
```

### 範例

第一行有一個n (n <= 100000)
接下來有n行
每一行一開始有一個數字，代表哪一種操作
如果數字為1，代表刪除操作
如果數字為2，請輸出當前stack的頂端元素
如果數字為3，請在讀入一個整數丟進堆疊

```
#include <iostream>
#include <stack>
using namespace std;

int main() {
    int n;
    int cmd;
    cin >> n;     
    stack<int> MyStack; //宣告stack資料結構
    
    while (n--) { //執行n次
        cin >> cmd;
        switch (cmd) {
            case 1:
                MyStack.pop(); //將最上面的數字刪除
                break;
            case 2:
                cout << MyStack.top() << endl; //MyStack.top()將回傳最上方的數字
                break;
            case 3:
                cin >> cmd;
                MyStack.push(cmd); //將「cmd」放到Stack的最上層
        }
    }
    return 0;
}

輸入 →
5
3 10
3 15
2
1
2

輸出 →
15
10
```

