---
layout: post
title: SQL基本操作
categories: article
author: shiyi
tags:
  - SQL
image:
  feature: SQL.png
---

## DML(数据操纵语言)

-   SELECT - 从数据库表中获取数据
-   UPDATE - 更新数据库表中的数据
-   DELETE - 从数据库表中删除数据
-   INSERT INTO - 向数据库表中插入数据

## DDL(数据定义语言)

-   CREATE DATABASE - 创建新数据库
-   ALTER DATABASE - 修改数据库
-   CREATE TABLE - 创建新表
-   ALTER TABLE - 变更（改变）数据库表
-   DROP TABLE - 删除表
-   CREATE INDEX - 创建索引（搜索键）
-   DROP INDEX - 删除索引

## SQL表约束

-   NOT NULL 不接受 NULL 值,如果不向字段添加值，就无法插入新记录或者更新记录。
-   UNIQUE 唯一标识
-   PRIMARY KEY 主键
-   FOREIGN KEY 外键
-   CHECK 限制列中的值的范围
-   DEFAULT 设置默认值
