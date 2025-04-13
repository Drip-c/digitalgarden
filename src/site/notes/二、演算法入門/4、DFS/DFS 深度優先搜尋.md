---
{"dg-publish":true,"permalink":"/二、演算法入門/4、DFS/DFS 深度優先搜尋/"}
---


### 先備知識

- Pre-Order Traversal，其Visiting順序：「Current(V)-left(L)-right(R)」

![Pasted image 20231030105906.png](/img/user/Picture/Pasted%20image%2020231030105906.png)

- 上圖得A B D E G H C F (中 → 左 → 右)

### 名詞解釋

- Graph → 圖形
- vertex → 頂點
- edge → 邊
- descendant → 後代
- ancestor → 祖先

### 需要資料項目

- time：在整個DFS()的過程會有一條「時間軸」，若Graph中有n個vertex，「時間軸」上一              共會有2n個「時間點」
- discover與finish array：每個vertex會被標記上兩個「時間點」，分別是「被發現                                                        (discover)」的時間與「結束(finish)」的時間：
```
 → discover：例如，vertex(B)被vertex(A)找到，則discover[B]會是discover[A]加一，表示                vertex(B)在整個時間軸上是在vertex(A)之後被找到
 
 → finish：若vertex(B)已經經由有效edge探索過所有與之相連的vertex，表示以vertex(B)為起點            的探索已經結束，便標上finish[B]
```
- color array：利用顏色標記哪些vertex已經「被發現」與「結束」。
```
 → 白色表示該vertex還沒有「被發現」
 → 灰色表示該vertex已經「被發現」，但是還沒有「結束」
 → 黑色表示該vertex已經「結束」
```
- predecessor array：記錄某個vertex是被哪一個vertex找到的，如此便能回溯路徑

### 流程

#### 初始化

1. 先把time設為0
2. 把所有vertex塗成白色
3. 把所有vertex的predecessor清除
4. 把所有vertex的discover與finish設成0

#### 範例

- 以vertex(A)作為起點
1. 將vertex(A)塗成灰色
2. 將discover[A]設為++time → discover[A]=1
3. 尋找所有與vertex(A)相連之vertex，只要遇到第一個仍為**白色**的vertex，便把該vertex設為新的起點，並將該vertex之predecessor設為vertex(A)
4. 此時進入「剛發現vertex(A)」，並且尚未結束「以vertex(A)作為起點」的階段
---
- 當vertex(A)、vertex(B)、vertex(D)皆已變灰 → 以vertex(E)作為起點
1. 將vertex(E)塗成灰色
2. 將discover[E]設為++time → discover[E]=4
3. 找不到與vertex(E)相連之白色vertex → 「以vertex(E)作為起點」之搜尋已經結束
4. 將finish[E]設為++time → finish[E]=5
5. 回到vertex(E)的predecessor → 繼續探索其他vertex(D)能夠走到的vertex
---
- 回到vertex(D) → 發現vertex(F)為白色
1. 將vertex(F)塗成灰色
2. 把discover[F]設為++time → discover[F]=6
3. 尋找與vertex(F)相連之白色vertex作為起點
......

#### 流程圖

![DFS_Flow.gif](/img/user/Picture/DFS_Flow.gif)

#### 程式碼

```
#include <iostream>
#include <vector>
#include <list>
#include <queue>
#include <iomanip>      // for std::setw()

class Graph{
private:
    int num_vertex;
    std::vector< std::list<int> > AdjList;
    int *color,             // 0:white, 1:gray, 2:black
        *predecessor,
        *discover,
        *finish;
public:
    Graph():num_vertex(0){};
    Graph(int N):num_vertex(N){
        // initialize Adj List
        AdjList.resize(num_vertex);
    };
    void AddEdgeList(int from, int to);
    void BFS(int Start);    
    void DFS(int Start);
    void DFSVisit(int vertex, int &time);
};

void Graph::DFS(int Start){
    color = new int[num_vertex];           // 配置記憶體位置
    discover = new int[num_vertex];
    finish = new int[num_vertex];
    predecessor = new int[num_vertex];

    int time = 0;                          // 初始化
    for (int i = 0; i < num_vertex; i++) { 
        color[i] = 0;
        discover[i] = 0;
        finish[i] = 0;
        predecessor[i] = -1;
    }

    int i = Start;
    for (int j = 0; j < num_vertex; j++) { // 檢查所有Graph中的vertex都要被搜尋到
        if (color[i] == 0) {               // 若vertex不是白色, 則進行以該vertex作為                                                起點之搜尋
            DFSVisit(i, time);
        }
        i = j;                             // j會把AdjList完整走過一遍, 確保所有                                                    vertex都被搜尋過
    }
}

void Graph::DFSVisit(int vertex, int &time){   // 一旦有vertex被發現而且是白色, 便進入DFSVisit()
    color[vertex] = 1;                         // 把vertex塗成灰色
    discover[vertex] = ++time;                 // 更新vertex的discover時間
    for (std::list<int>::iterator itr = AdjList[vertex].begin();   // for loop參數                                                                        太長
         itr != AdjList[vertex].end(); itr++) {                    // 分成兩段
        if (color[*itr] == 0) {                // 若搜尋到白色的vertex
            predecessor[*itr] = vertex;        // 更新其predecessor
			  DFSVisit(*itr, time);              // 立刻以其作為新的搜尋起點, 進入新                                                      的DFSVisit()
        }
    }
    color[vertex] = 2;                         // 當vertex已經搜尋過所有與之相連的vertex後, 將其塗黑
    finish[vertex] = ++time;                   // 並更新finish時間
}

int main(){
    // 定義一個具有八個vertex的Graph
    Graph g2(8);
    // 建立如圖三之Graph
    g2.AddEdgeList(0, 1);g2.AddEdgeList(0, 2); 
    g2.AddEdgeList(1, 3);
    g2.AddEdgeList(2, 1);g2.AddEdgeList(2, 5);
    g2.AddEdgeList(3, 4);g2.AddEdgeList(3, 5);
    // AdjList[4] is empty
    g2.AddEdgeList(5, 1);
    g2.AddEdgeList(6, 4);g2.AddEdgeList(6, 7);
    g2.AddEdgeList(7, 6);

    g2.DFS(0);    // 以vertex(0), 也就是vertex(A作為DFS()的起點

    return 0;
}
```

### ancestor-descendant關係

1. 若discover[X]比discover[Y]大，而且finish[X]比finish[Y]小，表示vertex(X)比vertex(Y)較晚「被發現」，而且較早「結束」，則vertex(X)必定是vertex(Y)的descendant
2. 若discover[X]比discover[Y]小，而且finish[X]比finish[Y]大，表示vertex(X)比vertex(Y)較早「被發現」，而且較晚「結束」，則vertex(X)必定是vertex(Y)的ancestor

### edge類型

1. Tree edge → 若vertex(Y)是被vertex(X)發現，則edge(X,Y)即為Tree edge
2. Back edge → 所有指向ancestor的edge，稱為Back edge
3. Forward edge → 所有指向descendant但**不是Tree edge**的edge，稱為Forward edge
4. Cross edge → 若兩個vertex 1.不在同一棵Depth-First Tree上 
                                                 2.沒有「ancestor-descendant」的關係
                                              →稱為Cross edge

![Pasted image 20231106163942.png](/img/user/Picture/Pasted%20image%2020231106163942.png)