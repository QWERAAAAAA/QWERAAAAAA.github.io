[TOC]



#### 一、高精度与其背后的基础知识

1.在C++中数据类型位数有限，有高精度后可以处理大位数的数据了。

2.高精度算法实际上是用数组模拟竖式加法。

3.涉及基础知识：数组、字符串、计算。

---

#### 二、基本思想

##### 竖式加法

<img src="https://tva1.sinaimg.cn/large/e6c9d24ely1gzfkj1g235j207w05yq2t.jpg" alt="截屏2022-02-16 17.25.16" style="zoom:50%;" />

特点一：低位对齐相加；

特点二：进位向高位进一；

特点三：相加位数不大于较高位数者的位数+1

---

#### 三、在编程中的逐步实现

【1.0版】加法例题：洛谷P1601 A+B Problem



##### 1.将数据读入——使用string字符串

由于我们处理的是大位数的数据，在读入数据时可能已经超出了一般数据类型的范围，所以我们使用string字符串可以解决这个问题。



```C++
int a[600],b[600],c[600];
string s1,s2;
int main(){
    cin>>s1>>s2;
    int lena=s1.size(),lenb=s2.size();
```



##### 2.存储到数组—— 倒序存储，低位对齐



(1)  通过倒序存储数组，a[0]和b[0]低位对应;

如果按正序存储，如a数组存入1234，b数组存入567，那么按a[0]与b[0]相加得到1+5=6，不符合竖式相加；



(2)  将字符串转化回数字存储到数组

只需要通过减去一个 '0' 即可。



```C++
for(int i=0;i<lena;i++)
        a[i]=s1[lena-1-i]-'0';
    for(int i=0;i<lenb;i++)
        b[i]=s2[lenb-1-i]-'0';
```



##### 3.模拟竖式加法【关键】

(1)  相加位数不大于较高位数者的位数+1 

这个特点表明新的数组的长度最大（注意是最大为:

```C++
lenc = max(lena,lenb) + 1;
```

(2)  重点考虑进位问题

```C++
for(int i=0;i<lenc;i++){
        c[i] += a[i] + b[i];    // 相当于 c[i]+a[i]+b[i]
        c[i+1] += c[i]/10;
        c[i] %= 10;
    }
```

<img src="https://tva1.sinaimg.cn/large/e6c9d24ely1gzfmnarhkbj20si0gedgp.jpg" alt="IMG_23F5A4F38243-1" style="zoom: 50%;" />

如图，以第一次循环为例。

c[0]完成加法运算后，值为11；

通过取整除法运算，将进位的1，提前存储到了c[1]中（我们多次使用“+=”运算，正是为了把提前存储的数加入到后面的运算中）；

通过取余再把个位存储到c[0]中；这一次循环完成了个位数的计算（包括进位）。



##### 4.输出 —— 倒序&处理前导0

```C++
 while(lenc>0 && c[lenc]==0) lenc--;
    for(int i=lenc;i>=0;i--)
        cout<<c[i];
```

(1)  处理前导0:

例如a数组存4321，b数组存765；lenc最初赋值为5；

那么c[lenc]数组中存入的是108100，使用while循环删除前导0。

同时限定lenc>0，保证0+0=0可以输出。

(2)  最后一步，倒序输出。



##### 5.完整代码

```C++
#include<iostream>
#include<string>
using namespace std;
int a[600],b[600],c[600];
string s1,s2;
int main(){
    cin>>s1>>s2;
    int lena=s1.size(),lenb=s2.size();
    for(int i=0;i<lena;i++)
        a[i]=s1[lena-1-i]-'0';
    for(int i=0;i<lenb;i++)
        b[i]=s2[lenb-1-i]-'0';
    int lenc=max(lena,lenb)+1;
    for(int i=0;i<lenc;i++){
        c[i] += a[i] + b[i];    // 相当于 c[i]+a[i]+b[i]
        c[i+1] += c[i]/10;
        c[i] %= 10;
    }
    while(lenc>0 && c[lenc]==0) lenc--;
    for(int i=lenc;i>=0;i--)
        cout<<c[i];
    return 0;
}
```

