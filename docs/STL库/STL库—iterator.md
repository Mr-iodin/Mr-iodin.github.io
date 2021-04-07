# STL库—iterator

### 1.STL库

​	STL库中，大体可以分为容器(顺序容器、关系容器)、迭代器、算法三大类。

​	iterator可以看作是STL容器的指针，可以更为方便地访问容器中的元素。

### 2.iterator的基本操作

##### 1.迭代器的声明

每个标准库容器都定义了一个名为iterator的成员，所以声明迭代器的时候要用
$$
容器名：：iterator\quad  变量名
$$
这种形式来定义迭代器，如：

```c++
vector<int>::iterator iter;
```

这句语句声明来一个名为iter的变量，它的数据类型是由`vector<int>`定义的`iterator`类型。

##### 2.begin和end操作

​	每种容器都定义了一对名为begin和end的函数，用于返回迭代器。如果容器中有元素的话，由begin返回指向第一个元素的迭代器。

```c++
vector<int>::iterator iter=ivec.begin();
```

​	上述语句把迭代器iter初始化为名为begin的vector操作的返回值。如果vector非空，初始化后，iter即指该元素为ivec[0]。

​	由end操作返回的一个指向vector的末端的元素的下一个迭代器。称为“超出末端迭代器”，表明它指向了一个不存在的元素。如果vector为空，begin返回的迭代器与end返回的迭代器相同。



##### 3.使用迭代器遍历容器

```c++
for(iter=容器.begin();iter!=容器.end();iter++)
{
  cout<<*iter<<'';
}
```

注：在关系容器（例如map）中，初始化iter为m.begin(),这时候如果输出*iter则会报错。因为此时map内部存储的是多个pair，此时的\*iter指向的将会是map里第一个pair。

`(*it).first` 会得到key，`(*it).second`会得到value。这等同于`it->first`和`it->second`。一般用`->`来访问关联容器中的元素。



##### 4.iterator其他操作

* iter+n :迭代器指向原来+n个位置元素；
* iter1==iter2 :如果两迭代器指向位置相同，返回true；
* iter1=iter2 ：将iter2指向的位置赋值给iter1；
* Iter1-iter2 ：返回iter1和iter2在容器内位置的差值；

##### 5.实例

iterater二分查找：

```c++
//
//  main.cpp
//  iterator
//
//  Created by suneann on 2021/4/3.
//
#include <iostream>
using namespace std;
#include <iterator>
#include <vector>

int main()
{
  vector <int> v;
  v.push_back(2);
  v.push_back(5);
  v.push_back(20);
  int temp = 0;
  cin>>temp;
  sort(v.begin(),v.end());//使用排列函数对容器vector中元素进行排序
  
  vector<int>::iterator beg=v.begin();
  vector<int>::iterator end=v.end();
  vector<int>::iterator mid=v.begin()+(end-beg)/2;
  
  while(mid!=end&&*mid!=temp)
  {
    if(temp<*mid)
      end=mid;
    else
      beg=mid+1;
      
    mid=beg+(end-beg)/2;
  }
  
  if(*mid==temp)
    cout<<"find"<<endl;
  else
    cout<<"not fins"<<endl;
  
  return 0;
}
```

