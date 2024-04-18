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