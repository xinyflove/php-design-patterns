# Factory Method Pattern

工厂方法模式是[简单工厂模式](https://php-design-patterns.gitbook.io/docs/~/edit/drafts/-LSmlduIgDLh7pftnXoj/simple-factory-pattern)的仅一步深化， 在工厂方法模式中，我们不再提供一个统一的工厂类来创建所有的对象，而是针对不同的对象提供不同的工厂。也就是说每个对象都有一个与之对应的工厂。

## 模式定义

工厂方法模式\(Factory Method Pattern\)又称为工厂模式，也叫虚拟构造器\(Virtual Constructor\)模式或者多态工厂\(Polymorphic Factory\)模式，它属于类创建型模式。在工厂方法模式中，工厂父类负责定义创建产品对象的公共接口，而工厂子类则负责生成具体的产品对象，这样做的目的是将产品类的实例化操作延迟到工厂子类中完成，即通过工厂子类来确定究竟应该实例化哪一个具体产品类。

## 实例

我们还是以计算器控制程序为例。 现在需要设计一个这样的运算类，它具有多种运算方法（运算器），用来计算加减乘除。每种运算方法都会有`getResult()`方法返回运算结果， 下面我们完成这个运算类。

首先完成运算方法（运算器）的设计，编写一个运算方法的公共接口

```php
// 运算方法公共接口
interface Operation {
	public function getResult($arg1,$arg2);
}
```

下面就是编写具体的运算方法，每种运算方法都实现`Operation` 接口

加法运算方法

```php
class OperstionAdd implements Operation {

    public function __construct()
    {
        echo ' OperstionAdd: created';
    }

    public function getResult($arg1, $arg2)
	{
		// TODO: Implement getResult() method.
		$result = $arg1 + $arg2;
		echo ' 计算结果:' . $result;
	}
}
```

减法运算方法

```php
class OperstionSub implements Operation {

    public function __construct()
    {
        echo ' OperstionSub: created';
    }

    public function getResult($arg1, $arg2)
    {
        // TODO: Implement getResult() method.
        $result = $arg1 - $arg2;
        echo ' 计算结果:' . $result;
    }
}
```

乘法运算方法

```php
class OperstionMul implements Operation {

    public function __construct()
    {
        echo ' OperstionMul: created';
    }

    public function getResult($arg1, $arg2)
    {
        // TODO: Implement getResult() method.
        $result = $arg1 * $arg2;
        echo ' 计算结果:' . $result;
    }
}
```

除法运算方法

```php
class OperstionDiv implements Operation {

    public function __construct()
    {
        echo ' OperstionDiv: created';
    }

    public function getResult($arg1, $arg2)
    {
        // TODO: Implement getResult() method.
        $result = $arg1 / $arg2;
        echo ' 计算结果:' . $result;
    }
}
```

下面就跟是跟简单工厂模式不一样了， 现在我们按照定义所说定义一个抽象的工厂接口`OperationFactory`。

```php
// 运算工厂接口
interface OperationFactory {
  public function getOperation();
}
```

里面有一个`getOperation()`方法返回我们的Operation 类，接下来我们把上面定义好的每个运算方法都提供一个工厂类，这些工厂类实现了OperationFactory 。

加法运算工厂

```php
class OperstionAddFactory implements OperationFactory {

  public function getOperation()
  {
    // TODO: Implement getOperation() method.
    return new OperstionAdd();
  }
}
```

减法运算工厂

```php
class OperstionSubFactory implements OperationFactory {

  public function getOperation()
  {
    // TODO: Implement getOperation() method.
    return new OperstionSub();
  }
}
```

乘法运算工厂

```php
class OperstionMulFactory implements OperationFactory {

  public function getOperation()
  {
    // TODO: Implement getOperation() method.
    return new OperstionMul();
  }
}
```

除法运算工厂

```php
class OperstionDivFactory implements OperationFactory {

  public function getOperation()
  {
    // TODO: Implement getOperation() method.
    return new OperstionDiv();
  }
}
```

在每个工厂类中我们都通过复写的`getOperation()`方法返回各自的运算方法对象。

 客户端使用

加法运算

```php
$OperationFactory = new OperstionAddFactory();
$Operation = $OperationFactory->getOperation();
$Operation->getResult(1,2);
```

减法运算

```php
$OperationFactory = new OperstionSubFactory();
$Operation = $OperationFactory->getOperation();
$Operation->getResult(6,2);
```

乘法运算

```php
$OperationFactory = new OperstionMulFactory();
$Operation = $OperationFactory->getOperation();
$Operation->getResult(3,2);
```

除法运算

```php
$OperationFactory = new OperstionDivFactory();
$Operation = $OperationFactory->getOperation();
$Operation->getResult(14,2);
```

可以看到上面四段代码，分别进行了不同的运算方法计算，不同之处在于针对不同的运算方法声明了不同的工厂，进而创建了相应的运算方法。

通过这个实例各位小伙伴是不是对工厂模式有了进一步的理解呢，和简单工厂对比一下，最根本的区别在于，**简单工厂模式只有一个统一的工厂类**，**而工厂方法模式是针对每个要创建的对象都会提供一个工厂类**，这些工厂类都实现了一个工厂基类（本例中的OperaitonFactory ）。

## **适用场景**

 （1）客户端不需要知道它所创建的对象的类。例子中我们不知道每个运算方法具体叫什么名，只知道创建它的工厂名就完成了创建过程。  
（2）客户端可以通过子类来指定创建对应的对象。  
以上场景使用于采用工厂方法模式。

