##  发展史：
* JDBC-> Dbutils->JDBCTemplete  工具  
编写sql - 预编译 - 设置参数 - 执行sql - 封装结果  
* Hibernate:  
  全自动 ROM 框架  Object Relation Mapping  
  JavaBean ---  中间过程  ---- DbRecord  
  不能优化
* Mybatis  
  编写sql放在配置文件中间，其他步骤黑盒处理  
  sql与Java编码分离，sql是开发人员控制 半自动 轻量级  
    
# HelloWorld
1. 根据 xml 配置文件 创建一个SqlSessionFactory对象 有数据源的运行环境信息
2. sql映射文件，配置了每一个sql，以及sql的封装规则
3. 讲sql映射文件注册在全局配置文件中
4. 写代码：
   1. 根据全局配置文件得到sqlSessionFactory
   2. 使用sqlSession工厂，获取到SqlSession对象使用他来执行crud， 一个session就是一个会话，用完关闭
   3. 用sql的卫衣哦标志来告诉Mybatis自信哪个sql，sql都是保存在sql映射文件中的
5. SqlSession 和connection一样都是非线程安全的, 每次使用都应该去获取新的对象，不应该放在成员变量中。
6. mapper接口没有实现类，但是mybatis会为这个借口生成一个代理对象， `sqlSession.getMapper(EmployeeMapper.class)` 
7. 两个重要的配置文件，一个是mybatis全局配置， 一个是 sql-mapper映射文件, 保存了每一个sql语句的映射信息，讲sql抽取出来。
# Configuration 
## Properties
1. `properties` resource引入类路径下资源  url引入网络或者磁盘路径文件
2. xml文件 通过 `${}` 引入属性变量
## Setting
1. `mapUnderscoreToCamelCase` 帮助数据库下划线格式映射为小驼峰形式  
    `<setting name="mapUnderscoreToCamelCase" value="true">`
2. `typeAliases` 别名处理器  给Java类型起别名  
    old: mapper.xml `<select id = "getEmpById" resultType ="com.xdfsd.sfdsdfsd.sdf">`  
    new : 
    ```
    <typeAliases>
    <!-- 默认是小写类名 -->
    <!-- 别名不区分大小写 -->
    <typeAlias type ="com.sdfsd.sfsd" >

    <typeAlias type ="com.sdfsd.sfsd" alias="sdfs">
    <!-- 批量别名 -->
    <package name = "com.sdfsd">
    </typeAliases>
    ```

    注解开发
    `@Alias("sdfsd)`
## `TypeHandlers` 
  类型处理器 Java类型和数据库类型映射
## `Plugins` 插件
   1. Executor 
   2. ParameterHandler
   3. ResultSetHandler
   4. StatementHandler
## Environment
mybatis可以配置多种环境，default指定环境  
transactionManager:事务管理器  
  type: JDBC｜MANAGED   
DataSource: UNPOLLED | POOLED | JNDI

```
<environments default="test">
  <environment id="test">
  <transactionManager type=""></transactionManager>
  <dataSource type=""></dataSource>
  </environment>
  <environment id="develop">
  <transactionManager type=""></transactionManager>
  <dataSource type=""></dataSource>
  </environment>
</environments>
```
## DatabaseIdProvider 
多数据库支持
```
<databaseIdProvider type="DB_VENDOR"/> 
```
## mappers
注册一个sql映射  
resource: 引用类路径下的sql映射文件  
url: 引用网路路径或者磁盘路径下的sql映射文件  
class: 引用接口  


```
<mappers>
  <mapper  resource = "EmployeeMapper.xml"/>
</mappers>
```

## mybatis-config.xml namespace
1. 当只使用XML来配置mapper接口时，就是我们把sql配置在EmployeeMap.xml 中时，若我们把namespace设置为mapper接口的路径时，我们不需要为Sqlsession addMapper 
2. 若不是，则必须要`session.getConfiguration().addMapper(EmployeeMapper.class)`
   
## CRUD
1. mybatis支持返回值 Integer Long Boolean
2. sqlSessionFactory.openSession() 需要手动提交  
  sqlSessionFactory.openSession(true) 自动提交
   