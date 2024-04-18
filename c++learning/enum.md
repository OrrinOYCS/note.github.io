# 枚举类
- 可以跟冒号指定数据类型，底层是整数类型所以可以用int、char
- 如果光给了枚举类的变量名没有值默认从0开始增加
- 在成员变量初始化的时候为了将范围限定在枚举类中要将使用枚举类的类名
- 在函数中有枚举类，要使用枚举常量的时候如在`log`函数中有枚举类`level`，`level`中有枚举常量`high`<br>
那么在调用枚举常量`high`的时候只需要写**log::high**而不需要显式指明枚举类`level`
```cfgrlanguage
#include <iostream>

class Log {
//主动修饰为public
public:
    enum LogLevel : int
    {
        //默认递增，第一个默认从零开始
        levelError = 0, levelWarning, levelInfo
    };
private:
    //默认为warning级别
    //为了保证将数值限定在enum中所以将int类型改为LogLevel型
    LogLevel m_level = levelWarning;
    //②定义想到的public函数
public:
    void setLevel(LogLevel level) {
        //③这里需要一个私有成员变量接参数，去定义私有成员变量，用m_开头
        m_level = level;
    }
    void error(const char* message) {
        if (m_level >= levelError) 
            std::cout << "[error]: " << message << std::endl;
    }
    void warning(const char* message) {
        if (m_level >= levelWarning)
            std::cout << "[warning]: " << message << std::endl;
    }
    void info(const char* message) {
        if (m_level >= levelInfo)
            std::cout << "[info]: " << message << std::endl;
    }
};

int main()
{
    //①去main函数设计会有哪些功能
    Log log;
    log.setLevel(Log::levelInfo);
    log.error("hihihi");
    log.info("wowowo");
    log.info("sisisi");
    std::cin.get();
}


```