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
### 2.3. 从属效应
一个文件**应该**要么只做不产生从属效应的操作如定义类、函数、常量等，要么只做会产生从属效应的逻辑处理操作，但是不应该同时包含这两者。

直接声明类、函数、变量是不会产生从属效应的，从属效应可以由引入一个文件产生。

从属效应包括但不仅限于：生成输出、直接使用`require`或`include`、连接外部服务、通过ini_set修改php配置、抛出错误或异常、修改全局变量静态变量、读文件写文件等。

下面是一个我们应该避免的即有申明又产生从属效应的文件反例：

```
<?php
// 从属效应:更改了php配置
ini_set('error_reporting', E_ALL);

// side effect: 引入了一个文件
include "file.php";

// 从属效应：生成输出
echo "<html>\n";

// 申明函数
function foo()
{
    // 函数体
}
```

下面是一个我们提倡的只有申明操作不包含从属效应的证明例子：

```
<?php
// 申明
function foo()
{
    // function body
}

// 条件什么不属于从属效应
if (! function_exists('bar')) {
    function bar()
    {
        // 函数体
    }
}
```

## 3.命名空间和类名

命名空间和类必须遵循PSR-0和PSR-4“自动加载”原则。

这意味着每个类要有一个它自己的文件，并且每个类要在一个至少一级（顶级的组织名称）的命名空间内。

类名**必须**申明成`StudlyCaps`形式。

php5.3及之后的版本**必须**使用正式的命名空间。

例如：

```
<?php
// PHP 5.3 及以上:
namespace Vendor\Model;

class Foo
{
}
```

php5.2之前版本的类名**应该**使用伪命名空间的写法，约定俗成使用顶级的组织名称如 Vendor_为类前缀。

如：

```
<?php
// PHP 5.2.x and earlier:
class Vendor_Model_Foo
{
}
```


## 4.类常量、属性、方法
类包含所有的普通类(classes)、接口(interfaces)和特性(traits)。

### 4.1.常量

常量**必须**所有字母都大写，单词间用下划线分割。 如：

```
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```

### 4.2. 属性
类的属性可以用`$StudlyCaps`、`$camelCase`、 `$under_score`形式都行，本规范不做强制统一。

但是无论采用哪种形式，在一个范围内应该是统一的。这个范围可以是整个团队、整个包、整个类、整个方法。

### 4.2. 方法
方法名**必须**申明成`camelCase()`小写开头驼峰形式。



