[TOC]



### 树的抽象数据类型定义

基本操作：

1. InitTree(&T)	——	构造树
2. DestroyTree(&T) ——  销毁树
3. CreateTree(&T, definition) —— 按definition构造出树
4. ClearTree(&T) —— 将树清为空树
5. TreeEmpty(T) —— 若树为空树，返回True，否则返回False
6. TreeDepth(T) —— 返回树的深度
7. Root(T) —— 返回树的根
8. Value(T, cur_e) —— cur_e是树T中的某个节点，返回cur_e的值
9. Assign(T, cur_e, value) —— cur_e是树T中的某个节点，节点cur_e赋值为value
10. Parent(T, cur_e) —— cur_e是树T中的某个节点，cur_e非根节点则返回它的双亲
11. LeftChild(T, cur_e) —— 返回左孩子
12. RightSibling(T, cur_e) —— 返回右兄弟
13. InsertChild(&T,p,i,c) —— 插入c为T中p所指节点的第i棵子树
14. DeleteChild(&T,p,i) —— 删除T中p所指节点的第i棵树
15. TraverseTree(T) —— 按某种次序对T的每一个节点访问一次



### 二叉树的抽象数据类型定义

基本操作：

- 1-12基本一致

1. InsertChild(&T,p,LR,c) —— 根据LR为0或1，插入c为T中p所指节点的左或右子树
2. DeleteChild(&T,p,LR) —— 根据LR为0或1，删除T中p所指节点的左或右子树
3. PreOrderTraverse(T) ——先序遍历
4. PostOrderTraverse(T) —— 后序遍历
5. LevelOrderTraverse(T) —— 中序遍历



---



### 二叉树的存储结构



#### 顺序存储结构

