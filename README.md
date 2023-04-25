# Health_project

### 今天尝试着做了一下，传智健康项目，他day01主要讲了一些什么呢？

- 刚开始都是一些项目搭建和项目结构的叙述，阿巴阿巴一堆，然后我有一个疑惑点，就是meaven中pom.xml里打pom包和war包有啥区别
- 其实这个很好理解，在pom配置文件中打pom包意思就是该项目没有具体的代码实现，仅作为一个依赖的存在。然后如果配置文件中打war包则代表这个项目是一个web项目，最终可以打包为（WAR Web Archive），可以部署在web容器里。同时，如果配置文件里打了jar包，就是将项目编译打包为可执行的Java程序。通过命令行运行。
- 那么为什么接口常常被打成jar包呢？（因为接口老是挨打 哈哈哈） 其实就是因为我们的接口嘛~需要供其他开发者调用，所以通过打jar包形式将代码和所需依赖打包成一个整体供其他开发者调用。这种方式的好处就是，不需要我们刚开始一样百度（通过第三方渠道）各种依赖和资源包去下载。。。。
- 然后就是这个项目通过meaven父级管理，然后在health_parent pom.xml中我们用了“dependencyManagement”这个标签 这个标签就是我们的坐标管理，写了这个标签后，我们的坐标资源不会被子类继承（要不然 父类写了一大堆 然后子类也是一大堆 可麻烦了~）
- 工程与工程之间也可以相互依赖，比如我health_common/pom.xml第一好了以后 就可以在health_interface中依赖它
- 然后我还需要创建服务的提供方 health_provider ，它的打包方式肯定是war，因为以后要部署在web容器里，他是作为服务的单独部署，存放服务类，Dao接口啊和Mapper映射文件的。
- 还有什么是com.github.pagehelper.PageHelper 他其实就是一个搭配MyBatis使用的一个分页插件，若要使用分页功能，则可以集成PageHelper插件，以快捷地实现在本地线程环境中自动进行分页处理。它的好处有哪些呢？ https://v.flomoapp.com/mine/?memo_id=NjUxODY5NTE 
- 然后这次项目关于MyBatis的配置我们是教给spring框架的，然后mybaits里只有一个分页插件，然后就是我们也吧Spring框架拆分成了三个部分，一个是dao持久层，一个是tx事务管理部分，还有一个就是service就是连接我们的dubbo服务部分。
- 然后这次在dao层我们配置了数据库的连接池，同时使用了阿里云的【com.alibaba.druid.pool.DruidDataSource】连接池，这个连接池具体细节我就不讲了，总之很复杂，但是他特别特别的厉害，它拥有监控功能，可以预防SQL注入攻击，而且还有连接池缓存优化，巴拉巴拉一大堆好处。用它！哦对了她还可以配置防火墙。具体细节介绍看这个连接吧： https://v.flomoapp.com/mine/?memo_id=NjUxODgxMjM 
-  其实他是一个小工具，就像小孩子用的可以画图的铅笔，他专门管理Java程序与数据库之间的关系，帮助我们保存和读取数据。DruidDataSource 还有一个cool 的特点，它会把访问数据库的流量进行“防火墙”保护，在web应用中避免了SQL注入攻击所造成的安全风险。（嘿嘿嘿 我喜欢SQL注入攻击！）
- 阿巴阿巴 配置文件里还有开启org.mybatis.spring.mapper.MapperScannerConfigurer 这个东西 其实这个就是一个包扫描生成动态代理对象，他有什么作用呢，它的作用通过在配置文件中指定需要扫描的哪些组件（即:class路径下某个包名），让Spring来自动帮我们进行创建和注册包中所有bean定义与其他数据元。阿巴阿巴就是很方便省的我们自己去手动创建BEAN了。
- 然后在事务管理器中我们需要开启事务管理控制的注解支持

\#JavaEE/colincora_health