---
layout: post
title: "腾讯（后台开发日常实习一面）"
date: 2026-02-19
categories: [面经]
tags: [腾讯, 面经, 后台开发]
---

## 算法题

**LC121. 买卖股票的最佳时机**（easy）

面试官要求用动态规划解决。

### 解法思路

```java
public int maxProfit(int[] prices) {
    if (prices == null || prices.length == 0) return 0;
    int minPrice = prices[0];
    int maxProfit = 0;
    for (int i = 1; i < prices.length; i++) {
        minPrice = Math.min(minPrice, prices[i]);
        maxProfit = Math.max(maxProfit, prices[i] - minPrice);
    }
    return maxProfit;
}