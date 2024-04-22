# 数组 
```cfgrlanguage
//数组初始化
//创建长度为5的int类型的名为example的数组
int example[5];
//在内存中是连续的数据存储，所以[]中是偏移量

std:: cout<<exmple[0]<<std::endl;
//会输出数组中的第一个元素

std:: cout<<exmple<<std::endl;
//这里的example整体被输出的时候是一个指针
//所以我们还可以写成
int* ptr = example
//声明一个指针将指针example赋值给ptr指针

```

## 当我们想在新建数组前就固定指定好数组长度

写成`const int size = 5`是不行的，成需要在编译之前就知道数组的长度
这时，我们用`static`关键字修饰即可解决问题
```cfgrlanguage
static const int size = 5;
int example[size];
```


## 新建数组两种不同方式的对比
```cfgrlanguage
//在栈上建立数组
int exmple[5];

//在堆上建立数组
int* another = new int[5]
```
- `栈`上建立在到达函数结尾花括号时被销毁，`堆`上建立在程序将它销毁前都是活跃的，活得更久
- `销毁数组`：`delete[] another`

## 为什么更多的使用堆上建立数组（new的方法）
1. 堆上建立的`生存期`更久
2. `间接寻址`

## c++11中的array

**std::array**
- 有了边界检查
- 有了直接的反映大小的size()。 ps：没有的时候通过sizeof（array）/（array类型长度）得到大小
- 更安全

**std::array**初始化
```cfgrlanguage
#include<array>
//std::array<类型，大小> 名称
std:: array<int,5> example

//访问大小
example.size();
```