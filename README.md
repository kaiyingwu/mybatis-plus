# mybatis-plus

## 一、mybatis-plus简介：

Mybatis-Plus（简称MP）是一个 Mybatis 的增强工具，在 Mybatis 的基础上只做增强不做改变，为简化开发、提高效率而生。

## 二、mybatis-plus配置

### 1.引入依赖,最新版本可以去[官网](https://baomidou.com/#/)获取

```
<!-- spring -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>4.3.14.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-orm</artifactId>
            <version>4.3.14.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>4.3.14.RELEASE</version>
            <scope>test</scope>
        </dependency>
        <!-- mp 依赖 -->
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus</artifactId>
            <version>2.3</version>
        </dependency>
```

### 2.分页插件配置

```
@Configuration
public class MybatisPlusConfig {
        /**
         *   mybatis-plus分页插件
         */
        @Bean
        public PaginationInterceptor paginationInterceptor() {
            PaginationInterceptor page = new PaginationInterceptor();
            page.setLimit(-1);
            return page;
        }
}
```

### 3.注意事项

集成mybatis-plus要把mybatis、mybatis-spring去掉，避免冲突

## 三、mybatis-plus的使用

### 简单数据操作：

1.insert

```
对应实体类中添加以下注解，可自动识别表（字段驼峰对应）
@TableName("表名")
save();//单存
saveBatch();//批量存
```

2.update

 ```
 T(实体类)
 this.update(Wrappers.<T>lambdaUpdate().in(T::匹配参数,匹配值).set(T::修改参数,修改值));
 ```
 
 3.select
 
 ```
 T(实体类)
 QueryWrapper<T> queryWrapper = new QueryWrapper<>();
 queryWrapper.lambda()
        .eq(T::实体类参数, 参数值)
        .eq(T::实体类参数, 参数值);
 int count = this.count(queryWrapper);//查询条数
 
 List<T> list = this.list(queryWrapper);//多数据查询
 
 //分页查询
 IPage<SourcePlatformDO> page = new Page<>(页数, 每页大小);
 IPage<SourcePlatformDO> pageDb = this.page(page,Wrappers<T>lambdaQuery().eq(T::参数,参数值).orderByAsc(T::参数));
 
 ```
 
 ### 常用条件构造器参数
 
 ```
 where	WHERE 语句，拼接 + WHERE 条件
 
 and	AND 语句，拼接 + AND 字段=值
 
 or	OR 语句，拼接 + OR 字段=值
 
 eq	等于=
 
 ne	不等于<>
 
 gt	大于>
 
 ge	大于等于>=
 
 lt	小于<
 
 le	小于等于<=
 
 like	模糊查询 LIKE
 
 notLike	模糊查询 NOT LIKE
 
 orderBy	排序 ORDER BY
 
 orderAsc	ASC 排序 ORDER BY
 
 orderDesc	DESC 排序 ORDER BY
 ```
