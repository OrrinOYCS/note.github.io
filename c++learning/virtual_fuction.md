# 虚函数
- 为了实现继承后的多态
- 实现方法：在`基类`中要被重写的方法前加关键字`virtual`, 在`派生类`重写的函数后加关键字`override`
```cfgrlanguage
#include <iostream>
class Entity{
public:
    float x,y;
    virtual void Move{
        std::cout<<"moving"<<std::endl;
    }
};
class Player: public Entity{
    void Move() override{
        srd::cout<<"player moving"<<srd::endl;
    }
int main(){
    Entity* player = new Player();
    //输出player moving
    player->Move();
    
}
};
```
- 使用指针的时候用`->`指向成员方法，静态变量外部类变量使用`::`
# 纯虚函数
- 纯虚函数是特殊的虚函数
- 纯虚函数命名方法是在虚函数声明后加`=0`
```cfgrlanguage
 virtual void Move = 0;
```
- 纯虚函数强制要求派生类实现方法，否则无法调用