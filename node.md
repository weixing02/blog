#### const和static的用法

- https://www.cnblogs.com/jiabei521/p/3335676.html

#### const和static在类中使用的注意事项

- static变量不能在类中初始化，需要在类外进行初始化：```数据类型 类名::变量名 = 值```
- const变量必须在类的初始化列表或者构造函数中初始化，因为变量属于对象，在对象创建的时候才进行初始化；
- const成员函数：const加在尾部，表示成员函数不会修改值，并且也不能调用其他的non-const成员函数；
- const int* p和int* const p：前者表示指针指向的值不能变，后者表示指针本身不能变；
- const对象的动态数组，要进行初始化；

![pic](https://images0.cnblogs.com/blog/460416/201310/06213505-b2b476ac85a34805a6696745b9ff3faa.png)

#### 类的大小计算

- 空类占一个字节
- 类的非虚函数不计算在内，无论是否是静态（即使有析构函数、构造函数、static静态成员函数、普通成员函数）
- 如果类中有虚函数，则需要有一个指针指向虚函数表，函数的开头就是这个指针，占4个字节（无论有多少个虚函数，只需要一个虚函数表，占4字节）
- 如果只有一个int、一个char，则是4+1=5，按4字节对齐就是8字节
- 子类的大小要加上父类的大小，子类和父类共享一个虚函数表
- 