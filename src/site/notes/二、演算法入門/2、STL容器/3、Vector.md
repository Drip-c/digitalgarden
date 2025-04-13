---
{"dg-publish":true,"permalink":"/二、演算法入門/2、STL容器/3、Vector/"}
---


- 類似一般常見的陣列(Array)

### 使用方式

#### 標頭檔

```
#include <vector>
```

#### 宣告

```
vector<儲存變數型態> vector名稱;

ex.
vector<string> vector_string;
vector< vector<int> > vector_2D; // vector裡面再存一個vector，達到2D陣列的效果
```

#### 基本操作

- push_back( 資料 )：將資料新增到Vector**尾部**
- ［元素位置］：讀寫「元素位置」的資料
- size()：回傳vector目前有幾筆資料

### 範例

```
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> vec;
    vec.push_back(5);
    vec.push_back(4);
    vec.push_back(3);
    vec.push_back(2);
    vec.push_back(1);
    
    cout << vec.size() << endl;
    for (int i = 0; i < vec.size(); i++) {
        cout << vec[i] << ' ';
    }
    vec[1] = -1;
    for (int i = 0; i < vec.size(); i++) {
        cout << vec[i] << ' ';
    }
    
    return 0;
}

輸出 →
5
5 4 3 2 1
5 -1 3 2 1
```
