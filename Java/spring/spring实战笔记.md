# spring实战笔记

## DI - 依赖注入

由来

任何重要的应用都需要至少两个相互合作的类来完成业务逻辑。通常，每个对象都要自己负责得到它合作（依赖）的对象，这会导致代码耦合度变高且难以测试。

依赖注入是spring做的最基本的事情，依赖注入通常被称为反向控制，是因为获取依赖对象的方式反转了，以前是自己创建，现在是容器将对象注入进来，由容器控制对象的生命周期。

Greeting Service接口将实现从接口中分离出来

```java
public interface GreetingService {
  void sayGreeting();
}
```

Greeting ServiceImpl负责打印问候语

```java
public class GreetingServiceImpl implements GreetingService {
  private String greeting;
  public GreetingServiceImpl() {}
  public GreetingServiceImpl(String greeting) {
    this.greeting = greeting;
  }
  
  public void sayGreeting() {
    System.out.println(greeting);
  }
  
  public void setGreeting(String greeting) {
    this.greeting = greeting;
  }
}
```

从程序中可以看到GreetingServiceImpl类只有一个属性，可以使用构造方法和属性的setter两种方法赋值。

在Spring中配置Hello World

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemalocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans-2.0.xsd">
	<bean id = "greetingService"
        class = "com.springinaction.chapter01.hello.GreetingServiceImpl">
   	<prooerty name="greeting" value="Buenos Dias!" />
  </bean>
</beans>
```

***<beans>***是Spring配置文件的根元素，**<bean>**是元素用来在Spring容器中定义一个类以及它的配置信息。id表示greetingServiceBean的名字，class属性表示Bean的全路径类名。

<property>元素表示设置属性值，<property>是通过调用Bean的setter方法来设置属性值的。

<constructor-arg>元素是通过构造方法来设置属性值的。



### 装配

创建应用组件之间关联的动作叫做装配。spring装配组件的方法：

- XML



## AOP

### 由来

系统通常有很多组件组成，每个组件负责一部分功能，但是这些组件经常带有一些除了核心功能之外的附加功能。比如系统服务日志、事务管理和安全经常被融入到一些其他功能模块中。由于它们总是分布在应用的很多组件中，所以这些系统服务通常叫做交叉业务。这会导致代码的双重复杂性：

- 实现系统级业务的代码在多个组件中复制。意味着你要修改这些业务逻辑，需要到各个模块中去修改。就算你将这些业务代码抽象为一个独立的模块，其他模块只是调用这一个方法，但是这个方法调用还是分布在很多地方。
- 你的组件会因为那些与自己核心业务无关的代码而变得混乱。

### 概述

AOP可以帮助我们将这些服务模块化，并把它们声明式地应用在需要它们的地方，使得组件更加关注于自身业务，不用关心涉及到的其他系统服务。

DI使软件松散链接成为可能，AOP可以捕捉应用中经常使用的功能，把它转化为可重用组件。

### AOP示例

```java
// 使用AOP之前
package com.springinaction.chapter01.knight;
import org.apache.log4j.Logger;

public class Minstrel {
  private static final Logger SONG = Logger.getLogger(Minstrel.class);
  
  public void singBefore(Knight knight) {
    Song.info("Fa la la; Sir " + knight.getName() + "is so brave!");
  }
  
  public void singAfter(Knight knight) {
    SONG.info("Tee-hee-he; Sir " + knight.getName() + "did embark on a quest!");
  }
}

// KnightOfTheRoundTable
....
private Minstrel minstel;
public Void setMinstrel(Minstrel minstrel) {
  this.minstrel = minstrel;
}
....
  
public HolyGrail embarkOnQuest() throws QuestFailedException {
  minstrel.singBefore(this);
  HolyGrail grail = quest.embark();
  minstrel.singAfter(this);
  return grail;
}
```

```java
// 使用AOP之后

```



