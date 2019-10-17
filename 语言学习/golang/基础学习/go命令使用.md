# simple go demo 

go 工具链
    go command args
    build
                 目标操作系统  cpu类型
        跨平台编译 GOOS=linux GOARCH=amd64 

    install 
        会把打包好的文件 放到pkg中
    get
        获取第三方包 默认会从git 仓库取
    fmt 
        统一代码风格 格式化代码
    test
        运行当前包目录下的tests
        [go test] [go test -v] -v 信息更加详细
        go test 命名一般使用 xxx_test.go xxx--文件名

go test  的使用

```
文件名格式 xxx_test.go 必须是_test结尾
定义 方法 首字母大写
T 传参 (t *testing.T)
t.SkipNow() 跳过接下来的执行结果
t.Run() shun xun
 ```    
    
go的benchmark
