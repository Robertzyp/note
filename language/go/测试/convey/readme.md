# 网页测试工具
可在controller test 和service test执行
## 安装
`go get github.com/wallclockbuilder/convey`

## 使用
```go
// 不同convey 互不影响
Convey("Normal: ", t, func() {
    // 模拟service 返回值
    addrSvc.EXPECT().Create(Any()).Return(nil)
    // 模拟http 请求数据
    payload := strings.NewReader("{\n\t\"mobilephone\": \"234\"\n}")
    // 封装请求参数
    req, _ := http.NewRequest("POST", url, payload)
    // 添加请求头
		req.Header.Add("Content-Type", "application/json")
		req.Header.Add("cache-control", "no-cache")
    response := new(tests.Response)
    // 模拟请求
    ctx := e.NewContext(req, response)
    // 模拟set 参数
    ctx.Set(constants.UserID, uint(1))
    ctx.SetParam .... // 含有多种方法
    // 指定controller 方法
    addressCtrl.Create(ctx)
    // 查看期望返回值
    So(response.StatusCode, ShouldEqual, 200)
    
})
```