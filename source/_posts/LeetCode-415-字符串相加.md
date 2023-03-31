---
title: LeetCode_415-字符串相加
date: 2023-03-29 16:26:03
categories: 
- LeetCode
tags: 
- 字符串
---

## 题目链接

[LeetCode_415-字符串相加](https://leetcode.cn/problems/add-strings/)

## 关键词
字符串

## 题目概述

给定两个字符串形式的非负整数 num1 和num2 ，计算它们的和并同样以字符串形式返回。

你不能使用任何內建的用于处理大整数的库（比如 BigInteger）， 也不能直接将输入的字符串转换为整数形式。

## 示例：

```java
输入：num1 = "11", num2 = "123"
输出："134"
    
输入：num1 = "456", num2 = "77"
输出："533"
```

## 代码：
```java
class Solution {
    public String addStrings(String num1, String num2) {
        int add = 0;
        int i = num1.length() - 1;
        int j = num2.length() - 1;
        StringBuffer ans = new StringBuffer();
        while(i >= 0 || j >= 0 || add != 0) {
            //两个数字位数不同怎么处理，这里我们统一在指针当前下标处于负数的时候返回0
            //等价于对位数较短的数字进行了补零操作，这样就可以除去两个数字位数不同情况的处理
            int x = i >= 0? num1.charAt(i) - '0' : 0;
            int y = j >= 0? num2.charAt(j) - '0' : 0;
            int sum = x + y + add;
            ans.append(sum % 10);
            add = sum / 10;
            i--;
            j--;
        }
        ans.reverse();
        return ans.toString();
    }
}
```

