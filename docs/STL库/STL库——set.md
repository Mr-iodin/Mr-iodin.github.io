# STL库——SET容器

### 1.SET介绍

* set容器，是一种实现了平衡二叉树的数据结构，容器中的数据不能重复，即每个数据都是唯一的，并且会对存进去的数据进行自动排序；
* 构造set集合的主要目的是为了快速检索、去重与排序，使用set前，需要在程序头文件中包含声明`#include <set>`；

### 2.SET常用函数

* `insert()` ——插入元素；
* `erase()`——删除元素；
* `find()`——返回一个指向被查找元素的迭代器；
* `begin()`——返回指向第一个元素的迭代器；
* `end()`——返回指向最后一个元素的迭代器；
* `claer()`——清除所有元素；
* `size()`——集合中元素的数目；
* `swap()`——交换两个集合变量；
* `empty()`——如果集合为空，返回true；
* `rbegin()`——返回指向集合中最后一个元素的反向迭代器；
* `rend()`——返回指向集合中最后一个元素的反向迭代器；
* `count()`——返回某个值元素的个数；

### 3.SET容器的基本操作

* 创建对象

  ```c++
  set<类型> 对象名;	//如：set<int> a
  
  set<类型,比较结构体> 对象名;	//如：set<int,myComp> a;
  
  set<const set&>;	//通过拷贝构造函数创建对象
  //如 set<int> a1;	set<int> a2(a1);
  
  set<first,last>;	//用迭代器区间[first,last)所指元素，创建一个set对象
  //如 int a[]={1,2,3,4,5};	set<int> s(a,a+5);
  ```

  

* 添加元素

  * `insert(key_value)`:将某一个键值插入到set中，返回值是`pair<set<int>::iterator,bool>`,`bool`标志着插入是否成功，而`iterator`代表插入的位置，若该键值已经在set中，则`iterator`表示已存在在该键值在`set`中的位置。

    ```c++
    set<int> a;
    a.insert(1);
    a.insert(2);
    a.insert(2);//重复的元素不会被插入
    ```

    

  * `insert(first,last)`:

    ```c++
    int a[]={1,2,3};
    set<int> s;
    s.insert(a,a+3);
    ```

* 删除元素

  * `erase(kry_value)`:删除键值key_value的值；

    ```c++
    a.erase(1);
    ```

  * `erase(iterator)`:删除迭代器iterator指向的值；

    ```c++
    a.erase(a.begin());//删除a的第一个元素
    ```

  * `erase(first,second)`:删除迭代器[first,second)之间的值；

    ```c++
    a.erase(a.begin(),a.end());
    ```

  * `a.clear()`:删除a中所有元素；

  ​    set中的erase()操作上不进行任何错误检查的，比如定位器的是否合法等，所以用的时候自己一定要注意。

* 遍历访问

  * 顺序遍历：

    ```c++
    set<int> a;
    set<int>::iterator it=a.begin();
    for(;it!=a.end();it++)
      cout<<*it<<endl;
    ```

  * 反序遍历

    ```c++
    set<int> a;
    set<int>::reverse_iterator rit=a.rbegin();
    for(;rit!=a.rend();rit++)
      cout<<*rit<<endl;
    ```

    关联容器的迭代器不支持`it+n`操作，仅支持`it++`操作；

* 查找元素

  `find(key_value)`:如果找到查找的键值，则返回该键值的迭代器的位置。否则返回集合最后一个元素后一个位置的迭代器，即`end()`;

  ```c++
  int b[]={1,2,3,4,5};
  set<int> a(b,b+5);
  set<int>::iterator it;
  it=a.find(3);
  if(it!=a.end()) cout<<*it<<endl;
  else cout<<"该元素不存在"<<endl;
  it=a.find(10);
  if(it!=a.end()) cout<<*it<<endl;
  else cout<<"该元素不存在"<<endl;
  /*
  3
  该元素不存在
  */
  ```

### 4.自定义比较函数

​	set容器在判定已有元素a和新插入元素b是否相等时，是这么做的：

1. 将a作为左操作数，b作为右操作数，调用比较函数，并返回比较值；

2. 将b作为左操作数，a作为右操作数，再调用一次比较函数，并返回比较值；

   也就是说，假设有比较函数`f(x,y)`，要对已有的元素a和新插入的元素b进行比较时，会先对`f(a,b)`操作，再进行`f(b,a)`操作，然后返回两个`bool`值；

   * 若1、2两步返回都是false，则认为a、b是相等的，则b不会被插入set容器中；

   * 若1返回true而2返回false，则b要排在a的后面，反之则b要排在a的前面；

   * 如果1、2两步返回值都是true，则可能发生未知行为；

     

##### 4.1 自定义比较结构体

首先定义比较结构体

```c++
struct myComp
{
  bool operator()(const 类型 &a,const 类型 &b)//重载“()”操作符
  {
    ...;
    return ...;
  }
};
```

然后定义set

```c++
set<类型,myComp> s;
```

【例】自定义一个从大到小排序

```c++
#include <iostream>
#include <set>
#include <cstdio>
using namespace std;

struct myComp
{
    bool operator()(const int &a,const int &b)
  {
    if(a!=b)
      return a>b;
    else return false;
  }
};

int main()
{
  set<int,myComp> s;
  s.insert(1);
  s.insert(5);
  s.insert(4);
  s.insert(2);
  s.insert(1);
  set<int,myComp>::iterator it=s.begin();
  for(;it!=s.end();it++)
    cout<<*it<<' ';
  cout<<endl;
}
/*
5 4 2 1 
*/
```

##### 4.2 重载"<"操作符

首先在结构体中重载"<"操作符，自定义排序规则；

```c++
struct 结构体
{
  bool operator<(condt 结构体类型 &a)
  {
    ...;
    return (...);
  }
};
```

然后，定义set；

```c++
set<类型> s;
```

【例】对含有姓名、编号、成绩的结构体根据从小到大排序，同时根据编号去重。

```c++
#include <iostream>
#include <set>
#include <cstdio>
using namespace std;
struct Student
{
  string name;
  int num;
  double grade;
  bool operator<(const Student &a)const
  {
    if(a.num==num)
      return false;
    else return a.num>num;
  }
};

int main()
{
  set<Student> a;
  set<Student>::iterator it;
  Student stu;
  stu.name="John";stu.num=3256;stu.grade=85.5;
  a.insert(stu);
  stu.name="Tom";stu.num=1749;stu.grade=90.1;
  a.insert(stu);
  stu.name="BOb";stu.num=3256;stu.grade=60.4;
  a.insert(stu);
  for(it=a.begin();it!=a.end();it++)
    cout<<(*it).num<<" "<<(*it).name<<' '<<(*it).grade<<endl;
}
/*
1749 Tom 90.1
3256 John 85.5
*/
```



### 5.真题

【错误票据】

某涉密单位下发了某种票据。并要在年终所有收回。

每张票据有唯一的ID号。全年全部票据的ID号是连续的。但ID的開始数码是随机选定的。

由于工作人员疏忽。在录入ID号的时候发生了一处错误，造成了某个ID断号，另外一个ID重号。

你的任务是通过编程，找出断号的ID和重号的ID。

如果断号不可能发生在最大和最小号。

**输入格式**
要求程序首先输入一个整数N(N<100)表示后面数据行数。

接着读入N行数据。

每行数据长度不等。是用空格分开的若干个（不大于100个）正整数（不大于100000）。请注意行内和行末可能有多余的空格，你的程序须要能处理这些空格。

每一个整数代表一个ID号。

**输出格式**
要求程序输出1行。含两个整数m n，用空格分隔。

当中，m表示断号ID。n表示重号ID


**样例输入**

```
2
5 6 8 11 9
10 12 8
```

**样例输出**

```
7 9
```

【分析】

​	输入后排序，利用set判断是否重复缺失

**代码**

```c++
#include <iostream>
#include <set>
#include <cstdio>
#include <stdio.h>

using namespace std;

int main()
{
  set<int> a;
  int n;
  scanf("%d",&n);
  int m;
  int sec;
  int loc;//分别记录重复和缺失
  pair<set<int>::iterator,bool> pr;
  while(scanf("%d",&m)!=EOF)
  {
    pr=a.insert(m);
    if(!pr.second)
        sec=*pr.first;
  }
  set<int>::iterator it=a.begin();
  set<int>::iterator iter=it++;
  for(;it!=a.end();it++,iter++)
  {
    if(*(it)-(*iter)!=1)
    {
      loc=*(iter)+1;
      break;
    }
  }
  printf("%d %d",loc,sec);
  return 0;
}
```

[存在点问题]



