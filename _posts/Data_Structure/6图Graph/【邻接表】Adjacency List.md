> 图的链式存储结构。

一维数组存表头节点表（顶点表） ➕ 单链表存边表（按邻接点存放）

#### 采用邻接表表示法创建无向图

【算法步骤】

1. 输入总顶点数、总边数
2. 依次输入点的信息存入顶点表中，使得每个表头节点的指针域初始化为NULL
3. 创建邻接表。依次输入每条边依附的两个顶点，确定这两个顶点的序号i和j之后，将此边节点分别插入vi和vj对应的两个边链表的头部。(因为无向图是“双向的”)

```
// 图的邻接表存储结构
#include<iostream>
using namespace std;
#define MVNum 100       //最大顶点数
#define OK 1
typedef char VerTexType;    // 假设顶点的数据类型为字符型

typedef struct ArcNode{         // 边节点
    int adjvex;                 // 该边所指向顶点的位置
    struct ArcNode *nextarc;    // 指向下一条的指针
    OtherInfo info;             // 与边相关的信息
}ArcNode;

typedef struct VNode{           // 顶点信息
    VarTexType data;
    ArcNode *firstarc;
}Vnode, AdjList[MVNum];         //AdjList 表示邻接表类型（一维数组）

typedef struct          // 邻接表
{
    AdjList vertices;
    int vexnum, arcnum;         // 图的当前顶点数和边数
}ALGraph;

// 采用邻接表表示法创建无向网
Status CreateUDN(ALGraph &G){
    cin>>G.vexnum>>G.arcnum;
    for(i=0; i<G.vexnum; i++){
        cin>>G.vertices[i].data;
        G.vertices[i].firstarc = NULL;
    }

    for(k = 0; k<G.arcnum; k++){
        cin>>v1>>v2;
        i = LocateVex(G, v1);
        j = LocateVex(G, v2);
        p1 = new ArcNode;
        p1 -> adjvex = j;
        p1 -> nextarc = G.vertices[i].firstarc;     // 先将next域置空，等待进一步操作
        G.vertices[i].firstarc = p1;
        p2 - new ArcNode;
        p2 -> adjvex = i;
        p2 -> nextarc = G.vertices[j].firstarc;
        G.vertices[j].firstarc = p2;
    }
    return OK;
}
```



【算法分析】

1. 时间复杂度是O（n+e）
2. 建立有向图的邻接表类似，每度一个顶点对<i,j>，仅需要生成一个邻接点序号为j的边表节点，并插入vi的边链表头部即可。
3. 建立网的邻接表，可以将边的权值存储在info域中。
