# STL(Standard Template Library)

>[runoob.com](https://www.runoob.com/cplusplus/cpp-stl-tutorial.html)

`C++` 标准模板库的核心包括以下重要组件：
* 容器(Containers)
各种数据结构，包括向量（vector）、链表（list）、队列（queue）、栈（stack）、集合（set）、映射（map）等。

* 算法(Algorithms)
用于对容器中的元素进行各种操作，包括排序、搜索、复制、移动、变换等。这些算法在使用时**不需要关心容器的具体类型**，只需要指定要操作的范围即可。

* 迭代器(Iterators)
**用于遍历容器中的元素**，允许以统一的方式访问容器中的元素，而**不用关心容器的内部实现细节**。包括：随机访问迭代器、双向迭代器、前向迭代器和输入输出迭代器等。

* 函数对象(Function Objects)
函数对象是**可以像函数一样调用的对象**，可以用于算法中的各种操作。包括：一元函数对象、二元函数对象、谓词等。

* 适配器(Adapters)
**用于将一种容器或迭代器适配成另一种容器或迭代器**，以满足特定的需求。包括：栈适配器（stack adapter）、队列适配器（queue adapter）和优先队列适配器（priority queue adapter）等。

## 容器
用来存储数据的序列，它们提供了**不同的存储方式和访问模式**

### 序列容器
存储元素的**序列**，允许双向遍历（todo：list支持双向遍历？）

* `std::vector`
1. 动态数组，支持快速随机访问


* `std::deque`
1. 双端队列，支持快速插入和删除

* `std::list`
1. 链表，支持快速插入和删除，但不支持随机访问

### 关联容器
存储**键值对**，每个元素都有一个键（key）和一个值（value），并且**通过键来组织元素**。（todo：set也是存储键值对？）

* `std::set`
1. 集合，不允许重复元素

* `std::multiset`
1. 多重集合，允许多个重复元素具有相同的键

* `std::map`
1. 映射，每个键映射到一个值

* `std::multimap`
1. 多重映射，存储了键值对（pair），其中键是唯一的，但值可以重复，允许一个键映射到多个值

### 无序容器
C++11 引入；哈希表，支持快速的查找、插入和删除

* `std::unordered_set`
1. 无序集合

* `std::unordered_multiset`
1. 无序多重集合
   
* `std::unordered_map`
1. 无序映射
   
* `std::unordered_multimap`
1. 无序多重映射