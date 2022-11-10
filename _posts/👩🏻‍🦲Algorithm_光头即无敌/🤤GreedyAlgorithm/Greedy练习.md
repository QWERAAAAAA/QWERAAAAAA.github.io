[TOC]

## 1.汽车加油问题

题目来源：王晓东《算法设计与分析》

一辆汽车加满油后可行驶 n公里。旅途中有若干个加油站。设计一个有效算法，指出应 在哪些加油站停靠加油，使沿途加油次数最少。

**输入格式:**
第一行有 2 个正整数n和 k（k<=1000 )，表示汽车加满油后可行驶n公里，且旅途中有 k个加油站。 第二行有 k+1 个整数，表示第 k 个加油站与第k-1 个加油站之间的距离。 第 0 个加油站表示出发地，汽车已加满油。 第 k+1 个加油站表示目的地。

**输出格式:**
输出最少加油次数。如果无法到达目的地，则输出“No Solution!”。

**输入样例:**

```
7 7
1 2 3 4 5 1 6 6
```

**输出样例:**

```
4
```

### 我的思路

将距离进行小到大排序，然后从头开始与n/2比较，如果大于n/2则需要加油，因为之后的距离会越来越大。

但是这对于本次没加油，下一次的行程就不适用了，而且从n/2开始判断加or不加油，对于那些距离很近的情况怎么办？子问题划分不合理。



### 大佬的code

```C++
#include<iostream>
using namespace std;
int main(){
	int n,k;
	cin>>n>>k;
	int a[2000];
	int i;
	for(i=0;i<=k;i++){
		cin>>a[i];
		if(a[i]>n) {
			cout<<"No Solution!";
			return 0;
		}
	}
	int count=0;//最少加油次数
	int trans;//暂存的油 
     trans=n;
	for(i=0;i<=k;){
		if(trans-a[i]>0) {
			trans=trans-a[i];
			i++;
		}
		else{
			trans=n;
			count++;
		}
	}
	cout<<count;
	
}
```



仔细分析分析这段很巧妙的代码

```C++
for(i=0;i<=k;){
		if(trans-a[i]>0) {				// 只要满油距离>加油站距离，我就不加（贪心选择策略）
			trans=trans-a[i];
			i++;										// 我只管++，让后面的帮我善后。
		}													// 剩下的就是解决子问题了（擦屁股）
  
		else{											// 如果下一段行程跑不到，那他就进入else语句，
			trans=n;								// 而else语句里只加油，不++，说明是为上一段行程补上的一次油
			count++;								// 加了油后，接下来这次行程又进入循环来判断这次需不需要加油。
		}
}
```



## 2. 排队接水问题

有n个人在一个水龙头前排队接水，假如每个人接水的时间为Ti，请编程找出这n个人排队的一种顺序，使得n个人的平均等待时间最小。

**输入格式**:

共两行，第一行为n(1≤n≤1000)；第二行分别表示第1个人到第n个人每人的接水时间T1，T2，…，Tn，每个数据之间有1个空格。

**输出格式**:

输出为这种排列方案下的平均等待时间(输出结果精确到小数点后两位)。

**输入样例**:

```in
10
56 12 1 99 1000 234 33 55 99 812
```

**输出样例**:

```out
291.90
```



并不是最快的人先接水最优。

```c++
#include<iostream>
#include<algorithm>
#include<iomanip>
using namespace std;
int main(){
    int n;
    cin>>n;
    int t[1000];
    for(int i = 0; i < n; i++)
        cin>>t[i];
    sort(t,t+n);
    float aver = 0;
    for(int i = 1; i < n; i++){
        t[i] += t[i-1];
        aver += t[i];
    }
    cout<<fixed<<setprecision(2)<<aver/n;
    return 0;
}
```

### 大佬的code

// 又是我理解不了为何的代码。

```C++
#include<iostream>
#include<algorithm>
#include<iomanip>
using namespace std;
int main(){
    int n;
    cin>>n;
    int t[1000];
    for(int i = 0; i < n; i++)
        cin>>t[i];
    sort(t,t+n);
    float aver = 0;
    for(int i = 0; i < n; i++){
        for(int j = 0; j < i; j++)
            aver +=t[j];
    }
    cout<<fixed<<setprecision(2)<<aver/n;
    return 0;
}
```



奇了怪了，什么测试点没过？

```C++
#include<iostream>
#include<algorithm>
using namespace std;

struct Area{
    int a,b;
};
bool cmp(Area A1, Area A2){
    return A1.a < A2.a;
}
int main(){
    int n;
    Area ex[1000];
    cin>>n;
    for(int i=0; i<n; i++)
        cin >> ex[i].a>> ex[i].b;
    sort(ex,ex+n,cmp);
    int count=0;
    for(int i = 0; i<n; ){
        if(ex[i].b >= ex[i+1].a){
            ex[i+1].b = ex[i].b;
            i++;
        }
        else{
            count++;
            i++;
        }
    }
    cout << count;
    return 0;
}
```



### 大佬的code

```C++
#include<iostream>
#include<algorithm>
using namespace std;

struct Area{
    int a,b;
};
bool cmp(Area A1, Area A2){
    return A1.b < A2.b;
}
int main(){
    int n;
    Area ex[1000];
    cin>>n;
    for(int i=0; i<n; i++)
        cin >> ex[i].a>> ex[i].b;
    sort(ex,ex+n,cmp);
    int count=1;
    int c = 0;
    for(int i = 1; i<n;){
        if(ex[c].b >= ex[i].a){
            i++;
        }
        else{
            count++;
            c = i;
        }
    }
    cout << count;
    return 0;
}
```



## 3. 最优合并问题

题目来源：王晓东《算法设计与分析》

给定k 个排好序的序列, 用 2 路合并算法将这k 个序列合并成一个序列。
假设所采用的 2 路合并算法合并 2 个长度分别为m和n的序列需要m+n-1 次比较。试设
计一个算法确定合并这个序列的最优合并顺序，使所需的总比较次数最少。
为了进行比较，还需要确定合并这个序列的最差合并顺序，使所需的总比较次数最多。

**输入格式**:

第一行有 1 个正整数k，表示有 k个待合并序列。
第二行有 k个正整数，表示 k个待合并序列的长度。 

**输出格式**:

输出最多比较次数和最少比较次数。

**输入样例**:

在这里给出一组输入。例如：

```in
4
5 12 11 2 
```

**输出样例**:

在这里给出相应的输出。例如：

```out
78 52
```



### My Code一个测试点未过

```C++
#include<iostream>
#include<algorithm>
using namespace std;
int main(){
    int k; 
    int lenth[1000];
    cin >> k;
    for(int i = 0; i < k; i++)
        cin >> lenth[i];
    sort(lenth,lenth+k);
    int Max = 0, Min = 0;
    int temp1 =lenth[0];
    int temp2 = lenth[k-1];
    for(int i = k-2; i >= 0; i--){
        Max += (temp2+lenth[i]-1);
        temp2 += lenth[i];
    }
    for(int i = 1; i < k; i++){
        Min += (temp1+ lenth[i] -1);
        temp1 += lenth[i];
    }
    cout << Max << " " << Min;
    return 0;
}
```

优化了一下，但是还是未AC

```C++
#include<iostream>
#include<algorithm>
using namespace std;
int main(){
    int k; 
    int lenth[1000];
    cin >> k;
    for(int i = 0; i < k; i++)
        cin >> lenth[i];
    sort(lenth,lenth+k);
    int Max = 0, Min = 0;
    int temp1 =lenth[0];
    int temp2 = lenth[k-1];
    for(int i = k-2; i >= 0; i--){
        if(temp2 == 0 || lenth[i] == 0)
            Max = Max;
        else
            Max += (temp2+lenth[i]-1);
        temp2 += lenth[i];

    }
    for(int i = 1; i < k; i++){
        if(temp1 == 0 || lenth[i] == 0)
            Min = Min;
        else
            Min += (temp1+ lenth[i] -1);
        temp1 += lenth[i];
    }
    cout << Max << " " << Min;
    return 0;
}
```



AC代码

为啥非要用两个数组

```C++
#include<iostream>
#include<algorithm>
using namespace std;
bool cmp(int x, int y){
    return x>y;
}
int main(){
    int k; 
    int max[1000], min[1000];
    cin >> k;
    for(int i = 0; i < k; i++){
        cin >> max[i];
        min[i] = max[i];
    }
    int Max = 0, Min = 0;
    for(int i = 0; i < k-1; i++){
        sort(max+i, max+k, cmp);
        Max += (max[i+1]+max[i]-1);
        max[i+1] += max[i];
    }
    for(int i = 0; i < k-1; i++){
        sort(min+i, min+k);
        Min += (min[i+1]+ min[i] -1);
        min[i+1] += min[i];
    }
    cout << Max << " " << Min << endl;
    return 0;
}
```



## 4.找零钱问题

```C++
#include<iostream>
#include<algorithm>
using namespace std;
int main(){
    int pay, con;
    int w[7] = {100,50,20,10,5,2,1};
    cin >> pay >> con;
    int i = 0, count = 0;
    int rest = pay - con;
    while(true){
        if(rest > w[i])
            break;
        else
            i++;
    }
    while(rest>0){
        while(rest >= w[i]){
            rest -= w[i];
            count++;
        }
        if(count == 0);
        else
            cout << w[i] << " " << count << endl;
        count = 0;
        if(rest < w[i]){
            i++;
        }
    }
    return 0;
}
```

一切的技巧都在while循环体内语句的设计顺序中！！！虽然最后一个测试点未过。。。

我AC啦～

```C++
#include<iostream>
#include<algorithm>
using namespace std;
int main(){
    int pay, con;
    int w[7] = {100,50,20,10,5,2,1};
    cin >> pay >> con;
    int i = 0, count = 0;
    int rest = pay - con;
    while(true){
        if(rest >= w[i])
            break;
        else
            i++;
    }
    while(rest>0){
        while(rest >= w[i]){
            rest -= w[i];
            count++;
        }
        if(count == 0);
        else
            cout << w[i] << " " << count << endl;
        count = 0;
        if(rest < w[i]){
            i++;
        }
    }
    return 0;
}
```

等于的情况，这些细节要考虑到位！
