# Java 反序列化漏洞利用

## 0x00 Java序列化和反序列化

Java 序列化：把 Java 对象转换为字节序列的过程便于保存在内存、文件、数据库中，ObjectOutputStream类的 writeObject() 方法可以实现序列化。
Java 反序列化：把字节序列恢复为 Java 对象的过程，ObjectInputStream 类的 readObject() 方法用于反序列化。

>一个类的对象要想序列化成功，必须满足两个条件：
1. 该类必须实现 java.io.Serializable 接口。
2. 该类的所有属性必须是可序列化的。如果有一个属性不是可序列化的，则该属性必须注明是短暂的。

## 0x01 Java反序列化漏洞成因
反序列化接口可以构造恶意对象序列化数据输入。       
利用java的反射等机制来执行代码。     


## 0x02 Java反序列化基础知识

简单的来说就是RMI注册的服务可以让 JNDI 应用程序来访问，调用。

- JNDI (Java Naming and Directory Interface) 是一个应用程序设计的 API，为开发人员提供了查找和访问各种命名和目录服务的通用、统一的接口。JNDI 支持的服务主要有以下几种：DNS、LDAP、 CORBA 对象服务、RMI 等。
- RMI(Remote Method Invocation) 即 Java 远程方法调用，一种用于实现远程过程调用的应用程序编程接口，常见的两种接口实现为 JRMP(Java Remote Message Protocol ，Java 远程消息交换协议)以及 CORBA。


## 0x03 如何发现反序列化漏洞

### 反序列化函数
```
ObjectInputStream.readObject
ObjectInputStream.readUnshared
XMLDecoder.readObject
Yaml.load
XStream.fromXML
ObjectMapper.readValue
JSON.parseObject
```
## 0x04 反序列化漏洞利用
### 1.[框架]Spring
#### Spring Framework 4.2.4 反序列化漏洞
POC:   https://github.com/zerothoughts/spring-jndi
![](https://images.seebug.org/content/images/2017/06/14968351994824.png-w331s)
分析：http://llfam.cn/2019/11/11/spring_4.2.4_unser/
### 2.[组件]Apache Commons Collections
分析：https://www.iswin.org/2015/11/13/Apache-CommonsCollections-Deserialized-Vulnerability/
### 3.[组件]Fastjson
分析： https://paper.seebug.org/1318/
### 4.[组件]Shiro
分析： https://paper.seebug.org/1503/

### 5. Apache Solr
### 3. WebLogic


## Ref
- [深入理解 JAVA 反序列化漏洞](https://paper.seebug.org/312/#2)
- https://yinwc.github.io/2020/02/08/java%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96%E6%BC%8F%E6%B4%9E
- http://llfam.cn/2019/11/11/spring_4.2.4_unser/
- https://www.iswin.org/2015/11/13/Apache-CommonsCollections-Deserialized-Vulnerability/
- https://paper.seebug.org/1318/
