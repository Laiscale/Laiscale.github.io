---
title: LeetCode_496-下一个更大元素I
date: 2023-03-29 16:13:29
categories: 
- LeetCode
tags: 
- 哈希表
- 字符串
---

## 题目链接

[LeetCode_496-下一个更大元素I](https://leetcode.cn/problems/next-greater-element-i/)

## 关键词
哈希表， 字符串

## 题目概述

nums1 中数字 x 的 下一个更大元素 是指 x 在 nums2 中对应位置 右侧 的 第一个 比 x 大的元素。

给你两个 没有重复元素 的数组 nums1 和 nums2 ，下标从 0 开始计数，其中nums1 是 nums2 的子集。

对于每个 0 <= i < nums1.length ，找出满足 nums1[i] == nums2[j] 的下标 j ，并且在 nums2 确定 nums2[j] 的 下一个更大元素 。如果不存在下一个更大元素，那么本次查询的答案是 -1 。

返回一个长度为 nums1.length 的数组 ans 作为答案，满足 ans[i] 是如上所述的 下一个更大元素 。

## 示例：

```java
输入：nums1 = [4,1,2], nums2 = [1,3,4,2].
输出：[-1,3,-1]
解释：nums1 中每个值的下一个更大元素如下所述：
- 4 ，用加粗斜体标识，nums2 = [1,3,4,2]。不存在下一个更大元素，所以答案是 -1 。
- 1 ，用加粗斜体标识，nums2 = [1,3,4,2]。下一个更大元素是 3 。
- 2 ，用加粗斜体标识，nums2 = [1,3,4,2]。不存在下一个更大元素，所以答案是 -1 。

输入：nums1 = [2,4], nums2 = [1,2,3,4].
输出：[3,-1]
解释：nums1 中每个值的下一个更大元素如下所述：
- 2 ，用加粗斜体标识，nums2 = [1,2,3,4]。下一个更大元素是 3 。
- 4 ，用加粗斜体标识，nums2 = [1,2,3,4]。不存在下一个更大元素，所以答案是 -1 。
```

## 代码：
```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        //nums1 是 nums2 的子集
        HashMap<Integer, Integer> map = new HashMap<>();
        int n1 = nums1.length;
        int n2 = nums2.length;
        int[] ans = new int[n1];
        //可以记录nums2中：将每一个数字作为key，位置下标为value
        for(int m = 0; m < n2; m++) {
            map.put(nums2[m], m);
        }
        //遍历nums1，获取每一个数字
        for(int i = 0; i < n1; i++) {
            //然后从map中获取该数字对应的下标（该下标对应的是nums2中该数字的下标）
            int k = map.get(nums1[i]);
            //做该判断是因为如果k为nums2的最后一个数字的话，下方的j=k+1就会越界
            //所以如果该数字如果为nums2的最后一个数字的话，name他一定没有比它大的下一个元素，返回-1。
            if(k == n2 - 1) ans[i] = -1; 
            for(int j = k + 1; j < n2; j++) {
                if(nums2[j] > nums2[k]) {
                    ans[i] = nums2[j];
                    break;
                }
                if(j == n2 - 1 && nums2[j] <= nums2[k]) {
                    ans[i] = -1;
                }
            }
        }
        return ans;
    }
}
```
