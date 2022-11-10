

#### 阶乘函数

```cpp
#include<iostream>
using namespace std;

long Fact(long n){
    if (n == 0) return 1;
    else return n*Fact(n-1);
}

int main(){
    long num;
    cin>>num;
    long Fact(num);
}

// 报错日志1：没有输出
// 调试结果：
// 1. long Fact这里又定义了一个long类型的Fact变量 —— 函数调用直接用函数名。
// 2. return 只是让这个函数最后的值为它，但是你需要自己输出。

#include<iostream>
using namespace std;

long Fact(long n){
    if (n == 0) return 1;
    else return n*Fact(n-1);
}

int main(){
    long num;
    cin>>num;
    cout<<Fact(num);
}
```

#### 斐波那契数列

```

```



#### 7-1 求最大元素值

> n个元素的数组的最大元素可以用递归计算出来。
> 定义方法：int max(int x, int y) 它返回x和y两个整数中的较大值。
> 试用递归编写方法：int arraymax(int[] a, int n) 它使用递归返回数组a的最大元素值。
> 终止条件：n==2
> 递归步骤：arraymax=max(max(a[0],...,a[n-2]), a[n-1])
>
> - 输入格式:
>
> 第一行的第一个元素是输入元素个数n (1<n<=30)，第二个元素之后是输入n个元素；
>
> - 输出格式:
>
> 按格式要求输出相邻两个元素的最大值，例如输出的第一项是a[0]和a[1]之间的最大值；第二项为之前的最大值与a[2]之间的最大值，依次类推，直到最后输出n个元素数组的最大元素值。
>
> - 输入样例:
>
> ```in
> 5 1 3 2 5 3
> ```
>
> - 输出样例:
>
> ```out
> max(1,3)=3 max(3,2)=3 max(3,5)=5 max(5,3)=5 5
> ```

```cpp
#include<iostream>
using namespace std;
int MAX=0;
int max(int x, int y){
    return MAX = x>y?x:y;
}
int arraymax(int a[], int n){
    if(n == 2) return max(a[n-2],a[n-1]);
    else return arraymax(max(a[n-2]),n-1);
}
int main(){
    int n, a[100];
    cin>>n;
    for(int i=0;i<=n;i++){
        cin>>a[i];
    }
    cout<<arraymax(a[n],n);
    return 0;
}

//报错日志1:
// 
```

