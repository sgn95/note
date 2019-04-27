# Go mod 使用

---
为了告别GOPATH 使用go mod
go modules 是golang 1.11版本添加的新特性

## 使用
### 环境变量设置 GO111MODULE

Go1.11 的 module 是GO111MODULE的环境变量 变量分别由三个值 off on auto
GO111MODULE=off  go命令不会使用module功能 相反的 他还是会在rendor和GOPATH目录中查找依赖包 这种模式也是GOPATH模式

GO111MODULE=on go命令开启module功能 而不会访问GOPATH 这种模式称作module-aware 模式, 这种模式下GOPATH不在go build时 扮演导入角色 但是下载依赖包还是保存在GOPATH/pkg/mod目录下

GO111MODULE=auto 这种是默认模式  如果项目目录不在GOPATH/src下并且目录下没有go.mod文件 或者GOPATH/src下面子目录包含go.mod才会启用
    
