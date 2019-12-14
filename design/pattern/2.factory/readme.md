### 工厂方法
1. 模型动机
  - 简单工厂把所有创建放到一个地方，添加删除需要更改，不满足开闭原则
2. 定义
  - 工厂父类提供一个接口，子类具体去实现创建类
3. 结构
  - 抽象产品
  - 具体产品
  - 抽象工厂
  - 具体工厂
  - 总结
    - 工厂为所有的产品制作了一个工厂
4. 时序图
  - client->createFactory->create->product->Used
  - ![时序图](./seq_FactoryMethod.jpg)
5. 代码分析
```php
interface IFactory {}
class FactoryA{
  function newO(){
    return new ProductA
  }
}
class ProductA{}

// 相当于客户端知道要调用什么工厂
class Client {
  function test(){
    $p = new FactoryA;
    $p->newO();
  }
}
```

6. 模式分析
  - 感觉是把 控制权交给了客户端

7. 实用环境
  - 客户端知道要调用工厂，不在乎内部逻辑
8. 总结
  - 工厂方法可以使工厂的类，创建完全有客户端控制，工厂变更，只改变自己的，符合开闭原则
  - 类容易过多、客户端必须要知道调用的工厂