本文中的关键词“MUST|必须”、“MUST NOT|禁止”、“REQUIRE|要求”、“SHALL|将要”、“SHALL NOT|不会”、“SHOULD|应该”、“SHOULD BOT|不应该”、“RECOMMENDED|建议”、“MAY|可能”和“OPTIONAL|可选”的详细描述可参考RFC 2119。
## 1.概述
本章制定了从文件路径来实现自动加载类的规则。这个规则十分适配，可以作为其他自动加载规则的补充，包括PSR-0。本章还介绍了如何设置文件路径才能被自动加载。

## 2.详细说明

1. 这里说的术语“类”包括普通类、接口、特性和其他相似的结构。
2. 一个合格的类名应该是如下结构的： `\<命名空间>(\<子命名空间>)*\<类名>`
  
  * 合格的类名**必须**有以组织命名的顶级命名空间
  * 合格的类名**可能**有一个或多个子命名空间
  * 合格的类名**必须**有一个终止类名
  * 合格的类名任意部分中的下划线都没有特殊含义
  * 合格的类名**可以**由任意大小写字母组成
  * 所有类名都是区分大小写的
  
3. 当加载一个符合上述所说命名规则合格的类时：

 * 合格的类去掉最前面的命名空间分隔符，前面连续的一个或多个命名空间和子命名空间，作为“命名空间前缀”，其必须与至少一个“文件基目录”相对应；
 * The contiguous sub-namespace names after the “namespace prefix” correspond to a subdirectory within a “base directory”, in which the namespace separators represent directory separators. The subdirectory name MUST match the case of the sub-namespace names.
 * 结尾类名以文件名加.php命名。文件名**必须**和类名一致。
 
4. 自动加载起**禁止**抛出异常，**禁止**有任何级别的报错，并且**不应该**有返回值

## 3.实例
下表展示了符合规范完整类名、命名空间前缀和文件基目录所对应的文件路径。

| 完整类名 | 命名空间前缀 | 文件目录 | 文件名 |
| --- | --- | --- | --- |
| \Acme\Log\Writer\File_Writer | Acme\Log\Writer | ./acme-log-writer/lib/ | ./acme-log-writer/lib/File_Writer.php |
| \Aura\Web\Response\Status | Aura\Web | /path/to/aura-web/src/ | /path/to/aura-web/src/Response/Status.php |
| \Symfony\Core\Request | Symfony\Core | ./vendor/Symfony/Core/ | ./vendor/Symfony/Core/Request.php |
| \Zend\Acl | Zend | /usr/includes/Zend/ | /usr/includes/Zend/Acl.php |

更多关于本规范的实例可参阅[相关实例](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader-examples.md)

注意：实例并不属于规范的一部分，且随时会有所变动。
