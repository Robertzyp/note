# mockgen controller 测试工具
## 安装
`go get -u github.com/efritz/go-mockgen/...`

## 使用
source = service 源文件 

internal/mock = 生成文件目录 

`mockgen --source=goods.go > internal/mock/`

### 引入以下依赖
```go
	mocks "github.com/fpay/microkit-go/internal/tests/mocks"
	. "github.com/golang/mock/gomock"
	"github.com/labstack/echo"
        . "github.com/smartystreets/goconvey/convey
  
  // 初始化controller
  func genAddressCtrl(t *testing.T) (*AddressController, *mocks.MockAddressService, func()) {
	ctrl := NewController(t)
	addrSvc := mocks.NewMockAddressService(ctrl)
	addressCtrl := NewAddressController(addrSvc)
  return addressCtrl, addrSvc, ctrl.Finish
 } 
  func TestAddressController_Create(t *testing.T) {
	addressCtrl, addrSvc, teardown := genAddressCtrl(t)
	defer teardown()
  e := echo.New()
}
	url := "http://localhost:11189/v1/order"
  // 网页测试工具
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