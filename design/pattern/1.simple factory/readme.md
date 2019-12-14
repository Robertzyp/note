### 简单工厂 
1. 模型动机
  - 一个系统可以提供不同外观的按钮，子类修改从父类继承的方法进行重写,外部调用逻辑不变
2. 模式定义
  - 又称静态工厂，根据不同的参数返回不同的实例，被创建的类属于同一个父类
3. 模式结构
  - 工厂角色：负责实现创建所有实例的内部逻辑
  - 抽象产品角色：抽象产品角色所创建的父类，描述所有实例的初始化接口
  - 具体产品角色：创建目标，所有创建的对象都充当这个角色的某个具体类的实例。

  - 总结
    - 工厂角色-> 实例化类的代理
    - 抽象产品角色-> 外部抛出的公共接口
    - 具体产品角色-> 具体的实现类
4. 时序图
  - client->factory->createProduct->used
  - ![时序图](./seq_SimpleFactory.jpg)

5. 代码分析
```php
interface IProduct{}
class ProductA extends IProduct{}
class ProductB extends IProduct{}

class Factory {
  function New(IProduct $a) {
    if($a == "a") {
      return new ProductA;
    }

    if($a == "b") {
      return new ProductB;
    }
  } 
}
```

6. 模式分析
  - 创建与使用逻辑分离
  - 静态方法使用方便
  - 增减工厂需要增加配置
7. 使用环境
  - 客户端不需要知道细节，对创建的对象实现不关心