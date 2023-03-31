---
title: LeetCode_771-宝石与石头
date: 2023-03-29 16:50:07
categories: 
- LeetCode
tags: 
- 字符串
- 哈希表
---

## 题目链接

[LeetCode_771-宝石与石头](https://leetcode.cn/problems/jewels-and-stones/)

## 关键词
字符串，哈希表

## 题目概述

给你一个字符串 jewels 代表石头中宝石的类型，另有一个字符串 stones 代表你拥有的石头。 stones 中每个字符代表了一种你拥有的石头的类型，你想知道你拥有的石头中有多少是宝石。

字母区分大小写，因此 "a" 和 "A" 是不同类型的石头。

- `jewels` 中的所有字符都是 **唯一的**

## 示例：

```java
输入：jewels = "aA", stones = "aAAbbbb"
输出：3
    
输入：jewels = "z", stones = "ZZ"
输出：0
```

## 代码：
```java
class Solution {
    public int numJewelsInStones(String jewels, String stones) {
        Set<Character> set = new HashSet<>();
        for(int i = 0; i < jewels.length(); i++) {
            set.add(jewels.charAt(i));
        }
        int count = 0;
        for(int j = 0; j < stones.length(); j++) {
            //需要注意的是Set中判断是否存在key用contains(), 不是containsKey()
            if(set.contains(stones.charAt(j))) {
                count++;
            }
        }
        return count;
    }
}
```

