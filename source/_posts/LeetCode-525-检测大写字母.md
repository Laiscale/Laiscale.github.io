---
title: LeetCode_525-检测大写字母
date: 2023-03-29 16:28:41
categories: 
- LeetCode
tags: 
- 字符串
---

## 题目链接

[LeetCode_525-检测大写字母](https://leetcode.cn/problems/detect-capital/)

## 关键词
字符串

## 题目概述

我们定义，在以下情况时，单词的大写用法是正确的：

- ​    全部字母都是大写，比如 "USA" 。
- ​    单词中所有字母都不是大写，比如 "leetcode" 。
- ​    如果单词不只含有一个字母，只有首字母大写， 比如 "Google" 。

给你一个字符串 word 。如果大写用法正确，返回 true ；否则，返回 false 。

## 示例：

```java
输入：word = "USA"
输出：true
    
输入：word = "FlaG"
输出：false
```

## 代码：
```java
class Solution {
    public boolean detectCapitalUse(String word) {
        int len = word.length();
        //统计大写字母个数
        int count = 0;
        //首字母
        Character flag = word.charAt(0);
        for(int i = 0; i < len; i++) {
            Character ch = word.charAt(i);
            if(ch >= 'A' && ch <= 'Z') {
                count++;
            }
        }
        //当大写字母个数等于字符串长度，或者大写字母个数不存在（即全为小写字母）时，返回true
        if(count == len || count == 0) return true;
        //如果大写字母个数为1， 则必须要同时满足flag为大写字母才行
        if(count == 1 && (flag >= 'A' && flag <= 'Z')) return true;
        //其他情况返回false
        return false;
    }
}
```
