---
title: LeetCode_389-找不同
date: 2023-03-29 16:01:15
categories: 
- LeetCode
tags: 
- 哈希表
- 字符串
---

## 题目链接

[LeetCode_389-找不同](https://leetcode.cn/problems/find-the-difference/)

## 关键词
哈希表， 字符串

## 题目概述

给定两个字符串 `s` 和 `t` ，它们只包含小写字母。

字符串 `t` 由字符串 `s` 随机重排，然后在随机位置添加一个字母。

请找出在 `t` 中被添加的字母。

## 示例：

```java
输入：s = "abcd", t = "abcde"
输出："e"
解释：'e' 是那个被添加的字母。

输入：s = "", t = "y"
输出："y"

最后执行的输入：
"ymbgaraibkfmvocpizdydugvalagaivdbfsfbepeyccqfepzvtpyxtbadkhmwmoswrcxnargtlswqemafandgkmydtimuzvjwxvlfwlhvkrgcsithaqlcvrihrwqkpjdhgfgreqoxzfvhjzojhghf"
"qhxepbshlrhoecdaodgpousbzfcqjxulatciapuftffahhlmxbufgjuxstfjvljybfxnenlacmjqoymvamphpxnolwijwcecgwbcjhgdybfffwoygikvoecdggplfohemfypxfsvdrseyhmvkoovx"
```

## 代码：
```java
class Solution {
    public char findTheDifference(String s, String t) {
        //定义一个哈希表
        HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        //字符串长度有s.length(),【数组的话为nums.length】
        for(int i = 0; i < s.length(); i++) {
            Character ch = s.charAt(i);
            //最开始时直接map.put(ch, 1),但这样会导致如果字符串中有重复的字符的话，会报错
            map.put(ch,map.containsKey(ch)?map.get(ch)+1:1);
        }
        Character add = ' ';
        int j = 0;
        while(j < t.length()) {
            Character ch = t.charAt(j);
            if(map.containsKey(ch) && map.get(ch) > 0) {
                map.put(ch, map.get(ch)-1);
            }
            //当key不存在或key的value值为负数是，即为添加的数
            else add = ch;
            j++;
        }
    return add;
    }
}
```

## 官方的**位运算**（没想到）
```java
class Solution {
    public char findTheDifference(String s, String t) {
        char ans = t.charAt(t.length()-1);
        //异或运算
        for(int i = 0; i < s.length(); i++) {
            ans ^= s.charAt(i);
            ans ^= t.charAt(i);
        }
        return ans;
    }
}
```