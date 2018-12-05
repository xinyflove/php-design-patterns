# Abstract Factory Pattern

抽象工厂模式是围绕一个超级工厂创建其他工厂。该超级工厂又称为其他工厂的工厂。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。  
在抽象工厂模式中，接口是负责创建一个相关对象的工厂，不需要显式指定它们的类。每个生成的工厂都能按照工厂模式提供对象。

## 模式介绍

**模式定义**  
抽象工厂模式\(Abstract Factory Pattern\)：提供一个创建一系列相关或相互依赖对象的接口，而无须指定它们具体的类。抽象工厂模式又称为Kit模式，属于对象创建型模式。

**意图**  
提供一个创建一系列相关或相互依赖对象的接口，而无需指定它们具体的类。

**主要解决**  
主要解决接口选择的问题。

**何时使用**  
系统的产品有多于一个的产品族，而系统只消费其中某一族的产品。

**如何解决**  
在一个产品族里面，定义多个产品。

**关键代码**  
在一个工厂里聚合多个同类产品。

## 模式结构

抽象工厂模式包含如下角色：

* AbstractFactory：抽象工厂
* ConcreteFactory：具体工厂
* AbstractProduct：抽象产品
* Product：具体产品

## 使用场景

1、QQ 换皮肤，一整套一起换。   
2、生成不同操作系统的程序。

## **优点**

当一个产品族中的多个对象被设计成一起工作时，它能保证客户端始终只使用同一个产品族中的对象。

## **缺点**

产品族扩展非常困难，要增加一个系列的某一产品，既要在抽象的 Creator 里加代码，又要在具体的里面加代码。

##  **注意事项**

产品族难扩展，产品等级易扩展。

##  应用实例

第一步， 为形状创建一个接口。

```php
interface Shape {
    public function draw();
}
```

第二步， 创建实现接口的实体类。

```php
class Rectangle implements Shape {

    public function draw()
    {
        // TODO: Implement draw() method.
        echo " 画长方形 ";
    }
}
class Square implements Shape {

    public function draw()
    {
        // TODO: Implement draw() method.
        echo " 画正方形 ";
    }
}
class Circle implements Shape {

    public function draw()
    {
        // TODO: Implement draw() method.
        echo " 画圆形 ";
    }
}
```

第三步， 为颜色创建一个接口。

```php
interface Color {
    public function fill();
}
```

第四步， 创建实现接口的实体类。

```php
class Red implements Color {

    public function fill()
    {
        // TODO: Implement fill() method.
        echo " 填充红色 ";
    }
}
class Green implements Color {

    public function fill()
    {
        // TODO: Implement fill() method.
        echo " 填充绿色 ";
    }
}
class Blue implements Color {

    public function fill()
    {
        // TODO: Implement fill() method.
        echo " 填充蓝色 ";
    }
}
```

第五步， 为 Color 和 Shape 对象创建抽象类来获取工厂。

```php
abstract class AbstractFactory {
    abstract public function getShape($shape);
    abstract public function getColor($color);
}
```

第六步， 创建扩展了 AbstractFactory 的工厂类，基于给定的信息生成实体类的对象。

```php
class ShapeFactory extends AbstractFactory {

    public function getShape($shapeType)
    {
        // TODO: Implement getShape() method.
        if(empty($shapeType)){
            return null;
        }
        if($shapeType == 'CIRCLE'){
            return new Circle();
        } else if($shapeType == 'RECTANGLE'){
            return new Rectangle();
        } else if($shapeType == 'SQUARE'){
            return new Square();
        }
        return null;
    }

    public function getColor($colorType)
    {
        // TODO: Implement getColor() method.
        return null;
    }
}
class ColorFactory extends AbstractFactory {

    public function getShape($shapeType)
    {
        // TODO: Implement getShape() method.
        return null;
    }

    public function getColor($colorType)
    {
        // TODO: Implement getColor() method.
        if(empty($colorType)){
            return null;
        }
        if($colorType == 'RED'){
            return new Red();
        } else if($colorType == 'GREEN'){
            return new Green();
        } else if($colorType == 'BLUE'){
            return new Blue();
        }
        return null;
    }
}
```

第七步， 创建一个工厂创造器/生成器类，通过传递形状或颜色信息来获取工厂。

```php
class FactoryProducer {
    public static function getFactory($choice)
    {
        if($choice == 'SHAPE'){
            return new ShapeFactory();
        } else if($choice == 'COLOR'){
            return new ColorFactory();
        }
        return null;
    }
}
```

第八步， 客户端调用，使用 FactoryProducer 来获取 AbstractFactory，通过传递类型信息来获取实体类的对象。

```php
// 获取形状工厂
$shapeFactory = FactoryProducer::getFactory('SHAPE');
// 获取形状为 Circle 的对象
$shape1 = $shapeFactory->getShape("CIRCLE");
// 调用 Circle 的 draw 方法
$shape1->draw();
// 获取形状为 Rectangle 的对象
$shape2 = $shapeFactory->getShape("RECTANGLE");
// 调用 Rectangle 的 draw 方法
$shape2->draw();
// 获取形状为 Square 的对象
$shape3 = $shapeFactory->getShape("SQUARE");
// 调用 Square 的 draw 方法
$shape3->draw();

// 获取颜色工厂
$colorFactory = FactoryProducer::getFactory('COLOR');
// 获取颜色为 Red 的对象
$color1 = $colorFactory->getColor("RED");
// 调用 Red 的 fill 方法
$color1->fill();
// 获取颜色为 Green 的对象
$color2 = $colorFactory->getColor("GREEN");
// 调用 Green 的 fill 方法
$color2->fill();
// 获取颜色为 Blue 的对象
$color3 = $colorFactory->getColor("BLUE");
// 调用 Blue 的 fill 方法
$color3->fill();
```

 执行程序，输出结果：

 画圆形 画长方形 画正方形 填充红色 填充绿色 填充蓝色

