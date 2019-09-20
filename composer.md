1. 配置阿里云packagelist地址`composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/`
## 安装使用组件
1. php组件获取网站:[PackageList](https://packagist.org/)
2. 在项目根目录运行`composer require league/csv`
3. 完成后会在根目录下生成`vendor`文件夹、`composer.json`文件、`composer.lock`文件。`composer.lock`应加入到版本控制中，确保项目各个环境php组件版本相同。
4. 如需下载最新版本的组件并更新`composer.lock`，可以使用`composer update`命令
5. 在项目代码中引入vendor下面的`autoload.php`
```
    require 'vendor/autoload.php';
```