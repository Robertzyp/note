### laravel

#### 流程
  1. 接口请求->middleware->controller -> service-> model-> controller-> json-response
#### 服务
  1. 服务提供者 注册服务，添加门面调用
  2.  bootstrap/app.php 

### 事件
  1. 事件->监听者 event   app/Providers/EventServiceProvider.php 添加事件与监听者绑定
#### 队列
  1. 运行队列 php artisan queue:work rabbitmq --queue=name --daemon
  2. $this->release(10); 手动释放任务
  3. 检查重试次数 $this->attempts()
  4. 指定队列  `$job = (new SendReminderEmail($user))->onQueue('emails');`
  5. 分发队列  ` $this->dispatch($job);`
  6. 延迟任务  ` $job = (new SendReminderEmail($user))->delay(60);`
  7. Supervisor linux下进程监控软件
  8. php artisan queue:failed 运行失败的任务
  9. php artisan queue:retry 5 重试ID
  10. php artisan queue:forget 5 删除失败任务
  11. php artisan queue:flush 删除所有失败任务