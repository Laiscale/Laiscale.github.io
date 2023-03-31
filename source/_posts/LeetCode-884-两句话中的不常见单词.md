---
title: LeetCode_884-两句话中的不常见单词
date: 2023-03-29 16:15:55
categories: 
- LeetCode
tags: 
- 哈希表
- 字符串
---

## 题目链接

[LeetCode_290-单词规律](https://leetcode.cn/problems/uncommon-words-from-two-sentences/)

## 关键词
哈希表， 字符串

## 题目概述

句子 是一串由空格分隔的单词。每个 单词 仅由小写字母组成。

如果某个单词在其中一个句子中恰好出现一次，在另一个句子中却 没有出现 ，那么这个单词就是 不常见的 。

给你两个 句子 s1 和 s2 ，返回所有 不常用单词 的列表。返回列表中单词可以按 任意顺序 组织。

## 示例：

```java
输入：s1 = "this apple is sweet", s2 = "this apple is sour"
输出：["sweet","sour"]
    
输入：s1 = "apple apple", s2 = "banana"
输出：["banana"]

最后执行的输入：
"s z z z s"
"s z ejt"
    
最后执行的输入：
"fd kss fd"
"fd fd kss"
```

## 代码：
```java
class Solution {
    public String[] uncommonFromSentences(String s1, String s2) {
        HashMap<String, Integer> map = new HashMap<>();
        String[] str1 = s1.split(" ");
        String[] str2 = s2.split(" ");
        List<String> tmpList =new ArrayList();
        //不能直接创建数组，因为不知道输出的数组长度
        //如果像下面定义长度的话，会有多余的输出，如：["sweet","sour","null","null"]
        // String[] res = new String[str1.length];
        for(String sa : str1) {
            map.put(sa, map.containsKey(sa)? map.get(sa)+1 : 1);
            //不能这里删除，如果后面存在就会报错，如那两个
            // if(map.get(sa) > 1) {
            //     map.remove(sa);
            // }
        }

        for(int i = 0; i < str2.length; i++) {
            if(map.containsKey(str2[i])) {
                // map.remove(str2[i]);
                //不能减1，这样很难比较，如第一个最后的输入
                map.put(str2[i], map.get(str2[i])+1);
            }
            else {
                map.put(str2[i], 1);
            }
        }
        //因为不能定义数组，j也就不需要了
        // int j = 0;
        //两种方法都可以
        // for(Map.Entry<String, Integer> entry : map.entrySet()) {
        //     if(entry.getValue() == 1) {
        //         res[j] = entry.getKey();
        //         j++;
        //     }
        // }
        for(String key : map.keySet()) {
            if(map.get(key) == 1) {
               tmpList.add(key);
            }
            
        }
        String[] res = tmpList.toArray(new String[tmpList.size()]);
        return res;
    }
}
```
