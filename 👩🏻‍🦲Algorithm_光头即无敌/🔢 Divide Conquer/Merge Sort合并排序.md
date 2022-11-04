# 合并排序

> **基本思想：**将待排序元素分成大小大致相同的两个子集合，分别对两个子集合进行排序，最终将排好序的子集合并成要求的排好序的集合。

![img](https://tva1.sinaimg.cn/large/008vxvgGgy1h7qpvskwo9j31360u0q7n.jpg)

## 原理

先将无序序列**利用二分法划分为子序列，直至每个子序列只有一个元素**(单元素序列必有序)，**然后再对有序子序列逐步(两两)进行合并排序**。合并方法是循环的将两个有序子序列当前的首元素进行比较，较小的元素取出，置入合并序列的左边空置位，直至其中一个子序列的最后一个元素置入合并序列中。最后将另一个子序列的剩余元素按顺序逐个置入合并序列尾部即可完成排序。整体过程如下图：
![img](https://tva1.sinaimg.cn/large/008vxvgGgy1h7qpxbkwvkg308c05040x.gif)



## 递归实现

```C++
void MergeSort(int a[], int left, int right){
	if(left < right){									// 至少有两个元素
    int i = (left + right)/2;				// 取中点
    MergeSort(a, left, i);					// 对左边序列再“分”
    MergeSort(a, i+1, right);				// 对右边序列再“分”
    Merge(a,b,left,i,right);
  }
}

void Merge(int c[], int d[], int l, int m, int r){		//
  int i = l, j = m + 1; k = l;
  while((i <= m) && (j <= r)){
    if(c[i] <= c[j])
      d[k++] = c[i++];
    else
      d[k++] = c[j++];
    
    if(i>m){		
      // 说明此时，子序列1已经遍历完了，只需要把子序列2的剩余元素放入d[]数组中即可。
      for(int q = j; q <= r; q++)
        d[k++] = c[q];
    }
    else{			
      // 说明此时，子序列2已经遍历完了，只需要把子序列1的剩余元素放入d[]数组中即可。
      for(int q = i; q <= m; q++)
        d[k++] = c[q];
    }
  }
}
```



## 非递归实现

```C
void MergeSort(int a[],int n){
  int *b = new int [n];
  int s = 1;
  while (s < n){
    MergePass(a,b,s,n);
    s += s;
    MergePass(b,a,s,n);
    s += s;
  }
}

void MergePass(int x[], int y[], int s, int n){			// 
  int i = 0;
  while(i <= n-2*s){
    Merge(x, y, i, i+s-1, i+2*s-1);
    i = i + 2*s;
  }
  if(i + s < n)
    Merge(x, y, i, i+s-1, n-1);
  else
    for(int j = i; j <= n-1; j++)
      y[j] = x[j];
}

void Merge(int c[], int d[], int l, int m, int r){		//
  int i = l, j = m + 1; k = l;
  while((i <= m) && (j <= r)){
    if(c[i] <= c[j])
      d[k++] = c[i++];
    else
      d[k++] = c[j++];
    
    if(i>m){		
      // 说明此时，子序列1已经遍历完了，只需要把子序列2的剩余元素放入d[]数组中即可。
      for(int q = j; q <= r; q++)
        d[k++] = c[q];
    }
    else{			
      // 说明此时，子序列2已经遍历完了，只需要把子序列1的剩余元素放入d[]数组中即可。
      for(int q = i; q <= m; q++)
        d[k++] = c[q];
    }
  }
}
```

**代码分析：**

### Merge函数——实现排序的算法

- **参数介绍：**`void Merge(int c[], int d[], int l, int m, int r)`

​		`实现合并c[1:m]和c[m+1:r]到d[1:r]中`

```
int c[] —— 待排序的序列	
		l —— 指向数组最左端（表示子序列1）， r —— 指向数组最右端（表示子序列2）
		m —— 指向中间（用于划分）
int d[] —— 排序后存入的目标数组
```



- **内部用于比较的参数：**  `int i = l, j = m + 1; k = l;`

```
i —— 用于第一个子序列的遍历，指向序列头l
j —— 用于第二个子序列的遍历，指向序列头m+1
k —— 用于存放入d[]数组的位置更新
```



