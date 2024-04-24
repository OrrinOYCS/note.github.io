# 字符串
```cfgrlanguage
//必须声明为const常量
const char* name = "Orrin";
//这样写不代表是像数组一样在堆上声明的
int* array = new int[5];
//string不能像array一样用delete删除释放
delete[] array;
//经验规则 ：没有new就没有delete
```
- `char* name`是一个指针，之所以能输出完字符串后正确结束是因为内存中有一个`\0`结束符
```cfgrlanguage
//声明固定长度string
cahr name2[5] = {'O','r','r','i','n'};会输出Orrin+乱码，因为不知道哪里结束
cahr name2[6] = {'O','r','r','i','n','\0'}，会正常输出Orrin
//"双引号是string， ‘单引号是char
```
## std::string
- 要导入`#include <string>`
```cfgrlanguage
//当我们将string只做引用而不去改变它的值时候，用const常量+&进行引用会节省创造副本的开销
void printstring(const std::string& Str){
    std::cout<<Str<<std::endl;
}
```