# Factory Method Pattern

工厂方法模式是常用的设计模式之一。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。  
在工厂方法模式中，我们在创建对象时不会对客户端暴露创建逻辑，并且是通过使用一个共同的接口来指向新创建的对象。  
工厂方法模式和简单工厂模式区别在于，简单工厂模式只有一个工厂，通过传参来确定生成的需要使用对象，而工厂方法模式对于每个需要使用的对象分别创建对应的工厂，通过生成指定的工厂来生成需要使用的对象，感觉它俩没有本质的不同。

## 模式**介绍**

**模式定义**  
工厂方法模式\(Factory Method Pattern\)又称为工厂模式，也叫虚拟构造器\(Virtual Constructor\)模式或者多态工厂\(Polymorphic Factory\)模式，它属于类创建型模式。在工厂方法模式中，工厂父类负责定义创建产品对象的公共接口，而工厂子类则负责生成具体的产品对象，这样做的目的是将产品类的实例化操作延迟到工厂子类中完成，即通过工厂子类来确定究竟应该实例化哪一个具体产品类。

 **模式意图**  
定义一个创建对象的接口，让其子类自己决定实例化哪一个工厂类，工厂模式使其创建过程延迟到子类进行。

**主要解决**  
主要解决接口选择的问题。

**何时使用**  
我们明确地计划不同条件下创建不同实例时。

**如何解决**  
让其子类实现工厂接口，返回的也是一个抽象的产品。

**关键代码**  
创建过程在其子类执行。

## 模式结构

工厂方法模式包含如下角色：

* Product：抽象产品
* ConcreteProduct：具体产品
* Factory：抽象工厂
* ConcreteFactory：具体工厂

## **使用场景**

 1、日志记录器：记录可能记录到本地硬盘、系统事件、远程服务器等，用户可以选择记录日志到什么地方。 

2、数据库访问，当用户不知道最后系统采用哪一类数据库，以及数据库可能有变化时。 

3、设计一个连接服务器的框架，需要三个协议，"POP3"、"IMAP"、"HTTP"，可以把这三个作为产品类，共同实现一个接口。

## **优点**

1、一个调用者想创建一个对象，只要知道其名称就可以了。 

2、扩展性高，如果想增加一个产品，只要扩展一个工厂类就可以。 

3、屏蔽产品的具体实现，调用者只关心产品的接口。

## **缺点**

每次增加一个产品时，都需要增加一个具体类和对象实现工厂，使得系统中类的个数成倍增加，在一定程度上增加了系统的复杂度，同时也增加了系统具体类的依赖。这并不是什么好事。

##  **注意事项**

作为一种创建类模式，在任何需要生成复杂对象的地方，都可以使用工厂方法模式。有一点需要注意的地方就是复杂对象适合使用工厂模式，而简单对象，特别是只需要通过 new 就可以完成创建的对象，无需使用工厂模式。如果使用工厂模式，就需要引入一个工厂类，会增加系统的复杂度。

## 应用实例

我们以日志记录器作为例子，记录数据可以存在mysql、redis和file中，他们有共同的方法wirte\(\)。

第一步，我们要创建这三种方式的父类或者公共接口，也就是抽象产品。

```php
interface Log {
    public function write();
}
```

第二步，我们创建这三种方式具体操作的类，也就是具体产品。

```php
class MysqlLog implements Log{

    public function write()
    {
        // TODO: Implement write() method.
        echo "把日志存在mysql.";
    }
}
class RedisLog implements Log {

    public function write()
    {
        // TODO: Implement write() method.
        echo "把日志存在redis.";
    }
}
class FileLog implements Log {

    public function write()
    {
        // TODO: Implement write() method.
        echo "把日志存在file.";
    }
}
```

第三步，创建这三种方式工厂的父类或者公共接口，也就是抽象工厂。

```php
interface LogFactory {
    public function getLog();
}
```

第四步，我们创建生成这三种方式具体操作的类的工厂，也就是具体工厂。

```php
class MysqlFactory implements LogFactory{

    public function getLog()
    {
        // TODO: Implement getLog() method.
        return new MysqlLog();
    }
}
class RedisFactory implements LogFactory{

    public function getLog()
    {
        // TODO: Implement getLog() method.
        return new RedisLog();
    }
}
class FileFactory implements LogFactory{

    public function getLog()
    {
        // TODO: Implement getLog() method.
        return new FileLog();
    }
}
```

第五步，客户端调用来记录日志。

```php
$logObj = new MysqlFactory();
$logObj ->getLog()->write();
// 运行结果：把日志存在mysql.
$logObj = new RedisFactory();
$logObj ->getLog()->write();
// 运行结果：把日志存在redis.
$logObj = new FileFactory();
$logObj ->getLog()->write();
// 运行结果：把日志存在file.
```



