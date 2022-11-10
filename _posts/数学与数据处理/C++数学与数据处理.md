[TOC]

### 一、C++开三次方根/C++开根号

一个函数解决，这个函数在 math.h里头

`#include<math.h>`

`pow(x,n)` 这个函数是x的n次幂的意思

`那么pow(100,1.0/3)就是开三次方了`

注意：浮点数要用1.0/3（每个分数 分母都要有一位小数位）否则整除结果为1



---

### 二、C++输出定长数据不足在前补零

头文件iomanip，

```C++
cout<<setw(4)<<setfill('0')<<x<<endl;  
```

​	setfill里面一定要是字符！！



---

### 三、小数点位数

头文件iomanip

```C++
cout<<fixed<<setprecision(2);
//保留小数点后2位，精度声明语句,对之后的数字都有效。
cout<<s<<endl;
```

setprecision（n）这个函数

它如果单独使用是用来保留n位有效数字的

但是当它和fixed在一起搭档的时候，他们组合出来的作用是保留小数点后n位的数字。



---

### 四、向下取整 vs 向上取整

向下取整：19.2 —— 取为20

向上取整：19.2 —— 取整为19



---

### 五、sort()函数

\#include<algorithm>

sort函数的模板有三个参数：

```C++
void sort (RandomAccessIterator first, RandomAccessIterator last, Compare comp);
```

（1）第一个参数first：是要排序的数组的起始地址。

（2）第二个参数last：是结束的地址（最后一个数据的后一个数据的地址）

（3）第三个参数comp是排序的方法：可以是从升序也可是降序。如果第三个参数不写，则默认的排序方法是从小到大排序。

```C++
int a[20];
sort(a,a+20);
```



---

### 六、有效数字

```C++
#include<iomanip>
cout<<setprecision(5)<<a;
// 输出5位有效数字；会四舍五入。
```



---

### 七、控制输出末尾空格

```C++
	for(int i=0;i<n;i++){
		if(i==0){
			cout<<arr[i];
		}
		else cout<<" "<<arr[i];
	}
```



---

### 八、sizeof()与size()

sizeof是表达式类型的大小，size是内部元素的个数

sizeof的用法：`sizeof(a)`   a的长度

size的用法：`a.size()`  a的元素个数

两者都在iostream库内就有



---

### 九、字符串复制

strcpy vs strncpy

strcpy（目标串地址，源串的开始地址）：从源串的开始到结尾('\0')完全拷贝到目标串地址

strncpy（目标串地址，源串的开始地址，n）：从源串的开始拷贝n个字符到目标串地址，n大于源串长度时，遇到'\0'结束；n小于源串长度时，到第n个字符结束，但不会在目标串尾补'\0'
