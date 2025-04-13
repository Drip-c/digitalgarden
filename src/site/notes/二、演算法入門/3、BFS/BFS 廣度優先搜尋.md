---
{"dg-publish":true,"permalink":"/二、演算法入門/3、BFS/BFS 廣度優先搜尋/"}
---



### 先備知識

- 在Binary Tree中進行Level-Order Traversal，level代表了node與root之距離

![Pasted image 20231106200343.png](/img/user/Picture/Pasted%20image%2020231106200343.png)

- Level=2：path(A-B)、path(A-C)之length為1
- Level=3：path(A-B-D)、path(A-B-E)、path(A-C-F)之length為2
- Level=4：path(A-B-E-G)、path(A-B-E-H)之length為3

### 名詞解釋

- level → 層級
- node → 節點
- root → 根
- path → 路徑
- length → 長度
- front → 前面

### 需要資料項目

- queue：如同Level-Order Traversal，BFS()將使用queue來確保「先被搜尋到的vertex，就先                成為新的搜尋起點」
- color array：利用color標記哪些vertex已經被找到，哪些還沒有
```
 → 白色表示該vertex還沒有被找過
 → 灰色表示該vertex已經被某個vertex找過
 → 黑色表示該vertex已經從queue的隊伍中移除
```
- distance array：記錄每一個vertex與起點vertex之距離
- predecessor array：記錄某個vertex是被哪一個vertex找到的，如此便能回溯路徑

### 流程

#### 初始化

1. 把所有vertex塗成白色
2. 把所有vertex的distance設為無限大(表示從起點vertex走不到，或者還沒有走到)
3. 把所有vertex的predecessor清除
4. 建立空的queue

#### 範例

- 把起點vertex(A)推進queue
1. 將vertex(A)塗成灰色
2. distance[A]設為0
3. predecessor[A]不更動
---
- 以queue的front當作新的起點搜尋 → 新的起點是vertex(A)
1. 檢查所有與vertex(A)相鄰的vertex
2. 將vertex(B)、vertex(C)、vertex(D)的color塗成灰色
3. 將distance[B]、distance[C]、distance[D]設成distance[A]+1=1
4. 將predecessor[B]、predecessor[C]、predecessor[D]設成vertex(A)
5. 把三個vertex按照「找到」的順序，依序推進queue裡
6. 把vertex(A)塗黑
---
- 以queue的front當作新的起點搜尋 → 新的起點是vertex(B)
1. 檢查所有與vertex(B)相鄰的vertex
2. 將vertex(E)的color塗成灰色
3. 將distance[E]設成distance[B]+1=2
4. 將predecessor[E]設成vertex(B)
5. 將vertex(E)推進queue
6. 把vertex(B)塗黑
......

#### 參考圖

![Pasted image 20231204102916.png](/img/user/Pasted%20image%2020231204102916.png)

#### 程式碼

```
#include <iostream>
#include <vector>
#include <list>
#include <queue>

class Graph{
private:
    int num_vertex;
    std::vector< std::list<int> > AdjList;
    int *color,             // 0:白色, 1:灰色, 2:黑色
        *distance,          // 0:起點, 無限大:從起點走不到的vertex
        *predecessor;       
public:
    Graph():num_vertex(0){};           // default constructor
    Graph(int N):num_vertex(N){        // constructor with input: number of vertex
        // initialize Adjacency List
        AdjList.resize(num_vertex);
    };
    void AddEdgeList(int from, int to);
    void BFS(int Start);
};

void Graph::AddEdgeList(int from, int to){
    AdjList[from].push_back(to);
}

void Graph::BFS(int Start){

    color = new int[num_vertex];
    predecessor = new int[num_vertex];
    distance = new int[num_vertex];

    for (int i = 0; i < num_vertex; i++) {  // 初始化
        color[i] = 0;                       
        predecessor[i] = -1;                // -1表示沒有predecessor
        distance[i] = num_vertex+1;         // num_vertex個vertex, 
    }                                       // 最長距離 distance = num_vertex -1條                                                 edge

    std::queue<int> q;
    int i = Start;

    for (int j = 0; j < num_vertex; j++) {  
        if (color[i] == 0) {                // 第一次i會是起點vertex
            color[i] = 1;                  
            distance[i] = 0;                
            predecessor[i] = -1;            
            q.push(i);
            while (!q.empty()) {
                int u = q.front();                  // u 為新的搜尋起點
                for (std::list<int>::iterator itr = AdjList[u].begin();        
                     itr != AdjList[u].end(); itr++) {                         
                    if (color[*itr] == 0) {                // 若被「找到」的vertex是                                                               白色
                        color[*itr] = 1;                   // 塗成灰色
                        distance[*itr] = distance[u] + 1;  
                        predecessor[*itr] = u;             // 更新被「找到」的vertex                                                               的predecessor
                        q.push(*itr);                      // 把vertex推進queue
                    }
                }
                q.pop();        // 把u移出queue
                color[u] = 2;   // 並且把u塗成黑色
            }
        }
    }
}

int main(){
    Graph g1(9);    
    g1.AddEdgeList(0, 1);g1.AddEdgeList(0, 2);g1.AddEdgeList(0, 3);
    g1.AddEdgeList(1, 0);g1.AddEdgeList(1, 4);
    g1.AddEdgeList(2, 0);g1.AddEdgeList(2, 4);g1.AddEdgeList(2, 5);g1.AddEdgeList(2, 6);g1.AddEdgeList(2, 7);
    g1.AddEdgeList(3, 0);g1.AddEdgeList(3, 7);
    g1.AddEdgeList(4, 1);g1.AddEdgeList(4, 2);g1.AddEdgeList(4, 5);
    g1.AddEdgeList(5, 2);g1.AddEdgeList(5, 4);g1.AddEdgeList(5, 8);
    g1.AddEdgeList(6, 2);g1.AddEdgeList(6, 7);g1.AddEdgeList(6, 8);
    g1.AddEdgeList(7, 2);g1.AddEdgeList(7, 3);g1.AddEdgeList(7, 6);
    g1.AddEdgeList(8, 5);g1.AddEdgeList(8, 6);

    g1.BFS(0);    

    return 0;
}
```

