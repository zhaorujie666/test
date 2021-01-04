### SpringCloud Alibaba添加nacos配置文件

```yml
#bootstrap.yml
server:
	port: (端口号)
spring:
	application:
		name: （注册到nacos中的应用户名称）
	cloud:
		nacos:
			discovery:
				server-addr: 127.0.0.1:8848
```

### nacos配置中心

```yml
server:
	port: 3377

spring:
	application:
		name: （注册到nacos中的应用户名称）
	cloud:
		nacos:
			discovery:
				server-addr: 127.0.0.1:8848
			config:
				server-addr: 127.0.0.1:8848
				namespace: 10e261cd-dd92-467a-b6c3-a0a5c40d3769  #命名空间的id,现在nacos创建命名空间
        		group: DEFAULT_GROUP #分组
	
```

这样是为了直接可以获取nacos上的配置信息

```java
@RefreshScope //注意添加nacos的配置动态实时刷新
public class ConfigClientController{
    @Value("${config.info}") 
    //config.info是在nacos上配置的文件内容
    private String configInfo;
}
```



### 启动文件

```java
@SpringBootApplication
@EnabledDiscoberyClient
public class Application{
    public static void main(String[] args){
        SpringApplication.run(Application.class, args);
    }
}
```



#### linux防火墙命令

**一、重启后永久性生效：**

**开启：**

```
chkconfig iptables on
```

**关闭：**

```
chkconfig iptables off
```

**二、即时生效，重启后失效：**

**开启：**

```
service iptables start
```

**关闭：**

```
service iptables stop
```