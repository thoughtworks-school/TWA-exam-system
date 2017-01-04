欢迎你来到这里，你可以用这个项目练习在 Java 技术栈上快速实现 RESTful 的 API。

### 业务背景
思沃学院每年都会举办暑期特训营，在校大学生可以报名参加这个特训营，为了保证学员在同一个起跑线上，我们要对他们进行逻辑和编程能力的测试。
为了减少工作量，我们打算做一个系统来让学生考试。
系统有两个角色：`学生`和`管理员`。

学生可以做如下事情：
* 注册
* 登录
* 维护补充信息
* 报名考试
* 进行逻辑测试
* 进行编程测试

管理员可以：
* 登录
* 导入题库
* 创建考试
* 开启考试
* 关闭考试
* 导出成绩

因为采用前后端分离的架构，你只需要实现 API 即可。
所有的需求用 Issues 描述，你只需要按顺序一条一条实现即可，验收条件包括：
* 能运行通过的接口测试
* Migration 脚本（如果对表结构有变更）
* 通过所有的 Check Style 检查

也就是说`./gradlew build` 能够成功执行。

运行项目
==========

### 开发环境
- 确保开发环境下有jdk8，以及mysql 5.5+
- 使用下面的脚本,提前在mysql中建好数据库

```
DROP DATABASE IF EXISTS `gaia`; CREATE SCHEMA `gaia` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
```

- 使用`./gradlew cleanIdea idea`生成Intellij工程
- 使用`Intellij`打开生成的`gaia.ipr`文件
- 找到`GaiaApplication`这个类，运行`main()`方法启动服务器

### 测试服务器是否启动正常

- 检查启动中有无异常log
- 打开浏览器，访问<http://localhost:8080/gaia/rest/application.wadl>，看是否有API列表输出
- 打开浏览器，访问<http://localhost:8080/gaia/rest/product/1>，看是否返回包含`"errorCode":"RESOURCE_NOT_FOUND"`这样的出错信息
- 在数据库console中，使用后面的脚本在数据库中插入一条数据`insert into gaia.PRODUCT (`name`, `time_created`) values ('product_name', NOW());`
- 在数据库console中，使用`select * from gaia.PRODUCT`，查看是否已插入数据成功，并记下数据的`id`
- 加入上一步记下的`id`为`1`，打开浏览器，访问<http://localhost:8080/gaia/rest/product/1>
- 检查浏览器的返回是否是 `{"id":1,"name":"product_name","timeCreated":1474615151000}`，其中`timeCreated`对应的数字可能会略有不同

### 查看所有API 地址及请求所需方式、参数

- 中心服务器：<http://localhost:8080/gaia/rest/application.wadl>

*注意：更改localhost到你希望查看的服务器IP*

开始闯关 #1
