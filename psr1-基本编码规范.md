# 基本编码规范

本章规范制定了标准编码元素规则，用以确保共享php代码之间的高互通性。

本文中的关键词“MUST|必须”、“MUST NOT|禁止”、“REQUIRE|要求”、“SHALL|将要”、“SHALL NOT|不会”、“SHOULD|应该”、“SHOULD BOT|不应该”、“RECOMMENDED|建议”、“MAY|可能”和“OPTIONAL|可选”的详细描述可参考[RFC 2119](http://www.ietf.org/rfc/rfc2119.txt)。

## 1. 总览
* 文件**必须**以<?php或<?=标签开始
* 文件编码**必须**为不带BOM的UTF8
* Files SHOULD either declare symbols (classes, functions, constants, etc.) or cause side-effects (e.g. generate output, change .ini settings, etc.) but SHOULD NOT do both. （翻译不出来，怎么感觉原文就有问题……）
* 命名空间和类必须遵循PSR-0和PSR-4的“自动加载”标准。（译者注：PSR-0已经废弃）
* 文件名**必须**以`StudlyCaps`形式命名
* 类常量**必须**所有字母必须全部大写，单词间用下划线分隔
* 方法名必须以`camelCase`形式命名

## 2. 文件
### 2.1. php标签
php代码**必须**用长标签`<?php ?>`或者短标签`<?= ?>`，禁止使用其他自定义的标签。
### 2.2. 字符编码
php代码**必须**使用不带BOM的UTF8编码。
### 2.3. 副作用
一个文件**应该**要么只做不产生副作用的操作如定义类、函数、常量等，要么只做会产生副作用的逻辑处理操作，但是不应该同时包含这两者。
副作用是指
