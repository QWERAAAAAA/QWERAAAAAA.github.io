> 借助二维数组来表示元素之间的关系

**一个用于存储邻接矩阵的二维数组 ➕ 一个一维数组来存储顶点信息**（核心）

- 有向图的邻接矩阵 存储0/1——表示元素之间的关系
- 网的邻接矩阵 存储权值和∞ ——表示元素之间的关系+权重



#### 采用邻接矩阵表示法创建无向网

【算法步骤】

1. 输入总顶点数和总边数。
2. 依次输入点的信息并将其存入顶点表中。
3. 初始化邻接矩阵。使得每个权值初始化为极大值。
4. 构造邻接矩阵。依次输入每条边依附的顶点和其权值，确定两个顶点在图中的位置之后，使相应边赋予相应的权值，同时使其对称边赋予相同的权值。



【细节注意】

1. 步骤：输入总顶点数、总边数 ——> 输入顶点表 ——> 初始化邻接矩阵置♾️ ——> 构造邻接矩阵

2. 如何构造邻接矩阵：

   1. 通过两点确定一条边 < v1,   v 2>，依次输入点的data   v1，v2
   2. 输入这条边的权值w
   3. 通过LOCATE函数在顶点表中找到 V1和   V2的下标，分别赋值给i和j，
   4. 这样可以定位到矩阵中的位置【i】【j】了
   5. 将w赋值给这个位置，同时也赋值给它对称的位置。

   

```
// 图的邻接矩阵存储表示
#include<iostream>
using namespace std;

#define MaxInt 32767    // 表示极大值，∞
#define MVNum 100   // 最大顶点数
#define OK 1

typedef char VerTexType;    // 假设顶点的数据类型为字符型
typedef int ArcType;    // 假设边的权值类型为整数
typedef struct {
    VerTexType vexs[MVNum];     // 顶点表
    ArcType arcs[MVNum][MVNum];      // 邻接矩阵
    int vexnum, arcnum;         // 图当前点数和边数
}AMGraph;

// 采用邻接矩阵表示法创建无向网

ArcType CreateUDN(AMGraph &G){
    cin>>G.vexnum>>G.arcnum;    // 输入总顶点数，总边数
    for(i=0;i<G.vexnum;i++)     // 依次输入点的信息
        cin>>G.vexs[i];
    for(i=0;i<G.vexnum;++i){        // 初始化邻接矩阵，边的权值置为极大值
        for(j=0; j<G.vexnum; ++j)
        G.arcs[i][j] = MaxInt;
    }
    for(i=0; i < G.arcnum; k++){    // 构造邻接矩阵!!!
        cin>>v1>>v2>>w;                 
        i = LocateVex(G,v1);
        j = LocateVex(G,v2);
        G.arcs[i][j] = w;
        G.arcs[j][i] = G.arcs[i][j];
    }
    return OK;
}
```



【算法分析】

1. 算法的时间复杂度是O(n^2)
2. 若要建立无向图，只需要改动两个地方
   1. 初始化邻接矩阵时，将边的权值均初始化为0
   2. 构造邻接矩阵时，将权值w改为常量值1即可

