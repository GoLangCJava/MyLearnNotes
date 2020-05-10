题目链接：[pow](https://leetcode-cn.com/problems/powx-n/)

实现 [pow(*x*, *n*)](https://www.cplusplus.com/reference/valarray/pow/) ，即计算 x 的 n 次幂函数。

**示例 1:**

```
输入: 2.00000, 10
输出: 1024.00000
```

**示例 2:**

```
输入: 2.10000, 3
输出: 9.26100
```

**示例 3:**

```
输入: 2.00000, -2
输出: 0.25000
解释: 2-2 = 1/22 = 1/4 = 0.25
```

**说明:**

- -100.0 < *x* < 100.0
- *n* 是 32 位有符号整数，其数值范围是 [−231, 231 − 1] 。

## 思路

裸的快速幂，递归与非递归都可以实现。

## 代码

递归版：

```cpp
class Solution
{
  public:
    double po(double x, int n)
    {
        if (n == 0)
            return 1.0;
        double y = po(x, n / 2);
        if (n & 1)
            return y * y * x;
        else
            return y * y;
    }
    double myPow(double x, int n)
    {
        if (n > 0)
            return po(x, n);
        return 1.0 / po(x, n);
    }
};
```

非递归版：

```cpp
class Solution
{
public:
    double hpow(double x, long long n)
    {
        double ans = 1.0;
        while (n)
        {
            if (n & 1)
                ans *= x;
            x *= x;
            n >>= 1;
        }
        return ans;
    }
    double myPow(double x, int n)
    {
        long long ln = n;
        if (ln < 0)
            return 1.0 / hpow(x, -ln);
        return hpow(x, ln);
    }
};
```

