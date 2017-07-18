### PHP编码规范

### 文件字符编码
统一使用`UTF-8`,无BOM头，禁止使用`GBK,ASCII,ISO8859`等字符编码


#### 文件名命名

#### 标记
文件第一行使用`<?php`开始，

文件结束时不使用 `?>`

#### 文件版权
```php
<?php

/*********************************************************************
 *            Copy Right (c) 2017 TSoftware Co., Ltd.                
 *
 * Author:          tsoftware<admin@yantao.info>
 * Date:            2017-7-18 11:49:29
 * Description:     Basic function description
 * Version:         1.0.0.170718-alpha
 * History:
 *      tsoftware<admin@yantao.info> 2017-07-18 Add user_name field
 *********************************************************************/
```

#### 命名空间
基于命名空间需要符合PSR-4

`capsheaf/src/Fundation/Container/ClassName.php`

```php
//上方空出一行
namespace TSoftware\Call;
//此处空出一行
use TSoftware\Exception\MethodProphecyException;
use TSoftware\Container\MethodProphecy;
use TSoftware\Container\ObjectProphecy;
//此处距离下方代码空出一行
```

### 命名规范
#### 变量
使用匈牙利+驼峰法定义，不能使用下划线分割的变量，`mixed`类型变量直接使用驼峰法
```php
$sUserName = 'Cindy';
$hFile = fopen('file.dat');
$nSize = 4096;
$userInfoObj = new UserInfo();

function funcReturnMixedVal(){
    return $returnVal;
}

```
#### 类
类名使用大写字符开头的驼峰法表示，中括号放在类名定义的下一行
```php
class ClassName 
{

}
```

#### 常量
##### 全局常量
define的常量名使用下划线分割的大写字母表示，禁止使用小写字母

一般全局常量
```php
define('ROOT_ABS_PATH', __DIR__);
```
命名空间下的常量
```php
namespace TSoftware
define('SCOPED_ROOT_ABS_PATH', __DIR__);
```
##### 类常量
```php
class ClassName
{
    const constant = 'constant value';
}
```


### 注释

#### 普通注释

```php
//单行注释

/* 
 * 多行注释
 * 多行注释
 */
 
```

#### 函数注释

```php
/**
 * 添加一个用户
 * @param string $userName 用户名
 * @param int $age 用户年龄
 * @param string $age 电话
 * @return string|boolean|class
 */
public function AddUser($userName, $age, $tel = '10086')
{
    return $ret;
}

```


### 语言结构

#### if

```php
if ((condition1) || (condition2)) {
    action1;
} elseif ((condition3) && (condition4)) {
    action2;
} else {
    defaultaction;
}
```

应将多个长的if条件拆分到多行
```php
if ($condition1
    || $condition2
    && $condition3
    && $condition4
) {
    //code here
}
```

或者可以将第一个条件与其它条件对齐
```php
if (   $condition1
    || $condition2
    || $condition3
) {
    //code here
}
```

应将复杂的if条件集合移动到if之前进行处理
```php
$needSendMail = ($condition1 || $condition2);
$needSendSms = ($condition3 && $condtion4);
if ($needSendMail || $needSendSms) {
    //code here
}
```

#### switch

switch的条件分支应该整体缩进，条件分支最后空出一行（最后一个条件分支除外）
```php
switch (condition) {
    case 1:
        action1;
        break;
    
    case 2:
        action2;
        break;
    
    default:
        defaultaction;
        break;
}
```

#### 三元运算符

三元运算符用于变量赋值时
```php
$a = $condition1 && $condition2
    ? $foo : $bar;

$b = $condition3 && $condition4
    ? 'foo_man_this_is_too_long_what_should_i_do'
    : 'bar';
```
### 缩进和行宽

#### 缩进
使用四个空格，禁止使用`tab`或者其它宽度的缩进

```php
function indenting(){
    $obj = new ClassName();//4空格缩进
    $obj->doCallback(function (){
        echo 'FUNC';//4空格缩进
    });
}

```

#### 行宽
为了增加可读性，行宽原则上为75-80个字符左右，超出应考虑换行

```php
if ($condA < 10 || $condB < 10 || $condC < 10 || $condD || $condE < 10 
    || $condF < 10 || $condG < 10 || $condH < 10)
```

但最后出现的为字符串除外
```php
$longString = 'You are strongly encouraged to always use curly braces even in situations where they are technically optional. Having them increases readability and decreases the likelihood of logic errors being introduced when new lines are added. ';
```

### 字符串
#### 字符串定义
常规字符串使用单引号包含, 只有在字符串中出现单引号的情况下才使用双引号
```php
$str = 'I am a string.';

$str = "Don't use double qoute if not necessary";
```
#### 字符串拼接
拼接字符串时不能在双引号包含的字符串中嵌入变量，使用单独的`.`号连接。
```php
$content = 'Contents';
$str = 'Prefix '.$content.' Surfix';
```

### 函数
#### 函数调用
函数调用时函数名称和起始括号间不能有空格:
```php
$var = foo($bar, $baz, $quux);
```
连续同类型的函数调用可以插入空格字符保持对齐,来增强可读性:
```php
$short         = foo($bar);
$long_variable = foo($baz);
```
当变量长度差异超过8字符后，上述规则不适用:
```php
$short = foo($bar);
$thisVariableNameIsVeeeeeeeeeeryLong = foo($baz);
```

连续的同一个函数调用可以添加空格字符将参数对齐:
```php
$this->callSomeFunction('param1',     'second',        true);
$this->callSomeFunction('parameter2', 'third',         false);
$this->callSomeFunction('3',          'verrrrrrylong', true);
```

Author: <http://www.yantao.info/>

Copy Right (c) 2017 WWW.YANTAO.INFO