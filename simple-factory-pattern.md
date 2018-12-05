# Simple Factory Pattern

简单工厂模式其实并不算是一种设计模式，更多的时候是一种编程习惯。

## 模式定义

简单工厂模式\(Simple Factory Pattern\)：又称为静态工厂方法\(Static Factory Method\)模式，它属于类创建型模式。在简单工厂模式中，可以根据参数的不同返回不同类的实例。简单工厂模式专门定义一个类来负责创建其他类的实例，被创建的实例通常都具有共同的父类。

## 模式结构

简单工厂模式包含如下角色：

* Factory：工厂角色工厂角色负责实现创建所有实例的内部逻辑
* Product：抽象产品角色抽象产品角色是所创建的所有对象的父类，负责描述所有实例所共有的公共接口
* ConcreteProduct：具体产品角色具体产品角色是创建目标，所有创建的对象都充当这个角色的某个具体类的实例。

## 实例

        创建一个计算器控制程序，可以计算给定两个数的加减乘除得到结果。每种运算方法都会有`getResult()`方法返回计算结果，不看代码先考虑一下如何通过该模式设计完成此功能。

　　由题可知加减乘除都属于一种运算方法，并且都具有`getResult`方法，所以首先可以定义一个接口或者抽象类，作为这四个运算方法的公共父类，并在其中声明一个公共的draw方法。

运算接口（抽象产品角色）

```php
interface Operation {
	public function getResult($arg1,$arg2);
}
```

{% hint style="info" %}
这里定义成抽象类也是可以的，只不过接口是更高一级的抽象，所以习惯定义成接口，而且接口支持多实现，方便以后扩展。
{% endhint %}

 下面就是编写具体的运算方法，每种运算方法都实现`Operation` 接口

加法类 实现运算接口（具体产品角色）

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

减法类 实现运算接口（具体产品角色）

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

乘法类 实现运算接口（具体产品角色）

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

除法类 实现运算接口（具体产品角色）

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

 下面是工厂类的具体实现

运算工厂类（工厂角色）

```php
class OperationFactory {

    public static function createOperation($operate)
    {
        $oper = '';
        switch ($operate){
            case '+':
                $oper = new OperstionAdd();
                break;
            case '-':
                $oper = new OperstionSub();
                break;
            case '*':
                $oper = new OperstionMul();
                break;
            case '/':
                $oper = new OperstionDiv();
                break;
        }
        return $oper;
    }
}
```

在这个工厂类中通过传入不同的`$operate`可以`new`不同的运算方法，返回结果为具体的运算类，这个就是简单工厂核心的地方了。

客户端使用

加法

```php
$oper = OperationFactory::createOperation('+');
$oper->getResult(1,2);
```

减法

```php
$oper = OperationFactory::createOperation('-');
$oper->getResult(4,2);
```

乘法

```php
$oper = OperationFactory::createOperation('*');
$oper->getResult(3,2);
```

除法

```php
$oper = OperationFactory::createOperation('/');
$oper->getResult(8,2);
```

 只通过给`OperationFactory`传入不同的参数就实现了各种运算方法的计算。以上就是简单工厂方式。

##  **适用场景**

其实由定义也大概能推测出其使用场景，首先由于只有一个工厂类，所以工厂类中创建的对象不能太多，否则工厂类的业务逻辑就太复杂了，其次由于工厂类封装了对象的创建过程，所以客户端应该不关心对象的创建。总结一下适用场景：  
　　（1）需要创建的对象较少。  
　　（2）客户端不关心对象的创建过程。

