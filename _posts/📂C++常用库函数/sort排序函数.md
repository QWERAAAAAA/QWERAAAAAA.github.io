[TOC]

## 前言

顾名思义，sort()就是用来排序的函数，它根据具体情况使用不同的排序方法，效率较高。
一般来说，不推荐使用C语言中的qsort函数，原因是qsort用起来比较繁琐，涉及很多指针的操作。
而且sort在实现中避免了经典快速排序中可能出现的会导致实际复杂度退化到O(n2)的极端情况。
话不多说了，下面我们来了解一下sort()函数的使用。

## 使用sort

需要的头文件

```C++
	#include<algorithm>
```

**使用的方式如下:**

`sort(首元素地址(必填), 尾元素地址的下一个地址(必填), 比较函数(非必填));`

比较函数可以根据自身需要填写，如果不写比较函数，则默认对前面给出的区间进行递增排序。



例子：对int、double、char型数组排序

![img](https://tva1.sinaimg.cn/large/008vxvgGgy1h7wvtpy823j31350kr77y.jpg)

![img](https://tva1.sinaimg.cn/large/008vxvgGgy1h7wvty0tcbj30zr0dlwgr.jpg)

我们应该知道，如果需要对序列进行排序，那么序列中的元素一定要有**可比性**，因此需要制定排序规则来建立这种可比性。
特别是像结构体，本身并没有大小关系，需要人为制订比较的规则。

sort的第三个可选参数就是compare函数(一般写作cmp函数)，用来实现这个规则。



## 实现比较函数cmp

如果想要从大到小排序，则要使用比较函数cmp来 " 告诉 " sort何时要交换元素(让元素的大小比较关系反过来)。

![img](https://tva1.sinaimg.cn/large/008vxvgGgy1h7wvvbaad2j31290g1tbf.jpg)





## 结构体数组的排序

定义结构体如下：

```
struct student{
	int x,y;
};
```

- 如果想将结构体数组按照x从大到小排序，可以这样写cmp函数。

```
bool cmp(student a,student b)
{
	return a.x > b.x;//按x值从大到小对结构体排序 
}
```

- 如果想要先按x从大到小排序(即一级排序)，但当x相等的情况下，按照y的大小从小到大排序(即二级排序)。那么cmp的写法是:

```C++
bool cmp(student a,student b)
{
	if(a.x==b.x)//x值相等时按y从小到大排 
	{
		return a.y<b.y;
	} 
	return a.x>b.x;//按x值从大到小对结构体排序 
}
// 或
bool cmp(student a,student b)
{
	if(a.x != b.x)//x值不相等时按x从大到小排 
    return a.x>b.x;
	else 
	return a.y<b.y;//x相等时按y值从小到大对结构体排序 
}
```



## 容器的排序

在STL标准容器中，只有vector、string、deque是可以使用sort的。
这是因为像set、map这种容器是用红黑树实现的(了解即可)，元素本身有序，故不允许使用sort排序。

例子：对vector、string排序

![在这里插入图片描述](https://tva1.sinaimg.cn/large/008vxvgGgy1h7ww0jcnuhj30tr0g576h.jpg)

![在这里插入图片描述](https://tva1.sinaimg.cn/large/008vxvgGgy1h7ww0nw7rmj30s00c0q4v.jpg)