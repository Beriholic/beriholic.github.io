---
categories: code
---
# Mashmokh and ACM

## 题目描述

Mashmokh's boss, Bimokh, didn't like Mashmokh. So he fired him. Mashmokh decided to go to university and participate in ACM instead of finding a new job. He wants to become a member of Bamokh's team. In order to join he was given some programming tasks and one week to solve them. Mashmokh is not a very experienced programmer. Actually he is not a programmer at all. So he wasn't able to solve them. That's why he asked you to help him with these tasks. One of these tasks is the following.

A sequence of  l  integers  b1,b2,...,bl(1<=b1<=b2<=...<=bl<=n) is called good if each number divides (without a remainder) by the next number in the sequence. More formally ![](https://cdn.luogu.com.cn/upload/vjudge_pic/CF414B/c97c90bdd5f34b7b09ca5088db0c88621395bd9c.png) for all i(1<=i<=l-1).

Given n and k find the number of good sequences of length k. As the answer can be rather large print it modulo 1000000007(10^9+7).

## 输入格式

The first line of input contains two space-separated integersn,k (1<=n,k<=2000).

## 输出格式

Output a single integer — the number of good sequences of length kmodulo 1000000007(10^9+7).

## 样例1

### 样例输入1

```
3 2
```

### 样例输出1

```
5
```

## 样例2

### 样例输入2

```
6 4
```

### 样例输出2

```
39
```

## 样例3

### 样例输入3

```
2 1
```

### 样例输出3

```
2
```

## 提示

In the first sample the good sequences are:[1,1],[2,2],[3,3],[1,2],[1,3].

## 代码

```cpp
#include "bits/stdc++.h"

const int MOD = 1e9 + 7, MAX = 2001;
int dp[MAX][MAX];

int main() {
    std::ios::sync_with_stdio(false);
    
    int n, k;
    std::cin>>n>>k;
            

    //dp[i][j] 表示长度为i,最大元素为j的方案数

    //状态转移方程为：dp[i][j]+=dp[i-1][j*cnt];
    //dp[i][j]的状态由上一长度推出，即dp[i-1][j*len]中的i-1;
    //题目可知，后一个数都能被前面一个数整除，也就是成倍数关系，所以状态转移方程为dp[i][j]+=dp[i-1][j*cnt]


    //dp初始化,显而易见初始化为：长度为1时，最大元素从一到n的方案数为一
    for (int i = 1; i <= n; i++) {
        dp[1][i] = 1;
    }


    for (int i = 2; i <= k; i++) {//遍历长度，因为初始化为1,上一状态为i-1,所以初始化状态为i-1=1,i=2
        for (int j = 1; j <= n; j++) {//遍历元素
            for (int cnt = 1; cnt * j <= n; cnt++) {//成倍数关系
                dp[i][j] = (dp[i][j] + dp[i - 1][j * cnt]) % MOD;
            }
        }
    }

    //重新回顾，题目求的是长度为k,最大元素为1到n的方案数
    int ans = 0;
    for (int i = 1; i <= n; i++) {//小火收汁
        ans = (ans + dp[k][i]) % MOD;
    }

    std::cout << ans;
    return 0;
}
```
