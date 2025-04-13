---
{"dg-publish":true,"permalink":"/二、演算法入門/2、STL容器/5、Map/"}
---


- 讀取陣列要透過索引值(Index)
- 索引值**為字串或範圍很大時**用

### 使用方法

#### 標頭檔

```
#include <map>
```

#### 宣告方式

- 給定兩個變數型態，第一個為index的型態，第二為儲存資料的型態

```
map<long long int, int> a;
map<string, int> b;
```

#### 基本操作

- 當成陣列存取
- 儲存的變數**預設為0**

```
#include <iostream>
#include <map>
using namespace std;

int main() {
    string index;
    index = "123";
    map<string, int> m;
    m[index]++;
    cout << m[index];
    
    return 0;
}

輸出 →
1
```

### 範例

```
#include <iostream>
#include <map>
using namespace std;

int main() {
    map<string, int> m;
    m["hello"] = 10;
    m["apple"] = 5;
    m["cpp"] = 11;
    for (map<string, int>::iterator it = m.begin();
        it != m.end(); it++) {
        cout << "Index: " << it->first << "   value: "
             << it->second << endl;
     }
     
     return 0;
 }

輸出 →
Index: apple value: 5
Index: cpp value: 11
Index: hello value: 10
```
