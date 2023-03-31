---
title: LeetCode_290--单词规律
date: 2023-03-29 15:36:49
categories: 
- LeetCode
tags: 
- 哈希表
- 字符串
---

## 题目链接

[LeetCode_290-单词规律](https://leetcode.cn/problems/word-pattern/)

## 关键词
哈希表， 字符串

## 题目概述

给定一种规律 pattern 和一个字符串 s ，判断 s 是否遵循相同的规律。

这里的 遵循 指完全匹配，例如， pattern 里的每个字母和字符串 s 中的每个非空单词之间存在着双向连接的对应规律。

## 示例：

```java
输入: pattern = "abba", s = "dog cat cat dog"
输出: true

输入:pattern = "abba", s = "dog cat cat fish"
输出: false

输入: pattern = "aaaa", s = "dog cat cat dog"
输出: false
```

## 代码：
```java
class Solution {
    public boolean wordPattern(String pattern, String s) {
        //定义两个map，来一对一的映射
        HashMap<Character, String> map = new HashMap<>();
        HashMap<String, Character> set = new HashMap<>();
        String[] strs = s.split(" ");
        //长度必须一致
        if (strs.length != pattern.length()) return false;
        int i = 0, j = 0;
        while (i < pattern.length() && j < strs.length) {
            Character ch = pattern.charAt(i);
            //下面两种是不存在的情况
            if (map.containsKey(ch) && !map.get(ch).equals(strs[j]))   return false;
            if (set.containsKey(strs[j]) && set.get(strs[j]) != ch) 
                return false;
            map.put(ch, strs[j]);
            set.put(strs[j], ch);
            i++; j++;
        }
        return true;
    }  
}
```