# vue通用后台

目标是快速搭建一个可用的后台界面，
todo:
分为几个主要的部分：

* 侧边栏：上面是一个logo，下面是可展开的各级菜单。点击菜单项时，右边会展示相应的内容。
* Header：展示当前登录的用户名和面包屑导航，还可能有自定义的一些菜单之类
* 内容区：展示具体的内容，跟业务有关的
* Footer：展示copyright之类的
* 还有些看不到的，比如登录、注销等

搭建一个框架，用配置文件的方式，生成这样一个界面。

todo:

1.定义自己的侧边栏（最好是[src/menu.js]，
2.定义点击侧边栏菜单时在右边渲染什么组件（zai[src/index.js]其实就是Router的配置），
包括header/footer/登录校验/单点登录等，
3.可以配置（在[src/config.js]。

在此基础上，我只要根据不同的后台系统的业务逻辑，
去写不同的vue组件，再配置下菜单就可以了。


但能否更简化些呢？在各种运营后台中，最常见的操作是什么？
我的感觉，最常见的就是各种数据库表的CRUD。我们经常赋予数据库字段各种业务意义。
比如将某条记录的status字段改为-1，表示屏蔽这个商品；或者新增一个商品，其实就是某个表新增一条记录之类的。运营的很多操作，是不是都能简化成CRUD？
于是写了一个通用的CRUD组件，我称之为Table。

也是分为几个部分：
todo:

*1.查询条件区：其实就是个表单，所有表单项都是由配置文件生成的（在[src/schema/test.querySchema.js]，支持各种数据类型
* 2各种操作：提供常用的CRUD/导入/导出等操作
* 3查询结果展示：就是一个表格，这个表格的schema也是可配置的（在[src/schema/test.dataSchema.js]
* 4针对单条数据的操作：也是可配置的（参考[src/schema/testAction.dataSchema.js]

只用关心自己的schema文件就可以了，不用在意渲染出来是什么样子。利用Table组件，就可以快速实现对某个表的CRUD了（其实不只可以用于数据库，符合这种操作模式的都可以用）。

