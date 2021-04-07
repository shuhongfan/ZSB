
> 本次整理试题来源于：[zqxLonely](http://www.cnblogs.com/zqxLonely/)，再次感谢老师。

> 原文链接：https://bingyishow.top/Technical-article/16.html

----------

## 练习题总览

```
    第一部分
        韩信点兵
        兰州烧饼
        进制转换
        第几天？
        成绩转换
    第二部分
        求实数的绝对值。
        计算球体积
        两点距离
        ASCII码排序
        数值统计
    第三部分
        最小公倍数
        公约数和公倍数
        5个数求最值
        素数筛子算法
        分数加减法
    第四部分
        第二小整数
        奇偶数分离
        奇偶位互换
        统计硬币
        汉字统计
    第五部分
        偶数求和
        杨辉三角
        统计字符
        完数
        素数回文
    第六部分
        快速排序
        开门人和关门人
        鸡兔同笼
        日期计算
        开灯问题
    第七部分
        字符串替换
        字母统计
        字符串逆序输出
        交换输出
        比较字母大小
    第八部分
        猴子吃桃问题
        九九乘法表
        16进制的简单运算
        三角形面积
        平方和与立方和
    第九部分
        水仙花数
        多项式求和
        绝对值排序
        首字母变大写
        a/b + c/d
```

----------


## 第一部分

### 韩信点兵

> 相传韩信才智过人，从不直接清点自己军队的人数，只要让士兵先后以三人一排、五人一排、七人一排地变换队形，而他每次只掠一眼队伍的排尾就知道总人数了。输入3个非负整数a,b,c ，表示每种队形排尾的人数（a<3,b<5,c<7），输出总人数的最小值（或报告无解）。已知总人数不小于10，不超过100 。

 - 输入
输入3个非负整数a,b,c ，表示每种队形排尾的人数（a<3,b<5,c<7）。例如,输入：2 4 5

 - 输出
输出总人数的最小值（或报告无解，即输出No answer）。实例，输出：89

```
#include <stdio.h>

int main(){
    int a;
    int b;
    int c;
    int i;
    
    scanf("%d%d%d",&a,&b,&c);
    
    for(i=10;i<=100;i++){
        if(i%3==a && i%5==b && i%7==c){
            printf("%d\n",i);
            break;
        }
    }
    
    if(i==101)
        printf("No answer\n");
    
    
    return 0;
}
```

### 兰州烧饼

> 烧饼有两面，要做好一个兰州烧饼，要两面都弄热。当然，一次只能弄一个的话，效率就太低了。有这么一个大平底锅，一次可以同时放入k个兰州烧饼，一分钟能做好一面。而现在有n个兰州烧饼，至少需要多少分钟才能全部做好呢？

 - 输入
依次输入n和k，中间以空格分隔，其中1 <= k,n <= 100000

 - 输出
输出全部做好至少需要的分钟数

 - 提示
如样例，三个兰州烧饼编号a,b,c，首先a和b，然后a和c，最后b和c，3分钟完成

```
#include <stdio.h>

int main(){
    int n;
    int k;
    int total;
    int result;
    
    while(scanf("%d%d",&n,&k)!=EOF){
        total=n*2;
        
        if(total<k){  //没有考虑到total<k的情况 
            printf("2\n");
            continue;
        }

        result=total/k;
    
        if(total%k!=0)
            result++;
        
        printf("%d\n",result);
    }
    
    return 0;
}
```
### 进制转换

> 输入一个十进制数N，将它转换成R进制数输出。

 - 输入
输入数据包含多个测试实例，每个测试实例包含两个整数N(32位整数)和R（2<=R<=16, R<>10）。

 - 输出
为每个测试实例输出转换后的数，每个输出占一行。如果R大于10，则对应的数字规则参考16进制（比如，10用A表示，等等）。

```
#include <stdio.h>

int main(){
    int number;
    int system;
    char s[50];
    int i;
    int length;
    int flag;
    
    while((scanf("%d%d",&number,&system))!=EOF){
        i=0;
        flag=0;
        
        if(number<0){
            number=-number;
            flag=1;
        }
        
        while(number){
            if(number%system<=9){
                s[i]=(number%system)+'0';
            }
            
            else if(number%system==10)
                s[i]='A';
                
            else if(number%system==11)
                s[i]='B';
            
            else if(number%system==12)
                s[i]='C';
                
            else if(number%system==13)
                s[i]='D';
                
            else if(number%system==14)
                s[i]='E';
                
            else if(number%system==15)
                s[i]='F';
                
            number/=system;
            i++;
        }
        length=i;
        
        if(flag==1)
            printf("-");
            
        for(i=length-1;i>=0;i--)
            printf("%c",s[i]);
            
        printf("\n");
        
        
        
    }
        
    
    return 0;
}
```

### 第几天？

> 给定一个日期，输出这个日期是该年的第几天。

 - 输入
输入数据有多组，每组占一行，数据格式为YYYY/MM/DD组成，具体参见sample input ,另外，可以向你确保所有的输入数据是合法的。

 - 输出
对于每组输入数据，输出一行，表示该日期是该年的第几天。

```
#include <stdio.h>
 
int main(){
    int a;
    int b;
    int c;
    int i;
    int day[13];
    int sum;
     
    day[1]=31;
    day[2]=28;
    day[3]=31;
    day[4]=30;
    day[5]=31;
    day[6]=30;
    day[7]=31;
    day[8]=31;
    day[9]=30;
    day[10]=31;
    day[11]=30;
    day[12]=31;
     
    while((scanf("%d/%d/%d",&a,&b,&c))!=EOF){
        sum=0;
         
        for(i=1;i<=b-1;i++)
            sum+=day[i];
             
        sum+=c;
         
        if((a%400==0 || (a%4==0 && a%100!=0)) && b>=3)
            sum++;
             
        printf("%d\n",sum);
    }
     
     
    return 0;
}
```

### 成绩转换

> 输入一个百分制的成绩M，将其转换成对应的等级，具体转换规则如下：
90~100为A;
80~89为B;
70~79为C;
60~69为D;
0~59为E;

```
#include <stdio.h> 

int main(){
    int T;
    int n;
    char c;
    
    scanf("%d",&T);
    
    while(T--){
        scanf("%d",&n);
        
        if(n>=90)
            c='A';
            
        else if(n>=80)
            c='B';
            
        else if(n>=70)
            c='C';
            
        else if(n>=60)
            c='D';
            
        else
            c='E';
            
        printf("%c\n",c);
    } 
    return 0;
}
```


----------


## 第二部分

### 求实数的绝对值。

> 求实数的绝对值。

 - 输入
输入数据有多组，每组占一行，每行包含一个实数。
 - 输出
对于每组输入数据，输出它的绝对值，要求每组数据输出一行，结果保留两位小数。

```
#include <stdio.h>
 
int main(){
    double number;
     
    while((scanf("%lf",&number)!=EOF)){
        if(number<0)
            number=-number;
             
        printf("%.2lf\n",number);
    }
    return 0;
}
```

### 计算球体积

> 根据输入的半径值，计算球的体积。

 - 输入
输入数据有多组，每组占一行，每行包括一个实数，表示球的半径。
 - 输出
输出对应的球的体积，对于每组输入数据，输出一行，计算结果保留三位小数。

```
#include <stdio.h>
#define PI 3.1415927
 
int main(){
    double r;
    double result;
     
    while((scanf("%lf",&r))!=EOF){
        result=4.0*PI*r*r*r/3.0;
         
        printf("%.3lf\n",result);
    }
     
    return 0;
}
```

### 两点距离

> 输入两点坐标（X1,Y1）,（X2,Y2）(0<=x1,x2,y1,y2<=1000),计算并输出两点间的距离。

 - 输入
第一行输入一个整数n（0<n<=1000）,表示有n组测试数据;随后每组占一行，由4个实数组成，分别表示x1,y1,x2,y2,数据之间用空格隔开。
 - 输出
对于每组输入数据，输出一行，结果保留两位小数。

```
#include <stdio.h> 
#include <math.h>

int main(){
    int T;
    double a;
    double b;
    double c;
    double d;
    double distance;
    
    scanf("%d",&T);
    
    while(T--){
        scanf("%lf%lf%lf%lf",&a,&b,&c,&d);
        
        distance=sqrt((a-c)*(a-c)+(b-d)*(b-d));
        
        printf("%.2lf\n",distance);
    }
    return 0;
}
```

### ASCII码排序

> 输入三个字符（可以重复）后，按各字符的ASCII码从小到大的顺序输出这三个字符。

 - 输入
第一行输入一个数N,表示有N组测试数据。后面的N行输入多组数据，每组输入数据都是占一行，有三个字符组成，之间无空格。
 - 输出
对于每组输入数据，输出一行，字符中间用一个空格分开。

```
#include <stdio.h>

int main(){
    char a;
    char b;
    char c;
    char temp;
    int T;
    
    scanf("%d",&T);
    getchar();
    
    while(T--){
        scanf("%c%c%c",&a,&b,&c);
        getchar();
        
        if(a>b){
            temp=a;
            a=b;
            b=temp;
        }
        
        if(a>c){
            temp=a;
            a=c;
            c=temp;
        }
        
        if(b>c){
            temp=b;
            b=c;
            c=temp;
        }
        
        printf("%c %c %c\n",a,b,c);
    }
    return 0;
}
```

### 数值统计

> 统计给定的n个数中，负数、零和正数的个数。

 - 输入
输入数据有多组，每组占一行，每行的第一个数是整数n（n<100），表示需要统计的数值的个数，然后是n个实数；如果n=0，则表示输入结束，该行不做处理。
 - 输出
对于每组输入数据，输出一行a,b和c，分别表示给定的数据中负数、零和正数的个数。

```
#include <stdio.h>
 
int main(){
    int n;
    int i;
    int a;
    int b;
    int c;
    double number;
     
    while(1){
        a=0;
        b=0;
        c=0;
        scanf("%d",&n);
         
        if(n==0)
            break;
             
        for(i=0;i<n;i++){
            scanf("%lf",&number);
             
            if(number<0)
                a++;
                 
            else if(number==0)
                b++;
                 
            else
                c++;
        }
         
        printf("%d %d %d\n",a,b,c);
    }
    return 0;
}
```


----------


## 第三部分

### 最小公倍数

> 给定两个正整数，计算这两个数的最小公倍数。

 - 输入
输入包含多组测试数据，每组只有一行，包括两个不大于1000的正整数.
 - 输出
对于每个测试用例，给出这两个数的最小公倍数，每个实例输出一行。

```
#include <stdio.h>
 
int get_LCM(int a,int b);
 
int main(){
    int a;
    int b;
     
    while((scanf("%d%d",&a,&b))!=EOF){
        printf("%d\n",get_LCM(a,b));
    }
     
    return 0;
}
 
int get_LCM(int a,int b){
    int temp;
    int remainder;
    int A;
    int B;
     
    A=a;
    B=b;
     
    if(a<b){
        temp=a;
        a=b;
        b=temp;
    }
     
    while(a%b){
        remainder=a%b;
        a=b;
        b=remainder;
    }
     
    return A*B/b;
}
```

### 公约数和公倍数

> 小明被一个问题给难住了，现在需要你帮帮忙。问题是：给出两个正整数，求出它们的最大公约数和最小公倍数。

 - 输入
第一行输入一个整数n（0<n<=10000)，表示有n组测试数据;随后的n行输入两个整数i,j（0<i,j<=32767)。
 - 输出
输出每组测试数据的最大公约数和最小公倍数

```
#include <stdio.h>

int main(){
    int a;
    int b;
    int temp;
    int T;
    int a_save;
    int b_save;
    
    scanf("%d",&T);
    
    while(T--){
        scanf("%d%d",&a,&b);
        
        if(a<b){
            temp=a;
            a=b;
            b=temp;
        }
        
        a_save=a;
        b_save=b;
        while(a%b!=0){
            temp=a%b;
            a=b;
            b=temp;
        }
        
        printf("%d %d\n",b,a_save*b_save/b);
    }    
    return 0;
}
```

### 5个数求最值

> 设计一个从5个整数中取最小数和最大数的程序

 - 输入
输入只有一组测试数据，为五个不大于1万的正整数
 - 输出
输出两个数，第一个为这五个数中的最小值，第二个为这五个数中的最大值，两个数字以空格格开。

```
#include <stdio.h>

int main(){
    int number;
    int min;
    int max;
    int i;
    
    for(i=0;i<5;i++){
        scanf("%d",&number);
        
        if(i==0){
            min=number;
            max=number;
            continue;
        }
        
        if(number<min)
            min=number;
            
        if(number>max)
            max=number;
    }
    
    printf("%d %d\n",min,max);
    
    return 0;
}
```

### 素数筛子算法

> 现在给你一个正整数N，要你快速的找出在2.....N这些数里面所有的素数。

 - 输入
给出一个正整数数N(N<=2000000)、但N为0时结束程序。、测试数据不超过100组
 - 输出
将2~N范围内所有的素数输出。两个数之间用空格隔开

```c
#include <stdio.h>
#include <string.h>
#include <math.h>
#define N 2000001
  
int main(){
    int i;
    int j;
    char flag[N];
    memset(flag,'0',N);
    flag[0]='1';
    flag[1]='1';
  
    for(i=2;i<=sqrt(N);i++){
        if(flag[i]=='0'){
            for(j=i*i;j<N;j+=i){
                flag[j]='1';
            }
        }
    }
  
    int number;
      
    while(1){
        scanf("%d",&number);
  
        if(number==0)
            break;
  
        for(i=2;i<=number;i++){
            if(flag[i]=='0')
                printf("%d ",i);
        }
              
        printf("\n");
    }
  
    return 0;
}
```

### 分数加减法

> 编写一个C程序，实现两个分数的加减法

 - 输入

输入包含多行数据 
每行数据是一个字符串，格式是"a/boc/d"。 
其中a, b, c, d是一个0-9的整数。o是运算符"+"或者"-"。 
数据以EOF结束 
输入数据保证合法

 - 输出
对于输入数据的每一行输出两个分数的运算结果。 注意结果应符合书写习惯，没有多余的符号、分子、分母，并且化简至最简分数

```c
#include <stdio.h> 

int gcd(int a,int b);

int main(){
    int a;
    int b;
    int c;
    int d;
    char sign;
    int fenmu;
    int fenzi;
    char temp;
    
    while(scanf("%d/%d%c%d/%d",&a,&b,&sign,&c,&d)!=EOF){
        fenmu=b*d/gcd(b,d);
        
        if(sign=='+')
            fenzi=a*fenmu/b+c*fenmu/d;
        
        else
            fenzi=a*fenmu/b-c*fenmu/d;
            
        if(fenzi==0){  //分子为0直接输出0 
            printf("0\n");
            continue;
        }
        
        temp='+';
        if(fenzi<0){  //当为负数时，化为正数，标记负号 
            fenzi=-fenzi;
            temp='-';
        }
        
        if(temp=='-')  //有负号时输出负号 
            printf("-");
        
        if(fenzi%fenmu==0)  //如果整除时直接输出商 
            printf("%d\n",fenzi/fenmu);
            
        else   //不整除时以分数的形式输出 
            printf("%d/%d\n",fenzi/gcd(fenmu,fenzi),fenmu/gcd(fenmu,fenzi));
    }
    return 0;
}

int gcd(int a,int b){
    int temp;
    
    if(a<b){
        temp=a;
        a=b;
        b=temp;
    }
    
    while(a%b!=0){
        temp=a%b;
        a=b;
        b=temp;
    }
    
    return b;
}
```

----------


## 第四部分

### 第二小整数

> 求n个整数中倒数第二小的数。每一个整数都独立看成一个数，比如，有三个数分别是1，1，3，那么，第二小的数就是1。

 - 输入

输入包含多组测试数据。
输入的第一行是一个整数C，表示有C测试数据；
每组测试数据的第一行是一个整数n，表示本组测试数据有n个整数（2<=n<=10），接着一行是 n个整数 (每个数均小于100);

 - 输出
请为每组测试数据输出第二小的整数，每组输出占一行。

```
#include <stdio.h>

int main(){
    int T;
    int n;
    int i;
    int min;
    int min_flag;
    int number[11];
    
    scanf("%d",&T);
    
    while(T--){
        scanf("%d",&n);
        
        for(i=0;i<n;i++){
            scanf("%d",&number[i]);
            
            if(i==0){
                min=number[0];
                min_flag=0;
            }
                
            if(number[i]<min){
                min=number[i];
                min_flag=i;
            }
        } 
        
        for(i=0;i<n;i++){
            if(i!=min_flag){
                min=number[i];
                break;
            }
        } 
        
        for(i=0;i<n;i++){
            if(i!=min_flag && number[i]<min)
                min=number[i];
        }
        
        printf("%d\n",min);
    }
            
    return 0;
}
```

### 奇偶数分离

> 有一个整型偶数n(2<= n <=10000),你要做的是：先把1到n中的所有奇数从小到大输出，再把所有的偶数从小到大输出。 

 - 输入
第一行有一个整数i（2<=i<30)表示有 i 组测试数据；每组有一个整型偶数n。
 - 输出
第一行输出所有的奇数。第二行输出所有的偶数

```
#include <stdio.h>

int main(){
    int T;
    int i;
    int n;
    
    scanf("%d",&T);
    
    while(T--){
        scanf("%d",&n);
        for(i=1;i<=n;i++){
            if(i%2==1){
                if(i==1)
                    printf("%d",i);
                
                else
                    printf(" %d",i);
            }
        }
        
        printf("\n");
        
        for(i=1;i<=n;i++){
            if(i%2==0){
                if(i==2)
                    printf("%d",i);
                
                else
                    printf(" %d",i);
            }
        }
        
        printf("\n");
        
        if(T!=0)
            printf("\n");
    }

    return 0;
}
```

### 奇偶位互换

> 给定一个长度为偶数位的0,1字符串，请编程实现串的奇偶位互换。

 - 输入

输入包含多组测试数据；
输入的第一行是一个整数C，表示有C测试数据；
接下来是C组测试数据，每组数据输入均为0,1字符串，保证串长为偶数位(串长<=50)。

 - 输出
请为每组测试数据输出奇偶位互换后的结果；每组输出占一行。

```
#include <stdio.h>
#include <string.h>

int main(){
    int T;
    char s[51];
    int length;
    char temp;
    int i;
    
    scanf("%d",&T);
    
    while(T--){
        scanf("%s",s);
        length=strlen(s);
        
        for(i=0;i<length-1;i+=2){
            temp=s[i];
            s[i]=s[i+1];
            s[i+1]=temp;
        }
        
        printf("%s\n",s);
    }
            
    return 0;
}
```

### 统计硬币

> 假设一堆由1分、2分、5分组成的n个硬币总面值为m分，求一共有多少种可能的组合方式（某种面值的硬币可以数量可以为0）。

 - 输入
输入数据第一行有一个正整数T，表示有T组测试数据；接下来的T行，每行有两个数n,m，n和m的含义同上。
 - 输出
对于每组测试数据，请输出可能的组合方式数；每组输出占一行。

```
#include <stdio.h>

int main(){
    int T;
    int amount;
    int sum;
    int one_amount;
    int two_amount;
    int five_amount;
    int a;
    int b;
    int c;
    int result;
    
    scanf("%d",&T);
    
    while(T--){
        result=0;
        scanf("%d%d",&amount,&sum);
        one_amount=sum/1;
        two_amount=sum/2;
        five_amount=sum/5;
        
        for(a=0;a<=one_amount;a++){
            for(b=0;b<=two_amount;b++){
                for(c=0;c<=five_amount;c++){
                    if((a+b+c)==amount && (a*1+b*2+c*5)==sum)
                        result++;
                }
            }
        }
        printf("%d\n",result);
    }
            
    return 0;
}
```

### 汉字统计

> 统计给定文本文件中汉字的个数。

 - 输入
输入文件首先包含一个整数n，表示测试实例的个数，然后是n段文本。
 - 输出
对于每一段文本，输出其中的汉字的个数，每个测试实例的输出占一行。

```
#include <stdio.h>

int main(){
    int T;
    char c;
    int amount;
    
    scanf("%d",&T);
    getchar();
    
    while(T--){
        amount=0;
        while((c=getchar())!='\n'){
            if(c<0 || c>127)
                amount++;
        }
        printf("%d\n",amount/2);
    }
        
    
    return 0;
}
```


----------


## 第五部分

### 偶数求和

> 有一个长度为n(n<=100)的数列，该数列定义为从2开始的递增有序偶数，现在要求你按照顺序每m个数求出一个平均值，如果最后不足m个，则以实际数量求平均值。编程输出该平均值序列。

 - 输入
输入数据有多组，每组占一行，包含两个正整数n和m，n和m的含义如上所述。
 - 输出
对于每组输入数据，输出一个平均值序列，每组输出占一行。

```
#include <stdio.h>

int main(){
    int sequence[101];
    int i;
    int j;
    int n;
    int m;
    int result;
    int remainder;
    int flag;
    
    for(i=0;i<101;i++)
        sequence[i]=(i+1)*2;
        
    while((scanf("%d%d",&n,&m))!=EOF){
        result=0;
        j=1;
        flag=0;
        
        remainder=n%m;
        
        for(i=0;i<=n;i++){
            if(j<=m){
                result+=sequence[i];
            }
            
            else{
                if(flag==0)
                    printf("%d",result/m);
                    
                else
                    printf(" %d",result/m);
                    
                flag=1;
                j=1;
                result=sequence[i];
            }    
            j++;
        }
        
        if(remainder){
            printf(" %d",(result-sequence[n])/remainder);
        }
        
        printf("\n");
    }
        
        
            
    
    return 0;
}
```
### 杨辉三角

> 还记得中学时候学过的杨辉三角吗？具体的定义这里不再描述，你可以参考以下的图形：
1
1 1
1 2 1
1 3 3 1
1 4 6 4 1
1 5 10 10 5 1

 - 输入
输入数据包含多个测试实例，每个测试实例的输入只包含一个正整数n（1<=n<=30），表示将要输出的杨辉三角的层数。
 - 输出
对应于每一个输入，请输出相应层数的杨辉三角，每一层的整数之间用一个空格隔开，每一个杨辉三角后面加一个空行。

```
#include <stdio.h>   //本来不会做的，但是编着编着就出来了，么么哒 

int main(){
    int n;
    int triangle[31][31];
    int i;
    int j;
    
    while((scanf("%d",&n))!=EOF){
        for(i=0;i<31;i++)
            for(j=0;j<31;j++)
                triangle[i][j]=0;
        
        triangle[0][0]=1;
        triangle[1][0]=1;
        triangle[1][1]=1;
                
        for(i=2;i<n;i++){
            triangle[i][0]=1;
            triangle[i][i]=1;
            for(j=1;j<=i;j++){
                triangle[i][j]=triangle[i-1][j]+triangle[i-1][j-1];
            }
        }
        
        for(i=0;i<n;i++){
            for(j=0;j<n;j++){
                if(triangle[i][j]!=0){
                    if(j==0)
                        printf("%d",triangle[i][j]);
                        
                    else
                        printf(" %d",triangle[i][j]);
                }
            }
                
            printf("\n");
        }
        
        printf("\n");
        
    } 
    return 0;
}
```

### 统计字符

> 统计一个给定字符串中指定的字符出现的次数

 - 输入
测试输入包含若干测试用例，每个测试用例包含2行，第1行为一个长度不超过5的字符串，第2行为一个长度不超过80的字符串。注意这里的字符串包含空格，即空格也可能是要求被统计的字符之一。当读到'#'时输入结束，相应的结果不要输出。

 - 输出

对每个测试用例，统计第1行中字符串的每个字符在第2行字符串中出现的次数，按如下格式输出：
c0 n0
c1 n1
c2 n2
... 
其中ci是第1行中第i个字符，ni是ci出现的次数。

```
#include <stdio.h> 
#include <string.h>

int main(){
    char s1[6];
    char s2[81];
    int s1_length;
    int s2_length;
    int i;
    int j;
    int time;
    char c;

    while(1){
        i=0;    //s1包含空格
        while((c=getchar())!='\n'){
            s1[i]=c;
            i++;
        }
        s1[i]='\0';

        if(s1[0]=='#')    
            break;

        i=0;    //s2包含空格
        while((c=getchar())!='\n'){
            s2[i]=c;
            i++;
        }
        s2[i]='\0';

        s1_length=strlen(s1);
        s2_length=strlen(s2);

        for(i=0;i<s1_length;i++){
            time=0;
            for(j=0;j<s2_length;j++){
                if(s1[i]==s2[j])
                    time++;
            }

            printf("%c %d\n",s1[i],time);
        }
    }
    return 0;
}
```

### 完数

> 完数的定义：如果一个大于1的正整数的所有因子之和等于它的本身，则称这个数是完数，比如6，28都是完数：6=1+2+3；28=1+2+4+7+14。

 - 输入
输入数据包含多行，第一行是一个正整数n，表示测试实例的个数，然后就是n个测试实例，每个实例占一行，由两个正整数num1和num2组成,(1<num1,num2<10000) 。
 - 输出
对于每组测试数据，请输出num1和num2之间（包括num1和num2）存在的完数个数。

```
#include <stdio.h>

int if_perfect_number(int number);

int main(){
    int T;
    int number1;
    int number2;
    int temp;
    int i;
    int amount;

    scanf("%d",&T);

    while(T--){
        amount=0;
        scanf("%d%d",&number1,&number2);

        if(number1>number2){
            temp=number1;
            number1=number2;
            number2=temp;
        }

        for(i=number1;i<=number2;i++){
            if(if_perfect_number(i)==1)
                amount++;
        }

        printf("%d\n",amount);
    }
    return 0;
}

int if_perfect_number(int number){
    int i;
    int sum;

    sum=0;

    for(i=1;i<=number/2;i++){
        if(number%i==0)
            sum+=i;
    }

    if(sum==number)
        return 1;

    else
        return 0;
}
```

### 素数回文

> xiaoou33对既是素数又是回文的数特别感兴趣。比如说151既是素数又是个回文。现在xiaoou333想要你帮助他找出某个范围内的素数回文数，请你写个程序找出 a 跟b 之间满足条件的数。(5 <= a < b <= 100,000,000);

 - 输入
这里有许多组数据，每组包括两组数据a跟b。
 - 输出
对每一组数据,按从小到大输出a，b之间所有满足条件的素数回文数（包括a跟b）每组数据之后空一行。

```
#include <stdio.h>
#include <string.h>
#include <math.h>

#define N 10000000   //9999999是题目要求范围的最大回文数
char flag[N];

int palindrome_number(int number);

int main(){
    int i;
    int j;
    int a;
    int b;

    memset(flag,'0',N);
    flag[0]='1';
    flag[1]='1';

    for(i=2;i<=sqrt((double)N);i++){
        if(flag[i]=='0'){
            for(j=i*i;j<N;j+=i)
                flag[j]='1';
        }
    }

    while(scanf("%d%d",&a,&b)!=EOF){
        for(i=a;i<=b;i++){
            if(i>N-1)
                continue;

            if(palindrome_number(i)==1 && flag[i]=='0')
                printf("%d\n",i);
        }

        printf("\n");
    }

    return 0;
}

int palindrome_number(int number){
    int array[9];
    int i;
    int length;
    int flag;

    i=0;
    while(number){
        array[i]=number%10;
        i++;
        number/=10;    
    }
    length=i;

    flag=0;
    for(i=0;i<length/2;i++){
        if(array[i]!=array[length-i-1]){
            flag=1;
            break;
        }
    }

    if(flag==1)
        return 0;

    else
        return 1;
}
```


----------


## 第六部分

### 快速排序

> 给你n个整数，请按从大到小的顺序输出其中前m大的数。

 - 输入
每组测试数据有两行，第一行有两个数n,m(0<n,m<1000000)，第二行包含n个各不相同，且都处于区间[-500000,500000]的整数。
 - 输出
对每组测试数据按从大到小的顺序输出前m大的数。

```
#include <stdio.h>

void quickSort(int a[],int left,int right);
int array[1000001];

int main(){
    int n;
    int m;
    int i;
    
    while(scanf("%d%d",&n,&m)!=EOF){
        for(i=0;i<n;i++)
            scanf("%d",&array[i]);
            
        quickSort(array,0,n-1);
        
        for(i=n-1;i>n-m-1;i--){
            if(i==n-1)
                printf("%d",array[i]);
                
            else
                printf(" %d",array[i]);
        }
        
        printf("\n");
    }
    
    return 0;
}

void quickSort(int a[],int left,int right){
    int i;
    int j;
    int temp;
    
    i=left;
    j=right;
    temp=a[left];
    
    if(left>=right)
        return;
        
    while(i!=j){
        while(i<j && a[j]>=temp)
            j--;
            
        if(i<j){
            a[i]=a[j];
        }
            
            
        while(i<j && a[i]<=temp)
             i++;
             
        if(i<j){
            a[j]=a[i];
        }
    }
    a[i]=temp;
    
    quickSort(a,left,i-1);
    quickSort(a,i+1,right);    
}
```

### 开门人和关门人

> 每天第一个到机房的人要把门打开，最后一个离开的人要把门关好。现有一堆杂乱的机房签 
到、签离记录，请根据记录找出当天开门和关门的人。

 - 输入

测试输入的第一行给出记录的总天数N ( > 0 )。下面列出了N天的记录。 
每天的记录在第一行给出记录的条目数M ( > 0 )，下面是M行，每行的格式为 

证件号码 签到时间 签离时间 

其中时间按“小时:分钟:秒钟”（各占2位）给出，证件号码是长度不超过15的字符串。

 - 输出

对每一天的记录输出1行，即当天开门和关门人的证件号码，中间用1空格分隔。 
注意：在裁判的标准测试输入中，所有记录保证完整，每个人的签到时间在签离时间之前， 
且没有多人同时签到或者签离的情况。

```
#include <stdio.h>
#include <string.h>

int main(){
    int N;
    int M;
    int i;
    char ID[16];
    char minID[16];
    char maxID[16];
    char s1[9];
    char s2[9];
    char time1[7];
    char time2[7];
    char minTime[7];
    char maxTime[7];

    scanf("%d",&N);

    while(N--){
        scanf("%d",&M);

        for(i=0;i<M;i++){
            scanf("%s%s%s",ID,s1,s2);
            time1[0]=s1[0];
            time1[1]=s1[1];
            time1[2]=s1[3];
            time1[3]=s1[4];
            time1[4]=s1[6];
            time1[5]=s1[7];
            time1[6]='\0';

            time2[0]=s2[0];
            time2[1]=s2[1];
            time2[2]=s2[3];
            time2[3]=s2[4];
            time2[4]=s2[6];
            time2[5]=s2[7];
            time2[6]='\0';

            if(i==0){
                strcpy(minID,ID);
                strcpy(maxID,ID);
                strcpy(minTime,time1);
                strcpy(maxTime,time2);
                continue;
            }

            if(strcmp(time1,minTime)<0){
                strcpy(minID,ID);
                strcpy(minTime,time1);
            }

            if(strcmp(time2,maxTime)>0){
                strcpy(maxID,ID);
                strcpy(maxTime,time2);
            }
        }

        printf("%s %s\n",minID,maxID);


    }
    
    
    return 0;
}
```

### 鸡兔同笼

> 已知鸡和兔的总数量为n,总腿数为m。输入n和m,依次输出鸡和兔的数目，如果无解，则输出“No answer”(不要引号)。

 - 输入
第一行输入一个数据a,代表接下来共有几组数据，在接下来的(a<10)、a行里，每行都有一个n和m.(0<m,n<100)
 - 输出
输出鸡兔的个数，或者No answer

```
#include <stdio.h> 

int main(){
    int T;
    int n;
    int m;
    
    scanf("%d",&T);
    
    while(T--){
        scanf("%d%d",&n,&m);
        
        if((m-2*n)>=0 && (m-2*n)%2==0 && (4*n-m)>=0 && (4*n-m)%2==0)
            printf("%d %d\n",(4*n-m)/2,(m-2*n)/2);
            
        else
            printf("No answer\n");    
    }
    return 0;
}
```

### 日期计算

> 如题，输入一个日期，格式如：2010 10 24 ，判断这一天是这一年中的第几天。 

 - 输入
第一行输入一个数N（0<N<=100）,表示有N组测试数据。后面的N行输入多组输入数据，每行的输入数据都是一个按题目要求格式输入的日期。
 - 输出
每组输入数据的输出占一行，输出判断出的天数n

```
#include <stdio.h> 

int main(){
    int T;
    int a;
    int b;
    int c;
    int i;
    int day[13];
    int amount;
    
    day[1]=31;
    day[2]=28;
    day[3]=31;
    day[4]=30;
    day[5]=31;
    day[6]=30;
    day[7]=31;
    day[8]=31;
    day[9]=30;
    day[10]=31;
    day[11]=30;
    day[12]=31;
    
    scanf("%d",&T);
    
    while(T--){
        scanf("%d%d%d",&a,&b,&c);
        
        amount=0;
        for(i=1;i<b;i++)
            amount+=day[i];
        amount+=c;
        
        if((a%400==0 || (a%4==0 && a%100!=0)) && i>=3)
            amount++;
            
        printf("%d\n",amount);
    }
    return 0;
}
```

### 开灯问题

> 有n盏灯，编号为1~n，第1个人把所有灯打开，第2个人按下所有编号为2 的倍数的开关（这些灯将被关掉），第3 个人按下所有编号为3的倍数的开关（其中关掉的灯将被打开，开着的灯将被关闭），依此类推。一共有k个人，问最后有哪些灯开着？输入：n和k，输出开着的灯编号。k≤n≤1000

 - 输入
输入一组数据：n和k
 - 输出
输出开着的灯编号

```
#include <stdio.h> 
#include <string.h>

int main(){
    int n;
    int k;
    int flag[1001];
    int i;
    int j;
    
    scanf("%d%d",&n,&k);
    memset(flag,0,sizeof(int)*1001);
    
    for(i=1;i<=k;i++){
        for(j=1;j<=n;j++){
            if(j%i==0){
                if(flag[j-1]==0)
                    flag[j-1]=1;
                    
                else
                    flag[j-1]=0;
            }
        }
    }
    
    for(i=0;i<n;i++){
        if(flag[i]==1){
            printf("%d",i+1);
            flag[i]=0;
            break;
        }
    }
    
    for(i=0;i<n;i++){
        if(flag[i]==1)
            printf(" %d",i+1);
    }
    
    printf("\n");
    
    return 0;
}
```


----------


## 第七部分

### 字符串替换

> 编写一个程序实现将字符串中的所有"you"替换成"we"

 - 输入

输入包含多行数据 
每行数据是一个字符串，长度不超过1000 
数据以EOF结束

 - 输出
对于输入的每一行，输出替换后的字符串

```
#include <stdio.h> 
#include <string.h>

int main(){
    char c;
    char s[1001];
    int i;
    int length;
    
    while(scanf("%c",&c)!=EOF){
        i=0;
        while(c!='\n'){
            s[i]=c;
            i++;
            c=getchar();
        }
        s[i]='\0';
        length=strlen(s);
        
        for(i=0;i<length-2;i++){  //这里处理很巧妙，直接赋值即可，真是高 
            if(s[i]=='y' && s[i+1]=='o' && s[i+2]=='u'){
                s[i]='w';
                s[i+1]='e';
                s[i+2]='\0';  //赋值为'\0'，是因为其他位置的字符不可能为'\0'   
            }        
        }
        
        for(i=0;i<length;i++){
            if(s[i]!='\0')
                printf("%c",s[i]);
        }
            
        printf("\n");
    }    
    return 0;
}
```

### 字母统计

> 现在给你一个由小写字母组成字符串，要你找出字符串中出现次数最多的字母，如果出现次数最多字母有多个那么输出最小的那个。

 - 输入
第一行输入一个正整数T（0<T<25）随后T行输入一个字符串s,s长度小于1010。
 - 输出
每组数据输出占一行，输出出现次数最多的字符；

```
#include <stdio.h> 
#include <string.h>

int main(){
    char s[1100];
    int T;
    int amount[27];
    int i;
    int max;
    char c;
    
    scanf("%d",&T);
    
    while(T--){
        scanf("%s",&s);
        
        memset(amount,0,sizeof(int)*27);
        
        for(i=0;s[i]!='\0';i++){
            amount[s[i]-'a'+1]++;
        }
        
        for(i=1;i<=26;i++){
            if(amount[i]!=0){
                c=i-1+'a';
                max=amount[i];
                break;
            }
        }
        
        for(i=1;i<=26;i++){
            if(amount[i]>max){
                c=i-1+'a';
                max=amount[i];
            }
        }
        
        printf("%c\n",c);
    }
    return 0;
}
```

### 字符串逆序输出

> 给定一行字符，逆序输出此行（空格.数字不输出）

 - 输入

第一行是一个整数N(N<10)表示测试数据的组数）
每组测试数据占一行，每行数据中间有且只有一个空格（这样你可以把此行当成两个字符串读取）。
每行字符长度不超过40
并且保证输入的字符只有空格（1个），数字，小写字母三种

 - 输出
对应每行测试数据，逆序输出（空格和数字不输出）

```
#include <stdio.h> 
#include <string.h>
#include <ctype.h>

int main(){
    char s[50];
    int T;
    int length;
    int i;
    
    scanf("%d",&T);
    getchar();
    
    while(T--){
        gets(s);
        length=strlen(s);
        
        for(i=length-1;i>=0;i--){
            if(isalpha(s[i]))
                printf("%c",s[i]);
        }
        
        printf("\n");
    }
    return 0;
}
```

### 交换输出

> 输入n(n<100)个数，找出其中最小的数，将它与最前面的数交换后输出这些数。(如果这个第一个数就是最小的数，则保持原样输出，如果最小的数有相同的按照前面的交换)

 - 输入
输入数据有多组，每组占一行，每行的开始是一个整数n，表示这个测试实例的数值的个数，跟着就是n个整数。n=0表示输入的结束，不做处理。
 - 输出
对于每组输入数据，输出交换后的数列，每组输出占一行。

```
#include <stdio.h> 

int main(){
    int n;
    int number[101];
    int i;
    int min;
    int flag;
    int temp;
    
    while(1){
        scanf("%d",&n);
        
        if(n==0)
            break;
            
        for(i=0;i<n;i++)
            scanf("%d",&number[i]);
            
        flag=0;
        min=number[0];
        
        for(i=0;i<n;i++){
            if(number[i]<min){
                min=number[i];
                flag=i;
            }
        }
        
        temp=number[0];
        number[0]=number[flag];
        number[flag]=temp;
        
        for(i=0;i<n;i++){
            if(i!=0)
                printf(" ");
                
            printf("%d",number[i]);
        }
        printf("\n");
    }
    return 0;
}
```

### 比较字母大小

> 任意给出两个英文字母，比较它们的大小，规定26个英文字母A,B,C.....Z依次从大到小。

 - 输入
第一行输入T，表示有T组数据；接下来有T行，每行有两个字母，以空格隔开；
 - 输出
输出各组数据的比较结果，输出格式见样例输出；（注意输出严格按照输入的顺序即输入是A B，输出时必须是A?B）

```
#include <stdio.h> 

int main(){
    int T;
    char a;
    char b;
    char compare;
    
    scanf("%d",&T);
    getchar();
    
    while(T--){
        scanf("%c %c",&a,&b);
        getchar();
        
        if(a==b)
            compare='=';
            
        else if(a>b)
            compare='<';
            
        else
            compare='>';
            
        printf("%c%c%c\n",a,compare,b);
    }
    return 0;
}
```


----------


## 第八部分

### 猴子吃桃问题

> 有一堆桃子不知数目，猴子第一天吃掉一半，又多吃了一个，第二天照此方法，吃掉剩下桃子的一半又多一个，天天如此，到第m天早上，猴子发现只剩一只桃子了，问这堆桃子原来有多少个？ (m<29)

 - 输入
第一行有一个整数n,表示有n组测试数据（从第二行开始，每一行的数据为：第m天）；
 - 输出
每一行数据是桃子的总个数

```
#include <stdio.h> 

int main(){
    int T;
    int m;
    int i;
    int result;
    
    scanf("%d",&T);
    
    while(T--){
        scanf("%d",&m);
        
        result=1;
        for(i=1;i<=m;i++)
            result=(result+1)*2;
            
        printf("%d\n",result);    
    }
    return 0;
}
```

### 九九乘法表

> 小时候学过的九九乘法表也许将会扎根于我们一生的记忆,现在让我们重温那些温暖的记忆,请编程输出九九乘法表.
现在要求你输出它的格式与平常的 不同啊! 是那种反过来的三角形啦，具体如下图：
每两个式子之前用一个空格 隔开。。。

 - 输入
第一有一个整数N，表示有N组数据（N<10）接下来由N行，每行只有一个整数M(1<=M<=9);
 - 输出
对应每个整数M，根据要求输出乘法表的前N行,具体格式参见输入输出样例和上图.每两组测试数据结果之间有一个空行隔开，

```
#include <stdio.h>
#include <math.h>

int main(){
    int T;
    int n;
    int i;
    int j;
    
    scanf("%d",&T);
    
    while(T--){
        scanf("%d",&n);
        
        for(i=1;i<=n;i++){
            for(j=i;j<=9;j++){
                if(j!=i)
                    printf(" ");
                
                printf("%d*%d=%d",i,j,i*j);
            }
            printf("\n");
        }
        
        if(T!=0)
            printf("\n");    
    }
    return 0;
}
```

### 16进制的简单运算

> 现在给你一个16进制的加减法的表达式，要求用8进制输出表达式的结果。

 - 输入

第一行输入一个正整数T（0<T<100000）
接下来有T行，每行输入一个字符串s（长度小于15)字符串中有两个数和一个加号或者一个减号，且表达式合法并且所有运算的数都小于31位

 - 输出
每个表达式输出占一行，输出表达式8进制的结果。

```
#include <stdio.h>

int main(){
    int a;
    int b;
    int sum;
    int T;
    char c;
    
    scanf("%d",&T);
    
    while(T--){
        scanf("%x%c%x",&a,&c,&b);
        
        if(c=='+')
            sum=a+b;
            
        else
            sum=a-b;
            
        if(sum<0){   //只有当sum为__int64类型时，才要进行正负的判断
            sum=-sum;
            printf("-");
        }
        
        printf("%o\n",sum);
    }
    
    
    
    return 0;
}
```

### 三角形面积

> 给你三个点，表示一个三角形的三个顶点，现你的任务是求出该三角形的面积

 - 输入
每行是一组测试数据，有6个整数x1,y1,x2,y2,x3,y3分别表示三个点的横纵坐标。（坐标值都在0到10000之间）输入0 0 0 0 0 0表示输入结束。测试数据不超过10000组
 - 输出
输出这三个点所代表的三角形的面积，结果精确到小数点后1位（即使是整数也要输出一位小数位）

```
#include <stdio.h>
#include <math.h>

int main(){
    int x1;
    int y1;
    int x2;
    int y2;
    int x3;
    int y3;
    double s;
    
    while(1){
        scanf("%d%d%d%d%d%d",&x1,&y1,&x2,&y2,&x3,&y3);
        
        if(x1==0 && y1==0 && x2==0 && y2==0 && x3==0 && y3==0)
            break;
                
        s=fabs((double)x1*y2-x2*y1+x3*y1-x1*y3+x2*y3-x3*y2)/2;
    
        printf("%.1lf\n",s);
    }
    
    return 0;
}
```

### 平方和与立方和

> 给定一段连续的整数，求出他们中所有偶数的平方和以及所有奇数的立方和。

 - 输入
输入数据包含多组测试实例，每组测试实例包含一行，由两个整数m和n组成。
 - 输出
对于每组输入数据，输出一行，应包括两个整数x和y，分别表示该段连续的整数中所有偶数的平方和以及所有奇数的立方和。你可以认为32位整数足以保存结果。

```
#include <stdio.h>
 
int main(){
    int a;
    int b;
    int i;
    int temp;
    int oushu_sum;
    int jishu_sum;
     
    while((scanf("%d%d",&a,&b))!=EOF){
        oushu_sum=0;
        jishu_sum=0;
         
        if(a>b){
            temp=a;
            a=b;
            b=temp;
        }
         
        for(i=a;i<=b;i++){
            if(i%2==0){
                oushu_sum+=(i*i);
            }
             
            else
                jishu_sum+=(i*i*i);
        }
         
        printf("%d %d\n",oushu_sum,jishu_sum);
    }
     
    return 0;
}
```


----------


## 第九部分 

### 水仙花数

> 春天是鲜花的季节，水仙花就是其中最迷人的代表，数学上有个水仙花数，他是这样定义的：

“水仙花数”是指一个三位数，它的各位数字的立方和等于其本身，比如：153=1^3+5^3+3^3。

现在要求输出所有在m和n范围内的水仙花数。

 - 输入
输入数据有多组，每组占一行，包括两个整数m和n（100<=m<=n<=999）。
 - 输出

对于每个测试实例，要求输出所有在给定范围内的水仙花数，就是说，输出的水仙花数必须大于等于m,并且小于等于n，如果有多个，则要求从小到大排列在一行内输出，之间用一个空格隔开;
如果给定的范围内不存在水仙花数，则输出no;
每个测试实例的输出占一行。

```
#include <stdio.h>
 
int main(){
    int a;
    int b;
    int temp;
    int i;
     
    int number1;
    int number2;
    int number3;
    int flag;
     
    while((scanf("%d%d",&a,&b))!=EOF){
        flag=0;
        if(a>b){
            temp=a;
            a=b;
            b=temp;
        }
         
        for(i=a;i<=b;i++){
            number1=i%10;
            number2=i/10%10;
            number3=i/100;
             
            if(i==(number1*number1*number1+number2*number2*number2+number3*number3*number3)){
                if(flag==0)
                    printf("%d",i);
                     
                else
                    printf(" %d",i);
                flag=1;
            }
        }
         
        if(flag==0)
            printf("no");
             
        printf("\n");
    }
     
    return 0;
}
```

### 多项式求和

> 多项式的描述如下：

1 - 1/2 + 1/3 - 1/4 + 1/5 - 1/6 + ...

现在请你求出该多项式的前n项的和。

 - 输入
输入数据由2行组成，首先是一个正整数m（m<100），表示测试实例的个数，第二行包含m个正整数，对于每一个整数(不妨设为n,n<1000），求该多项式的前n项的和。
 - 输出
对于每个测试实例n，要求输出多项式前n项的和。每个测试实例的输出占一行，结果保留2位小数。

```
#include <stdio.h>
 
double get_result(int number);
 
int main(){
    int n;
    int number;
     
    scanf("%d",&n);
     
    while(n--){
        scanf("%d",&number);
         
        printf("%.2lf\n",get_result(number));
    }
     
    return 0;
}
 
double get_result(int number){
    int i;
    int temp=1;
    double result=0;
     
    for(i=1;i<=number;i++){
        result+=(1.0/i*temp);
        temp=-temp;
    }
     
    return result;
}
```

### 绝对值排序

> 输入n(n<=100)个整数，按照绝对值从大到小排序后输出。题目保证对于每一个测试实例，所有的数的绝对值都不相等。

 - 输入
输入数据有多组，每组占一行，每行的第一个数字为n,接着是n个整数，n=0表示输入数据的结束，不做处理
 - 输出
对于每个测试实例，输出排序后的结果，两个数之间用一个空格隔开。每个测试实例占一行。

```
#include <stdio.h>
#include <math.h>
 
int main(){
    int n;
    int number[101];
    int i;
    int j;
    int temp;
     
    while(1){
        scanf("%d",&n);
         
        if(n==0)
            break;
             
        for(i=0;i<n;i++)
            scanf("%d",&number[i]);
             
        for(i=0;i<n-1;i++){
            for(j=i+1;j<n;j++){
                if(fabs(number[i])<(fabs(number[j]))){
                    temp=number[i];
                    number[i]=number[j];
                    number[j]=temp;
                }
            }
        }
         
        for(i=0;i<n;i++){
            printf("%d",number[i]);
             
            if(i!=n-1)
                printf(" ");
        }
         
        printf("\n");
         
    }
     
         
    return 0;
}
```

### 首字母变大写

> 输入一个英文句子，将每个单词的第一个字母改成大写字母。

 - 输入
输入数据包含多个测试实例，每个测试实例是一个长度不超过100的英文句子，占一行。
 - 输出
请输出按照要求改写后的英文句子。

```
#include <stdio.h>
#include <ctype.h>
 
int main(){
    char c;
    int flag;
     
    while((scanf("%c",&c))!=EOF){
        flag=1;
         
        while(c!='\n'){
            if(islower(c)!=0 && flag==1){
                c=toupper(c);
                flag=0;
            }
             
                 
            if(c==' ')
                flag=1;
             
            printf("%c",c);
             
            c=getchar();
        }
         
        printf("\n");
    }
             
    return 0;
}
```

### a/b + c/d

> 给你2个分数，求他们的和，并要求和为最简形式。

 - 输入
输入首先包含一个正整数T（T<=1000），表示有T组测试数据，然后是T行数据，每行包含四个正整数a,b,c,d（0<a,b,c,d<1000），表示两个分数a/b 和 c/d。
 - 输出
对于每组测试数据，输出两个整数e和f，表示a/b + c/d的最简化结果是e/f，每组输出占一行。

```
#include <stdio.h>

int get_gcd(int a,int b);

int main(){
    int T;
    int a;
    int b;
    int c;
    int d;
    int lcm;
    int temp;
    int gcd;
    
    scanf("%d",&T);
    
    while(T--){
        scanf("%d%d%d%d",&a,&b,&c,&d);
        lcm=b*d/get_gcd(b,d);
        
        temp=(lcm/b*a+lcm/d*c);
        gcd=get_gcd(temp,lcm);
        
        printf("%d %d\n",temp/gcd,lcm/gcd);    
    }        
    return 0;
}

int get_gcd(int a,int b){
    int temp;
    int remainder;
    
    if(a<b){
        temp=a;
        a=b;
        b=temp;
    }
    
    while(a%b){
        remainder=a%b;
        
        a=b;
        b=remainder;
    }
    
    return b;
}
```


 - 如果您想转载这些内容，还望标明来源：https://bingyishow.top