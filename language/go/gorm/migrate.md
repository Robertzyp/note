# 数据库迁移
## 使用工具 goose

### 安装
`go get -u github.com/pressly/goose/cmd/goose`

### 使用
`goose create add_some_column sql`
`goose up //执行所有sql` 
`goose up-to // 执行制定sql` 