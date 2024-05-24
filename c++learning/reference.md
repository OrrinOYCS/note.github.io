# 引用

- 注意`引用声明`和`取地址符`的区别，不是一个东西<br>
引用声明：`int& ref`,&和int在一起和ref分开<br>
取地址符：`&ref`， &和ref在一起的

**和类型在一起的时候是引用，和变量在一起的时候是取地址**

- 引用不是真正意义上的变量，所以一旦声明要给它赋值<br>
比如 `int& ref = a` ,但是不可以写为`int& ref`

- 引用常在写函数时候用来减少拷贝开销，是一个语法糖
- 举例：
```cfgrlanguage
int main(){
    a = 5;
    add(a);
    return a;
}
#声明add函数的形参时候用到引用
add(int& value){
    value++
}
```
完全等同于
```cfgrlanguage
int main (){
    a = 5;
    #传a地址
    add(&a);
    return a;
}
#用指针修改数值,用指针接参
add(int* value){
    #解指针后进行自增
    (*value)++
}
```
但是用引用比第二种用指针少了地址传递以及解指针的麻烦