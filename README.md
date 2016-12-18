#Mybatis分页插件 - PageHelper

如果你也在用Mybatis，建议尝试该分页插件，这一定是<b>最方便</b>使用的分页插件。

分页插件支持任何复杂的单表、多表分页，部分特殊情况请看[重要提示](http://git.oschina.net/free/Mybatis_PageHelper/blob/master/wikis/Important.markdown)。

想要使用分页插件？请看[如何使用分页插件](http://git.oschina.net/free/Mybatis_PageHelper/blob/master/wikis/HowToUse.markdown)。

##物理分页

该插件目前支持以下数据库的<b>物理分页</b>:

 1. `Oracle`
 2. `Mysql`
 3. `MariaDB`
 4. `SQLite`
 5. `Hsqldb`
 6. `PostgreSQL`
 7. `DB2`
 8. `SqlServer(2005,2008)`
 9. `Informix`
 10. `H2`
 11. `SqlServer2012`
 12. `Derby`

配置`dialect`属性时，可以使用小写形式：

`oracle`,`mysql`,`mariadb`,`sqlite`,`hsqldb`,`postgresql`,`db2`,`sqlserver`,`informix`,`h2`,`sqlserver2012`,`derby`

在4.0.0版本以后，`dialect`参数可以不配置，系统能自动识别这里提到的所有数据库。

对于不支持的数据库，可以实现`com.github.pagehelper.parser.Parser`接口，然后配置到`dialect`参数中(4.0.2版本增加)。

<b>特别注意：</b>使用SqlServer2012数据库时，需要手动指定`sqlserver2012`，否则会使用2005的方式进行分页。

##MyBatis工具网站:[http://mybatis.tk](http://www.mybatis.tk)

##分页插件支持MyBatis3.1.0+(支持最新版本)

##分页插件5.0

由于分页插件5.0版本和4.2.x实现完全不同，所以master分支为5.x版本，4.2.x 作为一个分支存在，如果有针对 4.2.x 的 PR，请注意提交到分支版本。

##分页插件最新快照版本为5.0.0-SNAPSHOT

##分页插件最新版本为4.2.1

###Maven坐标

```xml  
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper</artifactId>
    <version>4.2.1</version>
</dependency>
```  

###下载JAR包

分页插件pagehelper.jar： 

 - https://oss.sonatype.org/content/repositories/releases/com/github/pagehelper/pagehelper/
 
 - http://repo1.maven.org/maven2/com/github/pagehelper/pagehelper/

###由于使用了sql解析工具，你还需要下载jsqlparser.jar

####4.1.0及以后版本需要0.9.5版本

 - http://repo1.maven.org/maven2/com/github/jsqlparser/jsqlparser/0.9.5/

####4.1.0以前版本需要0.9.1版本

 - http://repo1.maven.org/maven2/com/github/jsqlparser/jsqlparser/0.9.1/

##4.2.1

- 解决`SimpleCache`类遗留问题导致的错误 [#143](http://git.oschina.net/free/Mybatis_PageHelper/issues/143) fix by [dhhua](https://github.com/dhhua)

##4.2.0

- 使用新的方式进行分页，4.2版本是从5.0版本分离出来的一个特殊版本，这个版本兼容4.x的所有功能，5.0版本时为了简化分页逻辑，会去掉部分功能，所以4.2是4.x的最后一个版本。
- 支持 MyBatis 3.1.0+ 版本
- 增加对 Derby 数据库的支持
- 对除 informix 外的全部数据库进行测试，全部通过
- PageHelper增加手动清除方法`clearPage()`
- 解决 SqlServer 多个`with(nolock)`时出错的问题
- 对CountMappedStatement 进行缓存，配置方式见BaseSqlUtil 319行
- 由于SqlServer的sql处理特殊，因此增加了两个SQL缓存，具体配置参考SqlServerDialect类
- 添加 sqlserver 别名进行排序功能，在解析sql时，会自动将使用的别名转换成列名 by panmingzhi
- 新增`sqlCacheClass`参数，该参数可选，可以设置sql缓存实现类，默认为`SimpleCache`，当项目包含guava时，使用`GuavaCache`，也可以通过参数`sqlCacheClass`指定自己的实现类，有关详情看`com.github.pagehelper.cache`包。
- 解决#135，增加/*keep orderby*/注解，SQL中包含该注释时，count查询时不会移出order by
- sqlserver没有orderby时，使用`order by rand()` #82 #118

##项目文档[wiki](http://git.oschina.net/free/Mybatis_PageHelper/wikis/home)：  

###[如何使用分页插件](http://git.oschina.net/free/Mybatis_PageHelper/blob/master/wikis/HowToUse.markdown)

如果要使用分页插件，这篇文档一定要看，看完肯定没有问题。

如果和Spring集成不熟悉，可以参考下面两个MyBatis和Spring集成的框架

<b>只有基础的配置信息，没有任何现成的功能，作为新手入门搭建框架的基础</b>

- [集成Spring3.x](https://github.com/abel533/Mybatis-Spring/tree/spring3.x)

- [集成Spring4.x](https://github.com/abel533/Mybatis-Spring)

这两个集成框架集成了MyBatis分页插件和MyBatis通用Mapper。

###[更新日志](http://git.oschina.net/free/Mybatis_PageHelper/blob/master/wikis/Changelog.markdown)

包含全部的详细的更新日志。

###[重要提示](http://git.oschina.net/free/Mybatis_PageHelper/blob/master/wikis/Important.markdown)

提示很重要，建议一定看一遍！

###[提交(gitosc)BUG](http://git.oschina.net/free/Mybatis_PageHelper/issues/new?issue%5Bassignee_id%5D=&issue%5Bmilestone_id%5D=)

##相关链接

对应于oschub的项目地址：http://git.oschina.net/free/Mybatis_PageHelper

对应于github的项目地址：https://github.com/pagehelper/Mybatis-PageHelper

Mybatis-Sample（分页插件测试项目）：[http://git.oschina.net/free/Mybatis-Sample](http://git.oschina.net/free/Mybatis-Sample)

Mybatis项目：https://github.com/mybatis/mybatis-3

Mybatis文档：http://mybatis.github.io/mybatis-3/zh/index.html  

Mybatis专栏： 

- [Mybatis示例](http://blog.csdn.net/column/details/mybatis-sample.html)

- [Mybatis问题集](http://blog.csdn.net/column/details/mybatisqa.html)  

作者博客：  

- http://my.oschina.net/flags/blog

- http://blog.csdn.net/isea533   

作者邮箱： abel533@gmail.com  

Mybatis工具群： <a target="_blank" href="http://shang.qq.com/wpa/qunwpa?idkey=29e4cce8ac3c65d14a1dc40c9ba5c8e71304f143f3ad759ac0b05146e0952044"><img border="0" src="http://pub.idqqimg.com/wpa/images/group.png" alt="Mybatis工具" title="Mybatis工具"></a>