# 顺序容器vector
- 可变长的动态数组
- 必须包含`#include<vector>`
- 支持随机访问迭代器
	- 根据下标随机访问某个元素时间为常数
	- 在尾部添加速度很快
	- 在中间插入慢
- 所有STL算法都能对vector使用
## vector的成员函数
### 构造函数初始化

|成员函数|作用|
|:-:|:-:|
|vector();|无参构造函数|
|vector(int n);|将容器初始化成有n个元素|
|vector(int n, const T& val);|假定元素类型是T，将容器初始化成有n个元素，每个元素都是val|
|vecotr(iterator first, iterator last);|将容器初始化为与别的容器上区间[first, last)一致的内容|
### 其他常用的成员函数

|成员函数|作用|
|:-:|:-:|
|void pop_back();|删除容器末尾的元素|
|void push_back(const T& val);|将val添加到容器末尾|
|int size();|返回容器中元素的个数|
|T& front();|返回容器中第一个元素的引用|
|T& back();|返回容器中最后一个元素的引用|
|void insert(iterator it,const T& val);|在it处插入元素val|
|T& at(int n);|返回容器中位于位置n的元素|

