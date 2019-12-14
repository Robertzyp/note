### 抽象工厂
1. 动机
  - 与工厂方法不同的是，一个工厂可以对应多个产品
2. 定义
  - 提供一个创建相互依赖对象的接口
3. 结构
  - 抽象工厂
  - 具体工厂
  - 抽象产品
  - 具体产品
4. 时序图
  - ![时序图](./seq_AbatractFactory.jpg)

5. 代码分析
 ```php
  interface IFactory();
  abstract FactoryA{
    function createA1();
    function createA2();
  }

  class CreateFactoryA {
    function createA1()
    function createA2(）
  }

  class client {
    function test() {
      $a = new CreateFactoryA();
      $a->createA1();
    }
  }

```

6. 总结
  - 感觉是对工厂的优化，同一款产品类可能有不同的产品但是操作是一样的，用抽象工厂进行约束，工厂提供不同的接口生产不同的实例