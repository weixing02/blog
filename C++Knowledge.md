#### 指针和引用的定义和性质区别

- 指针是一个变量，只不过这个变量存储的是一个地址，指向内存的一个存储单元；而引用跟原来的变量实质上是同一个东西，只不过是原变量的一个别名而已。
- 指针可以初始化为NULL，而引用则必须初始化；
- sizeof(引用)是指的被引用对象的大小；sizeof(指针)是指的指针的大小，通常为4；

#### 堆和栈的区别

- 栈一般是编译器来自动分配和释放的，用来存放参数和局部变量等，随着函数的结束自动被释放，并且栈的内存空间是连续的，向低地址遍历，可申请空间较小，当栈容量不足时栈溢出。
- 堆一般是程序员自己来控制内存的创建和释放的，用来存放全局或者静态变量，类似链表的方式来分配内存，所以可以申请的空间较大，而且比较自由。

#### malloc/free和new/delete的区别

- new自动计算需要分配的空间，而malloc需要手工计算字节数
- new是类型安全的，而malloc不是，比如：
  - int* p = new float[2]; // 编译时指出错误
  - int* p = malloc(2*sizeof(float)); // 编译时无法指出错误
- new operator 由两步构成，分别是 operator new 和 construct（new先调用malloc，再调用构造函数；delete先调用析构函数，再调用free）
- operator new对应于malloc，但operator new可以重载，可以自定义内存分配策略，甚至不做内存分配，甚至分配到非内存设备上。而malloc无能为力
- new将调用constructor，而malloc不能；delete将调用destructor，而free不能。
- malloc/free要库文件支持，new/delete则不要

#### 面向对象和面向过程的优缺点（C++/C的区别）

- 面向过程
　　- 优点：性能比面向对象高，因为类调用时需要实例化，开销比较大，比较消耗资源，比如单片机、嵌入式开发、Linux/Unix等一般采用面向过程开发，性能是最重要的因素。 
　　- 缺点：没有面向对象易维护、易复用、易扩展

- 面向对象
　　- 优点：易维护、易复用、易扩展，由于面向对象有封装、继承、多态性的特性，可以设计出低耦合的系统，使系统更加灵活、更加易于维护 
　　- 缺点：性能比面向过程低
  
#### struct和class的区别

- struct也可以实现继承、多态、包含成员函数；
- 最本质的一个区别就是默认的访问控制： 

  - 默认的继承访问权限：struct是public的，class是private的。

#### gcc的编译流程分为四个步骤，分别为：

- 预处理（Pre-Processing）
- 编译（Compiling）
- 汇编（Assembling）
- 链接（Linking）

#### define与const的区别

- 安全性
  - define是没有类型的，编译器只是把常量和名字联系起来，之后做替换，没有安全类型检查，可能会产生错误。
  - const要指定类型，有安全类型检查，存放在静态存储区中，比较安全。

- 内存空间
  - define会在每个用到的地方都拷贝一份进行替换，内存占用比较大。
  - const则只在静态存储区存放一个拷贝，内存占用小。
  
- 编译器处理方式：
  - define在预处理阶段就进行替换；
  - const在编译时确定；
  
- define可以定义一些简单的计算，而const不行；

  >C++中一般使用const而不使用define
  
#### C++中const和static的用法

- 


