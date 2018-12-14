# list和deque
## list容器
- 双向链表`#include<list>`
- 在任何位置插入/删除元素都是常数时间
- 不支持根据下标随机存取元素
- 具有所有顺序容器都有的成员函数
### 成员函数

|成员函数|作用|
|:-:|:-:|
|push_front|在链表最前面插入|
|pop_front|删除链表最前面的元素|
|sort|排序（list不支持STL算法的sort)|
|remove|删除和指定值相等的所有元素|
|unique|删除所有和前一个元素相同的元素(去重)|
|merge|合并两个链表，并清空被合并的链表|
|reverse|颠倒链表|
|void splice(iterator , T& sourceList, iterator first, iterator last)|在指定位置前面插入另一链表中的一个或多个元素，并在另一个链表中删除被插入的元素|

#### list容器的sort函数####
- list容器的迭代器不支持完全随机访问->不能用标准库中sort函数对它进行排序

-	```C++
	list<T> classname
	classname.sort(compare);//比较函数可以自己定义
	classname.sort();//无参版本，按<排序
	```

- list容器只能使用双向迭代器->不支持大于/小于比较运算符，[]运算符和随机移动（即类似“list::iterator + 2”的操作）
## deque
- 双向队列
- 必须包含头文件`#include<deque>
- 所有适用于vector的操作都适用于deque
- deque还有push_front,pop_front操作