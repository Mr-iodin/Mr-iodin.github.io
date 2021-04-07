# STL库—map

### 1.map

**map简介：**

* map是STL库中的一个关联式容器，可以建立key(first)和value(second)一对一联系，由key映射到value；
* map内部自建了一颗红黑树，可以对数据进行自动排序，所以map里的数据都是有序的，这也是我们通过map来简化代码的原因；
* 使用map声明头文件：`#include <map>`

**map特点：**

* 自动建立`key-value`的对应关系，key和value可以是你需要的任何类型；
* 快速查找、删除记录，根据key值查找的复杂度很低；
* key和value一一对应关系可以去重；

### 2.map基本操作

* 构造map

```c++
map<int,string> map_student;
//定义了一个由int映射到string的map，并命名为map_student
```

这里的first和second的数据类型可以是任意数据类型，包括自定义数据类型。

* 向map中插入数据

  方法一：把map用数组方式插入数据

```c++
#include <map>
#include <iostream>
#include <string>

using namespace std;
int main()
{
  map<int,string> map_student;
  map_student[1]="student1";
  map_student[2]="student2";
  map_student[1]="student1_1";
  
  map<int,string>::iterator iter;
  for(iter=map_student.begin();iter!=map_student.end();iter++)
  {
    cout<<iter->first<<"\t"<<iter->second<<endl;
  }
  return 0;
}

/*
output:

1	student1_1
2	student2
Program ended with exit code: 0

*/

```

​	方法二：用insert()插入数据（两种方法等价）

​		(1)`insert(map<int,string>::value_type(1,"student1"));`

​		(2)`insert(make_pair(1,"student1"));`

​		与方法一不同的是，`insert()`函数体现了映射的一一对应这一特性，即当map中有这个key时，就不能用insert插入这个数据了，但用方法一是可以覆盖原数据的。

```c++
#include <iostream>
#include <map>
#include <string>
using namespace std;
int main()
{
  map<int,string>map_student;
  map_student.insert(map<int,string>::value_type(1,"student1"));
  map_student.insert(make_pair(1,"student2"));
  map_student.insert(make_pair(2,"student2"));
  map_student.insert(make_pair(3,"student3"));
  
  map<int,string>::iterator iter;
  for(iter=map_student.begin();iter!=map_student.end();iter++)
  {
    cout<<iter->first<<"\t"<<iter->second<<endl;
  }
  return 0;
}

/*
output:

1	student1
2	student2
3	student3
Program ended with exit code: 0
*/
```

### 3.map的基本操作函数

* `begin()`:返回指向map首部的迭代器；
* `end()`:返回指向map尾部的迭代器；
* `empty()`:如果map为空就返回true，反之返回false；
* `find(n)`:返回指向元素n的迭代器；
* `count()`:统计n的出现次数（0或1）；
* `size()`：返回map中元素个数；

##### 1.遍历map

* 使用`begin()`和`end()`

```c++
include <iostream>
#include <map>
#include <string>
using namespace std;
int main()
{
  map<int,string>map_student;
  map_student.insert(map<int,string>::value_type(1,"student1"));
  map_student.insert(make_pair(1,"student2"));
  map_student.insert(make_pair(2,"student2"));
  map_student.insert(make_pair(3,"student3"));
  
  map<int,string>::iterator iter;
  for(iter=map_student.begin();iter!=map_student.end();iter++)
  {
    cout<<iter->first<<"\t"<<iter->second<<endl;
  }
  return 0;
}
```

* 使用类似于数组的方法

```c++
#include <iostream>
#include <map>
#include <string>
using namespace std;
int main()
{
  map<int,string>map_student;
  map_student.insert(map<int,string>::value_type(1,"student1"));
  map_student.insert(make_pair(1,"student2"));
  map_student.insert(make_pair(2,"student2"));
  map_student.insert(make_pair(3,"student3"));
  
  for(int i=1;i<=map_student.size();i++)
   //map_student是从0开始的
  {
    cout<<i<<"\t"<<map_student[i]<<endl;
  }
  return 0;
}
```

##### 2.find()查找

```c++
#include <iostream>
#include <map>

using namespace std;
int main()
{
  map<char,int> my_map;
  map<char,int>::iterator iter;

  my_map['a']=50;
  my_map['b']=100;
  my_map['c']=150;
  my_map['d']=200;
  
  cout<<'a'<<"\t"<<my_map.find('a')->second<<endl;
  cout<<'b'<<"\t"<<my_map.find('b')->second<<endl;
  cout<<'c'<<"\t"<<my_map.find('c')->second<<endl;
  cout<<'d'<<"\t"<<my_map.find('d')->second<<endl;
  cout<<'e'<<"\t"<<my_map.find('e')->second<<endl;
  cout<<"end"<<"\t"<<my_map.end()->second<<endl;
  return 0;
}

/*
output:

a	50
b	100
c	150
d	200
e	1746820297
end	1746820297

*/
```

用`find函数`来定位数据出现位置它返回的一个迭代器；

当数据出现时，它返回数据所在位置的迭代器；

如果map中没有要查找的数据，它返回的迭代器等于`end()`函数返回的迭代器；

##### 3.count()判断数据是否存在

```c++
#include <iostream>
#include <map>
using namespace std;

int main()
{
  map<int,string> map_student;
  map_student[1]="student1";
  map_student[2]="student2";
  map_student[1]="student3";
  
  if(map_student.find(4)==map_student.end())
    cout<<"没有4这个数据"<<endl;
  
  map_student.insert(make_pair(4,"student4"));
  
  if(map_student.find(4)==map_student.end())
    cout<<"没有4这个数据"<<endl;
  else
    cout<<4<<"\t"<<map_student[4]<<endl;
  
  return 0;
}
/*
output:

没有4这个数据
4	student4
Program ended with exit code: 0

*/
```

`count()`方法返回值是一个整数，1表示有这个元素，0表示没有这个元素。但无法定位数据的具体位置。

### 4.map在题目中的应用

* 去重；

* 排序；

* 计数；

  

##### 1.去重

​	利用映射一一对应性，把可能出现的重复数据设置为key值以 达到去重的目的。

##### 2.排序(按照key排序问题)

​	map是STL的一个模版类，以下是map定义：

```c++
template <class Key,class T,class Compare = less<Key>,class Allocator=allocator<pair<const Key,T>>> class map;
```

​	其实map<>里应该有三个变量，而第三个变量是排序方式，如果我们不指定排序方式的话，按照平时的写法，map就会按照模版中的less\<Key>进行排序。

**自定义Compare类：**

​	我们可以自定义一个Compare类，把这个类按照map模版，加在本该Compare类的位置上，就可以自定义key的排序方式了。

​	比如我建了一个学生-成绩map，原先是按照学生名字字典排序的。如果像按照降序、名字长度排序该如何实现呢？

* 默认cmp输出：

```c++
#include <iostream>
#include <map>
using namespace std;

int main()
{
  map<string,int>map_student;
  map<string,int>::iterator iter;
  
  map_student.insert(make_pair("ccc",100));
  map_student.insert(make_pair("bb",60));
  map_student.insert(make_pair("aaa",99));
  
  for(iter=map_student.begin();iter!=map_student.end();iter++)
  {
    cout<<iter->first<<"\t"<<iter->second<<endl;
  }
  return 0;
}
/*
output:
aaa	99
bb	60
ccc	100
*/
```

* 降序输出

```c++
#include <iostream>
#include <map>
using namespace std;

int main()
{
  map<string,int,greater<string>>map_student;//加上greater<string>
  map<string,int>::iterator iter;
  
  map_student.insert(make_pair("ccc",100));
  map_student.insert(make_pair("bb",60));
  map_student.insert(make_pair("aaa",99));
  
  for(iter=map_student.begin();iter!=map_student.end();iter++)
  {
    cout<<iter->first<<"\t"<<iter->second<<endl;
  }
  return 0;
}

/*

output:
ccc	100
bb	60
aaa	99

*/
```

* 自定义cmp按照长度升序输出

```c++
#include <iostream>
#include <map>
using namespace std;

class cmp
{
public:
    bool operator()(string a,string b) const
      //注意加const
      {
        return a.length()<=b.length();
      //注意加=，不然输出与预期不符
      };
};

int main()
{
  map<string,int,cmp>map_student;
  map<string,int>::iterator iter;

  map_student.insert(make_pair("ccc",100));
  map_student.insert(make_pair("bb",60));
  map_student.insert(make_pair("aaa",99));

  for(iter=map_student.begin();iter!=map_student.end();iter++)
  {
    cout<<iter->first<<"\t"<<iter->second<<endl;
  }
  return 0;
}

/*
output:
bb	60
aaa	99
ccc	100
*/
```

##### 3.计数

* 假设定义一个map\<string,int>map,输入数据s，计为first，map[s]++;



### 5.适用于map的题型

* 去重计数类题型；
* 可以打乱重新排列的问题；
* 有清晰的一对一关系；

### 6.实例

【密文搜索】

福尔摩斯从X星收到一份资料，全部是小写字母组成。
他的助手提供了另一份资料：许多长度为8的密码列表。
福尔摩斯发现，这些密码是被打乱后隐藏在先前那份资料中的。
请你编写一个程序，从第一份资料中搜索可能隐藏密码的位置。要考虑密码的所有排列可能性。
**数据格式：**
输入第一行：一个字符串s，全部由小写字母组成，长度小于1024*1024；
紧接着一行是一个整数n,表示以下有n行密码，1<=n<=1000
紧接着是n行字符串，都是小写字母组成，长度都为8
**要求输出：**
一个整数, 表示每行密码的所有排列在s中匹配次数的总和。

**样例输入：**

```
aaaabbbbaabbcccc
2
aaaabbbb
abcabccc
```

**样例输出：**

```
4
```

这是因为：第一个密码匹配了3次，第二个密码匹配了1次，一共4次。

**代码：**

自我感觉逻辑上没问题（反正跑样例没问题

```c++
#include <iostream>
#include <map>
#include <string.h>
#define Max 10001
using namespace std;

struct {
    char subw[10];
    map<char,int> char_num;
}count_num[Max];

int main(){

    string w;
    cin>>w;
    int n;
    int j;
    for(j=0;j<w.length()-8+1;j++)
    {
        w.copy(count_num[j].subw,8,j);
    }
    
    for(int i=0;i<j;i++)
    {
        for(int k=0;k<8;k++)
        {
            char a=count_num[i].subw[k];
            if(count_num[i].char_num.find(a)->first)
            {
                count_num[i].char_num[a]++;
            }
            else count_num[i].char_num.insert(make_pair(a,1));
        }
    }

    cin>>n;
    
    int result=0;
    map<char,int> ::iterator iter;
    for(int i=0;i<n;i++)
    {
        map<char,int> sub_cum;
        string subw1;
        cin>>subw1;
        for(int k=0;k<8;k++)
        {
            char a=subw1[k];
            if(sub_cum.find(a)->first)
            {
                sub_cum[a]++;
            }
            else sub_cum.insert(make_pair(a,1));
        }
        
        for(int s=0;s<j;s++)
        {
            bool p=true;
            for(iter=sub_cum.begin();iter!=sub_cum.end();iter++)
            {
                if(iter->second!=count_num[s].char_num[iter->first])
                    p=false;
            }
            if(p)
                result++;
        }
        sub_cum.clear();
    }
    
    cout<<result<<endl;
    return 0;
}
```

