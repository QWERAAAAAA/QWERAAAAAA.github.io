[TOC]



### 7-1 找最小的字符串

本题要求编写程序，针对输入的N个字符串，输出其中最小的字符串。

**输入格式：**

输入第一行给出正整数N；随后N行，每行给出一个长度小于80的非空字符串，其中不会出现换行符，空格，制表符。

**输出格式**：

在一行中用以下格式输出最小的字符串：

```
Min is: 最小字符串
```

**输入样例**：

```in
5
Li
Wang
Zha
Jin
Xian
```

**输出样例**：

```out
Min is: Jin
```

#### 🧠 问题

##### **什么是最小字符串？**

<img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h1fbiqv057j20u00xw0xc.jpg" alt="截屏2022-04-19 20.26.53" style="zoom: 50%;" />

##### **段错误的原因**

<img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h1fblteyvxj20n8154aef.jpg" alt="截屏2022-04-19 20.49.53" style="zoom:67%;" />

#### 上手敲代码

```c++
第一次：
#include<iostream>
#include<string>
using namespace std;
int main(){
    string arr[50];
    int n;
    cin>>n;
    for(int i=0;i<n;i++){
        cin>>arr[i];
    }
    string MIN = arr[0];
    for(int i=1;i<n;i++){
        for(int j=0;j<80;){
            if(arr[i][j] < MIN[j]){
            MIN = arr[i];
            break;
            }
        else if(arr[i][j] == MIN[j])
            j++;
        else break;
        }
        
    }
    cout<<"Min is: "<<MIN;
    return 0;
}

报错：1.格式错误：Min is: ——这里还有一个空格！	2.段错误 —— 数组长度设定太小的，溢出了

第二次代码AC
#include<iostream>
#include<string>
using namespace std;
#define MAXLEN 1000
int main(){
    string arr[MAXLEN];
    int n;
    cin>>n;
    for(int i=0;i<n;i++){
        cin>>arr[i];
    }
    string MIN = arr[0];
    for(int i=1;i<n;i++){
        for(int j=0;j<80;){
            if(arr[i][j] < MIN[j]){
            MIN = arr[i];
            break;
            }
        else if(arr[i][j] == MIN[j])
            j++;
        else break;
        }
        
    }
    cout<<"Min is: "<<MIN;
    return 0;
}
```



### 7-2 查找字符串 (10 分)

**编程实现**：
输入一个正整数repeat (0<repeat<10)，做repeat次下列运算：

输入一个字符，再输入一个以回车结束的字符串（少于80个字符），在字符串中查找该字符，如果找到，输出该字符在字符串中所对应的最大下标 (下标从0开始)；否则输出"Not Found"。输出格式为"index = %d\n" 

输入输出示例：括号内为说明

**输入样例**:

```in
2		(repeat=2)
m               (字符'm')
programming	(字符串"programming")
a		(字符'a')
1234		(字符串"1234")
```

**输出样例**:

```out
index = 7     	('m'在"programming"中对应的最大下标是7)
Not Found    	("1234"中没有'a')
```

#### 上手敲代码

```c++
#include<iostream>
#include<cstring>
using namespace std;
#define MAXLEN 1000
int main(){
    int repeat,pos=0,flag=0,i=0,j=0,len;
    string arr[MAXLEN];
    cin>>repeat;
    for(i=0;i<repeat*2;i++)
        cin>>arr[i];
    for(i=0;i<repeat*2;i+2){
        len = arr[i+1].size();
        for(j=0;j<len;j++){
            if(arr[i] == arr[i+1][j]){
                pos = j;
                flag = 1;
            }
        }
        if(flag) cout<<"index = "<<j;
        else cout<<"Not Found";
    }
    return 0;
}
// 代码报错：
error: invalid operands to binary expression ('std::string' (aka 'basic_string<char>') and 'std::basic_string<char>::value_type' (aka 'char'))
            if(arr[i] == arr[i+1][j]){
               ~~~~~~ ^  ~~~~~~~~~~~
 
                
#include<iostream>
#include<cstring>
using namespace std;
#define MAXLEN 1000
int main(){
    int repeat,pos=0,flag=0,i,j,len;
    string arr[MAXLEN];
    cin>>repeat;
    for(i=0;i<repeat*2;i++)		// 这里还是直接i++，而不用i+2
        cin>>arr[i];
    for(i=0;i<repeat*2;i++){
        if(i == 0 || i%2 == 0){		// 只要在这里加一个条件就可以实现排除i为奇数
            len = arr[i+1].size();
            for(j=0;j<len;j++){
                if(arr[i][0] == arr[i+1][j]){		
                  // 这样就可以实现char类型与char类型比较，而不是string类型和char类型比较
                    pos = j;
                    flag = 1;			// 加一个flag，来记录是否找到
                }
            }
            if(flag) cout<<"index = "<<pos<<endl;
            else cout<<"Not Found";
            flag = 0;	// 每次在下一次循环开始前，要把flag置零，为下一次循环做准备
        }
    }

    return 0;
}
```





```C++
AC code

#include <iostream>
using namespace std;
int main(){
    char a;
    int letters=0,digits=0,spaces=0,others=0;
    char input[50];
    scanf("%[^\n]", input);
    int i = 0;
         while ((a=input[i++])!=0)
         {
        if (a>='a'&&a<='z'||a>='A'&&a<='Z'){
            letters++;
        }
        else if (a>='0'&&a<='9'){
            digits++;
        }
        else if(a==' '){
            spaces++;
        }
        else
            others++;
    }
    cout<<"letters="<<letters<<",";
    cout<<"digits="<<digits<<",";
    cout<<"spaces="<<spaces<<",";
    cout<<"others="<<others;
}
 
```

