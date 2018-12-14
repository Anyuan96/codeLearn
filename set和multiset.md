#set和mulitset#
- 内部元素有序排列，新元素插入的位置取决于它的值，查找速度快
- 除了各容器都有的函数，还支持以下成员函数

|成员函数|作用|
|:-:|:-:|
|find|查找等于某个值的元素(x<y和y<x同时不成立即为相等|
|lower_bound|查找某个下界|
|upper_bound|查找某个上界|
|equal_range|同时查找上界和下界|
|count|计算等于某个值的元素个数|
|insert|插入一个元素或一个区间|
## pair模板##
```c++
template<class _T1, class T2>
struct pair{
typedef _T1 first_type;
typedef _T2 second_type;
_T1 first;
_T2 second;
pair():first(),second(){}
pair(const _T1& __a, const _T2& __b):first(__a),second(__b){}
template<class _U1,class _U2>
pair(const pair<_U1,_U2>& __p):first(__p.first),second(__p.second){}
};
```

## multiset##
```c++
template<class Key, class Pred = less<Key>,
	class A = allocator<Key> >
class multiset{...};
```

- Pred类型的变量决定了multiset中的元素，在multiset运行的过程中，比较两个元素x,y的大小的做法，就是生成一个Pred类型的变量，假定为op，若表达式op(x,y)返回值为true,则x比y小。Pred的缺省类型是less<Key>。
### less模板的定义###
```
template<class T>
struct less:public binary_function<T,T,bool>
{bool operator()(const T& x, const T& y){return x<y;}const;};//less模板是靠<来比较大小的。
```

### multiset的成员函数###
|成员函数|作用|
|:-|:-|
|iterator find(const T& val)|在容器中查找值为val的元素，返回其迭代器。如果找不到，返回end()。|
|iterator insert(constT& val)|将val插入到容器中并返回其迭代器|
|void insert(iterator first, iterator last);|将区间[first,last)插入容器|
|int count(const T& val)|统计有多少个元素的值和val相等|
|iterator lower_bound(const T& val)|查找一个最大的位置it，使得[begin(),it)中的所有元素都比val小|
|iterator upper_bound(const T& val)|查找一个最小的位置it，使得[it,end())中所有的元素都比val大|
|pair<iterator,iterator> equal_range(const T& val);|同时求得lower_bound和upper_bound|
|iterator erase(iterator it);|删除it指向的元素，返回其后面元素的迭代器|
### multiset的用法###

	```c++
	#include<set>
	using namespace std;
	class A{};
	int main(){
		multiset<A> a;
		a.insert(A());//error: multiset<A> a等价于multiset<A,less<A>> a; 插入元素时，multiset会将被插入元素和已有的元素进行比较。由于less模板是用<进行比较的，所以，这都要求A的对象能用<比较，即适当重载了<，而class A中并没有重载operator<;
	}
	//可以编译通过的例子
	#include<iostream>
	#include<set>
	using namespace std;
	template<class T>
	void Print(T first, T last){
		for(;first!=last;++first)
			cout<<*first<<" ";
		cout<<endl;
	}
	class A{
	private:
		int n;
	public:
		A(int n_):n(n_){}
		friend bool operator<(const A& a1, const A& a2){return a1.n < a2.n;}
		friend ostream& operator<<(ostream& o, const A& a2){o<<a2.n;return o;}
		friend class MyLess;
	};
	struct MyLess{
		bool operator()(const A& a1, const A& a2)
		{return (a1.n%10)<(a2.n%10);}
	};
	typedef multiset<A> MSET1;
	typedef multiset<A,MyLess> MSET2;
	int main(){
		const int SIZE = 6;
		A a[SIZE] = {4,22,19,8,33,40};
		MSET1 m1;
		m1.insert(a,a+SIZE);
		m1.insert(22);
		cout<<"1)"<<m1.count(22)<<endl;// 1) 2
		cout<<"2)"；Print(m1.begin(),m1.end());// 2) 4 8 19 22 22 33 40;
		MSET1::iterator pp = m1.find(19);
		if(pp != m1.end())
			cout<<"found"<<endl;// found
		cout<<"3)"<<*m1.lower_bound(22)<<","<<*m1.upper_bound(22)<<endl;//3) 22,33
		pp = m1.erase(m1.lower_bound(22),m1.upper_bound(22));
		cout<<"4)";Print(m1.begin(),m1.end());//4) 4 8 19 33 40
		cout<<"5)"<<*pp<<endl;// 5) 33
		MSET2 m2;
		m2.insert(a,a+SIZE);
		cout<<"6)";Print(m2.begin(),m2.end());//6)40 22 33 4 8 19
		return 0;
	}
	```
## set##
	```c++
	template<class Key, clss Pred = less<Key>, class A = allocator<Key>>
	class set{};
	```

插入set中已有的元素时，忽略插入

	```c++
	#include<iostream>
	#include<set>
	using namespace std;
	int main(){
		typedef set<int>::iterator IT;
		int a[5] = {3,4,6,1,2};
		set<int> st(a,a+5);
		pair<IT,bool> result;
		result = st.insert(5);
		if (result.second)
			cout<<*result.first<<"inserted"<<endl;
		if (st.insert(5).second)
			cout<<*result.first<<endl;
		else
			cout<<*result.first<<"already exits"<<endl;
		pair<IT,IT> bounds = st.equal_range(4);
		cout<<*bounds.first<<","<<*bounds.second;
		return 0;
	}
	```