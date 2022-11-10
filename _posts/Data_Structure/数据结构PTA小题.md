[TOC]



### 练习8:串和数组



**下面关于串的叙述中，哪一个是不正确的**

![截屏2022-04-14 19.44.21](https://tva1.sinaimg.cn/large/e6c9d24egy1h19hm28rxnj20oe0ayq3j.jpg)

**区分空格串和空串——类比：含有0的集合与空集**



---



**假设以行序为主序存储二维数组A=array[1..100,1..100]，设每个数据元素占2个存储单元，基地址为10，则LOC[5,5]=（ ）**

​		A.808	**B.818**	C.1010	D.1020

​		**这里标注了数组下标从1开始（1...100)**

> ![截屏2022-04-14 18.56.22](https://tva1.sinaimg.cn/large/e6c9d24egy1h19g85jx9mj20oy02m3yl.jpg)
>
> 公式：基地址+（n\*（i-1）+（j-1））*所占存储单元（字节数）



![截屏2022-04-14 19.01.45](https://tva1.sinaimg.cn/large/e6c9d24ely1h19gdpo6tfj21180boaar.jpg)

**A. 1,020**  	默认了数组下标从0开始



---



若串S=“software”，则其子串数目是____，其中空串和S串本身这两个字符串也算作S的字串

![截屏2022-04-14 19.35.50](https://tva1.sinaimg.cn/large/e6c9d24egy1h19hk96nxqj211e0ce3z0.jpg)

**B. 37**		不是2^n，与集合不同，它是不可分割的。子串数目：（8+7+6+5+4+3+2+1）+1





---



### 练习9:树和二叉树



![截屏2022-05-04 20.33.11](https://tva1.sinaimg.cn/large/e6c9d24egy1h1wnf6uuubj20yo0u03zo.jpg)

- 1-3 可以自己画一画

![截屏2022-05-04 20.38.29](https://tva1.sinaimg.cn/large/e6c9d24egy1h1wnks9c5uj21320u0q47.jpg)

![截屏2022-05-04 20.39.26](https://tva1.sinaimg.cn/large/e6c9d24egy1h1wnlji153j20zr0u075n.jpg)

- 例如：左子树/右子树为空的二叉树——度为1

![截屏2022-05-04 20.44.31](https://tva1.sinaimg.cn/large/e6c9d24egy1h1wnqtdix7j212i0gqt94.jpg)

- 可举例验证，确实没什么关系

![截屏2022-05-04 20.45.10](https://tva1.sinaimg.cn/large/e6c9d24egy1h1wnrhd9d4j20xu0foq4a.jpg)

- 二叉树每个节点均有两个孩子❌ 至多两个孩子

![截屏2022-05-04 20.46.10](https://tva1.sinaimg.cn/large/e6c9d24egy1h1wnsjqh0vj20ty0fcq3n.jpg)

![截屏2022-05-04 20.46.51](https://tva1.sinaimg.cn/large/e6c9d24egy1h1wnt951oaj214o0fut95.jpg)

![截屏2022-05-04 20.47.30](https://tva1.sinaimg.cn/large/e6c9d24egy1h1wntxlingj210o0e4dga.jpg)

- 具有3个节点的二叉树有几种形态？具有3个节点的树有几种形态？
  - ![IMG_A02E45810830-1](https://tva1.sinaimg.cn/large/e6c9d24egy1h1wnvvmixdj20wi0c2gnk.jpg)

![截屏2022-05-04 20.51.51](https://tva1.sinaimg.cn/large/e6c9d24egy1h1wnygx6fyj213i0h8jsu.jpg)

![截屏2022-05-04 20.53.27](https://tva1.sinaimg.cn/large/e6c9d24egy1h1wo03r01gj211k0e6wft.jpg)

- 排除法，通过举例验证也是正确的

![截屏2022-05-04 20.54.35](https://tva1.sinaimg.cn/large/e6c9d24egy1h1wo1a4pjoj20xk0di74r.jpg)

- 画出树的示例即可看出。
