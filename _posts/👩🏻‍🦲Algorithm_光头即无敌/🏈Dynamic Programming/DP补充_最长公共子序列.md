# 最长公共子序列LCS

> **概述**：给定两个序列 X={x1, x2, x3, ... , xm}和 Y={y1, y2, y3, ... ,yn}，找出X和Y的最长公共子序列。

目录：

[TOC]

## 基本概念

**子串的概念：**

<img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7pzz9g9tvj30g90dp0t2.jpg" alt="img" style="zoom: 67%;" />



**最长公共子序列的概念：**

X={A,B,C,B,D,A,B}，Y={B,D,C,A,B,A}，则序列{B,C,B,A}是X和Y的最长公共子序列。



## DP还是那三个步骤

1. **定义数组元素的含义**
2. **找到数组元素之间的关系式**
3. **找出初始值**



**(1)	定义数组元素的含义**

定义 `C[i][j]` 的含义为：**序列X第i位和序列Y第j位时的最长公共子序列的长度**。而序列X[n]={x1,x2,...,x(n-1)}，序列Y[m] = {y1,y2,...,y(m-1)}。这样，如果我们能够算出 `C[n-1][m-1]`，不就是我们要求的答案吗？



**（2）找出数组元素间的关系式**

**（3）找出初始条件**

> LCS的数组元素间的关系比较不一样。不太好分析。见图解。

**献上表达式，再分析：**

<img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7q06894plj30mi04yjrj.jpg" alt="img" style="zoom:67%;" />



`第一行和第一列都初始化为0.` 意思是：空字符与空字符的LCS为0、空字符与'A'的LCS为0、空字符与"AL"的LCS为0等等。

**对应表达式**：`C[i][j] = 0 	若i=0或j=0`

![IMG_3793](https://tva1.sinaimg.cn/large/008vxvgGgy1h7q2yau7xej30vc0hhab2.jpg)



`当'A'和'A'相同，把它斜上角的值copy下来再+1` 意思是：字符相同的时候，找它们前面记录的最长子序列+1 。而它们前面的LCS正好是它的斜上角的那个格的值。

**对应表达式**：`C[i][j] = C[i-1][j-1]+1 	若i,j>0,xi=yj`

![IMG_3794](https://tva1.sinaimg.cn/large/008vxvgGgy1h7q32ggedzj30v60hawfi.jpg)



`当'A'和'L'不相同，在它相邻（上和左）的两个格中选较大的copy过来` 意思是：字符不相同时，当前LCS从之前的最长子序列中copy过来，而之前最长的子序列要么在它上方，要么在它左侧，所有在之中选较大者。

**对应表达式**：`C[i][j] = max(C[i][j-1],C[i-1][j]) 	若i,j>0,xi≠yj`

![IMG_3795](https://tva1.sinaimg.cn/large/008vxvgGgy1h7q3c2hd17j30v50hegmn.jpg)



## Leetcode上非常经典的LCS题目

> 给定两个字符串 text1 和 text2，返回这两个字符串的最长 公共子序列 的长度。如果不存在 公共子序列 ，返回 0 。
>

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/longest-common-subsequence



```C++
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int arr[1000][1000] = {0};		// 完成第一步的初始化，完成了第一种情况
        int len1 = text1.size();
        int len2 = text2.size();
        for(int i = 1; i <= len1; ++i){		// 这里使用i++，j++也是一样的
            for(int j = 1; j <= len2; ++j){
                if(text1[i-1] == text2[j - 1])		// 相等的情况
                    arr[i][j] = arr[i-1][j-1]+1;
                else				// 不相等的情况
                    arr[i][j] = max(arr[i][j-1], arr[i-1][j]);
            }
        }
        return arr[len1][len2];		// 
    }
};
```

