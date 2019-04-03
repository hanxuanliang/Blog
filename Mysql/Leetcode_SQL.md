# LeetCode_SQL刷题

> **叹为观止！！！** 有些题的做法简直......

## Content

>- **2019.4.3**
>
>    - [**Big Countries**](#595. Big Countries)   
>    - [Swap Salary](#627. Swap Salary)

## 595. [Big Countries](https://leetcode.com/problems/big-countries/)

>如果一个国家的面积超过300万平方公里，或者人口超过2500万，那么这个国家就是大国家。

水题一个。就是在 `where` 条件写一个 `or`  就行。

```mysql
select name, population, area from world where area > 3000000 or population > 25000000;
```

## 627. [Swap Salary](<https://leetcode.com/problems/swap-salary/>)

> 给定一个 `salary` 表，如下所示，有 m=男性 和 f=女性 的值 。交换所有的 f 和 m 值（例如，将所有 f 值更改为 m，反之亦然）。要求使用一个更新（Update）语句，并且没有中间临时表。
>
> 请注意，你必须编写一个 Update 语句，不要编写任何 Select 语句。

但是看到这个题是懵圈的。在 `update` 怎么控制case？然后我就Stack Overflow了。**在mysql里面使用 update CASE WHEN/THEN/ELSE 一次性修改多行记录**。

```mysql
UPDATE salary SET sex = CASE 
	sex 
	WHEN 'm' THEN 'f'
    ELSE 'm'
    END;
```

对于这个语句举个网上的例子：

```mysql
UPDATE `table` SET `uid` = CASE
    WHEN id = 1 THEN 2952
    WHEN id = 2 THEN 4925
    WHEN id = 3 THEN 1592
    ELSE `uid`
    END
WHERE id  in (1,2,3)
```

此时的变量 `id` 是一个范围，而题目里面的只是一个字段。

### 其他做法

但是Solution里面有个为之一振的代码：

```mysql
update salary set sex = CHAR(ASCII('f') ^ ASCII('m') ^ ASCII(sex));
```

这里用到了异或的性质：

> **交换律**：${\displaystyle p\oplus q=q\oplus p}$
>
> **恒等律**：${\displaystyle p\oplus 0=p}​$
>
> **归零律**：${\displaystyle p\oplus p=0}$
>
> **自反**：${\displaystyle p\oplus q\oplus q=p\oplus 0=p}$

这里可以联想在C语言里面交换两个数的奇技淫巧：

```c++
a = a^b;
b = a^b;
a = a^b;
// 第二步：b = a^b^b = a; 后面的以此类推
```

其实里面所要求的就是一个条件判断，所以我们这里使用 `if` （百度啊） ：

```mysql
UPDATE salary 
SET sex=IF(sex='f','m','f');
/*
IF(expr1,expr2,expr3)
如果 expr1 是TRUE (expr1 <> 0 and expr1 <> NULL)，则 IF()的返回值为expr2; 否则返回值则为 expr3。IF() 的返回值为数字值或字符串值，具体情况视其所在语境而定。
注：感觉有点三元表达式一样
*/
```

