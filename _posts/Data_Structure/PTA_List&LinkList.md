[TOC]

### 练习一（绪论）

#### 鸡兔同笼

> 7-1 鸡兔同笼 (10 分)
>
> 一个笼子里面关了鸡和兔子（鸡有2只脚，兔子有4只脚，没有例外）。已经知道了笼子里面脚的总数a，问笼子里面至少有多少只动物，至多有多少只动物
>
> 输入格式:
>
> 第1行是测试数据的组数n，后面跟着n行输入。每组测试数据占1行，包括一个正整数a (a < 32768)。
>
> 输出格式:
>
> n行，每行输出对应一个输入。输出是两个正整数，第一个是最少的动物数，第二个是最多的动物数，两个正整数用空格分开。如果没有满足要求的情况出现，则输出2个0。

```C++
#include<iostream>
using namespace std;
int main(){
    int n,a[100],max=0,min=0;
    cin>>n;
    for(int i=0;i<n;i++){
        cin>>a[i];
    }
    for(int i=0;i<n;i++){
        if(a[i]%2!=0 || a[i]==0){			// 多多考虑，测试数据的多样性
            cout<<"0 0"<<endl;			// 奇数一定不可能
        }
        else {
            if(a[i]%4==0){		// 可以整除4
                max=a[i]/2;
                min=a[i]/4;
            }
            else{
                max=a[i]/2;		
                min=a[i]/4+1;			// 不可以整除4，一定余下一个2，所以min要+1
            }
            cout<<min<<" "<<max<<endl;
        }
    }
    return 0;
}
```

---

#### 4洗牌

> 输入规格:
> 洗牌是将一副扑克牌随机化的过程。因为标准的洗牌技术被认为是薄弱的，而且为了避免“内部工作”，即员工通过不充分的洗牌来与赌徒合作，许多赌场使用自动洗牌机。你的任务是模拟洗牌机。这台机器按照给定的随机顺序洗牌54张牌，并重复给定的次数。假设一副牌的初始状态为:
>
> S1, S2,…S13,
> H1, H2,…H13,
> C1, C2,…、C13、
> D1, D2,…D13,
> J1, J2
> 其中“S”代表“铁锹”，“H”代表“心”，“C”代表“俱乐部”，“D”代表“钻石”，“J”代表“小丑”。给定的顺序是在[1,54]中不同整数的排列。如果第i个位置的数字是j，这意味着将纸牌从位置i移动到位置j。
>
> 例如，假设我们只有5张纸牌:S3、H5、C1、D13和J2。给定洗牌顺序{4,2,5,3,1}，结果为:J2, H5, D13, S3, C1。如果我们再重复洗牌，结果是:C1, H5, S3, J2, D13。
>
> 每个输入文件包含一个测试用例。对于每种情况，第一行包含一个正整数K(≤20)，这是重复的次数。然后下一行包含给定的订单。一行中的所有数字用一个空格隔开。

```
2
36 52 37 38 3 39 40 53 54 41 11 12 13 42 43 44 2 4 23 24 25 26 27 6 7 8 48 49 50 51 9 10 14 15 16 5 17 18 19 1 20 21 22 28 29 30 31 32 33 34 35 45 46 47
```

```
S7 C11 C10 C12 S1 H7 H8 H9 D8 D9 S11 S12 S13 D10 D11 D12 S3 S4 S6 S10 H1 H2 C13 D2 D3 D4 H6 H3 D13 J1 J2 C1 C2 C3 C4 D1 S5 H5 H11 H12 C6 C7 C8 C9 S2 S8 S9 H10 D5 D6 D7 H4 H13 C5
```

```C++
#include <iostream>
using namespace std;
int main()
{
	// 1、存牌
	// S：1-13；H：14-26；C:27-39; D:40-52; J1:53; J2:54 
  // 这些字母标号可以考虑在输出时再把它们加进来！
	int card[55];
	for(int i=1;i<55;i++)
	{
		card[i]=i;
	}
	
	//2、输入洗牌顺序 
	int n,sort[55];
	cin>>n;
	for(int i=1;i<55;i++)
	{
		cin>>sort[i];
	}
	
	//3、按题目要求洗牌  //关键部分！
	int ans[55];
	while(n--)	// 洗牌次数
	{
		for(int i=1;i<55;i++)
		{
			ans[sort[i]]=card[i];		
		}
		for(int i=1;i<55;i++)
		{
			card[i]=ans[i];		//这里也要把card更新了，以便下一次洗牌。
		}
		
	} 
	
	//4、按要求输出
	for(int i=1;i<55;i++)
	{
		if(i!=1) cout<<" ";		// 真是逐点突破
		if(ans[i]>=1&&ans[i]<=13)  cout<<"S"<<ans[i];
		else if(ans[i]>=14&&ans[i]<=26) cout<<"H"<<ans[i]-13;
		else if(ans[i]>=27&&ans[i]<=39) cout<<"C"<<ans[i]-26;
		else if(ans[i]>=40&&ans[i]<=52) cout<<"D"<<ans[i]-39;
		else if(ans[i]>=53&&ans[i]<=54) cout<<"J"<<ans[i]-52; 
		
	} 
	return 0;
	
}

```



---

### 练习二（线性表）

#### jmu-ds-顺序表区间元素删除

> 若一个线性表L采用顺序存储结构存储，其中所有的元素为整数。设计一个算法，删除元素值在[x,y]之间的所有元素，要求算法的时间复杂度为O(n)，空间复杂度为O(1)。
>
> 输入格式:
>
> 三行数据，第一行是顺序表的元素个数，第二行是顺序表的元素，第三行是x和y。
>
> 输出格式:
>
> 删除元素值在[x,y]之间的所有元素后的顺序表。

```C++
//第一次：格式错误
#include<iostream>
using namespace std;
int main(){
	int n,arr[100],x,y;
	cin>>n;
	for(int i=0;i<n;i++)
	cin>>arr[i];
	cin>>x>>y;
	for(int i=0;i<n;i++){
		if(arr[i]<x || arr[i]>y)
		cout<<arr[i]<<" ";
	}
	return 0;
}

//第二次 AC
#include<iostream>
using namespace std;
int main(){
	int n,arr[100],x,y,a=0;
	cin>>n;
	for(int i=0;i<n;i++)
	cin>>arr[i];
	cin>>x>>y;
	for(int i=0;i<n;i++){
		if(arr[i]<x || arr[i]>y){
			arr[a]=arr[i];
			a++;
		}
	}
	for(int i=0;i<a;i++){
		if(i==0) cout<<arr[i];
		else cout<<" "<<arr[i];
	}
	return 0;
}
```





#### 基于顺序存储结构的图书信息表的创建和输出

> 定义一个包含图书信息（书号、书名、价格）的顺序表，读入相应的图书数据来完成图书信息表的创建，然后统计图书表中的图书个数，同时逐行输出每本图书的信息。
>
> 输入格式:
>
> 输入n+1行，其中前n行是n本图书的信息（书号、书名、价格），每本图书信息占一行，书号、书名、价格用空格分隔，价格之后没有空格。最后第n+1行是输入结束标志：0 0 0（空格分隔的三个0）。其中书号和书名为字符串类型，价格为浮点数类型。
>
> 输出格式:
>
> 总计n+1行，第1行是所创建的图书表中的图书个数，后n行是n本图书的信息（书号、书名、价格），每本图书信息占一行，书号、书名、价格用空格分隔。其中价格输出保留两位小数。
>
> 输入样例:
>
> 在这里给出一组输入。例如：
>
> ```in
> 9787302257646 Data-Structure 35.00
> 9787302164340 Operating-System 50.00
> 9787302219972 Software-Engineer 32.00
> 9787302203513 Database-Principles 36.00
> 9787810827430 Discrete-Mathematics 36.00
> 9787302257800 Data-Structure 62.00
> 9787811234923 Compiler-Principles 62.00
> 9787822234110 The-C-Programming-Language 38.00
> 0 0 0
> ```
>
> 输出样例:
>
> 在这里给出相应的输出。例如：
>
> ```out
> 8
> 9787302257646 Data-Structure 35.00
> 9787302164340 Operating-System 50.00
> 9787302219972 Software-Engineer 32.00
> 9787302203513 Database-Principles 36.00
> 9787810827430 Discrete-Mathematics 36.00
> 9787302257800 Data-Structure 62.00
> 9787811234923 Compiler-Principles 62.00
> 9787822234110 The-C-Programming-Language 38.00
> ```



```
#include <iostream>
#include <iomanip>
using namespace std;
typedef struct LNode
{
	string ISBN;
	string name;
	double price;
	struct LNode *next;
}LNode,*Linklist;
// 1 创建链表
int Create_to_count(Linklist &L)
{
	L=new LNode;
	L->next=NULL;
	Linklist s=L;
	string ISBN;
	string  name;
	double price;
	int num=0; 
	while(1)
	{
		cin>>ISBN>>name>>price;
		if(ISBN=="0"||name=="0"||price==0) break;
		Linklist p=new LNode;
		p->ISBN=ISBN;
		p->name=name;
		p->price=price;
		p->next=NULL;
		s->next=p;
		s=p;
		num++;
	}
	return num;
}
int main()
{
	Linklist L;
	int num=Create_to_count(L);
	Linklist r;
	r=L->next;
	cout<<num<<endl;
	while(r)
	{
		cout.precision(2);
		cout<<r->ISBN<<" "<<r->name<<" "<<fixed<<r->price;
		if(r->next) cout<<endl;
		r=r->next;
		
	}	
} 

```



#### 7-4 递增有序顺序表的插入

> 实验目的：1、掌握线性表的基本知识 2、深入理解、掌握并灵活运用线性表。3、熟练掌握线性表的存储结构及主要运算的实现 已知顺序表L递增有序，将X插入到线性表的适当位置上，保证线性表有序。。
>
> 输入格式:
>
> 第1行输入顺序表长度，第2行输入递增有序的顺序表，第3行输入要插入的数据元素X。
>
> 输出格式:
>
> 对每一组输入，在一行中输出插入X后的递增的顺序表。

```C++
#include<iostream>
using namespace std;
int main(){
	int n,arr[50],a;
	cin>>n;
	for(int i=0;i<n;i++){
		cin>>arr[i];
	}
	cin>>a;
	for(int i=0;i<n;i++){
		if(arr[i]<a){
			arr[i]=arr[i];
		}
		else{			//这个for循环写的有毛病。
			for(int j=0;j<n-i-1;j++){
				arr[n-j]=arr[n-1-j];
				arr[n-1-j]=arr[i];
			}
			arr[i]=a;
			break;
		}
	}
	for(int i=0;i<n+1;i++){
		cout<<arr[i]<<",";
	}
	return 0;
}


//自己改了几次 终于AC啦！
#include<iostream>
using namespace std;
int main(){
	int n,arr[50],a,b=0,c;
	cin>>n;
	for(int i=0;i<n;i++){
		cin>>arr[i];
	}
	cin>>a;
	for(int i=0;i<n;i++){
		if(arr[i]<a && arr[n-1]>=a){
			arr[i]=arr[i];
		}
		else if(arr[i]==a) {		// a直接和数组中的元素重复了，直接输出原数组就行了
			b=1;
			break;}
		else if(a>arr[n-1]){
			arr[n]=a;
			break;		//这个break一定要写，把a插入这个操作执行一次后，就完成任务啦
		}
		else{
			for(int j=0;j<n-i;j++){
				arr[n-j]=arr[n-1-j];
			}
			arr[i]=a;
			break;
		}
	}
  
	if(b==0) c=n+1;
	else c=n;
  
	for(int i=0;i<c;i++){
		cout<<arr[i]<<",";
	}
	return 0;
}

// 特殊数据：
3 {1 1 1} 2 
5 {1 3 5 7 9} 5
```

### 练习三 （链表）

```
#include<stdio.h>
#include<stdlib.h>

typedef int ElemType;
typedef struct LNode
{
    ElemType data;
    struct LNode *next;
}LNode,*LinkList;

LinkList Create();

int Locate(LinkList L, ElemType  e);

int main()
{
    ElemType e;
    LinkList L = Create();
    scanf("%d",&e);
    printf("%d",&e);
    printf("%d\n",Locate(L,e));
    return 0;
}

LinkList Create(void)
{
    LinkList head = NULL;
    LNode *p, *tail = NULL, copy;
    int n;
    while(1)
    {
        scanf("%d", &n);
        p = (LNode *)malloc(sizeof(LNode));
        
        if(head == NULL)
           head = p;
        else
           tail->next = p;
           
        p->data = n;
        p->next = NULL;
        tail = p;
        if(getchar()== '\n') break;

    }
    return head;
}

int Locate(LinkList L, ElemType  e){
    LinkList p;
    int count=1;
    p = L->next;
    while(p && p->data != e)
    {
        p=p->next;
        count+=1;
        }
    return count;
}
```

答案

```
int Locate ( LinkList L, ElemType e)
{
	LNode *p;
	int loc = 1;
	if(L==NULL)
		return 0;
	else{
 
		p = L->next;
		while(p!=NULL)
		{
			if(p->data!=e)
				{
					loc++;
					p = p->next;	
				}	
			else
				break;
		} 
		if(p==NULL)
		{
			return 0;
		}
		else
			return loc;
	}
}

```

#### 6-2 统计单链表元素出现次数 (5 分)

> 本题要求实现一个函数，统计带头结点的单链表中某个元素出现的次数。
>
> 函数接口定义：
>
> ```c++
> int GetCount ( LinkList L,ElemType e );
> ```
>
> L是带头结点的单链表的头指针，e是要统计次数的元素值。如果e在单链表中存在，函数GetCount返回其出现的次数；否则，返回0。
>
> 裁判测试程序样例：
>
> ```c++
> #include <stdio.h>
> #include <stdlib.h>
> 
> typedef int ElemType;
> typedef struct LNode
> {
>     ElemType data;
>     struct LNode *next;
> }LNode,*LinkList;
> 
> LinkList Create();/* 细节在此不表 */
> 
> int GetCount ( LinkList L, ElemType e);
> 
> int main()
> {
>     ElemType e;
>     LinkList L = Create();
>     scanf("%d",&e);
>     printf("%d\n", GetCount(L,e));
>     return 0;
> }
> LinkList Create()
> {
>     LinkList L,r,p;
>     ElemType e;
>     L = (LinkList)malloc(sizeof(LNode));
>     L->next = NULL;
>     r = L;
>     scanf("%d",&e);
>     while(e!=-1)
>     {
>         p = (LinkList)malloc(sizeof(LNode));
>         p->data = e;
>         p->next = r->next;
>         r->next = p;
>         r = p;
>         scanf("%d",&e);
>     }
>     return L;
> }
> 
> ```

```

int GetCount ( LinkList L, ElemType e){
    LNode *p;
    int count = 0;
    if(L==NULL)
        return 0;
    else{
        p = L->next;
    }
    while(p!=NULL){
        if(p->data!=e){
            p=p->next;
        }
        else {
            count+=1;
            p=p->next;
        }
    }
    return count;
}
```

#### **带头结点的单链表插入操作**

> 本题要求实现带头结点的单链表插入操作，插入成功返回1，否则返回0。
>
> 函数接口定义：
>
> ```c（gcc)
> int insert_link ( LinkList L,int i,ElemType e);
> ```
>
> L是单链表的头指针，i为插入位置，e是插入的数据元素，插入成功返回1，否则返回0。
>
> 裁判测试程序样例：
>
> ```c（gcc)
> #include <stdio.h>
> #include <stdlib.h>
> 
> typedef int ElemType;
> typedef struct LNode
> {
>     ElemType data;
>     struct LNode *next;
> }LNode,*LinkList;
> 
> LinkList Create();/* 细节在此不表 */
> void print( LinkList L);
> int insert_link ( LinkList L,int i,ElemType e);
>  
> int main()
> {
>     int position,insert_data;int flag;
>     LinkList L = Create();
>     scanf("%d",&position);
>     scanf("%d",&insert_data);    
>     flag=insert_link(L,position,insert_data);
>     if(flag) 
>     {
>         print(L);
>     }
>     else 
>     { 
>         printf("Wrong Position for Insertion");
>     }
>     return 0;
> }
> void print(LinkList L)
> { 
>     LinkList p;
>     p=L->next;
>     while (p)
>     {
>          printf("%d ", p->data);
>          p =p->next;
>     }
> }
> /* 请在这里填写答案 */
> ```
>
> 输入格式：
>
> 输入数据为三行，第一行是若干正整数，最后以-1表示结尾（-1不算在序列内，不要处理）。所有数据之间用空格分隔。 第二行数据是插入位置，第三行数据是被插入元素值。
>
> 输入样例：
>
> ```in
> 1 2 3 4 5 6 -1
> 2 
> 100
> ```
>
> 输出样例：
>
> ```out
> 1 100 2 3 4 5 6 
> ```

```
int insert_link ( LinkList L,int i,ElemType e)
{
    LinkList p=L,s;
    s=(LinkList)malloc(sizeof(LNode));
    int count=0;
    while(p)
    {
        count++;
        if(count==i)
        {
            s->data=e;
            s->next=p->next;
            p->next=s;
            return 1;
        }
        p=p->next;
    }
    return 0;
}
```

#### **6-4 带头结点的单链表删除操作 (5 分)**

> 本题要求实现删除单链表的第i个元素结点，删除成功返回1，否则返回0。
>
> 函数接口定义：
>
> ```c++
> int delete_link ( LinkList L,int i);
> ```
>
> L为单链表的头指针，i为删除结点的序号。
>
> 裁判测试程序样例：
>
> ```c（gcc)
> #include <stdio.h>
> #include <stdlib.h>
> 
> typedef int ElemType;
> typedef struct LNode
> {
>     ElemType data;
>     struct LNode *next;
> }LNode,*LinkList;
> 
> LinkList Create();/* 细节在此不表 */
> void print( LinkList L);
> int delete_link ( LinkList L,int i);
>  
> int main()
> {
>     
>     LinkList L = Create();
>     int position;int flag;
>     scanf("%d",&position);
>     flag=delete_link(L,position);
>     if(flag) 
>     {
>         print(L);
>     }
>     else 
>     { 
>         printf("Wrong Position for Deletion");
>     }
>     return 0;
> }
> void print(LinkList L)
> { 
>     LinkList p;
>     p=L->next;
>     while (p)
>     {
>         printf("%d ", p->data);
>         p =p->next;
>     }
> }
> 
> /* 请在这里填写答案 */
> ```
>
> 输入格式：
>
> 输入数据为两行，第一行是若干正整数，最后以-1表示结尾（-1不算在序列内，不要处理）。所有数据之间用空格分隔。 第二行数据是删除位置。
>
> 输入样例：
>
> ```in
> 1 2 3 4 5 6 -1
> 3
> ```
>
> 输出样例：
>
> 1 2 4 5 6 

```
int delete_link ( LinkList L,int i)
{
    if(i<=0) return 0;
    LinkList p = L;
    int cnt = 1;
    while(p&&cnt<i)
    {
        p = p->next;
        cnt++;
    }
    if(p->next==NULL) return 0;
    LNode*pre=p->next;
    p->next=pre->next;
    free(pre);//free()是C语言中释放内存空间的函数，通常与申请内存空间的函数malloc()结合使用，
    //可以释放由 malloc()、calloc()、realloc() 等函数申请的内存空间。
    return 1;
}
```

#### **7-2 单链表中确定值最大的结点 (10 分)**

> 输入若干个不超过100的整数，建立单链表，然后通过一趟遍历在单链表中确定值最大的结点。输出该结点的值及其序号。
>
> **输入格式:**
>
> 首先输入一个整数T，表示测试数据的组数，然后是T组测试数据。每组测试数据在一行上输入数据个数n及n个不超过100的整数。
>
> **输出格式:**
>
> 对于每组测试，输出单链表中值最大的结点的值和该结点的序号。输出格式如下： “max=dmax num=dnum” 其中，dmax表示最大的结点的值，dnum表示最大的结点的值所在结点的序号。若有多个相同的最大值，则以首次出现的为准。
>
> **输入样例:**
>
> ```in
> 1
> 30 85 97 43 70 69 29 77 22 64 25 55 39 95 69 99 61 97 69 59 12 88 55 75 66 13 75 36 85 67 69
> ```
>
> **输出样例:**
>
> ```out
> max=99 num=15
> ```

```
#include<stdio.h>
#include<stdlib.h>
#include<limits.h>//该头文件中定义了int的最大数INT_MAX和最小数INT_MIN
typedef struct node{
    int data;
    struct node *next;
}Node;
int main(){
    int T,n,value;
    scanf("%d",&T);
    while(T--){
        Node *p,*q,*head=NULL,*t;
        int max=INT_MIN,index=0,num=0;
        scanf("%d",&n);
        while(n--){
            scanf("%d",&value);
            index++;//用来记录当前的下标
            if(value>max){
                max=value;
                num=index;//记录当前最大值的下标
            }
            p=(Node*)malloc(sizeof(Node));
            p->next=NULL;
            if(head==NULL){
                head=p;
            }
            else{
                q->next=p;
            }
            q=p;
        }
        printf("max=%d num=%d\n",max,num);
    }
    return 0;
}


```

### 练习四

#### 线性表合并

> 求解一般集合的并集问题。 已知两个集合A和B，现要求一个新的集合A=AUB。例如，设 A=(7,5,3,11) B=(2,6,3) 合并后 A=(7,5,3,11,2,6)
>
> 输入格式:
>
> 第一行输入集合A的元素个数，第二行输入集合A的各元素值。 第三行输入集合B的元素个数，第四行输入集合B的各元素值。
>
> 输出格式:
>
> 输出完成合并后的集合A。
>
> 输入样例:
>
> 在这里给出一组输入。例如：
>
> ```in
> 4
> 7 5 3 11
> 3
> 2 6 3
> ```
>
> 输出样例:
>
> 在这里给出相应的输出。例如：
>
> ```out
> 7 5 3 11 2 6 
> ```

```
#include<iostream>
using namespace std;
int main(){
    int n,m,a[20],b[10],c=1,i=0;
    cin>>n;
    for(int i=0;i<n;i++) cin>>a[i];
    cin>>m;
    for(int i=0;i<m;i++) cin>>b[i];
    while(1){
        for(int j=0;j<n;j++){
            if(b[i]!=a[j]){
                a[n-1+c]=b[i];
                c+=1;
                break;
            }
        }
        i+=1;
        if(i==m-1)
            break;
    }
    for(int k=0;k<n+c-1;k++){
        if(k==0) cout<<a[k];
        else cout<<" "<<a[k];
    }
    return 0;
}
// 多种错误

```

```c
// AC code
#include<stdio.h>
int main(){
    int x,y,i,j,num;
    int count=0;
    scanf("%d",&x);
    count=x;
    int a[x+1000];
    for(i=0;i<x;i++){
        scanf("%d",&a[i]);
    }
    scanf("%d",&y);
    for(i=0;i<y;i++){
        scanf("%d",&num);
        int flag=0;
        for(j=0;j<x;j++){
            if(a[j]==num){
                flag=1;
                break;
            }
        }
        if(flag==0){
            a[count++]=num;
        }
    }
    printf("%d ",a[0]);
    for(i=1;i<count;i++){
        if(a[i]!=a[i-1])
            printf("%d ",a[i]);
    }
    return 0;
}

```

#### 删除重复元素

```
#include<iostream>
using namespace std;
int main(){
    int t,n,ori[100],fin[100],a=0;
    cin>>t;
    for(int i=0;i<t;i++){
        cin>>n;
        for(int j=0;j<n;j++)
            cin>>ori[j];
        for(int j=0;j<n-1;j++){
            for(int k=0;k<n-j-1;k++){
                if(ori[k]>=ori[k+1]){
                    int temp = ori[k];
                    ori[k]=ori[k+1];
                    ori[k+1]=temp;
                }
            }
        }
        // for(int j=0;j<n;j++) cout<<" "<<ori[j];
        fin[0]=ori[0];
        for(int j=0;j<n;j++){
                if(ori[j]!=fin[a]){
                    fin[a+1]=ori[j];
                    a++;
                }
        }
       for(int j=0;j<=a;j++){
           if(j==0) cout<<fin[j];
           else cout<<" "<<fin[j];
       }
    }
    return 0;
}
// WA 他就是想让我输出整个链表（后面可以添加数据）

// 知道问题在哪了。一组测试数据后没有把a置为0，导致第二组测试数据a值还为上组测试数据的a值。
// 但是还是格式错误！

```

```c
// AC_code 还是要熟练指针的运用
#include <stdio.h>
 
int chongfu(int *a, int n);
void zuixiao(int *a, int n);
int main()
{
    int t, i, j, n, x;
    scanf("%d",&t);                     //输入测试组数t
    for(i = 1; i <= t; i++)
    {
        scanf("%d",&n);
        int a[n];               //输入数组元素数
        for(j = 0; j < n; j++)
        {
            scanf("%d",&a[j]);          //给数组赋值
        }
        x = chongfu(a, n);              //对数组a进行了修改，并得到了返回值
        zuixiao(a, x);                  //对修改的数组进行排序
        for(j = 0; j < x; j++)          //按照格式输出
        {
            if(j == 0)
                printf("%d",a[j]);
            else
                printf(" %d",a[j]);
        }
        printf("\n");
 
    }
 
 
}
int chongfu(int *a, int n)                    //将重复数组元素删除的函数
{
    int *pa, *pb, *pc;
    for(pa = a; pa < a+n; pa++)               //从第一个开始往后比较
    {
        for(pb = pa+1; pb < a+n; pb++)
        {
            if(*pb == *pa)                    //当出现重复数的时候
            {
                for(pc = pb; pc < a+n-1; pc++)//从这个数开始，后面的数将前面的数覆盖掉
                {
                    *pc = *(pc+1);
                } 
                pb--;                         //因为位置前移了一个，所以pb要减一位
                n--;                          //用返回值将要输出的数组元素个数返回去
            }
        }
    }
    return n;
}
void zuixiao(int *a, int n)                   //比大小的函数，冒泡法
{
    int *pa, *pb, m;
    for(pa = a; pa < a+n; pa++)
    {
        for(pb = pa+1; pb < a+n; pb++)
        {
            if(*pb < *pa)
            {
                m = *pb;
                *pb = *pa;
                *pa = m;
            }
        }
    }
}
```

#### 集合减法

> 给定两个非空集合A和B，集合的元素为30000以内的正整数，编写程序求A-B。
>
> 输入格式:
>
> 输入为三行。第1行为两个整数n和m，分别为集合A和B包含的元素个数，1≤n, m ≤10000。第2行表示集合A，为n个空格间隔的正整数，每个正整数不超过30000。第3行表示集合B，为m个空格间隔的正整数，每个正整数不超过30000。
>
> 输出格式:
>
> 输出为一行整数，表示A-B，每个整数后一个空格，各元素按递增顺序输出。若A-B为空集，则输出0，0后无空格。
>
> 输入样例:
>
> ```in
> 5 5
> 1 2 3 4 5
> 3 4 5 6 7
> ```
>
> 输出样例:
>
> ```out
> 1 2 
> ```

```
#include <iostream>
#include <stdio.h>
#include <stdlib.h>
#define maxsize 10000
using namespace std;
typedef struct
{
    int data[maxsize];
    int length;
}sqlist;
int main()
{
    sqlist *c=(sqlist*)malloc(sizeof(sqlist));
    c->length=0;
    int n,m;
    cin>>n>>m;
    sqlist *a=new sqlist;
    sqlist *b=new sqlist;
    for(int i=0;i<n;i++)
        cin>>a->data[i];
    a->length=n;
    for(int j=0;j<m;j++)
        cin>>b->data[j];
    b->length=m;
    int i=0,j=0,x=0;
    while(i<a->length&&j<b->length)
    {
        if(a->data[i]<b->data[j])
        {
            c->data[x]=a->data[i];
            x++;
            i++;
        }
        else if(a->data[i]==b->data[j])
        {
            i++;
            j++;
        }
        else
            j++;
    }
    int y=i;
    for(int k=y;k<a->length;k++)
    {
        c->data[x++]=a->data[k];
    }
    c->length=x;
    if(c->length==0)
    {
        printf("0");
    }
    for(int i=0;i<c->length;i++)
    {
       
        printf("%d ",c->data[i]);
    }
    return 0;
}

```

#### 两个有序链表序列的交集

> 已知两个非降序链表序列S1与S2，设计函数构造出S1与S2的交集新链表S3。
>
> 输入格式:
>
> 输入分两行，分别在每行给出由若干个正整数构成的非降序序列，用−1表示序列的结尾（−1不属于这个序列）。数字用空格间隔。
>
> 输出格式:
>
> 在一行中输出两个输入序列的交集序列，数字间用空格分开，结尾不能有多余空格；若新链表为空，输出`NULL`。
>
> 输入样例:
>
> ```in
> 1 2 5 -1
> 2 4 5 8 10 -1
> ```
>
> 输出样例:
>
> ```out
> 2 5
> ```

```
#include<bits/stdc++.h>
using namespace std;
 
long long  a[1000005],b[1000005],c[1000005];
long long top1=0,top2=0,top3=0;    //使用了栈的思想来装数据
long long item;
 
 
int main()
{
	
	while(cin>>item)        //存a数组
	{
		if(item==-1)	break;
		else
			a[++top1] = item;
	}
	
	while(cin>>item)        //存b数组
	{
		if(item==-1)	break;
		else
			b[++top2] = item;
	}
	
 
	int p1=1,p2=1;            //双指针移动法
	while(p1<=top1&&p2<=top2)
	{
 
		if(a[p1]==b[p2])
		{
			c[++top3] = a[p1];
			p1++;
			p2++;
		}	
		else if(a[p1]<b[p2])	p1++;
		else			p2++;	
 
	}
	
 
	for(int i=1;i<=top3;i++)    //输出交集数组c
	{
 
		if(i==1)	cout<<c[i];
		else		cout<<" "<<c[i];
 
	}
 
	if(top3==0)	cout<<"NULL";
	
	return 0;
}
```

#### 两个有序链表合并

> 已知两个非降序链表序列S1与S2，设计函数构造出S1与S2合并后的新的非降序链表S3。 要求S3中没有重复元素。
>
> 输入格式:
>
> 输入分两行，分别在每行给出由若干个正整数构成的非降序序列，用−1表示序列的结尾（−1不属于这个序列）。数字用空格间隔。
>
> 输出格式:
>
> 在一行中输出合并后新的非降序链表，要求链表中没有重复元素。数字间用空格分开，结尾不能有多余空格；若新链表为空，输出NULL。
>
> 输入样例:
>
> 在这里给出一组输入。例如：
>
> ```in
> 1 3 3 5 8 -1
> 2 3 4 6 8 10 -1
> ```
>
> 输出样例:
>
> 在这里给出相应的输出。例如：
>
> ```out
> 1 2 3 4 5 6 8 10
> ```

```
#include <iostream>
using namespace std;
typedef struct LNode
{
  int data;
  struct LNode *next;
}LNode,*Linklist;

// 1 后插法创建链表 
void CreateList(Linklist &L)
{
	L=new LNode;
	L->next=NULL;
	Linklist p;
	Linklist s=L;
	int a;
	while(cin>>a&&a!=-1)
	{
		p=new LNode;
		p->data=a;
		p->next=NULL;
		s->next=p;
		s=p;
	}
}
// 2 链表归并 
void MergeList(Linklist &La,Linklist &Lb,Linklist &Lc)
{
    Linklist pa,pb,pc;
    pa=La->next; pb=Lb->next;
    Lc=La;
    pc=Lc;
    //La 和Lb 都非空 
    while(pa&&pb)
	{
        if(pa->data<pb->data&&pa->data!=pc->data) 
		{
            pc->next=pa; pc=pa; pa=pa->next;
         }
        else if(pa->data>pb->data&&pb->data!=pc->data) 
		 {
            pc->next=pb; pc=pb; pb=pb->next;
          }
        else if(pa->data==pb->data&&pa->data!=pc->data)
        {
        	pc->next=pa;
        	pc=pa;
        	pa=pa->next;
        	pb=pb->next;
		}
		else if(pa->data==pc->data) pa=pa->next;
		else if(pb->data==pc->data) pb=pb->next;
	}
	while(pa) 
	{
		if(pc->data!=pa->data)
		{
			pc->next=pa;pc=pa;
		}
		pa=pa->next;
		
	}
	while(pb)
	{
		if(pc->data!=pb->data)
		{
			pc->next=pb;pc=pb;
		}
		pb=pb->next;
	}
	pc->next=NULL;

}
int main()
{
	Linklist La,Lb,Lc;
	CreateList(La);
	CreateList(Lb);
	MergeList(La,Lb,Lc);	
	Linklist p=Lc->next;
	if(p==NULL) cout<<"NULL";
	while(p)
	{
		cout<<p->data;
		if(p->next!=NULL) {cout<<" ";
		}p=p->next;
    
	}
	return 0;
	
	
}


```

