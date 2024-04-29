# new 关键字
- new做了两件事
1. 分配内存
2. 调用构造函数

- `new 用delete a`,`new a[50] 用delete[] a`
- 如果有默认构造函数，可以直接省略括号`Entity* e = new Entity;`

> palcement new指定内存来源
先了解基本语法
```cfgrlanguage
int* b = new int[50];
Entity* e = new(b) Entity();
```