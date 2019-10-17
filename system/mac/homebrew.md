# 遇到问题 下载安装包失败
解决方法：https://lequ7.com/2019/08/20/richang/jie-jue-Homebrew-an-zhuang-ruan-jian-xia-zai-shi-bai/

```brew install rabbitmq```

查看缓存位置
```brew cache```

下载未能成功的下载包 放到缓存位置

```brew install rabbitmq -v```

看到缓存文件位置不同 移动下载好的安装包 放置 该文件夹 文件名称和下载名称应该一致 并去除.incomplete
