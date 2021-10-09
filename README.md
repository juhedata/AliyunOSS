AliyunOSS
---------

```
    ___     __    _                                    ____    _____   _____
   /   |   / /   (_)   __  __  __  __   ____          / __ \  / ___/  / ___/
  / /| |  / /   / /   / / / / / / / /  / __ \        / / / /  \__ \   \__ \
 / ___ | / /   / /   / /_/ / / /_/ /  / / / /       / /_/ /  ___/ /  ___/ /
/_/  |_|/_/   /_/    \__, /  \__,_/  /_/ /_/        \____/  /____/  /____/
                    /____/
```

AliyunOSS 是阿里云 OSS 官方 SDK 的 Composer 封装，支持任何 PHP 项目，包括 Laravel、Symfony、TinyLara 等等。


## 更新记录
* 2021-10-09 `Release v2.2.5` 修复dispatch参数传递顺序问题(curlmulti:289)
* 2021-01-19 `Release v2.2.4` 修复文件大小写不一致问题
* 2020-10-29 `Release v2.2.3` 添加根据Bucket选择oss城市
* 2017-03-08 `Release v2.0.0` v2 发布，在 API 易用性上进行了大量优化
* 2016-09-12 `Release v1.3.5` 加入文件元信息的设置功能
* 2016-07-20 `Release v1.3.4` 加入文件元信息的获取功能
* 2016-01-31 `Release v1.3.2` 获取指定虚拟文件夹下的所有文件
* 2015-10-23 `Release v1.3` 增加删除、复制、移动文件功能
* 2015-08-07 `Release v1.2` 修复内存泄露 bug
* 2015-01-12 `Release v1.1` 增加内外网配置分离
* 2015-01-09 `Release v1.0` 完善功能，增加 Laravel 框架详细使用教程及代码

## 安装

安装有两种方式：

### ① 直接编辑配置文件

将以下内容增加到 composer.json：

```json
require: {
    "juhedata/aliyun-oss": "^2.2"
}
```

然后运行 `composer update`。

### ② 执行命令安装

运行命令：

```bash
composer require juhedata/aliyun-oss
```

## 使用（以 Laravel 为例）

### 构建 Service 文件

新建 `app/services/OSS.php`，内容可参考：[OSS.php](https://github.com/juhedata/aliyun-oss/blob/master/example/OSS.php)，然后修改配置：

```php
... ...

  private $city = '青岛';

  // 经典网络 or VPC
  private $networkType = '经典网络';
  
  private $AccessKeyId = '';
  private $AccessKeySecret = '';

... ...
```

### 放入自动加载

#### 遵循 psr-0 的项目（如Laravel 4、CodeIgniter、TinyLara）中：
在 `composer.json` 中 `autoload -> classmap` 处增加配置：

```json
"autoload": {
    "classmap": [
      "app/services"
    ]
  }
```
然后运行 `composer dump-autoload`。

#### 遵循 psr-4 的项目（如 Laravel 5、Symfony）中：

无需配置，保证目录 `App/Services` 和命名空间 `namespace App\Services;` 一致即可自动加载。

### 使用

```php
use App\Services\OSS;

// 在外网上传一个文件并指定 options 如：Content-Type 类型
// 更多 options 见：https://github.com/juhedata/aliyun-oss/blob/master/src/oss/src/Aliyun/OSS/OSSClient.php#L142-L148
OSS::publicUpload('bucket', '目标 object 名', '本地文件绝对路径', [
    'ContentType' => 'application/pdf',
    ... ...
]);
```

更多用法等待着你去[发现](https://github.com/juhedata/aliyun-oss/blob/master/example/OSS.php)。

### Symfony 3 用法示例

如果你正在使用基于 Symfony 创建的第三方应用程序，而又恰好不懂命名空间及 Composer 自动加载，那么看下面就知道本库在 Symfony 中的用法了：

#### 构建 Service 文件

新建 `src/App/Services/OSS.php`，内容参考：[OSS.php](https://github.com/juhedata/aliyun-oss/blob/master/example/OSS.php)。

修改顶部的命名空间为 `namespace App\Services;`。

#### 放入自动加载

无需配置。

#### 使用

```php
use AppBundle\Services\OSS;

OSS::publicUpload('bucket', '目标 object 名', '本地文件绝对路径');
```

## License
除 “版权所有（C）阿里云计算有限公司” 的代码文件外，遵循 [MIT license](http://opensource.org/licenses/MIT) 开源。


