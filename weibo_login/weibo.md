## 微博第三方登录教程
____________
### 1. OAuth2.0协议
![OAuth2.0](http://osawa5fm6.bkt.clouddn.com/fef669f1ee8cad4438cc4ddbe2642df5.png)

### 2. 实现第三方登录的 前置条件
- 一个微博账号
- 可以供外网访问的web服务器（腾讯云，阿里云基本一年估计300元左右，如果是在读大学生还可以领取优惠，我之前在读大学的时候买的是腾讯云服务器，送了一个一年的.cn域名，每个月1元）。
- 你的域名需要通过备案（如果是国外的服务器与域名就不需要备案了）

### 3. AppKey和AppSecret申请
- 登录新浪微博开放平台，填写相关信息，通过开发者审核。地址：http://open.weibo.com
- 创建应用（此处是网站应用）：      
3.1 进入开放平台网站首页，点击网站接入，如图。
![weibo-index](http://osawa5fm6.bkt.clouddn.com/588e0d9fd3cb5f6fda59c2ae3b21aac0.png)
3.2 点击“立即接入”，填写应用名称：
![application-name](http://osawa5fm6.bkt.clouddn.com/761defa7881fcf117b69824ea3701932.png)
3.3 点击创建值周就会成功得到一个应用，应用就包含了Appkey和AppSecret。
![yanshi](http://osawa5fm6.bkt.clouddn.com/65396424790519d04a74899c44aa839c.png)
3.4 你还需要完善网站信息，主要是网站地址，后续回调验证需要用到。
![](http://osawa5fm6.bkt.clouddn.com/09548ba75515d28c3a2e1e78332abfb3.png)

### 4. 获取官方SDK
4.1 依次点击1,2,3
![sdk](http://osawa5fm6.bkt.clouddn.com/a73df12024a4501546ccfb4430ec4e30.png)
4.2 进入github下载资源
- 地址：https://github.com/xiaosier/libweibo
- 点击下载
![](http://osawa5fm6.bkt.clouddn.com/72c4e484776d31988f1bdc64e37677dc.png)

### 5. 项目配置
- 将sdk中的saetv2.ex.class.php文件拷贝到项目根目录下面。
- 创建config.php，并填写以下内容：
```php
<?php
header('Content-Type: text/html; charset=UTF-8');
define( "WB_KEY" , 'XXXXX' );
define( "WB_SEC" , 'xxxxxxxxxxxxxxxxx' );
define( "WB_CALLBACK_URL" , 'http://test2.aiboms.cn/callback.php' );

function debug($va1,$dump=false,$exit=true){
//自动获取调试名称
    if($dump){
        $func='var_dump';
    }else{
        $func=(is_array($va1)||is_object($va1))? 'print_r':'printf';
    }
// 输出到html
    echo '<pre>';
    $func($va1);
    echo '/<pre>';
    if($exit) exit;
}
```
- 添加入口文件index.php
```php
<html>
<head>
	<title>微博登录</title>
</head>
<?php $access_token = $_COOKIE['access_token']; ?>
<?php if (isset($access_token)) { ?>
	已登录
<?php } else { ?>
	<a href="wb_login.php">
		<img src="weibo_login.png"/>
	</a>
<?php } ?>
</html>
```
- 微博第三方登陆类
```php
<?php
require_once "saetv2.ex.class.php";
require_once "config.php";

$WB = new SaeTOAuthV2(WB_AKEY, WB_SKEY);
$redirect_uri = $WB->getAuthorizeURL(WB_CALLBACK_URL);
header("Location:".$redirect_uri);
```
- 调用接口（此处以发微博为例）
```php
<?php
<?php
require_once "saetv2.ex.class.php";
require_once "config.php";
$WB = new SaeTClientV2(WB_AKEY, WB_SKEY, $access_token);
//发送微博
$WB->update("欢迎访问南人的独立博客：code.aiboms.cn");
?>
```
> 具体其他接口请查看：http://open.weibo.com/wiki/%E5%BE%AE%E5%8D%9AAPI

### 实例代码
> 链接：https://pan.baidu.com/s/1t5tzX6X3ar8qVyb-T75QBQ
