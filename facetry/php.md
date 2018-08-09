#### 1.strlen()与mb_strlen()
- strlen统计单字节字符串的字符
- mb_strlen统计多字节的字符，但是需要制定编码和开启mbstring扩展
```php
<?php
//mb_strlen(),strlen()
$str_cn = "我是中国人";
echo "mb_strlen:".mb_strlen($str_cn,'gbk');
echo "<hr/>";
echo "mb_strlen:".mb_strlen($str_cn,'utf8');
echo "<hr/>";
echo "strlen:".strlen($str_cn);
```

#### 2.explode与preg_split
- explode与preg_split的唯一区别在于preg_split可以使用正则表达式来分割成数组。

#### 3.php中全局变量(9个)
- $_SESSION
- $_COOKIE
- $_GET
- $_POST
- $_SERVER
- $_ENV
- $_FILES
- $_REQUEST
- $GLOBALS


#### 4.不使用第三个变量就交换两个变量的值
- 使用list方法进行交换
```php
<?php
$a = 1;
$b = 2;
echo "a:".$a."   b:".$b;
echo "<hr/>";
list($a, $b) = array($b, $a);
echo "a:".$a."   b:".$b;
```
- 先组成数据
```php
<?php
$a = $a."-".$b;
$a = explode('-', $a);
echo $b = $a[0];
echo $a = $a[1];
```

#### 5.使用最少的代码得到三个数中的最大值
```php
<?php
function getMax($a, $b, $c){
  return $a > $b ? ($a>$c ? $a:$c):($b>$c?$b:$c)
}
```

#### 6.比较PHP中echo, print, print_r()的区别
- echo是一个语句，是一种语言结构，并不是函数，可以输出多个字符串
- print严格意义来说也不是函数，只是一种数据结构
- print_r是一个函数，可以输出数组，对象等复杂结构


#### 7.cookie既然是保存在浏览器的，它是如何传递到服务器的
- 使用http请求体传递到服务器中。


#### 8.get与post的区别
- get对于浏览器回退是无害的，但post会再次发送请求
- get可以用于浏览器标签收藏，但是post不行
- get和post本质上都是 tcp/ip请求，但是get只有一个tcp数据包（get把header和data一同传递），post会发送两个数据表（先发送一个header会得到100响应，然后再发送data数据表）。
- get会被浏览器主动缓存，但是post不行，除非手动设置
- get会把参数暴露在url中，post会把参数放置在request body中，所以相对而言post可能相对更安全。
- get基本上只支持url编码,post则支持多种编码格式。

#### 9.将1234567890转换成1,234,567,890
```php
<?php
function chuan($str){
  //首先利用strrev把字符串反转  0987654321
  $str = strrev($str);
  //然后利用chunk_split按照字符串长度切割 098,765,432,1
  $str = chunk_split($str,3,',');
  //其次再次把字符串反转  ,1,234,567,890
  $str = strrev($str);
  //最后把最前面的‘，’去除
  $str = ltrim($str,',');

  return $str;
}
```

#### 10.将www.baidu.com转化成moc.udiab
```php
<?php
$str = "www.baidu.com";
$str =str_replcae('www','',$str);
echo strrev($str);
```

#### 11.$_SERVER相关
- 当前脚本的名称: $_SERVER['SCRIPT_NAME']
- 上一个页面的URL: $_SERVER['HTTP_REFERENCE']
- 客户端IP:$_SERVER['REMOTE_ADDR']
- 服务器端IP:$_SERVER['SERVER_ADDR']


#### 12.设计一个函数，按照指定的字段排序
```php
<?php
function sort_array_by_column($arr,$column,$type='asc'){
      $new_arr = array();
      foreach($arr as $v){
          $new_arr[$v[$column]] = $v;
      }

      if($type == 'asc'){
          ksort($new_arr);
      }else{
          krsort($new_arr);
      }
      return $new_arr;
  }

  $arr = [
    ['id'=>1,'name'=>'zhangliang','age'=>23],
    ['id'=>6,'name'=>'tangying','age'=>27],
    ['id'=>3,'name'=>'houyu','age'=>24]
    ];

echo "<pre>";
print_r(sort_array_by_column($arr,'id'));
```

#### 13.PHP运用场景
- 服务器端脚本
- 命令行脚本
- 桌面程序


#### 14.写一个函数将open_a_door改变成OpenADoor
```php
<?php
function uper($str){
  $arr = explode('_',$str);
  $arr = array_map('ucfirst',$arr);
  echo implode('',$arr);
}
```
#### 15.一些重要的字符串函数
```php
$str = "kavinbright@163.com163";
```
- substr_count($str, 'a')统计字符串中a出现的次数。
- strrev()将字符串反转
- strstr($str,'@'); 返回指定字符串第一次出现的位置到字符剩余的部分；# 163.com163
- strlen()统计（单字节）字符串长度
- mb_strlen()统计多字节字符串长度
- strpos($str,'163');字符（串）第一次出现的位置
- substr($str,start,length)返回从start开始length长度的字符串

> 一些重要的数组函数
- array_map('function',$arr);数组中每一个值都作为function的参数执行一遍function
- array_rand($arr, n=1);随机返回数组中n(默认为1)个键名组成的数组

#### 16.PHP中global与$_GLOBALS的区别
- Global的作用是定义全局变量,但是这个全局变量不是应用于整个网站,而是应用于当前页面,包括include或require的所有文件。
- global可以将外部变量引入函数内部作为全局变量使用,函数内对全局变量的操作可以改变变量的值。
```php
<?php
$a = 12;
function get_count(){
	global $a;
	echo $a++;
}
get_count(); // 12
echo $a;     // 13
```
- global不能用来在函数外部定义全局变量
```<?php
global $a = 12;
function get_count(){
	echo $a;
}
get_count(); //报错
```
- $_BLOBALS是PHP内置的超全局变量，在整个Application中可以使用。
- $_BLOBALS的用法：$a = 1;$_BLOBALS['a'];

#### 17.改变数据类型的几种方法
```php
<?php
$a = "123";
(int)$a;
intval($a);
settype($a,'int')
```

#### 18.PHP中接口与抽象类的区别
- 抽象类不能够被实例化，只能被其他类继承。
- 接口可以实现多继承
- 抽象类abstract.接口interface
- 继承抽象类extends,实现接口implements
- 抽象类侧重于是什么，接口侧重于干什么
- 接口中的方法和属性都是public，而抽象类中可以有public,protected,private


#### 19.__autoload运行机制
- 魔术方法使用的条件是类文件的文件名必须和类名保持一致
- 当实例化某个类的时，如果没有包含类文件就会自动执行__autoload()函数，通过类名找到文件路径，如果该路径下趋势存在该文件则include或者require该类文件，然后实例化；如果没有该类文件则报错。

#### 20.静态和伪静态的区别
- 纯静态是真是存在的html文件，不需要向数据库查询得到数据
- 纯静态不容易受到黑客攻击
- 但是大量的静态网页存在，会提高网站成本
- 更新不方便
- 伪静态实质上是利用htaccess等技术实现路由重写
- 伪静态隐藏了真实的URL地址，所以相对安全
- 伪静态是每次其请求的时候生成，会对cpu造成压力
- 伪静态可以被搜索引擎收录

#### 21.博客无线分类的原理
- 创建表
```sql
CREATE TABLE category(
  cat_id smallint unsigned not null auto_increment primary key comment '类别 ID',
  cat_name VARCHAR(30) NOT NULL DEFAULT '' COMMENT '类别名称',
  parent_cat_id SMALLINT UNSIGNED NOT NULL DEFAULT 0 COMMENT '类别父 ID'
)engine=MyISAM charset=utf8;
```
```php
function tree($arr, $pid, $level_id){
  $list = array();
  foreach($arr as $v){
    if($v['parent_id'] === $pid){
      $v['level_id'] = $level_id++;
      $list[] = $v;
      tree($arr,$v['parent_id'], $level_id);
    }
  }
}
```
