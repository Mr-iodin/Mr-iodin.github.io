# STL库—iterator与vector

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

### 3.vector的基本操作

##### 1.vector简介

* vector是表示可变大小的数组的序列容器。vector采用连续存储空间来存储元素。可以用数组下标来访问vector元素；
* 刚开始vector会自动分配一段连续存储空间，在存储空间的元素超过了预配空间时，vector会重新配置空间，元素移动，释放旧内存空间，从而达到动态存储的效果；
* vector可以高效的访问元素、在末尾添加和删除元素。但vector对元素操作的复杂度上是根据到末尾距离成正比。

##### 2.声明与初始化

```c++
vector<int> ivec;	//声明一个int型的空向量
vector<int> ivec(5);	//声明一个大小为5的int向量
vector<int> ivec(10,1);	//声明一个大小为10，且值都为1的向量
vector<int> ivec(tmp);	//声明并且用tmp向量初始化ivec向量
vector<int> ivec(tmp.begin(),tmp.begin()+3);	//用向量tmp的第0个到第2个值初始化ivec

//注意点是，vector不能像数组一样用	{}来初始化
int arr[5]={1,2,3,4,5};
vector<int> ivec(arr,arr+5);//将数组arr元素用于初始化vec向量
//这里的初始化不包括arr[4]的元素，括号内的第二个变量表示地是ivec.end(),末尾迭代器都是指结束元素的下一个元素

vector<int> vec(&arr[2],&arr[4]);//将arr[2]~arr[4]范围内的元素作为vec的初始值。
vector<vector<int>> Array;//类似于二维数组
```



##### 3.vector的基本操作

* 末尾添加元素：vec.push_back();	//括号内的值为要添加的元素

* 尾部删除元素：vec.pop_back();

* 向量大小：vec.size();    //返回int值，向量内元素个数

* 向量判空：vec.empty();    //返回0或1

* 插入元素：vec.insert(pos,elem);    //在pos插入一个elem元素的拷贝，返回新数据的位置。

* vec.insert(pos, beg,end); //在pos位置插入[beg,end)区间的数据，无返回值；

* reserve(pos1,pos2); 将vector中的pos1～pos2元素逆序存储；

* vec.clear()；//清空vector

  注：如果要求多组输出的情况，一定要在输出后加上clear，否则原来的数据会保留在vector中。

##### 4.选用vector的情况

* 在需要使用数组的情况下，可以考虑用vector；

* 有丰富的操作（例如反转）；
* 无需考虑容器大小和数组越界之类的错位



##### 5.实例

【斐波拉切数列】

```c++
#include <iostream>
#include <vector>
using namespace std;
int main()
{
  vector <unsigned long long> v;
  unsigned int n;
  v.push_back(0);
  v.push_back(1);
  for(int i=2;i<50;i++)
  {
    v.push_back(v[i-1]+v[i-2]);
  }
  while(cin>>n)
  {
    cout<<v[n]<<endl;
  }
  return 0;
}
```

【判断是否存在回文串】

有些字符串是对称的，有些不是对称的，请将那些对称的字符串从小到大输出，字符串先以长度论大小，如果字符串相等，再以Ascll码值为排序标准；

* 输入描述：输入一个n，表示接下来有n组字符串，串长<=256;n<=1000;
* 输出描述：根据每个字符串，输出对称的那些串，并且要按从小到大的顺序输出；

```c++
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

using namespace std;

bool cmp(const string &s1,const string &s2)
{
    return s1.length()!=s2.length()?s1.length()<s2.length():s1<s2;
}
int main()
{
  int n;
  string w,t;
  cin>>n;
  vector<string> huiw1,v;
  
  for(int i=0;i<n;i++)
  {
      if(cin>>w)
        huiw1.push_back(w);
  }
  vector<string>::iterator iter;
  for (iter=huiw1.begin(); iter!=huiw1.end();iter++)
    {
      t=*iter;
      reverse(t.begin(),t.end());
      if(t==*iter)
      {
          v.push_back(*iter);
      }
  }
    sort(v.begin(),v.end(),cmp);
    for(iter=v.begin();iter!=v.end();iter++)
    {
        cout<<*iter<<endl;
    }
  return 0;
}

```



