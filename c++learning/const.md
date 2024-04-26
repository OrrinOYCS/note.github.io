# const关键字
- 三种使用情况
```cfgrlanguage
//将最大值定为const常量
const int MAX = 100;
//允许访问它
//不允许修改它
std::cout<<MAX<<std::endl;

//可以绕过const定义

//在堆上声明变量得到指针
int* a = new int;
//可做的事一：改变指针指向的内容
*a = 2;
//正常访问
std::cout<<*a<<std::endl;//2
//可做的事二：改变指针的值
//对const常量MAX做dereference
a = (int*)& MAX;
//(int*)是为了强制转换为int型指针，如果没有*会只被强制转换为int型数据
//&为了得到地址

std::cout<<*a<<std::endl;//100
```
> 使用情况1：不允许修改指针指向的内容，允许修改地址（放在指针*号之前）
> ```cfgrlanguage
> const int MAX = 100;
> //将指针添加const关键字声明不可修改指针指向的数据
> const int* a = new int;
>
> //改变指针指向的内容变得非法
> *a = 2;
>
> //访问指针指向的内容不受影响
> std::cout<<*a<<std::endl;//2
> //改变指针的地址是合法的
> a = (int*)& MAX;
> std::cout<<*a<<std::endl;//100
>```
> - 第一种使用情况中`const int* a = new int`等同于`int const* a = new int`

>使用情况2：不允许修改地址，允许修改地址指向的内容（放在指针*号之后）
> ```cfgrlanguage
>const int MAX = 100;
> //const声明不可修改指针地址
> int* const a = new int;
> //修改地址指向的内容是合法的
> > *a = 2;
> std::cout<<*a<<std::endl;//2
> //修改地址操作变成了非法
>  a = (int*)& MAX;
> //指针置空同样非法
> a = nullptr
> std::cout<<*a<<std::endl;//100
>``` 

>如果我们写`const int const* a = new int`两个const表示既不希望修改地址，也不希望修改地址指向的内容

>使用方法3：在class的方法中使用const
> getter、setter方法中多用在getter
> ```cfgrlanguage
> class Entity{
> private:
>   int x,y;
> public:
> //此处加入const修饰get方法强调只能做读取操作
>   int get_x() const{
>       //非法操作
>       x = 2;
>       //合法操作
>       return x;
>   }
>   void set_x(int x) {
>       //set方法本身就是要修改内容这里用const修饰没有意义
>       x = 3
>   }
> }
>```

```cfgrlanguage
 class Entity{
 private:
   int x,y;
 public:
   int get_x() const{
      return x;
     }
 }
 //在方法中传参的时候，我们不想复制函数所以使用引用（const Entity& e）
 //这意味着e是一个常量
 void printEntity(const Entity& e){
    //此时必须保证e调用到的方法不会涉及到修改内容，我们在get_x方法处有const做保证，否则报错
    std::cout<<e.get_x()<<std::endl;
 }
 int main(){
 Entity e;
 }
```
- 类似类和结构体一样，对编译产生不了什么实质性影响，是对代码进行了规范
- 承诺某些东西将是不变的
# mutable关键字
- 两种使用情况
>使用情况1：在const修饰的函数中使用
> ```cfgrlanguage
>   class Entity{
>   private:
>       std::string name;
>       //在这里用mutable修饰变量，可以让该变量被允许在const常量函数中调用是被允许修改修改
>       mutable int count = 0;
>   public:
>       //这个函数返回的是const string型的引用，这里用引用是让直接访问name位置，避免了不必要的数据复制
>       //第一个const 作用域函数的返回类型，表示返回的是一个常量引用
>       //第二个const 表明该函数整体是一个常量成员函数，不可修改调用对象状态（mutable对应的就是解决这个const的限制）
>       const std::string& getName() const{
>           //我们想让count变量在const修饰的函数中可以被修改，要将count定义时候用mutable修饰
>           count++;
>           return name;
>       }
>   }
>```

>使用情况2: lambda函数中使用
>```
>int x = 8;
>auto f = [=]() mutable{
>   x++;
>   std::cout<< x << std::endl;
>}
>>```

 