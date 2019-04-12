# SqlMock 数据库模拟工具 暂用于service单元测试
## 安装
`go get github.com/DATA-DOG/go-sqlmock`
## 使用、引入
```go
	"github.com/DATA-DOG/go-sqlmock"
	"github.com/fpay/microkit-go/internal/tests"
	. "github.com/smartystreets/goconvey/convey"
// 声明mockService
func MockAddressService(t *testing.T) (*AddressService, sqlmock.Sqlmock, func()) {
	db, mock, teardown := tests.MockDB(t)
	addrSvc := NewAddressService(db, &tests.MockSnowflake{})
	return addrSvc, mock, teardown
}
func TestAddressService_Get(t *testing.T) {
	addrSvc, mock, teardown := MockAddressService(t)
	defer teardown()
	Convey("NotFound: ", t, func() {
    // 声明所执行的sql 必须所有写的sql 都执行到 Gorm里面无Delete
    mock.ExpectQuery("^SELECT").WillReturnRows(sqlmock.NewRows([]string{"id"}).FromCSVString(""))
    mock.ExpectExec("^UPDATE").WillReturnResult(sqlmock.NewResult(1, 1))
    mock.ExpectExec("^INSERT INTO").WillReturnResult(sqlmock.NewResult(1, 1)
    // 添加事务
    mock.ExpectBegin()
		mock.ExpectQuery("^select").WithArgs(5).WillReturnRows(sqlmock.NewRows([]string{"stock"}).FromCSVString("10"))
		mock.ExpectExec("^update").WillReturnResult(sqlmock.NewResult(1, 1))
		mock.ExpectCommit()
    _, err := addrSvc.Get(8)
		So(err, ShouldEqual, codes.RecordNotFoundErr)
	})

	Convey("Normal", t, func() {
		mock.ExpectQuery("^SELECT").WillReturnRows(sqlmock.NewRows([]string{"id"}).FromCSVString("1"))
		_, err := addrSvc.Get(8)
		So(err, ShouldEqual, nil)
	})
}
```