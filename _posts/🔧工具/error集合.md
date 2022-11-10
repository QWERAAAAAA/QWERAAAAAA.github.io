[TOC]





#### error:comparisons like do not have their mathematical meaning

- 错误：比较好像没有数学意义.
- 原因：判断的语法有误。不能用 `if（a>=b>=c)`而需要像 `if((a>=b)&&(b>=c))`才行



---



#### pta测试点部分正确原因之一

- 想要用for循环不限循环 `for(int i=0;i<1000;i++){`，i<X,x的值要大一些，不然报错；
- 或者 干脆不限制 `for(int i=0; ;i++){`



---



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
- <img src="https://tva1.sinaimg.cn/large/e6c9d24egy1h1bo2gyfwsj20k60c4aaz.jpg" alt="截屏2021-11-24 上午12.09.06" style="zoom:80%;" />
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





---





#### MacBook升级后 vscode检测到#include错误解决办法

1、解决#include检测错误

在终端输入以下代码：

`gcc -v -E -x c++ -`

得到地址，在vs code中配置

2、MacBook升级后出现 `xcrun: error` 无法找到地址

在终端输入：

`xcode-select –install`

重装command line tools 就好了

3、更新后，在配置时要选macOS clang arm64





---





#### “zsh: abort” error

- “zsh:终止”错误

- 当您定义具有空维度的数组并使用大括号封闭的初始化器列表初始化该数组时，数组的大小由提供的初始化器列表元素决定。

  因此，就你的情况而言，`str`和`str2`的长度**刚好**足以分别容纳`"Hello, "`和`"World!"`的*弦*。

  因此，这里的问题是，目标缓冲区（作为`ft_strcat()`的第一个参数传递）绝对没有空间来保存*串联*结果。您正在访问越界内存，从而导致未定义的行为。

  在`while`循环的第一次迭代中，

  ```
  while (src[k])
      {
          dest[i + k] = src[k];
          //i++;
          k++;
      }
  ```

  索引`i+k`指向`dest`的越界内存。尝试使用索引访问内存位置后，您就会面临UB。

  您需要确保目的地有足够的空间来保存串联结果。为此，你可以有两种方法之一

  - 静态定义更大的数组大小，并将其用作目标。在这种情况下，您始终可以轻松检查实际大小与已使用的大小，因为这是一个字符类型数组，意在用作*字符串*（*提示：`sizeof`与`strlen()`*）。
  - 您可以使用指针，使用内存分配器函数根据需要分配一定数量的内存和`realloc()`