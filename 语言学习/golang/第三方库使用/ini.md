golang ini 库

安装  go get github.com/go-ini/ini

根据开发环境读取不同环境的变量 覆盖默认选项
``` package setting

import (
	"os"

	"gopkg.in/ini.v1"
)

// AppString 全局配置项
var AppString map[string]string

// SetUp 配置文件 配置 默认读取内容都是string
func SetUp() {
	conf, _ := ini.Load("conf/app.ini")
	defValue, _ := conf.GetSection(ini.DEFAULT_SECTION)
	AppString = defValue.KeysHash()
	if os.Getenv("runmode") == "dev" {
		devSetting, _ := conf.GetSection("dev")
		devSettingHash := devSetting.KeysHash()
		for key, value := range devSettingHash {
			AppString[key] = value
		}
	}
	if os.Getenv("runmode") == "prod" {
		prodSetting, _ := conf.GetSection("dev")
		prodSettingHash := prodSetting.KeysHash()
		for key, value := range prodSettingHash {
			AppString[key] = value
		}
	}
} ```