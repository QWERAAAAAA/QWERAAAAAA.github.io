上栗子🌰

```C++
int main(){
    string name;
    int id;
    float age, cpps, cppc;
    while(getchar() != '0'){
        while(getchar() != '\n'){
            cin>>name>>id>>age>>cpps>>cppc;
            Student stud(name, age, id, cpps,cppc);
            stud.Print();
        }
    }
    return 0;
}
```

这里我要实现——输入格式：每个测试用例占一行（学生姓名 学号 年龄 cpp成绩 cpp考勤）。当读入0时输入结束。

输入样例：

```
Bob 10001 18 75.5 4
Mike 10005 17 95.0 5
0
```

输出样例：

```
10001 Bob 75.9
10005 Mike 95.5
```

但是我的输出是这个样子的：

```
Bob 10001 18 75.5 4			// 输入
10001 b 75.9						// 输出
Mike 10005 17 95.0 5		// 输入
10005 ke 95.5						// 输出
```

先不说输出是不是应该一起，我这个名字它倒是给我吞了前两个字符。

**原因就是：getchar()这个函数拿走了我的字符！！！**

解决方法：

```c++
int main(){
    string name;
    int id;
    float age, cpps, cppc;
    while(true){
        cin>>name;
        if(name[0] == '0')
            break;
        else
            cin>>id>>age>>cpps>>cppc;
        Student stud(name, age, id, cpps, cppc);
        stud.Print();
    }
    return 0;
}
```

