# 字符串字面量
- 永远在内存只读区
```cfgrlanguage
const char* name = "Orrin";

```
## 使用literal进行字符串的append,用s链接就可以了
```cfgrlanguage
using namespace std::string_literals;
std::string name - "Orr"s + "hello";

```