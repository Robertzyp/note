## vue 脚手架
`vue init webpack my project`
### 开发
  1. 组件化开发
  2. props 组件间传递信息
  3. vuex 数据状态管理器
   - state 数据
   - getter 获取store 里数据 可以进行数据过滤
   - Mutation 同步更新 store 数据
   - action 异步提交mutation
   - module 数据源过大，进行分离model
  4. api 存放 所有接口请求的数据
  5. mock 数据 利用json-server
  6. 生命周期函数
   - data() 初始化变量
   - watch() 监听变量是否更改
   - computed() 目前多用于初始化store 数据 和getter 读取
   - components() 挂载用到的组件
   - methods() function 可在其他方法调用
   - mounted() 挂载
  7. style 加上scoped 组件内样式