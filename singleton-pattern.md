# Singleton Pattern

单例模式是最简单的设计模式之一。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。  
这种模式涉及到一个单一的类，该类负责创建自己的对象，同时确保只有单个对象被创建。这个类提供了一种访问其唯一的对象的方式，可以直接访问，不需要实例化该类的对象。

## 模式介绍 <a id="mo-shi-jie-shao"></a>

**模式定义**  
单例模式\(Singleton Pattern\)：单例模式确保某一个类只有一个实例，而且自行实例化并向整个系统提供这个实例，这个类称为单例类，它提供全局访问的方法。  
单例模式的要点有三个：一是某个类只能有一个实例；二是它必须自行创建这个实例；三是它必须自行向整个系统提供这个实例。单例模式是一种对象创建型模式。单例模式又名单件模式或单态模式。

**意图**  
保证一个类仅有一个实例，并提供一个访问它的全局访问点。

**主要解决**  
一个全局使用的类频繁地创建与销毁。

**何时使用**  
当您想控制实例数目，节省系统资源的时候。

**如何解决**  
判断系统是否已经有这个单例，如果有则返回，如果没有则创建。

**关键代码**  
构造函数是私有的。

##  模式结构

单例模式包含如下角色：

* Singleton：单例

##  使用场景

1、要求生产唯一序列号。   
2、WEB 中的计数器，不用每次刷新都在数据库里加一次，用单例先缓存起来。   
3、创建的一个对象需要消耗的资源过多，比如 I/O 与数据库的连接等。

## **优点：**

1、在内存里只有一个实例，减少了内存的开销，尤其是频繁的创建和销毁实例。   
****2、避免对资源的多重占用（比如写文件操作）。

## **缺点**

没有接口，不能继承，与单一职责原则冲突，一个类应该只关心内部逻辑，而不关心外面怎么样来实例化。

##  **注意事项**

* 提供一个自身的**静态私有**成员变量；
* 单例类的构造函数为**私有**；
* 提供一个**公有**的静态工厂方法。

##  应用实例

 最常用的地方是数据库连接，我们以数据库连接为例。

```php
class Database {
    private static $instance;

    private function __construct()
    {
        echo '连接数据库,';
    }

    public static function getInstance()
    {
        if(!self::$instance)
        {
            self::$instance = new Database();
        }
        return self::$instance;
    }

    public function execute()
    {
        echo '执行sql语句';
    }
}
```

客户端调用

```php
$db = Database::getInstance();
$db->execute();
```

运行结果：

 连接数据库,执行sql语句



 单例模式生成一个对象后，该对象可以被其它众多对象所使用。
