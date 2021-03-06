# Bean作用域

## 文件目录

与过滤规则的目录一样

```
src/
├── main
│   ├── java
│   │   └── com
│   │       └── hzj
│   │           ├── bean
│   │           │   └── Person.java
│   │           ├── config
│   │           │   ├── MainConfig.java
│   │           │   └── MyTypeFilters.java
│   │           ├── controller
│   │           │   └── BookController.java
│   │           ├── dao
│   │           │   └── BookDao.java
│   │           ├── main
│   │           │   └── Main.java
│   │           └── service
│   │               └── BookService.java
│   └── resources
└── test
    └── java
        └── com
            └── hzj
                └── test
                    └── IOCTest.java

```

## 单实例

1. 使用

`@Scope("singleton")`或者`@Scope`(里面不写value，默认就是singleton)

```java
package com.hzj.config;


import com.hzj.bean.Person;
import org.springframework.context.annotation.*;

/**
 * @author hzj
 */
@Configuration
@ComponentScan(value = "com.hzj")
public class MainConfig {


    /**
     * prototype: 多实例: ioc容器启动并调用方法创建对象放在容器中,每次获取的时候才会调用方法创建对象
     * singleton: 单实例(默认值),IOC容器启动会调用方法创建对象放到IOC容器中，以后每次获取就是从容器(map.get())中拿
     * request: 同一次请求创建一次实例(web环境,用的不多)
     * session: 同一次session创建一次实例(web环境,用的不多)
     * @return
     */
    @Scope("singleton")
    //@Scope("singleton") = @Scope
    @Bean("person")
    public Person person() {
        return new Person("hzj", 18);
    }
}

```

2. 规则

IOC容器启动会调用方法创建对象放到IOC容器中，以后每次获取就是从容器(map.get())中拿

## 多实例

1. 使用

`@Scope("prototype")`

```java
package com.hzj.config;


import com.hzj.bean.Person;
import org.springframework.context.annotation.*;

/**
 * @author hzj
 */
@Configuration
@ComponentScan(value = "com.hzj")

public class MainConfig {


    /**
     * prototype: 多实例: ioc容器启动并调用方法创建对象放在容器中,每次获取的时候才会调用方法创建对象
     * singleton: 单实例(默认值),IOC容器启动会调用方法创建对象放到IOC容器中，以后每次获取就是从容器(map.get())中拿
     * request: 同一次请求创建一次实例(web环境,用的不多)
     * session: 同一次session创建一次实例(web环境,用的不多)
     * @return
     */
    @Scope("prototype")
    //@Scope("singleton") = @Scope
    @Bean("person")
    public Person person() {
        return new Person("hzj", 18);
    }
}

```

2. 规则

ioc容器启动并调用方法创建对象放在容器中,每次获取的时候才会调用方法创建对象

