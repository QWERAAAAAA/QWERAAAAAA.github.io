> 以Java语言为例

### 一、 求余%的使用

> 操作符%的使用：求余、取模



#### 1⃣️ 判断奇偶

> 模2

偶数%2的结果总是0，而正奇数%2的结果总是为1.



#### 2⃣️ 计算星期几

> 模7

假设你和你的朋友计划10天后见面，那么10天后是星期几？假设今天是星期六。

算法设计：一周的模数为7（7为一周期）

`（ 6 + 10 ）% 7 = 2`

（ 今天 + n天后 ）模上周期 得到2 —— 为一周的第2天（星期二）

注意：第0天是指星期天。



#### 3⃣️ 将秒转为分钟

> 模60

```java
class DisplayTime{
    public static void main(String[] args){
        System.out.print("请输入秒钟：" );
        Scanner input = new Scanner(System.in);
        int second = input.nextInt();
        input.close();
        int mins = second/60;
        int newSecond = second%60;
        System.out.println("转换为分钟为：" + mins + "分" + newSecond + "秒");
    }
 }
```



