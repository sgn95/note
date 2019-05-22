# Go mod 使用

---
为了告别GOPATH 使用go mod
go modules 是golang 1.11版本添加的新特性

## vendor
vendor 是 1.5 release版本的发布 vendor 

## 使用
### 环境变量设置 GO111MODULE

Go1.11 的 module 是GO111MODULE的环境变量 变量分别由三个值 off on auto
GO111MODULE=off  go命令不会使用module功能 相反的 他还是会在rendor和GOPATH目录中查找依赖包 这种模式也是GOPATH模式

GO111MODULE=on go命令开启module功能 而不会访问GOPATH 这种模式称作module-aware 模式, 这种模式下GOPATH不在go build时 扮演导入角色 但是下载依赖包还是保存在GOPATH/pkg/mod目录下

GO111MODULE=auto 这种是默认模式  如果项目目录不在GOPATH/src下并且目录下没有go.mod文件 或者GOPATH/src下面子目录包含go.mod才会启用
    
### go mod命令

download 下载依赖module到本地chache
edit 编辑go.mod文件
graph 打印依赖模块图
init 在当下文件夹下初始化一个新的module
tidy 增加丢失的module 去掉未用的module
vendor 将依赖复制到vendor下
verify 校验依赖
why 解释为什么需要依赖

    go mod 提供了module require replace 和 exclude 四个命令
    module 语句指定包的名字 
    require 指定的依赖项模块 
    replace 语句可以替换依赖项模块
    exclude 语句可以忽略依赖项

### 国内防火墙的问题 *

建议设置 GOPROXY 环境变量 Go 1.11支持 如果设置了该环境变量 下载源代码会通过这个环境变量设置的地址 下载源代码 而不是直接下载
goproxy.io这个开元项目帮我实现了 我们想要的 只需要开发者设置 GOPROXY环境变量即可

windows 用户 
powerShell 命令行 执行
$env:GOPROXY = "https://goproxy.io"

Mac/Linux 命令行执行
export GOPROXY=https://goproxy.io


https://goproxy.io/

参考 https://segmentfault.com/a/1190000018264719
### eg 使用步骤
 
``` 
    mkdir demo
    cd demo
    go mod init demo
    go get ...
使用vscode开发 有错误警告 
    go mod vendor
```

go.sum 是记录所依赖的项目的版本的锁定。

本人使用vscode开发 settings.json 配置如下
```
{
    "go.useCodeSnippetsOnFunctionSuggest": true,
    "go.toolsGopath": "${workspaceFolder}",
    "go.formatTool": "goreturns",
    "go.autocompleteUnimportedPackages": true,
    "go.gopath": "G:/workspace"
}
```