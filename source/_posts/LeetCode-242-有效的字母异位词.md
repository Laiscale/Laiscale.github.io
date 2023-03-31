---
title: LeetCode_242-有效的字母异位词
date: 2023-03-29 16:33:24
categories: 
- LeetCode
tags: 
- 字符串
- 哈希表
- 位运算
---

## 题目链接

[LeetCode_242-有效的字母异位词](https://leetcode.cn/problems/valid-anagram/)

## 关键词
字符串, 哈希表，位运算

## 题目概述

给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。

注意：若 s 和 t 中每个字符出现的次数都相同，则称 s 和 t 互为字母异位词。

## 示例：

```java
输入: s = "anagram", t = "nagaram"
输出: true
 
输入: s = "rat", t = "car"
输出: false
```

## 代码：

### 方法一：
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        //方法一（哈希表）
        HashMap<Character, Integer> map = new HashMap<>();
        for(int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            map.put(ch, map.containsKey(ch)? map.get(ch)+1 : 1);
        }
        for(int j = 0; j < t.length(); j++) {
            char ch = t.charAt(j);
            if(map.containsKey(ch)) {
                map.put(ch, map.get(ch)-1);
            }
            else {
                map.put(ch, 1);
            }
        }

        int count = 0;
        for(char key : map.keySet()) {
            //必须设置为大于一，这样才行
            if(map.get(key) >= 1) {
                count++;
            }
        }        
        if(count == 0) return true;
        return false;
    }
}
```
### 方法二：（同时也是官方解法）   
```java
class Solution {
    public boolean isAnagram(String s, String t) { 
        //方法二（先排序，用equal比较）
        if(s.length() != t.length()) {
            return false;
        }
        char[] s1 = s.toCharArray();
        char[] t1 = t.toCharArray();
        Arrays.sort(s1);
        Arrays.sort(t1);
        return Arrays.equals(s1, t1);
    }
}
```
### 方法三：
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        //方法三（先排序，用位运算【相当与方法二的复杂(多余)化】）
        if(s.length() != t.length()) {
            return false;
        }
        char[] s1 = s.toCharArray();
        char[] t1 = t.toCharArray();
        Arrays.sort(s1);
        Arrays.sort(t1);
        int count = 0;
        for(int i = 0; i < s1.length; i++) {
            int ss = s1[i] - 'a';
            int tt = t1[i] - 'a';
            //(ss ^ tt)必须用括号括起来，这个是优先级问题
            //如果不括起来，执行时就是相当于这样子的运算顺序ss ^ （tt != 0）
            if((ss ^ tt) != 0) {
                count++;
            }
        }
        if(count == 0) return true;
        return false;
    }
}
```

**简洁的哈希表解法**
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        //长度不等肯定不对
        if(s.length() != t.length())
            return false;
        int[] alpha = new int[26];
        for(int i = 0; i< s.length(); i++) {
            alpha[s.charAt(i) - 'a'] ++;
            alpha[t.charAt(i) - 'a'] --;
        }
        for(int i=0;i<26;i++)
            if(alpha[i] != 0)
                return false;
        return true;
}
```
