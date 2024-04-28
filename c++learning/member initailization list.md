# 成员初始化列表
- 只能在构造函数中使用
- 使用成员初始化列表少了一次默认构造函数过程，对于数据密集型类，效率是有提高的，多用成员初始化列表
- 数据成员初始化顺序和他被声明的顺序保持一致

- 四种必须使用成员初始化列表的情况
```cfgrlanguage
//情况1：类成员有const类型，此类型在被调用前必须先被赋值，用成员初始化列表正好解决问题
class Entity{
private: 
    const int a;
public:
    A(int a):a(10){}
}
```

```cfgrlanguage
//情况2：类成员有&引用类型，此类型也是需要在被调用前先被初始化，用成员初始化列表正好解决这个问题
class Entity{
private:
    int& b;
public:
    B(int& n): b(3){}
}
```

```cfgrlanguage
//情况3：类本身就是class或者struct，有有参数的构造函数，没有无参构造函数
class Base{
public:
    //父类函数没有无参默认构造函数，有一个带参数的构造函数
    Base(int a){
        int m_num=0;
    }
private:
    int m_num;
class BaseChild: public Base{
public:
    BaseChild(){
        m_num=0;
    }
private:
    int m_num;
}
int main(){
    BaseChild a;//编译报错
}
//原因是BaseChild继承Base的时候没有显示指定Base的构造函数，Base定义的时候没有默认构造函数
//使用成员初始化列表可以解决问题
//解决方法：
BaseChild:Base(1){

}
}

```

- 按顺序声明举例
```cfgrlanguage
class CMyClass {
    CMyClass(int x, int y);
    int m_x;
    int m_y;
};

CMyClass::CMyClass(int x, int y) : m_y(y), m_x(m_y)
{
};
```


```cfgrlanguage
//使用初始化列表之前初始化的方式
class Entity{
private:
    std::string m_name;
public:
    //默认构造函数
    Entity(){
        m_name = "unknow";
    }
    //带参构造函数
    Entity(const std::string& name){
        m_name = name;
    }
    //构建一个常量方法返回name
    const std::string& getName() const{
        return m_name;
    }
    int main (){
        Entity e0;
        std::cout<< e0.getName() <<std::endl;//unknow
        Entity e1("Orrin");
        std::cout<< e1.getName() << std::endl;//Orrin
    }
}
```

- 通过初始化列表实现时候:
```cfgrlanguage
class Entity{
private:
    //添加一个分数参数；
    int score;
    std::string m_name;
public:
    //默认构造函数(使用初始化成员列表)
    //此处发生变化
    //将初始化的成员变量按照 `声明` 顺序写
    Entity(): m_score(100),m_name("Orrin"){
    }
    //带参构造函数
    Entity(const std::string& name): m_name(name){
    }
    //构建一个常量方法返回name
    const std::string& getName() const{
        return m_name;
    }
    int main (){
        Entity e0;
        std::cout<< e0.getName() <<std::endl;//unknow
        Entity e1("Orrin");
        std::cout<< e1.getName() << std::endl;//Orrin
    }
}
```
- 成员初始化列表作用
- `代码风格角度`: 如果参数比较多的时候，将构造函数中大量的参数初始化拿出来，代码足够简洁，其他的一些function如init()一目了然，知道构造函数的行为
- `功能角度`： 如果不使用成员初始化列表会初始化两次