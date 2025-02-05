# ACM模式

```C++

#include<iostream>

#include<vector>


usingnamespacestd;

```

*` using namespace std;`

*`while (cin >> a >> b)`: 不断从标准输入中读取两个整数(`int a, b`)，直到输入流结束（通常通过输入文件结束符 `EOF`来结束输入，例如在Windows中可以通过 `Ctrl + Z`加回车，在Linux或MacOS中可以通过 `Ctrl + D`来发送 `EOF`）；如果输入成功，`cin`返回 cin 对象本身，在布尔上下文中被视为 `true`，如果输入失败，`cin`的返回值在布尔上下文中被视为 `false`

*`while(cin >> s)`: 不断从标准输入中读取字符串（`string s`)，直到输入流结束。在 `C++`中，`cin >> s`通过 `空格' '、制表符（TAB）（'\t'）或换行符('\n')`来判断输入是否结束。如果用户直接按下回车键（换行符），cin会认为没有有效输入，字符串s会保持为空字符串。
