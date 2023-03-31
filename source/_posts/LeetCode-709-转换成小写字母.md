---
title: LeetCode_709-转换成小写字母
date: 2023-03-29 16:48:25
categories: 
- LeetCode
tags: 
- 字符串
---

## 题目链接

[LeetCode_709-转换成小写字母](https://leetcode.cn/problems/to-lower-case/)

## 关键词
字符串

## 题目概述

给你一个字符串 `s` ，将该字符串中的大写字母转换成相同的小写字母，返回新的字符串。

## 示例：

```java
输入：s = "Hello"
输出："hello"
    
输入：s = "here"
输出："here"
    
输入：s = "LOVELY"
输出："lovely"
```

## 代码：
```java
class Solution {
    public String toLowerCase(String s) {
        //方法一（一个个字符判断）
        StringBuffer ans = new StringBuffer();
        for(int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            if(ch >= 'A' && ch <= 'Z') {
                //先将字符ch转换为整型计算ASCII码，再转换为字符型输出字符
                //A~Z的ASCII码为65~90，字符a~z的ASCII码为97~122，
                //每个大小写字符的ASCII码都相差32,因此用大写字符的ASCII码 加上32即可得到该字符的小写形式
                ch = (char) (ch + 32);
                ans.append(ch);
            }
            else {
                ans.append(ch);
            }
        }
        return ans.toString();
        
        //方法二（调用函数）
        //仅需一行代码 //toUpperCase()为将小写字符串转变为大写字符串
        return s.toLowerCase();
    }
}
```
