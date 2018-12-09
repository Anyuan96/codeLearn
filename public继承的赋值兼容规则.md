# public继承的赋值兼容规则
```c++
class base{};
class derived: public base{};
base b;
derived d;
```
- 派生类对象可以赋值给基类对象 `b = d;`
- 派生类对象可以初始化基类引用 `base& br = d;`
- 派生类对象的地址可以赋值给基类指针 `base* pd = & d;`
- **如果派生方式是private或protected，则上述三条不可行** 