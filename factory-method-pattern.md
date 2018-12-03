# Factory Method Pattern

工厂方法模式是[简单工厂模式](https://php-design-patterns.gitbook.io/docs/~/edit/drafts/-LSmlduIgDLh7pftnXoj/simple-factory-pattern)的仅一步深化， 在工厂方法模式中，我们不再提供一个统一的工厂类来创建所有的对象，而是针对不同的对象提供不同的工厂。也就是说每个对象都有一个与之对应的工厂。

## 模式定义

工厂方法模式\(Factory Method Pattern\)又称为工厂模式，也叫虚拟构造器\(Virtual Constructor\)模式或者多态工厂\(Polymorphic Factory\)模式，它属于类创建型模式。在工厂方法模式中，工厂父类负责定义创建产品对象的公共接口，而工厂子类则负责生成具体的产品对象，这样做的目的是将产品类的实例化操作延迟到工厂子类中完成，即通过工厂子类来确定究竟应该实例化哪一个具体产品类。

## 实例

我们还是以计算器控制程序为例。 现在需要设计一个这样的运算类，它具有多种计算方式，用来计算加减乘除。每种计算方式都会有`getResult()`方法返回计算结果， 下面我们完成这个运算类。

 

```php
// 运算接口
interface Operation {
	public function getResult($arg1,$arg2);
}
```

{% hint style="info" %}
这里定义成抽象类也是可以的，只不过接口是更高一级的抽象，所以习惯定义成接口，而且接口支持多实现，方便以后扩展。
{% endhint %}

 下面就是编写具体的计算方式，每种计算方式都实现`Operation` 接口

加法

```php
// 加法类 实现运算接口
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

减法

```php
// 减法类 实现运算接口
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

乘法

```php
// 乘法类 实现运算接口
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

除法

```php
// 除法类 实现运算接口
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

 下面是工厂类的具体实现

## **适用场景**

