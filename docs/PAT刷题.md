# PAT刷题记录（1-16）

* 又来写bug了
* 没满分的都标记括号里了（等心情好再去看看
* 产量==质量（雾），就算是水水水水水水水题都写了干嘛不记（叉腰
* 每年总有那么几天用来折麽自己一下









* ？注释是什么



### 1.L1-001 Hello World! (5 分)

本题要求编写程序，输出一个短句“Hello World!”。

**输入格式:**

本题目没有输入。

**输出格式:**

在一行中输出短句“Hello World!”。

```c++
#include <iostream>
using namespace std;
int main(){
    cout<<"Hello World!"<<endl;
    return 0;
}
```

### 2.L1-002 打印沙漏 (20 分)

本题要求你写个程序把给定的符号打印成沙漏的形状。例如给定17个“*”，要求按下列格式打印

```
*****
 ***
  *
 ***
*****
```

所谓“沙漏形状”，是指每行输出奇数个符号；各行符号中心对齐；相邻两行符号数差2；符号数先从大到小顺序递减到1，再从小到大顺序递增；首尾符号数相等。

给定任意N个符号，不一定能正好组成一个沙漏。要求打印出的沙漏能用掉尽可能多的符号。

**输入格式:**

输入在一行给出1个正整数N（≤1000）和一个符号，中间以空格分隔。

**输出格式:**

首先打印出由给定符号组成的最大的沙漏形状，最后在一行中输出剩下没用掉的符号数。

**输入样例:**

```in
19 *
```

**输出样例:**

```out
*****
 ***
  *
 ***
*****
2
```

**代码：**

```c++
#include <iostream>
#include <cstdio>
using namespace std;
int main()
{
    int num;
    char w;
    scanf("%d %c",&num,&w);
    if(num==0)
        return 0;
    int count=2;
    num--;
    while(num>=(count*2-1)*2)
    {
        num=num-((2*count-1)*2);
        count++;
    }
    for(int i=count-1;i>0;i--)
    {
        for(int j=0;j<(count-1)-i;j++)
            cout<<" ";
        for(int k=i*2-1;k>0;k--)
            cout<<w;
        cout<<endl;
    }
    for(int i=2;i<=count-1;i++)
    {
        for(int j=0;j<(count-1)-i;j++)
            cout<<" ";
        for(int k=i*2-1;k>0;k--)
            cout<<w;
        cout<<endl;
    }
    cout<<num<<endl;
    return 0;
}
```

### 3.L1-003 个位数统计 (15 分)

给定一个 *k* 位整数 *N*=*d**k*−110*k*−1+⋯+*d*1101+*d*0 (0≤*d**i*≤9, *i*=0,⋯,*k*−1, *d**k*−1>0)，请编写程序统计每种不同的个位数字出现的次数。例如：给定 *N*=100311，则有 2 个 0，3 个 1，和 1 个 3。

**输入格式：**

每个输入包含 1 个测试用例，即一个不超过 1000 位的正整数 *N*。

**输出格式：**

对 *N* 中每一种不同的个位数字，以 `D:M` 的格式在一行中输出该位数字 `D` 及其在 *N* 中出现的次数 `M`。要求按 `D` 的升序输出。

**输入样例：**

```in
100311
```

**输出样例：**

```out
0:2
1:3
3:1
```

**代码：**

```c++
#include <iostream>
#include <cstdio>
#include <string>
#include <map>
using namespace std;
int main()
{
    string w;
    cin>>w;
    map<char,int> map_num;
    map<char,int>::iterator iter;
    for(int i=0;i<w.length();i++)
    {
        if(map_num.find(w[i])->first)
        {
            map_num[w[i]]++;
        }
        else
            map_num.insert(make_pair(w[i], 1));
    }
    for(iter=map_num.begin();iter!=map_num.end();iter++)
        cout<<iter->first<<":"<<iter->second<<endl;
    return 0;
}
```

### 4.L1-004 计算摄氏温度 (5 分)

给定一个华氏温度*F*，本题要求编写程序，计算对应的摄氏温度*C*。计算公式：*C*=5×(*F*−32)/9。题目保证输入与输出均在整型范围内。

**输入格式:**

输入在一行中给出一个华氏温度。

**输出格式:**

在一行中按照格式“Celsius = C”输出对应的摄氏温度C的整数值。

**输入样例:**

```in
150
```

**输出样例:**

```out
Celsius = 65
```

**代码：**

```c++
#include <iostream>
using namespace std;
int main()
{
    int f,c;
    cin>>f;
    f=f-32;
    c=(int)(5*f/9);
    cout<<"Celsius = "<<c<<endl;
    return 0;
}
```



### 5.L1-005 考试座位号 (15 分)

每个 PAT 考生在参加考试时都会被分配两个座位号，一个是试机座位，一个是考试座位。正常情况下，考生在入场时先得到试机座位号码，入座进入试机状态后，系统会显示该考生的考试座位号码，考试时考生需要换到考试座位就座。但有些考生迟到了，试机已经结束，他们只能拿着领到的试机座位号码求助于你，从后台查出他们的考试座位号码。

**输入格式：**

输入第一行给出一个正整数 *N*（≤1000），随后 *N* 行，每行给出一个考生的信息：`准考证号 试机座位号 考试座位号`。其中`准考证号`由 16 位数字组成，座位从 1 到 *N* 编号。输入保证每个人的准考证号都不同，并且任何时候都不会把两个人分配到同一个座位上。

考生信息之后，给出一个正整数 *M*（≤*N*），随后一行中给出 *M* 个待查询的试机座位号码，以空格分隔。

**输出格式：**

对应每个需要查询的试机座位号码，在一行中输出对应考生的准考证号和考试座位号码，中间用 1 个空格分隔。

**输入样例：**

```in
4
3310120150912233 2 4
3310120150912119 4 1
3310120150912126 1 3
3310120150912002 3 2
2
3 4
```

**输出样例：**

```out
3310120150912002 2
3310120150912119 1
```

**代码：**

```c++
#include <iostream>
#include <cstdio>
#define MAXStudent 1001
using namespace std;
struct{
    string id;
    int p,r;
}student_info[MAXStudent];
int main()
{
    string sid;
    int sp,sr;
    int n;
    cin>>n;
    for(int i=0;i<n;i++)
    {
        cin>>sid;
        cin>>sp>>sr;
        student_info[i].id=sid;
        student_info[i].p=sp;
        student_info[i].r=sr;
    }
    int m,sm;
    cin>>m;
    for(int i=0;i<m;i++)
    {
        cin>>sm;
        for(int j=0;j<n;j++)
        {
            if(student_info[j].p==sm)
                cout<<student_info[j].id<<" "<<student_info[j].r<<endl;
        }
    }
    return 0;
}
```

### 6.L1-006 连续因子 (20分-18分)

一个正整数 *N* 的因子中可能存在若干连续的数字。例如 630 可以分解为 3×5×6×7，其中 5、6、7 就是 3 个连续的数字。给定任一正整数 *N*，要求编写程序求出最长连续因子的个数，并输出最小的连续因子序列。

**输入格式：**

输入在一行中给出一个正整数 *N*（1<*N*<231）。

**输出格式：**

首先在第 1 行输出最长连续因子的个数；然后在第 2 行中按 `因子1*因子2*……*因子k` 的格式输出最小的连续因子序列，其中因子按递增顺序输出，1 不算在内。

**输入样例：**

```in
630
```

**输出样例：**

```out
3
5*6*7
```

**代码：**

```c++
#include <iostream>
#include <vector>
#include <cmath>
using namespace std;

int main()
{
    long long n;
    cin>>n;
    int x=0;
    vector<long long> sushu;
    for(long long i=2;i<double(sqrt(n));i++)
    {
        if(n%i==0)
        {
            sushu.push_back(i);
            x++;
        }
    }
    int max=0,maxz=0;
    int mz=0,w;
    for(int i=0;i<x;i++)
    {
        mz=0;
        w=i;
        while(sushu[i]==sushu[i+1]-1)
        {
            mz++;
            i++;
        }
        if(max<mz)
        {
            max=mz;
            maxz=w;
        }
    }
    if(x==0)
    {
        cout<<1<<endl<<n<<endl;
        return 0;
    }

    cout<<max+1<<endl;
    for(int i=0;i<max;i++)
    {
        cout<<sushu[maxz+i]<<'*';
    }
    cout<<sushu[maxz+max];

    return 0;
}
```

![截屏2021-04-08 下午1.51.50](/Users/suneann/Library/Application Support/typora-user-images/截屏2021-04-08 下午1.51.50.png)

​	在修改了几次无果之后，于是我找了一个[满分的答案](ttps://blog.csdn.net/liangzhaoyang1/article/details/51204989)（上边），基于我对题目的理解这一标准，我的答案（下边）比较正确一些（X异常自信的自我肯定）。

<img src="https://i.loli.net/2021/04/08/qzUM1lg2TtDrfLm.png" alt="截屏2021-04-08 下午1.54.58"  />

![](https://i.loli.net/2021/04/08/HlogQVzO457Kv3n.png)

过了，这题我读不明白。

### 7.L1-007 念数字 (10 分)

输入一个整数，输出每个数字对应的拼音。当整数为负数时，先输出`fu`字。十个数字对应的拼音如下：

```
0: ling
1: yi
2: er
3: san
4: si
5: wu
6: liu
7: qi
8: ba
9: jiu
```

**输入格式：**

输入在一行中给出一个整数，如：`1234`。

**提示：整数包括负数、零和正数。**

**输出格式：**

在一行中输出这个整数对应的拼音，每个数字的拼音之间用空格分开，行末没有最后的空格。如 `yi er san si`。

**输入样例：**

```in
-600
```

**输出样例：**

```out
fu liu ling ling
```

**代码：**

```c++
#include <iostream>
#include <map>
using namespace std;
int main()
{
    map<char,string> readnum;
    
    readnum.insert(make_pair('-', "fu"));
    readnum.insert(make_pair('0', "ling"));
    readnum.insert(make_pair('1', "yi"));
    readnum.insert(make_pair('2', "er"));
    readnum.insert(make_pair('3', "san"));
    readnum.insert(make_pair('4', "si"));
    readnum.insert(make_pair('5', "wu"));
    readnum.insert(make_pair('6', "liu"));
    readnum.insert(make_pair('7', "qi"));
    readnum.insert(make_pair('8', "ba"));
    readnum.insert(make_pair('9', "jiu"));
    
    string w;
    cin>>w;
    for(int i=0;i<w.length();i++)
    {
        if(i!=w.length()-1)
            cout<<readnum[w[i]]<<" ";
        else
            cout<<readnum[w[i]]<<endl;
    }
}
```

### 8. L1-008 求整数段和 (10 分)

给定两个整数*A*和*B*，输出从*A*到*B*的所有整数以及这些数的和。

**输入格式：**

输入在一行中给出2个整数*A*和*B*，其中−100≤*A*≤*B*≤100，其间以空格分隔。

**输出格式：**

首先顺序输出从*A*到*B*的所有整数，每5个数字占一行，每个数字占5个字符宽度，向右对齐。最后在一行中按`Sum = X`的格式输出全部数字的和`X`。

**输入样例：**

```in
-3 8
```

**输出样例：**

```out
   -3   -2   -1    0    1
    2    3    4    5    6
    7    8
Sum = 30
```

**代码：**

```c++
#include <iostream>
#include <cstdio>
using namespace std;
int main()
{
    int a,b;
    cin>>a>>b;
    int z=0,sum=0;
    
    for(int i=a;i<=b;i++)
    {
        printf("%5d",i);
        sum+=i;
        z++;
        if(z%5==0&&z!=b-a+1)
            cout<<endl;
    }
    cout<<endl<<"Sum = "<<sum;
    return 0;
}
```

### 9.L1-009 N个数求和 (20 分)

本题的要求很简单，就是求`N`个数字的和。麻烦的是，这些数字是以有理数`分子/分母`的形式给出的，你输出的和也必须是有理数的形式。

**输入格式：**

输入第一行给出一个正整数`N`（≤100）。随后一行按格式`a1/b1 a2/b2 ...`给出`N`个有理数。题目保证所有分子和分母都在长整型范围内。另外，负数的符号一定出现在分子前面。

**输出格式：**

输出上述数字和的最简形式 —— 即将结果写成`整数部分 分数部分`，其中分数部分写成`分子/分母`，要求分子小于分母，且它们没有公因子。如果结果的整数部分为0，则只输出分数部分。

**输入样例1：**

```in
5
2/5 4/15 1/30 -2/60 8/3
```

**输出样例1：**

```out
3 1/3
```

**输入样例2：**

```
2
4/3 2/3
```

**输出样例2：**

```
2
```

**输入样例3：**

```
3
1/3 -1/6 1/8

3
-1/3 -5/6 -1/8
```

**输出样例3：**

```
7/24
```

**代码：**

* 辗转相除法求最大公约数和最小公倍数

```c++
int gcd(int a,int b)
{
    int r;
    while(b!=0)
    {
        r=a%b;
        a=b;
        b=r;
    }
    return a;
}
int lcd(int a,int b)
{
    return a*b/gcd(a,b);
}
```

* 完整代码

```c++
#include <stdio.h>
#include <iostream>
#include <string.h>
#include <cstdio>
#include <cmath>
using namespace std;
long int gcd(long int a,long int b)
{
    long int r;
    while(b!=0)
    {
        r=a%b;
        a=b;
        b=r;
    }
    return a;
}
long int lcd(long int a,long int b)
{
    return a*b/gcd(a,b);
}

int main()
{
    
    long int n,a,b;
    long int z[200];
    long int m[200];
    
    cin>>n;
    for(int i=0;i<n;i++)
    {
        scanf("%ld/%ld",&a,&b);
        z[i]=a;
        m[i]=b;
    }
    
    long int g=m[0];
    for(int i=0;i<n-1;i++)
    {
        g=lcd(g,m[i+1]);
    }
    
    long int zz,add_result=0;
    for(int i=0;i<n;i++)
    {
        zz=g/m[i];
        z[i]*=zz;
        add_result=add_result+z[i];
    }
    bool fuhao=true;
    if(add_result<0)
    {
        fuhao=false;
        add_result=-add_result;
    }
    if(g==0)
        return 0;
    if(add_result==0)
    {
        cout<<0<<endl;
        return 0;
    }
    
    if(add_result%g==0&&g<add_result)
    {
        if(fuhao)
            cout<<add_result/g<<endl;
        else
            cout<<-add_result/g<<endl;
        return 0;
    }
    
    if(g<add_result)
    {
        long int f=add_result/g;
        
        add_result=add_result-(f*g);
        long int z=gcd(add_result, g);
        if(!fuhao)
        {
            f=-f;
        }
        if(fuhao)
            cout<<f<<" "<<add_result/z<<"/"<<g/z<<endl;
        else cout<<f<<" -"<<add_result/z<<"/"<<g/z<<endl;
        return 0;
    }

    if(add_result<g)
    {
        long int f=gcd(g, add_result);
        if(fuhao)
            cout<<add_result/f<<"/"<<g/f<<endl;
        else cout<<"-"<<add_result/f<<"/"<<g/f<<endl;
    }

    return 0;
}
```

### 10.L1-010 比较大小 (10 分)

本题要求将输入的任意3个整数从小到大输出。

**输入格式:**

输入在一行中给出3个整数，其间以空格分隔。

**输出格式:**

在一行中将3个整数从小到大输出，其间以“->”相连。

**输入样例:**

```in
4 2 8
```

**输出样例:**

```out
2->4->8
```

**代码：**

```c++
#include <iostream>
#include <cstdio>
#include <vector>
using namespace std;
int main()
{
    int a,b,c;
    scanf("%d %d %d",&a,&b,&c);
    int Max;
    int Mid;
    int Min;
    Max=a>b?(a>c?a:c):(b>c?b:c);
    Min=a<b?(a<c?a:c):(b<c?b:c);
    Mid=(a+b+c)-(Max+Min);
    cout<<Min<<"->"<<Mid<<"->"<<Max<<endl;
    return 0;
}
```

### 11.L1-011 A-B (20 分)

本题要求你计算*A*−*B*。不过麻烦的是，*A*和*B*都是字符串 —— 即从字符串*A*中把字符串*B*所包含的字符全删掉，剩下的字符组成的就是字符串*A*−*B*。

**输入格式：**

输入在2行中先后给出字符串*A*和*B*。两字符串的长度都不超过104，并且保证每个字符串都是由可见的ASCII码和空白字符组成，最后以换行符结束。

**输出格式：**

在一行中打印出*A*−*B*的结果字符串。

**输入样例：**

```in
I love GPLT!  It's a fun game!
aeiou
```

**输出样例：**

```out
I lv GPLT!  It's  fn gm!
```

**代码：**

```c++
#include <iostream>
#include <string>
#include <vector>
#include <stdio.h>
using namespace std;

int main()
{
    string w;
    getline(cin,w);
    string sw;
    getline(cin,sw);
    vector<char> result;
    vector<char>::iterator iter;
    for(int i=0;i<w.length();i++)
    {
        bool p=true;
        for(int j=0;j<sw.length();j++)
            if(w[i]==sw[j])
                p=false;
        if(p)
            result.push_back(w[i]);
    }
    for(iter=result.begin();iter!=result.end();iter++)
    {
        cout<<*iter;
    }
    return 0;
}
```

### 12.L1-012 计算指数 (5 分)

真的没骗你，这道才是简单题 —— 对任意给定的不超过10的正整数*n*，要求你输出2*n*。不难吧？

**输入格式：**

输入在一行中给出一个不超过10的正整数*n*。

**输出格式：**

在一行中按照格式 `2^n = 计算结果` 输出2*n*的值。

**输入样例：**

```in
5
```

**输出样例：**

```out
2^5 = 32
```

**代码：**

```c++
#include <iostream>
#include <cmath>
using namespace std;
int main()
{
    int n;
    cin>>n;
    if(n==0)
    {
        cout<<"2^"<<n<<" = "<<1;
        return 0;
    }
    int s=1;
    for(int i=0;i<n;i++)
    {
        s*=2;
    }
    cout<<"2^"<<n<<" = "<<s;
    
    return 0;
}
```

### 13.L1-013 计算阶乘和 (10 分)

对于给定的正整数*N*，需要你计算 *S*=1!+2!+3!+...+*N*!。

**输入格式：**

输入在一行中给出一个不超过10的正整数*N*。

**输出格式：**

在一行中输出*S*的值。

**输入样例：**

```in
3
```

**输出样例：**

```out
9
```

**代码：**

```c++
#include <iostream>
using namespace std;
int main()
{
    int n;
    cin>>n;
    if(n==0)
    {
        cout<<0<<endl;
        return 0;
    }
    int r=1,s=0;
    for(int i=1;i<=n;i++)
    {
        r*=i;
        s+=r;
    }
    cout<<s<<endl;
    return 0;
}
```



### 14.L1-014 简单题 (5 分)

这次真的没骗你 —— 这道超级简单的题目没有任何输入。

你只需要在一行中输出事实：`This is a simple problem.` 就可以了。

**代码：**

```c++
#include <iostream>
using namespace std;
int main()
{
    cout<<"This is a simple problem."<<endl;
    return 0;
}
```

### 15.L1-015 跟奥巴马一起画方块 (15 分)

美国总统奥巴马不仅呼吁所有人都学习编程，甚至以身作则编写代码，成为美国历史上首位编写计算机代码的总统。2014年底，为庆祝“计算机科学教育周”正式启动，奥巴马编写了很简单的计算机代码：在屏幕上画一个正方形。现在你也跟他一起画吧！

**输入格式：**

输入在一行中给出正方形边长*N*（3≤*N*≤21）和组成正方形边的某种字符`C`，间隔一个空格。

**输出格式：**

输出由给定字符`C`画出的正方形。但是注意到行间距比列间距大，所以为了让结果看上去更像正方形，我们输出的行数实际上是列数的50%（四舍五入取整）。

**输入样例：**

```in
10 a
```

**输出样例：**

```out
aaaaaaaaaa
aaaaaaaaaa
aaaaaaaaaa
aaaaaaaaaa
aaaaaaaaaa
```

**代码：**

```c++
#include <iostream>
#include <cmath>
using namespace std;
int main()
{
    char c;
    float n;
    cin>>n>>c;
    
    for(int i=0;i<ceil(n/2);i++)
    {
        for(int  j=0;j<n-1;j++)
        {
            cout<<c;
        }
        cout<<c<<endl;
    }
    return 0;
}
```

### 16.L1-016 查验身份证 (15 分)

一个合法的身份证号码由17位地区、日期编号和顺序编号加1位校验码组成。校验码的计算规则如下：

首先对前17位数字加权求和，权重分配为：{7，9，10，5，8，4，2，1，6，3，7，9，10，5，8，4，2}；然后将计算的和对11取模得到值`Z`；最后按照以下关系对应`Z`值与校验码`M`的值：

```
Z：0 1 2 3 4 5 6 7 8 9 10
M：1 0 X 9 8 7 6 5 4 3 2
```

现在给定一些身份证号码，请你验证校验码的有效性，并输出有问题的号码。

**输入格式：**

输入第一行给出正整数*N*（≤100）是输入的身份证号码的个数。随后*N*行，每行给出1个18位身份证号码。

**输出格式：**

按照输入的顺序每行输出1个有问题的身份证号码。这里并不检验前17位是否合理，只检查前17位是否全为数字且最后1位校验码计算准确。如果所有号码都正常，则输出`All passed`。

**输入样例1：**

```in
4
320124198808240056
12010X198901011234
110108196711301866
37070419881216001X

4
320X219880824005X
12010X198901011234
110108196711301866
37070419881216001X
```

**输出样例1：**

```out
12010X198901011234
110108196711301866
37070419881216001X
```

**输入样例2：**

```
2
320124198808240056
110108196711301862
```

**输出样例2：**

```
All passed
```

**代码：**

```c++
#include<iostream>
#include<iomanip>
using namespace std;
int main()
{
    int a[17]= {7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2};
  	char b[11]= {'1','0','X','9','8','7','6','5','4','3','2'};
    int n,sum=0,error=0;
    string str;
    cin>>n;
    for(int i=0; i<n; i++)
    {
        cin>>str;
        for(int i=0; i<17; i++)
            sum=sum+(str[i]-'0')*a[i];
        sum=sum%11;
        if(b[sum]!=str[17])
        {
            error++;
            cout<<str<<endl;
        }
        sum=0;
    }
    if(error==0)
        cout<<"All passed"<<endl;
    return 0;
}
```

