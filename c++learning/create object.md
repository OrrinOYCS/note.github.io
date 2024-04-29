# 创建对象的两种方法

## 栈分配
- 生命周期和作用域相同，进行到作用域结束，自动销毁
```cfgrlanguage
void function(){
    Entity e;
}//离开作用域的时候被自动销毁
```
## 堆分配
- 生命周期不再受限制于作用域，生命周期由程序员显式控制
- new分配，delete释放（忘记释放可能会有内存泄漏）
```cfgrlanguage
void function(){
    Entity* e_ptr = new Entity();
    //用完要记得释放
    delete e_ptr;
}
```