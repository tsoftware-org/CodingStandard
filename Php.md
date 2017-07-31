## PHP编码规范


#### 文件字符编码

* 统一使用`UTF-8`，无BOM头，禁止使用`GBK、GB2312、GB18030、ASCII、ISO8859`等字符编码。
* 建议优先使用`LF`而不是`CRLF`作为换行符。


#### 文件名命名

* 全部文件名使用驼峰法`UpperCamelCase.php`命名。
* 文件名与文件中的类需要对应，如`ClassName`类，文件名则为`ClassName.php`。
* 每个对应文件名的文件仅能在其中定义一个类或者一个接口，严禁在同一个文件中定义多个。
* 单元测试代码必须与被测的类名相对应，如`ClassNameTest.php`。


#### 标记

* 在PHP文件第一行使用`<?php`开始标记，禁止使用短标记。

* 除模板外，代码应在该标记后换行书写，模板中可以使用`<?= ?>`来直接输出单个变量值。

* 任何纯PHP代码文件结束时不应使用 `?>`结束标记，其它一般情况使用该标记应换行书写，文件尾的结束标记`?>`之后必须换行。

```php

<html>
    <body>
        <p>Not a simple php file.</p>
    </body>
<?php
//换行
    echo $sFooterHtml;
    echo '</html>';
//文件结束时使用结束标记后必须换行(LF/CRLF)
?>

```





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
Author为文件的创建者或者Version主版本作者。

Version主版本为重大更新时递增，次版本为较大修改时递增，小版本为基本修改时递增，时间版本为此版本的修改时间。


#### 命名空间

* 文件名应该如：`TSoftware/src/Fundation/Container/ClassName.php`的形式。

* `use`只能用在命名空间`namespace`声明之后，中间空出一行书写。

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

建议使用基本类型限定+驼峰法的`typeUpperCamelCase`定义，不使用下划线分割的变量，存在转换的`mixed`类型变量直接使用驼峰法`lowerCamelCase`:

基本限定前缀规则:
* `s`表示字符串，如`sUserName`。
* `n`表示数字，包括integer，float/double，如`nCount，nSize，nOffset，nWeight`。
* `h`表示句柄，包括文件句柄，mysql等资源句柄，如`hFile，hMysql`。
* `arr`表示数组，如`arrUsersList`。
* `className`表示类实例化的对象，如`userInfoObj，fooBarInstance`。
* 要发生动态类型转换的变量不加前缀，使用`lowerCamelCase`，但是应该避免过多转换性赋值操作。

```php
$sUserName = 'Cindy';//字符串
$hFile = fopen('file.dat');//句柄
$nSize = 4096;//数字变量
$userInfoObj = new UserInfo();//对象

function funcReturnMixedVal(){
    return $returnVal;//可能为多种类型的变量
}

```

变量的命名应该能够基本自解释，不能为了精简导致不能识别变量的含义，为了它的意义更清晰可以长一点。

正确的例子:
```php
$singletonObjectsRegistry
$arrArgumentsLists
$sALotOfHtmlCode
```
错误的例子:
```php
$objRgstry
$argArr
$cx
```
> 例外是`for，while`循环中使用的`$i，$j，$k`变量。


#### 全局变量

```php
g_arrInstances = array();
g_nCount = 1024;
```


#### 类

* 类名使用大写字符开头的驼峰法`UpperCamelCase`表示，中括号放在类名定义的下一行。
* 类名必须为名词，不能为形容词，动词等。
* 不能直接实例化的抽象类必须以`Abstract`开头。
* 类命名必须符合实际含义，去掉命名空间后，还能准确表达类名的字面含义。

```php
class ClassName 
{

}
```

不好的例子:

|完全限定名|类名|备注 |
|----------|:---:|---:|
|\TSoftware\Flow\Session\Php        |Php        |The class is not a representation of PHP|
|\TSoftware\Cache\Backend\File 	    |File 	    |The class doesn’t represent a file!|
|\TSoftware\Flow\Session\Interface 	|Interface 	|Not allowed, “Interface” is a reserved keyword|
|\TSoftware\Foo\Controller\Default 	|Default 	|Not allowed, “Default” is a reserved keyword|
|\TSoftware\Flow\Objects\Manager 	|Manager 	|Just “Manager” is too fuzzy|

好的例子:

|完全限定名|类名|备注 |
|----------|:---:|---:|
|\TSoftware\Flow\Session\PhpSession 	        |PhpSession 	    |That’s a PHP Session
|\TSoftware\Flow\Cache\Backend\FileBackend 	    |FileBackend 	    |A File Backend
|\TSoftware\Flow\Session\SessionInterface 	    |SessionInterface 	|Interface for a session
|\TSoftware\Foo\Controller\StandardController   |StandardController |The standard controller
|\TSoftware\Flow\Objects\ObjectManager 	        |ObjectManager 	    |“ObjectManager” is clearer


#### 类成员变量

* 类成员变量，统一使用`$m_`前缀，置于常量定义之后，排序为`private，protected，public`，必要时进行对齐，成员变量初始化为null值时使用小写`null`，不能使用`NULL`。
* 禁止使用`var`定义变量，禁止定义以下划线`_`开头的变量名。

```php
class ClassName
{
    const       CONST_VAL   = 4096;//const常量放到顶部
    private     $m_hMysql   = null;
    protected   $m_sLink    = 'localhost:3306';
    public      $m_hImpl    = null;
}
```


#### 常量

##### 全局常量

* define的常量名使用下划线分割的大写字母表示，禁止使用小写字母，禁止定义大小写不敏感的常量。

* PHP常量`true, false, null`必须使用小写，禁止使用`True, TRUE, False, FALSE, NULL`等形式。

* 一般全局常量定义使用全大写字符，单词之间使用下划线，使用缩写要表意清楚。

```php
define('ROOT_ABS_PATH', __DIR__);
```

* 命名空间下的常量

```php
namespace TSoftware
define('SCOPED_ROOT_ABS_PATH', __DIR__);
```


##### 类常量

类常量置于成员变量和成员函数声明之前，使用下划线分隔的大写字母表示:

```php
class ClassName
{
    const CONSTANT_VALUE    = 'constant value';
    const BUFFER_SIZE       = 4096;
}
```


### 注释

#### 普通注释

* 普通单行注释位于注释点上方或者右方。

```php
//上方单行注释
$sPositionAbove;

$sPositionRight;//右方单行注释
```

* 普通多行注释位于注释点上方。

```php
/* 
 * 多行非DOC注释
 * 多行非DOC注释
 */
$sPositionAboveMulti; 
```

* 禁止使用Perl/Shell风格的`#`注释。


#### 函数注释

```php
/**
 * 添加一个用户的DOC注释
 * @param string $sUserName 用户名
 * @param int $nAge 用户年龄
 * @param string $sTel 电话
 * @return string|integer|float|boolean|class|resource 阐明返回的类型，若为API方法，需要在下方标记上返回的样本数据
 */
public function AddUser($sUserName, $nAge, $sTel = '10086')
{
    return $ret;
}

```


#### 类注释

```php
/**
 * 类注释
 */
class ClassName
{

}
```


#### 类成员变量和常量注释

```php
class ClassName
{
    /**
     * 常量的注释
     * @var string
     */
    const CONSTANT_VALUE    = 'constant value';
     
    /**
     * 成员变量的注释
     * @var int
     */
    protected $m_nTestedMethods = null;
}
```


### 语言结构

#### if

* `if`与整个判断条件之前的括号空一个空格，子判断条件与前后的逻辑操作符之间空一个空格，整个判断条件末尾的括号与中括号之间有一个空格。
* 严禁因为简短不使用中括号包含各个条件的执行语句。
* `elseif`连贯书写，禁止使用`else if`。

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
$bNeedSendMail = ($condition1 || $condition2);
$bNeedSendSms = ($condition3 && $condtion4);
if ($bNeedSendMail || $bNeedSendSms) {
    //code here
}
```


#### switch

* switch的条件分支应该整体缩进，每个条件分支最后空出一行（最后一个条件分支除外）
* 起始中括号与`switch`在同一行
* 若`case`子句完成后，需要继续执行下一个子句，需要明确注释提醒

```php
switch (condition) {
    case 1:
        action1;
        break;
    
    case 2:
        action2;
        //若没有break，而继续执行则需要进行提示
        
    case 3:
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

//遇到简单的字符串拼接操作时，可以放到同一行
$c = ($bOk ? 'Succees' : 'Failed').' Upload files';

```


#### foreach

```php
/** 
 * @var $product \TSoftware\SomePackage\Domain\Model\Product 
 */
foreach ($products as $key => $product) {
    $product->getTitle();
}
```


### 缩进和行宽

#### 缩进

使用四个空格，禁止使用`tab`或者其它宽度的缩进，使用tab键缩进时将IDE的tab设置为用4个空格字符表示。

```php
function indenting(){
    $obj = new ClassName();//4空格缩进
    $obj->doCallback(function (){
        echo 'FUNC';//4空格缩进
    });
}

```


#### 行宽
为了增加可读性，行宽原则上为80-120个字符左右，超出应考虑换行

```php
if ($condA < 10 || $condB < 10 || $condC < 10 || $condD || $condE < 10 || $condF < 10 || $condG < 10 || $condH < 10
    || $condI < 10 || $condJ < 10
) {
    //code here
}

```

但最后出现的为字符串除外

```php
$sLongString = 'You are strongly encouraged to always use curly braces even in situations where they are technically optional. Having them increases readability and decreases the likelihood of logic errors being introduced when new lines are added. ';
```


### 字符串

#### 字符串定义

常规字符串使用单引号包含，只有在字符串中出现单引号的情况下才使用双引号

```php
$sStr = 'I am a string.';

$sStr = "Don't use double qoute if not necessary";
```


#### 字符串拼接

拼接字符串时不建议在双引号包含的字符串中直接嵌入变量，使用单独的`.`号连接，禁止使用双引号中嵌入`$`变量来拼接字符串，`.`号之间不空格。

```php
$sContent = 'Contents';
//建议使用连接符拼接字符串和变量
$sStr = 'Prefix '.$sContent.' Surfix';

//简单的字符串可以直接使用双引号嵌入变量
$sStrSimple = "I am $sName";

//带有数组的变量禁止嵌入，且风格应统一
$sStrArr = 'My name is '.$arrInfo['name'].', age is '.$arrInfo['age'];
```

多行长的字符串拼接应该换行，每行中出现的变量应保持形式上的正确性:

```php
    $sParams  = 'action=login&token=MY_TOKEN'
    $sPostMsg = 'GET /index.php?'.$sParams
               .'Host: www.yantao.info'
               .'Cookies: PHPSID='.$sSidStored.'; HMAC=ccddd'
               .'User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:54.0) Gecko/20100101 Firefox/54.0';
```


### 函数

#### 函数/方法定义

* 函数定义时不能超过80行，40行为佳，超出80行考虑按功能点进行拆分，将子功能点放置到子函数中实现。
* 函数名使用`lowerCamelCase`驼峰法，私有函数禁止使用以`__`开头的命名方式。
* 函数名称应使用动词+名词或仅动词的形式，不能使用形容词等不能准确表示行为的函数名。
* 函数方法名称具有描述性，但同时应保持简洁。构造函数必须使用`__construct()`，禁止使用类名作为构造函数，且构造函数中不应该做不成功和抛出异常的事。 
* 函数主体的起始中括号应换行重新占一行开始书写，两个连续的函数定义之间使用两个空行分隔，函数代码中的不同逻辑块之间应该间隔一行。
* 类成员函数必须带有访问修饰符`public，protected，private`，严禁使用默认值。

```php
    public function myMethod()
    {
    
    }
```

* 类成员常量、变量定义的顺序为`const，private，protected，public`。
* 类成员函数定义的顺序为`public，protected，private`。
* 类构造函数置于公有函数定义集合的最前面，析构函数`__destruct()`置于公有函数定义集合的最后面。
* 类私有函数的定义应置于类成员函数集合的末尾。

```php
    private function someNiceMethodName()
    {
    
    }
```

* 若有多个成员函数修饰关键字，其顺序应为:

```php
    final public function funcName()
    final public static function funcName()
    abstract protected static function funcName()
```

* 虽然长但易于理解的函数名总比让人一头雾水的函数名强

```php
    function betterWriteLongMethodNamesThanNamesNobodyUnderstands()
    function singYmcaLoudly()
```


#### 函数调用

函数调用时函数名称和起始括号间不能有空格，参数之间以单个空格字符分隔:

```php
$var = foo($bar, $baz, $quux);
```

连续同类型的函数调用可以插入空格字符保持对齐，来增强可读性:

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


### 数组

#### 数组定义

* 一般情况下数组定义使用`array()`而不使用`[]`，在明确废弃对php5.4以下版本的兼容的情况下，请使用`[]`。
* 数组存在单个键值对，或者少量没有指定键名的子元素集合则可以在同一行书写。

```php
$arrOneKV = array('id' => 10086);
$arrFewVs = array('Gina', 'Tom', 'Cindy', 'Peter');
```

* 数组存在多个键值对形式的子元素，或者子元素较长时分行书写。

```php
$arrInstanceList = array(
    'foo'  => 'bar',
    'spam' => array(
        'author' => 'tsoftware',
        'name'   => 'Cindy',
    ),
);

//可以考虑对齐元素
$arrHttpRequests = array(
    'baidu'         => 'https://www.baidu.com',
    'google_map'    => 'http://map.google.com',
    'qq'            => 'http://qq.com',
)
```


Author: tsoftware <admin@yantao.info>

Copy Right (c) 2017 TSoftware.Org