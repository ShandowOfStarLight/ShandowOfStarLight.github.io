---
title: mysql重复数据删除
author: kai
date: 2022-11-17
category: spring
layout: post
---

## 用distinct联合去重

先用distinct把数据查出来然后将查出来的数据导入新表

## 使用窗口函数限制row_number()=1

用法
select xxx from (select xxx, row_number()over(partition by xxx) r from users) as q where r = 1;

## 使用窗口函数删除row_number()>1

用法
DELETE FROM users   WHERE id in (SELECT id, ROW_NUMBER () Over (PARTITION BY xxx ORDER  BY id) as r from users) q WHERE r > 1);

## grou by去重

对重复字段联合分组
