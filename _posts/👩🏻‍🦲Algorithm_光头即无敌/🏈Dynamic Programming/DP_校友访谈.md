

## **Description**

校友返校后，算法老师想知道是不是在校时算法学得越好，毕业后的薪酬越高。于是算法老师找出了校友们在校时算法的成绩单，并且询问了每位校友的薪酬。算法老师希望找出最长校友的序列，满足算法成绩是严格递增的，同时薪酬也是严格递增的。要求算法的时间复杂度为O(nlogn)

**Input**

第一行一个数字n，表示调查的校友总数， 1<=n<=100 下面n行，每行2个正整数用空格分隔，表示校友的算法成绩grade和薪酬salary, 0<=grade<=100, 0

**Output**

满足递增条件的校友序列最长的长度

**Sample Input** 

```
5 
76 300000 
82 500000 
93 900000 
89 200000 
65 100000
```

**Sample Output **

```
4
```

**Hint**

```
校友序列为（65，100000）、（76，300000）、（82，500000）、（93，900000）
```

## 我的WACode

```C++
#include<iostream>
using namespace std;

struct Stu{
    int grade;
    int salary;
};

int LS(Stu arr[],int n){
    int longest[n],max=0, j=0;
    int nowG, nowS;
    for(int i = 0; i<n; i++){
        longest[i] = 0;
    }
    
    for(int i = 0; i<n; i++){
        while(j<n){
            nowG = arr[i].grade;
            nowS = arr[i].salary;
            if((nowG < arr[j].grade) && (nowS < arr[j].salary)){
                longest[i]++;
                nowG = arr[j].grade;
                nowS = arr[j].salary;
                j++;
            }
            else   
                j++; 
        }
    }
    for(int i = 0; i< n; i++){
        if(longest[i] > longest[max])
            max = i;
    }
    return max;
}
int main(){
    int n;
    Stu smate[100];
    cin >> n;
    for(int i = 0; i<n; i++)
        cin >> smate->grade >> smate->salary;
    int Max = LS(smate, n);
    cout << Max;
    return 0;
}
```



## 大佬ACCode

**思路：**

> ***\*本题为最长递增子序列的变形，只需先按成绩进行排序，\****
>
> ***\*然后根据薪酬找出最长递增子序列\****
>
> ***\*dp[i]表示以第i个校友为结束的最长递增序列\****
>
> ***\*dp[i] = max{dp[i], dp[j] + 1}  0<=j<i  stu[j].salary<stu[i].salary && stu[j].grade < stu[i].grade\****

```C++
#include<iostream>
#include<algorithm>
using namespace std;

struct Stu{
    int grade;
    int salary;
}stu[100];

bool cmp(Stu a, Stu b){
    if(a.grade == b.grade)
        return a.salary < b.salary;
    else
        return a.grade < b.grade;
}

int dp[100];
int main(){
    int n;
    cin>>n;
    for(int i = 0; i<n; i++)
        cin>>stu[i].grade>>stu[i].salary;
    sort(stu,stu+n,cmp);
    dp[0] = 1;
    int max = 1;
    for(int i = 1; i <= n-1; i++){
        dp[i] = 1;
        for(int j=0; j<i; j++){
            if(stu[i].salary > stu[j].salary && stu[i].grade > stu[j].grade && dp[j]+1 > dp[i])
                dp[i] = dp[j] + 1;
        }
        if(dp[i] > max)
            max = dp[i];
    }
    cout << max << endl;
    return 0;
}
```