#### VScode中导入头文件出现：PCH 警告: 头停止点不能位于链接块中。未生成 IntelliSense PCH 文件

- 代码如下：

```c++
#include<iostream>
#include<string>  //在此次警告
using namespace std;
int main(){
    int n;
    string t;
    cin>>n;
    for(int i=0;i<n;i++)
    cin>>t;
}
```

- 在csdn挖到了答案，如图：
- <img src="/Users/m12j10/Library/Application Support/typora-user-images/截屏2021-11-24 上午12.09.06.png" alt="截屏2021-11-24 上午12.09.06" style="zoom:80%;" />
- 当然，也有人说直接禁用intellisense就行了，马上有人跳出来说这只是掩盖了，以后的问题会更大。
- 最后，代码改成这样就不会报错了

```
#include<string>
#include<iostream>
using namespace std;
int main(){
    int n;
    string t;
    cin>>n;
    for(int i=0;i<n;i++)
    cin>>t;
}
```

