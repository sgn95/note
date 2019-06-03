
Go语言处理error

Go 语言没有类似 Java 或 .NET 中的异常处理机制，虽然可以使用 defer、panic、recover 模拟，但官方并不主张这样做。Go 语言的设计者认为其他语言的异常机制已被过度使用，上层逻辑需要为函数发生的异常付出太多的资源。同时，如果函数使用者觉得错误处理很麻烦而忽略错误，那么程序将在不可预知的时刻崩溃。
Go 语言希望开发者将错误处理视为正常开发必须实现的环节，正确地处理每一个可能发生错误的函数。同时，Go 语言使用返回值返回错误的机制，也能大幅降低编译器、运行时处理错误的复杂度，让开发者真正地掌握错误的处理

Go处理错误的思想 
    
    通过返回error接口方式来处理函数的错误 再调用之后进行错误检查 如果调用该函数错误出现错误 就返回error接口的实现 指出具体的实现 指出具体的内容 如果执行成功 返回nil

    type error interface{
        Error() string
    }
    Error 可以通过一个

自定义error 任何定义实现了Error() string 函数 都可以认为是error 接口的实现 可以自己定义接口实现业务

    // 直接使用error.New来定义消息
    notFound := errors.New("404 not found")

    // 也可以使用fmt包中Errorf来添加
    fmt.Errorf("404 not found")
    


参考 https://studygolang.com/articles/20719#reply0