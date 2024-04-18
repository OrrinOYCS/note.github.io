# 构造函数
```cfgrlanguage
#include <iostream>
class Entity {
public:
    int X, Y;
    //构造函数与类同名，可带参数
    Entity(int x, int y) {
        X = x;
        Y = y;
    }

    void print() {
        std::cout << X << "," << Y <<std::endl;
    }
};


int main() {
    //有了构造函数，实例化的时候可以进行赋值
    Entity e(3, 4);
    e.print();
    std::cin.get();
}
```
## 默认构造函数删除
```cfgrlanguage
Entity() = delete;
```
# 析构函数
- 在调用函数结束的时候释放内存彻底销毁对象，避免内存泄露
- 名字和构造函数一样多个`~`<br>
如上边的函数的析构函数是`~Entity()`