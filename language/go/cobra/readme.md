# cobra go 服务托管工具
## 安装
`go get -u github.com/spf13/cobra/cobra`
## 使用
`cobra init// 初始化`

## 代码
```go
// 添加命令  
func init() {
	rootCmd.AddCommand(businessServerCmd)
}
```

## 启动服务
```go
go run entry/main.go b-server -c config.yaml

// 也可编译之后运行
go build entry/main.go
./main b-server
```