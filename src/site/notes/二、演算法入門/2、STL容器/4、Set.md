---
{"dg-publish":true,"permalink":"/二、演算法入門/2、STL容器/4、Set/"}
---


- 是一個集合 → 不會包含重複的元素
- 裡面的元素會**按照大小排序**

### 使用方式

#### 標頭檔

```
#include <set>
```

#### 宣告

```
set<儲存變數型態> set名稱;

ex.
set<int> a;
set<string> b; // 將採用字典順序方法排序
```

#### 基本操作

- insert( 資料 )：將資料新增到set裡面
- erase( 資料 )：將資料從set中移除
- begin()：回傳set一開始的迭代器(iterator)
- end()：回傳set尾部的迭代器
- a.find(資料)：群找資料，並回傳該資料的迭代器，
                        若不存在則回傳end()

### 範例

```
#include <iostream>
#include <set>
using namespace std;

int main() {
    set<int> s;
    
    s.insert(-1);
    s.insert(3);
    s.insert(1);
    s.insert(5);
    s.insert(7);
    s.insert(9);
    
    if (s.find(0) != s.end()) { //檢查0是否存在
        cout << "0 is in set!" << endl;
    }else {
        cout << "0 isn't in set!" << endl;
    }
    
    for (set<int>::iterator it = s.begin(); it != s.end(); it++) { //輸出set裡的資料
        cout << *it << ' ';
    }
    
    return 0;
}

輸出 →
0 isn't in set!
-1 1 3 5 7 9
```

- set< int >::iterator → 儲存int的set的迭代器 → set的指標

