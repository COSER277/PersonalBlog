# 作品介绍

## 开发模式

**整体项目开发模式：前后端分离模式-即前端负责页面渲染展示给客户，则后负责模型数据的接口服务**

## 技术选型

1. 前端
  1. VueJs
  2. ElementUI
  3. axios
2. 后端
  1. SpringBoot
  2. MySQL
  3. JWT
## 后端实现

1. 前言
2. 构建项目
  1. 新建
    1. ![图片](https://uploader.shimo.im/f/5gp4x8otr7YJrd84.png!thumbnail)
  2. 安装依赖
    1.   ![图片](https://uploader.shimo.im/f/mUvGMK0sgU10W1Ry.png!thumbnail)
3. mybatis-plus整合
  1. 依赖
```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-freemaker</artifactId>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>
 
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.2.0</version>
        </dependency>
    <!--  mp 代码说生成器-->
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-generator</artifactId>
            <version>3.2.0</version>
        </dependency>
```
  2. 配置mybatis-plus 分页插件
    1. 新建 config 目录并创建 MybatisPlusConfig Java Class文件
      1. ![图片](https://uploader.shimo.im/f/HoQK9bjOvOghVjez.png!thumbnail)
    2. 代码如下
```java
@Configuration
@EnableTransactionManagement
@MapperScan("com.coser.mapper")
public class MybatisPlusConfig {
    @Bean
    public PaginationInterceptor paginationInterceptor() {
        PaginationInterceptor paginationInterceptor = new PaginationInterceptor();
        // 设置请求的页面大于最大页后操作， true调回到首页，false 继续请求  默认false
        // paginationInterceptor.setOverflow(false);
        // 设置最大单页限制数量，默认 500 条，-1 不受限制
        // paginationInterceptor.setLimit(500);
        // 开启 count 的 join 优化,只针对部分 left join
        paginationInterceptor.setCountSqlParser(new JsqlParserCountOptimize(true));
        return paginationInterceptor;
    }
}
```
  3. 配置项目配置
    1. 更改原来的application.profile文件为yml格式
      1. ![图片](https://uploader.shimo.im/f/9Vp7U0texnppWOc3.png!thumbnail)
      2. 代码如下
```yaml
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbs:mysql://localhost:3306/数据库名?useUnicode=true&useSSL=false&characterEncoding=utf8&serverTimezone=Asia/Beijing
    username: root
    
    password: 密码
mybatis-plus:
  mapper-locations: classpath*:/mapper/*Mapper.xml
server:
  port: 8088
```
  4. 测试服务
  5. 打开 [http://localhost:8088](http://localhost:8088)
4. 创建数据库-MySQL
  1. 创建数据库 dragonhub
5. 代码生成器
  1. 即快速生成 entity、controller、mapper、service以及service/impl
  2. ![图片](https://uploader.shimo.im/f/tnnUUaeFdIXEMciv.png!thumbnail)
  3. 遇到的问题
    1. ![图片](https://uploader.shimo.im/f/FfOSSE7BogWB3gpa.png!thumbnail)
    2. 解决![图片](https://uploader.shimo.im/f/Aj9kxRksqUNZewyx.png!thumbnail)
    3. ![图片](https://uploader.shimo.im/f/uO2h6AkBxQWOZaX6.png!thumbnail)
  4. 测试一下
  1. 在 controller/BlogController
```java
/**
 *  前端控制器
 * @author coser
 * @since 2020-06-03
 */
@RestController
@RequestMapping("/blog")
public class BlogController {
    @Autowired
    IBlogService blogService;
    @GetMapping("/list")
    public List<Blog> list(){
        System.out.println();
        return blogService.list();
    }
```
![图片](https://uploader.shimo.im/f/SldfFPJDrefBrZF5.png!thumbnail)

1. 统一封装返回数据结果
  1. 新建 common/ResultBody类
```plain
package com.coser.dragonhub.common;
import lombok.Data;
import org.apache.ibatis.annotations.Result;
import java.io.Serializable;
import java.util.List;
@Data
public class ResultBody implements Serializable {
    private int code;
    private String msg;
    private Object data;


    public  static  ResultBody success(int code, String msg, List<?> data) {
        ResultBody result=new ResultBody();
        result.setCode(code);
        result.setMsg(msg);
        result.setData(data);
        return result;
    }
    public static ResultBody fail(int code,String msg,List<?> data) {
        ResultBody result=new ResultBody();
        result.setCode(code);
        result.setMsg(msg);
        result.setData(data);
        return result;
    }

    public String getMsg() {
        return msg;
    }
    public void setMsg(String msg) {
        this.msg=msg;
    }
    public Object getData() {
        return data;
    }
    public void setData(List<?> data) {
        this.data=data;
    }
    public int getCode() {
        return code;
    }
    public void setCode(int code) {
        this.code=code;
    }
}
```
  2. 在controller使用
    1. ![图片](https://uploader.shimo.im/f/DcGREOYDuSh5kzHf.png!thumbnail)
  3. 测试一下
    1. ![图片](https://uploader.shimo.im/f/3V5XSs8aC1tEy6g8.png!thumbnail)
# 前端实现

## 新建项目 

## 安装依赖

## 配置页面路由

### 登录页开发

### 登录发起请求

### 全局axios拦截

## 首页以及组件开发

## 博客列表页面开发

## 博客发表与编辑

## 用户与博主的功能权限

## 路由拦截

# 


