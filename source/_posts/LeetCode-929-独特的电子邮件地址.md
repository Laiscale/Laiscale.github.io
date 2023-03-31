---
title: LeetCode_929-独特的电子邮件地址
date: 2023-03-29 16:19:04
categories: 
- LeetCode
tags: 
- 哈希表
- 字符串
---

## 题目链接

[LeetCode_929-独特的电子邮件地址](https://leetcode.cn/problems/unique-email-addresses/)

## 关键词
哈希表， 字符串

## 题目概述

每个 有效电子邮件地址 都由一个 本地名 和一个 域名 组成，以 '@' 符号分隔。除小写字母之外，电子邮件地址还可以含有一个或多个 '.' 或 '+' 。

例如，在 alice@leetcode.com中， alice 是 本地名 ，而 leetcode.com 是 域名 。
如果在电子邮件地址的 本地名 部分中的某些字符之间添加句点（'.'），则发往那里的邮件将会转发到本地名中没有点的同一地址。请注意，此规则 不适用于域名 。

例如，"alice.z@leetcode.com” 和 “alicez@leetcode.com” 会转发到同一电子邮件地址。
如果在 本地名 中添加加号（'+'），则会忽略第一个加号后面的所有内容。这允许过滤某些电子邮件。同样，此规则 不适用于域名 。

例如 m.y+name@email.com 将转发到 my@email.com。
可以同时使用这两个规则。

给你一个字符串数组 emails，我们会向每个 emails[i] 发送一封电子邮件。返回实际收到邮件的不同地址数目。

## 示例：

```java
输入：emails = ["test.email+alex@leetcode.com","test.e.mail+bob.cathy@leetcode.com","testemail+david@lee.tcode.com"]
输出：2
解释：实际收到邮件的是 "testemail@leetcode.com" 和 "testemail@lee.tcode.com"。

输入：emails = ["a@leetcode.com","b@leetcode.com","c@leetcode.com"]
输出：3
```

## 代码：
```java
class Solution {
    public int numUniqueEmails(String[] emails) {
        Set<String> emailSet = new HashSet<String>();
        for (String email : emails) {
            //获取到'@'所处的位置
            int i = email.indexOf('@');
            //substring(0,i)获取'@'之前的字符串
            //然后根据'+'号分割，由此分割成两部分，需要的是第一部分，故有[0]
            //注意： . 、 $、 | 和 * 等转义字符，必须得加 \\。
            String local = email.substring(0, i).split("\\+")[0]; // 去掉本地名第一个加号之后的部分
            //需要把'.'替换为空，即去掉'.'
            local = local.replace(".", ""); // 去掉本地名中所有的句点
            emailSet.add(local + email.substring(i));
        }
        return emailSet.size();
    }
}
```
