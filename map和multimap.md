# map和multimap#
##multimap##
```c++
template<class Key, class T, class Pred = less<Key>, class A = allocator<T>>
class multimap{
	...
	typedef pair<const Key, T> value_type;
	...
};
```