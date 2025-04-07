# C/C++

## 内存操作

* C

1. `memcpy`
   * 用于在内存中复制数据
   * <string.h>    // C 语言标准库的头文件之一；该头文件提供了许多用于**操作内存和字符串的函数**。
   * 函数原型
   ```C
   /* dest: 目标内存地址
    * src: 源内存地址
    * n: 需要复制的字节数 */
   void *memcpy(void *dest, const void *src, size_t n);
   ```
   注：
   1. 确保目标内存有足够的空间来存储复制的数据
   2. 如果 `dest` 和 `src` 有重叠部分，`memcpy` 的行为是未定义的。**如果需要处理重叠内存区域的复制，应该使用 `memmove` 函数**。
2. `memmove`
   * 与 `memcpy` 功能类似，用于将 `src` 中的 `n` 个字节复制到 `dest` 中；区别是 `memmove` 允许源和目标内存有重叠部分
   * 函数原型
    ```C
    void *memmove(void *dest, const void *src, size_t n);
    ```
3. `memset`
    * 用于将目标内存 `S` 的前 `n` 个字节设置为指定的值 `c`（**`c` 会被转换为 `unsigned char`**）
    * 函数原型
    ```C
    void *memset(void *s, int c, size_t n);
    ```
4. `memcmp`
    * 用于比较两个内存区域 `S1` 和 `S2` 的前 `n` 个字节；返回值：如果 `S1` 和 `S2` 的前 `n` 个字节相等，返回 0；如果前者小于后者，返回负值；反之，返回正值
    * 函数原型
    ```C
    int memcmp(const void *s1, const void *s2, size_t n);
    ```
5. `memchr`
    * 用于在内存区域 `S` 的前 `n` 个字节中查找字符 `c`（**`c` 会被转换为 `unsigned char`**）；返回值：如果找到字符 `c`，返回该字符的指针，否则返回 `NULL`
    * 函数原型
    ```C
    void *memchr(const void *s, int c, size_t n);
    ```
6. `malloc`
    * 用于动态分配一块大小为 `size` 字节的内存空间，并返回指向该内存的指针；返回值：成功时返回指向分配内存的指针；失败时返回 `NULL`
    * 通常与 `free` 配合使用
    * 函数原型
    ```C
    void *malloc(size_t size);
    ```
7. `calloc`
    * 用于分配 `num` 个大小为 `size` 字节的内存块，并将所有字节初始化为 0；返回值：成功时返回指向分配内存的指针；失败时返回 `NULL`
    * 函数原型
    ```C
    void *calloc(size_t num, size_t size);
    ```
8. `realloc`
    * 用于重新分配内存块 `ptr` 的大小为 `size` 字节。如果 `ptr` 为 `NULL`，则等同于 `malloc(size)`；如果 `size` 为 0，则等同于 `free(ptr)`；返回值：成功时返回指向分配内存的指针；失败时返回 `NULL`
    * 函数原型
    ```C
    void *realloc(void *ptr, size_t size);
    ```
9. `free`
    * 释放之前通过 `malloc`、`calloc` 或 `realloc` 分配的内存
    * 函数原型
    ```C
    void free(void *ptr)
    ```

补充(该头文件中的其他函数)：
1. `strncpy`
   * 从源字符串 `src` 中复制最多 `n` 个字符到目标字符串 `dest`；返回值：目标字符串 `dest` 的指针
   * 函数原型
   ```C
   char *strncpy(char *dest, const char *src, size_t n);
   ```
2. `strncat`
    * 将源字符串 `src` 的前 `n` 个字符追加到目标字符串 `dest` 的末尾；返回值：目标字符串 `dest` 的指针
    * 函数原型
    ```C
    char *strncat(char *dest, const char *src, size_t n);
    ```
3. `strnlen`
    * 计算字符串 `s` 的长度，但最多计算 `maxlen` 个字符。用于安全地获取字符串长度，避免超出缓冲区
    * 函数原型
    ```C
    size_t strnlen(const char *s, size_t maxlen);
    ```

## 特有数据类型

* C

1. `size_t` 
    * `size_t` 是一个标准的数据类型，是一种无符号整数类型，定义在C语言的标准库中，通常用于表示大小或长度。
    * 在 `<stddef.h>` 头文件中定义，但它的定义也被包含在许多其他标准头文件中，例如 `<stdio.h>`、`<stdlib.h>`、`<string.h>` 等。因此，当你包含这些头文件时，`size_t` 通常也会被引入。
    * 用途 
      - 表示内存的大小（如 `malloc` 和 `sizeof` 的返回值）。
      - 表示数组或字符串的长度（如 `strlen` 和 `memcpy` 的参数）。
      - 作为函数的返回值或参数类型，用于确保类型安全和一致性。
    * 特点 
      - `size_t` 是无符号类型，这意味着它不能表示负数。
      - 它的大小（即占用的字节数）取决于平台和编译器。在32位系统上，`size_t` 通常是4字节；在64位系统上，通常是8字节。这种设计使得 `size_t` 能够表示足够大的值，以满足内存管理的需求。
   * 注意事项
     - 当使用 `size_t` 时，建议使用 `%zu` 作为格式化占位符，以确保在不同平台上都能正确打印其值。
     - 如果需要处理可能为负数的值，不要使用 `size_t`，而应选择其他合适的类型（如 `int` 或 `ssize_t`）。
2. 其他在 C 语言标准库中定义的数据类型
   * 这些数据类型主要用于提供跨平台的类型定义，确保程序在不同系统上具有一致的行为
   * C 语言标准库定义了许多数据类型，这些类型提供了明确的语义和跨平台的兼容性。使用这些类型可以提高代码的可移植性和可读性，尤其是在需要精确控制数据大小和类型的情况下。
   * 标准整数类型
        C 语言标准库（特别是`<stdint.h>`和`<inttypes.h>`）定义了一系列具有明确大小的整数类型，这些类型在不同平台上都保持一致的大小：
        - **`int8_t`**：8位有符号整数。
        - **`uint8_t`**：8位无符号整数。
        - **`int16_t`**：16位有符号整数。
        - **`uint16_t`**：16位无符号整数。
        - **`int32_t`**：32位有符号整数。
        - **`uint32_t`**：32位无符号整数。
        - **`int64_t`**：64位有符号整数。
        - **`uint64_t`**：64位无符号整数。
        这些类型在`<stdint.h>`头文件中定义，适用于需要精确控制数据大小的场景，例如嵌入式系统或网络编程。
   * 标准指针类型
         - **`size_t`**：无符号整数类型，用于表示对象的大小。通常用于数组长度、内存分配大小等。它在`<stddef.h>`、`<stdio.h>`、`<stdlib.h>`等头文件中定义。
         - **`ptrdiff_t`**：有符号整数类型，用于表示两个指针之间的差值。它在`<stddef.h>`头文件中定义。
         - **`intptr_t`**：有符号整数类型，其大小与指针相同，可用于存储指针值。
         - **`uintptr_t`**：无符号整数类型，其大小与指针相同，可用于存储指针值。
   * 浮点类型
         - **`long double`**：扩展精度浮点数。
         - **`float_t`** 和 **`double_t`**：在`<math.h>`中定义，分别表示至少与`float`和`double`一样精确的浮点类型，通常用于优化浮点运算。
    * 其他类型
         - **`wchar_t`**：宽字符类型，用于表示宽字符（如Unicode字符）。它在`<wchar.h>`头文件中定义。
         - **`FILE`**：文件流类型，用于文件操作。它在`<stdio.h>`头文件中定义。
         - **`jmp_buf`**：用于非局部跳转的缓冲区类型，与`setjmp`和`longjmp`函数配合使用。它在`<setjmp.h>`头文件中定义。
3. Linux中：
    在Linux编程中，以 _t 结尾的数据类型通常表示这是一个“类型定义”（Type Definition），即通过 typedef 或 using 关键字定义的类型。这种命名约定有助于区分原始类型（如 int、char 等）和通过 typedef 定义的自定义类型。特殊含义：
   1. 标准化和一致性：
       使用 _t 后缀可以明确表示这是一个特定的类型定义，而不是普通的变量名或函数名。这有助于提高代码的可读性和一致性。例如，ssize_t 是一个有符号的整数类型，用于表示大小或长度，而 size_t 是一个无符号的整数类型，用于表示大小或长度。通过 _t 后缀，可以清楚地区分它们的用途。
   2. 避免命名冲突：
       在大型项目中，可能会有多个库或模块定义类似的类型。使用 _t 后缀可以减少命名冲突的可能性。例如，dev_t 是一个用于表示设备号的类型，通过 _t 后缀可以避免与其他可能的 dev 类型冲突。
   3. 类型安全：
       使用 _t 后缀的类型定义可以提供更明确的类型信息，有助于编译器进行类型检查，从而提高代码的类型安全性。例如，pid_t 是一个用于表示进程ID的类型，通过 _t 后缀可以确保在使用时不会与其他整数类型混淆。
   - 常见的 _t 类型：
       以下是一些常见的以 _t 结尾的类型及其用途：
       size_t：无符号整数类型，用于表示大小或长度。
       ssize_t：有符号整数类型，用于表示大小或长度，可以表示负值。
       pid_t：用于表示进程ID的类型。
       uid_t：用于表示用户ID的类型。
       gid_t：用于表示组ID的类型。
       dev_t：用于表示设备号的类型。
       mode_t：用于表示文件模式的类型。
       off_t：用于表示文件偏移量的类型。
       time_t：用于表示时间的类型。
   - 总结：
       _t 后缀：表示这是一个通过 typedef 或 using 定义的类型，有助于提高代码的可读性和一致性。
       标准化：使用 _t 后缀可以减少命名冲突的可能性，并提供更明确的类型信息。
       类型安全：通过 _t 后缀的类型定义可以提高代码的类型安全性，避免类型混淆。
       通过这些 _t 类型，Linux编程中的代码更加清晰、一致且类型安全。

## 指针
1. 指针的值还是指针指向的值
```C
static const unsigned char fontdata_8x16[4096] = {..};

void lcd_pub_ascii(int x, int y, unsigned char c){
    unsigned char *dots = (unsigned char *)&fontdata_8x16[c * 16];
    int i, b;
    unsigned char byte;

    for(int i = 0; i < 16; i++){
        byte = dots[i];
        for(b = 7; b >=0; b--){
            if(byte & (1 << b)){
                lcd_put_pixel(x + 7 - b, y + i, 0xffffff);  // 白色
            }else{
                lcd_put_pixel(x + 7 - b, y + i, 0);         // 黑色
            }
        }
    }
}
```
其中 `byte = dots[i]`，那 `byte` 应该获得的是指针的值还是指针指向的值?

在C语言中，`byte = dots[i];` 这行代码中，`byte` 获得的是指针 `dots` 指向的值，而不是指针本身的值。具体来说：
- `dots` 是一个指向 unsigned char 的指针。
- **`dots[i]` 表示访问指针 dots 指向的数组中的第 i 个元素**。

因此，`byte = dots[i];` 将 `dots` 指向的数组中的第 `i` 个**元素的值**赋给变量 `byte`。

详细解释
指针和数组的关系：
- 在C语言中，**数组名可以被视为指向数组首元素的指针**。例如，`dots` 是一个指向 `unsigned char` 的指针。**`dots[i]` 等价于 `*(dots + i)`，即访问指针 `dots` 指向的数组中的第 `i` 个元素**。
- 代码中的 `dots[i]`：`dots[i]` 访问的是指针 `dots` 指向的数组中的第 `i` 个元素。

因此，`byte = dots[i];` 将 `dots` 指向的数组中的第 `i` 个元素的值赋给变量 `byte`。

2. 关于数组指针
- 在 linux 中调用 ioctl 函数时：
    ```C
    int fd;
    int len;
    unsigned int evbit[2];
    ...
    len = ioctl(fd, EVIOCGBIT(0, sizeof(evbit)), &evbit);
    ```
  - 在这里给 ioctl 传递的第三个参数为：`&evbit`，而不是 `evbit`:
    1. `&evbit`: 表示**对整个数组取址**，得到的是一个指向数组的指针；类型是 **unsigned int (*)[2]**，即指向一个包含两个 unsinged int 的数组的指针
    2. `evbit`:  数组名，当它作为参数传递时，会退化为**指向数组首元素的指针**；类型是 **unsigned int***，指向数组的第一个元素
    3. **unsigned int (*)[2]**: 是一个指向包含两个 unsigned int 的数组的指针。**它指向的是一个完整的数组对象，它的类型是一个数组指针**，而不是一个指针的指针，通常用于传递整个数组作为参数
    4. **unsigned int ****: 是一个指向指针的指针，它通常用于指向一个指针数组或动态分配的二维数组。它指向的是一个指针变量，**类型是指针的指针**，通常用于动态分配的二维数组或指针数组
    5. `unsigned int (*)[2]` 指向的是一个连续的内存块，包含两个 `unsigned int` 元素，`unsigned int **` 指向的是一个指针变量，该指针变量可以指向另一个指针或数组
    6. `ioctl` 在 `EVIOCGBIT` 这个 `request` 的情况下，要求第三个参数是一个指向缓冲区的指针，用于存储返回的数据，缓冲区大小由 `EVIOCGBIT` 的第二个参数 `len` 指定。使用 `&evbit` 明确告诉 `ioctl`，`evbit` 是一个完整的数组，避免歧义
  - 一个例子：
    ```C
    #include <stdio.h>

    void print_array(unsigned int (*arr)[2]){
        // 数组指针
        printf("Array elements: %u, %u.\n", (*arr)[0], (*arr)[1]);
    }

    void print_pointer(unsigned int** ptr){
        printf("Pointer elements: %u, %u.\n", **ptr, *(*ptr + 1));
        // 上述等价于：printf("Pointer elements: %u, %u.\n", *(ptr[0]), *(ptr[1]));
    }

    int main(){
        unsigned int arr[2] = {1, 2};
        unsigned int (*ptr1)[2] = &arr;     // 指向数组的指针

        unsigned int a = 1;
        unsigned int b = 2;
        unsigned int *ptr2 = &a;
        unsigned int *ptr3 = &b;
        unsigned int **ptr4 = &ptr2;        // 指向指针的指针

        print_array(ptr1);
        print_pointer(ptr4);

        return 0;
    }
    ```
    1. 在 `C/C++` 中，指针的下标操作符 `[]` 和解引用操作符 `*` 是可以结合使用的，且两种写法在功能上是等价的。
    2. 在表达式 `*(ptr[0])` 中，括号 `()` 是可以省略的，因为 `[]` 的优先级高于 `*`，但省略后可能会导致语义上的歧义，甚至引发编译错误。使用括号可以更清晰地表达意图，避免潜在的歧义。
    3. `print_pointer(ptr4);` 可能会访问到未被分配的内存而导致程序出错（未定义的行为，undefined behavior），因为在 `ptr2 = &a`、`a = 1`中并没有分配连续的内存空间给 `a`，所以使用 `*(*ptr + 1)` 是非法的。可以将上述代码修改为 `unsigned int values[2] = {1, 2}; unsigned int* ptr2 = values; unsigned int **ptr4 = &ptr2;`

## C++
### 左值与右值

#### 概念
1. 左值（lvalue）：**可以被取址的对象**，通常是一个变量名，表示对象的持久存储位置。eg：`int a = 10` 中 `a` 是一个左值。
2. 右值（rvalue）：通常一个临时对象，不能被取址，表示**一个即将销毁的对象**。

#### 左值引用和右值引用
- 左值引用
  1. 定义：左值引用是一种引用类型，它绑定到一个对象的地址，并且可以通过这个引用修改或访问对象的值。左值引用的申明方式：`Type&`。
  2. 特点：左值引用必须绑定到一个左值（即有名字的变量），不能绑定到临时对象（右值）；左值引用可以用于修改绑定的对象；左值引用通常用于函数参数传递，以避免拷贝对象，提高效率。
- 右值引用
  1. 定义：右值引用是 `C++ 11` 引入的一种引用类型，它绑定到一个临时对象（右值）。右值引用的申明方式：`Type&&`，eg：`int&& rref = 10; std::cout << rref << std::endl`。
  2. 特点：右值引用可以绑定到右值（如临时对象、字面量等），但*不能绑定到左值*；右值引用的主要用途是支持**移动语义（`move semantics`）和完美转发（`perfect forwarding`）**；移动语义允许将资源从一个对象转移到另一个对象，从而避免不必要的拷贝，提高效率。

#### 移动语义
1. `C++ 11` 引入了移动语义
2. **移动语义允许资源（如动态内存、文件句柄、网络连接等）在对象之间进行高效转移，而无需进行不必要的拷贝**。移动语义的核心是右值引用（T&&）和 `std::move` 函数。

#### `move` 函数

1. `std::move` 函数用于将对象的类型转换为右值引用（rvalue reference），从而允许**对象被“移动”而不是被复制**。
2. `std::move` 接受一个左值或右值作为参数，并将其转换为右值引用。从而对象可以被**移动构造函数或移动赋值运算符**接管，从而实现高效的资源转移。
3. 使用 `std::move` 时，需要确保资源对象不再使用被移动的资源。例如，在移动构造函数或移动运算符中，通常需要将源对象的资源置为无效状态（如设置为 `nullptr`）。虽然移动语义可以提高性能，但并不是所有情况下都需要使用 `std::move`。只有当对象的资源需要高效转移时，才应该使用移动语义。
4. 函数原型：
```C++
template <typename T>
typename remove_reference<T>::type&& move(T&& arg);
```
5. 移动构造函数和移动赋值运算符
```C++
class Resource{
public:
    int *data;

    // 移动构造函数
    Resource(Resource &&other) : data(other.data){
        // 确保源对象不再持有资源
        other.data = nullptr;
    }

    // 移动赋值运算符
    Resource& operator=(Resource &&other){
        if(this != &other){
            delete data;            // 释放当前对象的资源
            data = other.data;      // 接管资源
            other.data = nullptr;   // 确保源对象不再持有资源
        }
        return *this;
    }

    // 拷贝构造函数
    Resource(const Resource &other) : data(new int(*other.data)){}

    // 析构函数
    ~Resource(){
        delete data;
    }
}

Resource r1;
Resource r2 = std::move(r1);        // 调用移动构造函数

Resource r1;
Resource r2;
r2 = std::move(r1);                 // 调用移动赋值运算符
```

### C++ 对象的内存分配与声明、初始化
#### 栈分配对象
对于在栈上分配的对象（自动存储期对象），内存分配和初始化通常是在对象声明时同时发生的。
```C++
...
MyClass obj;
...
```
在上述示例中，当执行到 `MyClass obj;` 时，编译器会为 `obj` 在栈上分配内存。分配的大小是 `MyClass` 类型的大小。内存分配完成后，会立即调用 `MyClass` 的默认构造函数来初始化 `obj`。

#### 堆分配对象
对于在堆上分配的对象（动态存储期对象），内存分配和初始化是通过 `new` 操作符显示完成的。
```C++
MyClass *obj = new MyClass;
```
`new MyClass` 首先会调用 `operator new` 来分配内存。这个内存分配是动态的，发生在运行时。内存分配完成后，会立即调用 `MyClass` 的默认构造函数来初始化分配的内存。

#### 延迟初始化
在某些情况下，可以延迟对象的初始化，但这需要使用指针或其他简介方式。如：
```C++
MyClass *obj = nullptr;         // 声明指针，但不分配内存
obj = new MyClass;              // 分配内存并初始化
```

### 前置声明
```C++
// 一种预处理指令，用于防止头文件重复包含
// 在大多数现代编译器中被广泛支持，但不是标准 C++ 的一部分
// 如果项目需要跨平台或跨编译器，建议使用传统的头文件保护宏： #ifndef SOCKET_H...
#pragma once        
class InetAddress;  // 前置声明

class Socket {
private:
    int fd;

public:
    Socket();
    Socket(int);
    ~Socket();

    void bind(InetAddress*);
    void listen();
    void setnonblocking();

    int accept(InetAddress*); 
    int getFd(); 
};
```
- “class InetAddress; // 前置声明” ：在当前的代码文件中，提前声明了一个名为InetAddress的类。这是一种C++的编程技巧，用于在不包含完整类定义的情况下，告知编译器InetAddress是一个类的名字。这样做的好处是可以减少编译依赖，避免在头文件中相互包含导致的编译问题，同时也能提高编译效率。
- 在头文件中使用前置声明：
  1. **减少头文件之间的相互依赖**：当多个头文件之间相互包含时，容易导致复杂的依赖关系，甚至可能出现循环依赖。通过前置声明，可以避免直接包含头文件，从而简化依赖关系。
  2. **提高编译效率**：包含一个头文件意味着*编译器需要解析该头文件及其依赖的所有内容*。如果在头文件中使用前置声明，编译器只需要知道类名即可，而不需要解析完整的类定义，这样可以显著减少编译时间。
  3. **避免不必要的重新编译**：如果一个头文件中直接包含了另一个头文件，那么被包含的头文件的任何修改都会导致包含它的所有文件重新编译。而使用前置声明可以避免这种情况，因为前置声明本身不会因为被声明类的内部实现变化而需要重新编译。
- 在源文件中使用前置声明
  1. **延迟包含头文件**：如果某个类的定义在源文件中只被间接使用（例如，通过指针或引用），可以先使用前置声明，然后在需要使用该类的具体功能时再包含对应的头文件。这可以进一步优化编译效率。
  2. **分离接口和实现**：在某些设计模式（如`Pimpl`模式）中，前置声明可以用于隐藏实现细节。例如，可以在头文件中使用前置声明，而在源文件中包含实际的实现头文件。
- 在源文件中是否需要包含 `InetAddress` 对应的头文件
  1. 在源文件中，如果需要使用` InetAddress` 类的具体成员（如方法、属性等），则必须包含 `InetAddress` 对应的头文件。这是因为前置声明只告诉编译器 `InetAddress` 是一个类，但不会提供类的具体定义。如果需要访问类的成员，编译器必须知道类的完整定义。
