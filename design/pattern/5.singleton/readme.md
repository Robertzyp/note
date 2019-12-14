### 单例模式

1. 动机
  - 多个对象导致占用内存过多
  - 任务只能被并行的执行一个
2. 定义
  - 保证类只能被实例化一次
  - 全局可访问
3. 结构
  - 单例
4. 时序图
  - ![时序图](./seq_Singleton.jpg)
5. 代码分析 
```php
private $a = null;
private function __construct() {
  
}
private function getInstance() {
if($a == null) {
    return new self();
  }
  
  return $this->a;
}
private function __clone() {

}
```
6. 模式分析
  - 构造方法私有
  - 成员私有变量
  - 共有的获取方法

7. 总结
  - 全局可访问
  - 可以根据内部计数器 多例
  - 省资源
  - 可能存在线程安全问题