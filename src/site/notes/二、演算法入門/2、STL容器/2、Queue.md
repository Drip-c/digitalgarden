---
{"dg-publish":true,"permalink":"/二、演算法入門/2、STL容器/2、Queue/"}
---


- 中文為「**佇列**」
- **最早進的最早出來；最晚進的最晚出來**

### 使用方式

#### 標頭檔

```
#include <queue>
```

#### 宣告

```
queue<儲存變數型態> queue名稱;

ex.
queue<int> queue_int;
queue<string> queue_string;
```

#### 基本操作

- push( 資料 )：將資料放進Queue**尾部**
- front()：回傳最前方的資料
- pop()：移除最前方的資料
- empty()：回傳queue是否為空
                   1: 空
                   0: 有資料
- size()：回傳queue目前有幾筆資料

### 範例

```
#include <iostream>
#include <queue>
using namespace std;

int main() {
    queue<int> que;
    
    que.push(1);
    que.push(2);
    
    cout << que.front() << endl;
    
    que.push(3);
    
    que.pop();
    
    cout << que.front() << endl;
    cout << que.front() << endl;
    
    que.pop();
    
    cout << que.front() << endl;
    
    return 0;
}

輸出 →
1
2
2
3
```