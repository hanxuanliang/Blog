# STL基本API使用介绍

## 目录

> - [Vector](#Vector)
> - [**Set**](#Set)
> - [**String**](#String)
> - [**Map**](#Map)
> - [**Queue**](#Queue)
> - [**Priority_queue**](#Priority_queue)
> - [**Stack**](#Stack)
> - [**Pair**](#Pair)
> - [**Algorithm**](#Algorithm)

## Vector

- **定义**

  ```c++
  vector<typename> name;
  // 相当于一维数组 name[size], 不过是长度可变，所以 vector 被称为 “变长数组”
  vector<vector<int> > name;
  // 如果 typename 是 vector ，中间需要一个空格，避免编译时被认为是 ‘>>’ 移位符号
  ```

- **元素访问**

  ```c++
  vector<int> vi[100];
  
  vi[0]; vi[1];
  // 下标访问，范围是 [0, vi.size()-1]
  vector<int>::iterator it;
  // 使用迭代器访问，并且通过 *it 来访问 vector 里面的元素。下面做一个完整的例子：
  ```

  ```c++
  #include<stdio.h>
  #include<vector>
  
  using namespace std;
  
  int main() {
      vector<int> vi;
      for (int i = 0; i < 5; i++) 
          vi.push_back(i);	// push_back() 就是向vector后面添加一个元素 x
      
      vector<int>::iterator it = vi.begin();
      // vi.begin() 为 vi 的首地址的地址，而 it 指向这个地址
      for (int i = 0; i < vi.size(); i++)
          printf("%d\n", *(it + 1));
      return 0;
  }
  // 在这里我们可以看出：vi[i] 与 *(vi.begin() + i) 是等价的
  ```

  >`begin()`是 vi 取首元素的位置，那`end()`？这里要注意，`end()`并不是取 vi 的尾元素，而是`取尾元素地址的下一个地址`。`end()`作为迭代器的终止标志，不存放任何元素。因为美国人的思维比较习惯**左闭右开**，也就是`[begin, end)`。