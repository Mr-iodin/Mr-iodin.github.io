# sort自定义排序

### 1.基本概念

* 头文件：`#include <algorithm>`

* 算法复杂度：n*log2(n)

* 参数说明：
  $$
  sort(first,last,cmp)
  $$

  * first：为元素起始地址；
  * last：结束地址；
  * cmp：排序方法（默认为从小到大）；

### 2.自定义比较方法

##### 2.1 修改cmp函数

```c
bool cmp(int a,int b)
{
  return b<a;
}
//
sort(a,a+n,cmp);
```

系统默认当`a<b`时返回ture，也就是从小至大排序，可以通过修改cmp函数来实现从大至小排序。

##### 2.2 重载比较运算符

```c++
bool operator<(const Student &s1,const Student &s2)
{
  
  if(s1.age==s2.age)//如果年龄相同，按名字小到大排序
  {
    return s1.name<s2.name;
  }
  else return s1.age>s2.age;//若不相同，按年龄大到小排序
}
sort(a,a+n);
```

##### 2.3 声明比较类

```c++
struct cmp
{
  bool operator()(const Student &s1,const Student &s2)
  {
    if(s1.age==s2.age)
    {
      return s1.name<s2.name;
    }
    else return s1.age>s2.age;
  }
};
sort(a,a+n,cmp());
```



### 3.赛题

##### 3.1 日期问题

【题目】

> 小明正在整理一批历史文献。这些历史文献中出现了很多日期。小明知道这些日期都在1960年1月1日至2059年12月31日。令小明头疼的是，这些日期采用的格式非常不统一，有采用年/月/日的，有采用月/日/年的，还有采用日/月/年的。更加麻烦的是，年份也都省略了前两位，使得文献上的一个日期，存在很多可能的日期与其对应。
>
> 比如02/03/04，可能是2002年03月04日、2004年02月03日或2004年03月02日。
>
> 给出一个文献上的日期，你能帮助小明判断有哪些可能的日期对其对应吗？

**输入：**

```
一个日期，格式是"AA/BB/CC"。 (0 <= A, B, C <= 9)
```

**输出：**

```
输出若干个不相同的日期，每个日期一行，格式是"yyyy-MM-dd"。多个日期按从早到晚排列。
```



**样例输入**：

```
02/03/04
```

**样例输出**：

```
2002-03-04
2004-02-03
2004-03-02
```



【思路】

* 自定义date结构体；
* 对输入的三个数字按照年/月/日、月/日/年、日/月/年排序，再分别判断其合理性；
* 若合理存入数组中，最后去充按照要求排序输出；



【代码实现】

* 定义结构体并重载运算符< ;

```c
//定义结构体
struct data
{
  int year;
  int month;
  int day;
}x[100];

//重载<符号
bool operator<(const data& a,const data& b)
{
  if(b.year==a.year)
  {
    if(b.month==a.month)
    {
      return a.day<b.day;
    }
    return a.month<b.month;
  }
  return a.year<b.year
}
```

* 判断日期是否合理；

```c
int md[13]={0,31,28,31,30,31,30,31,31,30,31,30,31};
bool judge(data a)
{
  if(a.year<1960||a.year>2059)
  	return false;
  if<(a.month<=0||a.month>12)
    return false;
  if(a.year%400==0||(a.year%100!=0&&a.year%4==0))
    if(a.month==2)
      return a.day<=29||a.day>=1;
  return a.day>=1&&a.day<=md[a.month];
  else return a.day>=1&&a.day<=md[a.month];
}
```

* 日期合理则插入数组中；

```c
int cnt=0;
void myscanf(int a,int b,int c){
  date d;
  d.year=a;d.month=b;d.day=c;
  if(judge(d))
    x[cnt++]==d;
}
```

* 主函数

```c++
int main()
{
  int a,b,c;
  scanf("%d/%d/%d",&a,&b,&c);
  //年月日
  myscanf(1900+a,b,c);
  myscanf(2000+a,b,c);
  
  //月日年
  myscanf(1900+c,a,b);
  myscanf(2000+c,a,b);  
  
  //日月年
  myscanf(1900+c,b,a);
  myscanf(2000+c,b,a);   
  
  //对日期进行排序
  sort(x,x+cnt);
  
  for(int i=0;i<cnt;i++)
  {
    //去重
    if(x[i].year!=x[i-1].year||x[i].month!=x[i-1].month||x[i].day!=x[i-1].day)
      printf("%d-%02d-%02d\n",x[i].year,x[i].month,x[i].day);
  }
  return 0;
}
```

