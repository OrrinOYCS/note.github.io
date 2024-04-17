# 在类和结构体之外的静态
- static 声明之后会变为private类型属性<br>
比如在两个文件都声明`int a = 5`,编译的时候会报错重复定义<br>
这个时候将其中一个改为`extern int a`,编译的时候这里会去外部寻找<br>
如果这时候将另一个`int a = 5`改为`static int a = 5`,会链接时候发现找不到
- 在实际使用过程中，我们如果想使用相同的变量但是不希望产生编译重复错误时，我们可以给里每个文件中的这个变量过着方法都用`static`修饰
# 类和结构体中的静态
- 用`static`修饰的变量意味着在类的多个实例中，这个变量只有**一个**实例,只要有一个实例对这个变量进行修改那么其他实例再次访问时候也会得到已经修改的值
- 在类和结构体中的静态方法不能引用到类实例，同时类实例也不能引用静态变量和方法
```cfgrlanguage
struct Entity{
    int x,y;
    void print(){
        std::cout << x << "," << y <<endl;
    }
};
int main(){
    Entity e;
    e.x = 1;
    e.y = 2;
    e.print();
    Entity e2;
    e2.x = 3;
    e2.y = 4;
    e2.print();
}
```
- 上边的代码会输出1，2，3，4因为全局变量
```cfgrlanguage
struct Entity{
    static int x,y;
    static void print(){
        std::cout << x << "," << y <<endl;
    }
};

//静态变量必须在外部初始化
int Entity::x;
int Entity::y;

int main(){
    Entity e;
    Entity::x = 1;
    Entity::y = 2
    Entity e2;
    Entity::x = 3;
    Entity::y = 4;
    Entity::print();
}
```
- 上边的代码输出的是3，4因为static独立于结构体和类存在，所有引用到的实例都能修改