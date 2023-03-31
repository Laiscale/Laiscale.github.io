---
title: LeetCode_1002-查找公共字符
date: 2023-03-29 16:07:34
categories: 
- LeetCode
tags: 
- 哈希表
- 字符串
---

## 题目链接

[LeetCode_1002-查找公共字符](https://leetcode.cn/problems/find-common-characters/)

## 关键词
哈希表， 字符串

## 题目概述

给你一个字符串数组 words ，请你找出所有在 words 的每个字符串中都出现的共用字符（ **包括重复字符**），并以数组形式返回。你可以按 **任意顺序** 返回答案。

## 示例：

```java
输入：words = ["bella","label","roller"]
输出：["e","l","l"]
    
输入：words = ["cool","lock","cook"]
输出：["c","o"]
    
最后执行的输入：(代表通过了部分测试用例，执行该测试用例时失败了)
["cool","lock","cook"]
```

## 代码：(写了蛮久，需要注意)
```java
class Solution {
    public List<String> commonChars(String[] words) {
        HashMap<Character, Integer> map = new HashMap<>();
        List<String> res = new ArrayList<>();
        int i = 0;
        //在这里定义j时，由于j一直递增，不会变为0，导致i循环只会执行一次，因此要把它放到i循环里面
//        int j = 0;
        while(i < words.length) {
            int j = 0;
            HashMap<Character, Integer> tmp = new HashMap<>();
            while(j < words[i].length()) {
                Character ch = words[i].charAt(j);
                //把第一个字符串的结果存起来，然后下一个字符串与其比较
                //得到相同的字符，再继续与下一个字符串比较......
                if(i == 0) {
                    tmp.put(ch, tmp.containsKey(ch) ? tmp.get(ch) + 1 : 1);
                }
                if(i > 0) {
                    if(map.containsKey(ch)) {
                        if(tmp.containsKey(ch)) {
                            //这两步是不能这样写的，因为当字符串为这样时：["cool","lock","cook"]
                            //输出为["c", "o", "o"]，而预期结果为["c", "o"]
                        //    int k = Math.min(map.get(ch), tmp.get(ch));
                        //    tmp.put(ch, k + 1);
                            int a = map.get(ch);
                            int b = tmp.get(ch);
                            //必须先判断，如果前面key的value值大于前面，才能加1
                            if (a > b) {
                                tmp.put(ch, b+1);
                            }
                            else {
                                tmp.put(ch, b);
                            }
                        }
                        else {
                            tmp.put(ch, 1);
                        }
                    }
                }
                j++;
            }
            map.clear();
            map.putAll(tmp);
            tmp.clear();
            i++;
        }
        //entrySet() 方法返回映射中包含的映射的 Set 视图。
        //entrySet() 方法可以与 for-each 循环一起使用，用来遍历迭代 HashMap 中每一个映射项。
        for(Map.Entry<Character, Integer> entry : map.entrySet()) {
            for(int m = 0; m < entry.getValue(); m++) {
                res.add(String.valueOf(entry.getKey()));
            }
        }
    return res;
    }
}
```
