# 第十届蓝桥杯Java B组题

> **这是一道结果填空的题，你只需要算出结果后提交即可。本题的结果为一个整数，在提交答案时只填写这个整数，填写多余的内容将无法得分。**
>
> 看到这个......，那就尽量不写code就不写了，骗分就行！！！

## 试题 B: 不同子串

>**【问题描述】:**
>一个字符串的非空子串是指字符串中长度至少为 1 的连续的一段字符组成的串。例如，字符串`aaab` 有非空子串`a, b, aa, ab, aaa, aab, aaab`，一共 7 个。注意在计算时，只算本质不同的串的个数。请问，字符串`0100110001010001` 有多少个不同的非空子串？

### 思路

首先题目要求的字符串的长度不长，所以在时间复杂度上不需要太抠。其实截取子串知道起点，终点就可以。那么设置两层循环，外层起点，内层终点，在处理的时候使用`str.sunstr(i, len)`就可以取到`[i, j]`的子串，而且题目要求不重复，所以需要`set`去重即可。

```c++
#include<cstring>
#include<iostream>
#include<algorithm>
#include<unordered_set>

using namespace std;

int main() {
    string line;
    cin >> line;
    unordered_set<string> S;
    for (int i = 0; i < line.size(); i++)
        for (int j = i; j <= line.size(); j++)
            S.insert(line.substr(i, j - i + 1));
    cout << S.size() << endl;
    return 0;
}
```

![B_2](https://github.com/hanxuanliang/Blog/blob/master/Pic/B_B.jpg)

## 试题 C: 数列求值

> **【问题描述】:**
> 给定数列 1, 1, 1, 3, 5, 9, 17, …，从第 4 项开始，每项都是前 3 项的和。求第 20190324 项的最后 4 位数字。

### 思路：

其实就是斐波那契的变形，不管是前多少项相加。既然知道出处，code就简单了。需要注意的是`第 20190324 项的最后 4 位数字`，也就是该项对`10000`取模。但是我们是**最后对所求项取模**还是在**中途运算的过程中取模**。因为一般斐波那契要求的项数都很高，很容易溢出，而输出结果往往是所求项的模，所以我们就在中途计算过程中取模（`a%10 = (b + c)%10 = b%10 + c%10`）

```c++
#include<iostream>

using namespace std;

int main() {
    int a = 1, b = 1, c = 1;
    int n;
    cin >> n;
    while (--n) {
        int d = (a + b + c) % 10000;
        a = b, b = c, c = d;
    }
    cout << a << endl;
    return 0;
}
```

![B_2](https://github.com/hanxuanliang/Blog/blob/master/Pic/B_C.jpg)

## 试题 D: 数的分解

>**【问题描述】：**
>把 2019 分解成 3 个各不相同的正整数之和，并且要求每个正整数都不包含数字 2 和 4，一共有多少种不同的分解方法？注意交换 3 个整数的顺序被视为同一种方法，例如 1000+1001+18 和1001+1000+18 被视为同一种

## 思路

本质是`a+b+c`，条件是`a&b&c里面不能含有2|4`。那么枚举就好了。但是注意点是整数的顺序可能导致重复，那么我们在写的时候就人为设置`a<b<c`，这样就只计算了一次。另外整数里面不能有`2|4`，解决方法就是循环看每一位就行（`这一段的code可以作为模板记住 -> 解决位的问题`）

```c++
#include<iostream>

using namespace std;

bool check(int num) {
    while (num > 0) {
        int t = num % 10;
        if (t == 2 || t == 4) return true;
        num /= 10;
    }    
    return false;
}

int main() {
    int n;
    int res = 0;
    cin >> n;
    for (int a = 1; a <= n; a++) {
        for (int b = a + 1; b < n - a - b; b++) {
            int c = n - a - b;
            if (!check(a) && !check(b) && !check(c))
                res++;
        }
    }
    cout << res << endl;
    return 0;
}
```

![B_2](https://github.com/hanxuanliang/Blog/blob/master/Pic/B_D.jpg)

