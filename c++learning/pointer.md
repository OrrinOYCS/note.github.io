# 指针

- 指针就是指向`变量地址`的一个`变量`
- viod、int、double不重要

## 声明指针

- 举例： char* ptr = &var， 其中`char*` `(不是char *ptr, 是char* ptr)` 用来声明一个char也就是一个字节的指针， 用`&`问`var`变量的`内存地址`在哪里存入`ptr`中

## 解指针

- 指针存储了地址，要想返回`变量的值`要用到`解指针`，解指针： `*ptr` `这里*和ptr挨着`，用一个`*`访问地址背后变量的值

## 双指针、三指针

- 指针的指针`char** ptr2 = &ptr`