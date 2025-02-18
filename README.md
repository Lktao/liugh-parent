# bx-cloud

![](https://oscimg.oschina.net/oscnet/up-5d67fec24fa4f24eeb5e714ea93da59db22.png)
![](https://oscimg.oschina.net/oscnet/up-a908358bc735192b532b025861ee25460de.png)




### 一、背景

前后端分离已经成为互联网项目开发标准，它会为以后的大型分布式架构打下基础。[SpringBoot](https://projects.spring.io/spring-boot/)使编码配置部署都变得简单，越来越多的互联网公司已经选择SpringBoot作为微服务的入门级微框架。

[Spring Cloud Oauth2](https://projects.spring.io/spring-security-oauth/docs/oauth2.html)
Spring Cloud Security 为构建安全的SpringBoot应用提供了一系列解决方案，结合Oauth2可以实现单点登录、令牌中继、令牌交换等功能.

[Mybatis-Plus](https://github.com/baomidou/mybatis-plus)是一个 [Mybatis](http://www.mybatis.org/mybatis-3/) 的增强工具，有代码生成器，并且提供了类似hibernate的单表CRUD操作，又保留了mybatis的特性支持定制化 SQL。

[Nacos](http://dubbo.apache.org/zh-cn/docs/user/references/registry/nacos.html) 致力于帮助您发现、配置和管理微服务。Nacos 提供了一组简单易用的特性集，帮助您实现动态服务发现、服务配置管理、服务及流量管理。


[LCN](http://www.txlcn.org/zh-cn/)并不生产事务，LCN只是本地事务的协调工.一个高性能的分布式事务框架.


项目用到的技术:
Spring Boot +Spring Cloud +Spring Security Oauth2 +JWT +MybatisPlus +Mysql +Redis +Nacos +LCN +Zuul

|  工程名   | 说明  |
|  ----  | ----  |
| bx-commons  | 数据传输对象、常量\工具类、公共常量 |
| bx-core-server  | 核心服务,必须启动的两个服务|
| --register-config-center  | 注册配置中心(Nacos) |
| --user-center  |用户认证授权 |
| bx-gateway-zuul  | 网关 |
| bx-files-server  | 文件中心 |
| bx-transaction-server  | 分布式事务服务 |



### 二、项目特性

1.自定义@Log注解自动记录日志到数据库。


2.过滤请求参数，防止XSS攻击。


3.完成微信/微博/QQ第三方登录功能，完成用户名电话邮箱三种方式登录,WebSocket实时消息推送,短信登录注册等功能.

4.完成方法限流注解,重要防刷方法被访问距离下一次时间可调节

5.自己实现轻量级工作流,用状态机完成

6.整合快捷操作excel组件,加快开发速度

### 三、程序逻辑

1.填写用户名密码用POST请求访问/login接口，返回token令牌等信息，失败则直接返回身份错误信息。

2.在之后需要验证身份的请求的Headers中添加Authorization和登录时返回的token令牌。

3.服务端进行token认证，失败身份错误信息。


### 四、运行项目


-   通过git下载源码，本项目基于JDK1.8

-   采用Maven项目管理，模块化，导入IDE时直接选定liugh-parent的pom导入

-   本项目SpringCloud版，基本环境只需要启动MySQL，Redis和bx-core-server里的两个服务，其他服务根据需要启动。

-   每个项目中的sql文件对应一个数据库先创建好。

-   启动顺序Redis-->MySQL-->register-config-center(RegisterConfigCenter.java)-->user-center(UserCenterApplication.java)

-   修改bootstrap.properties中注册中心\数据库等地址，更新MySQL，Redis账号和密码。

-   访问登录接口：localhost:8000/oauth/user/token

    ![](https://oscimg.oschina.net/oscnet/up-55bdfe18f6a908ad3ed3ab9f6a750b65f21.png)

-   Content-Type用application/json方式，账号密码：
{
	"username":"admin",
	"password":"admin",
	"clientId":"system",
	"clientSecret":"system",
	"scope":"app",
	"grantType":"password"
}

-   获取token访问其他接口

-   注意!!!!!编译器请安装lombok插件,不然会报红
 

运行截图：

![](https://oscimg.oschina.net/oscnet/up-bc8acff8b14d093d3bf0ae0ea08df8576fe.png)










