# Go 为什么需要context
    在go中 创建一个goroutine 不会返回一个pid(线程id) 这样就导致不可以从外部终止线程 
    可以使用channel + select 的方式 来解决这个问题 
    但是当场景很复杂的时候 需要花费大量的精力去维护channel 与 协程的关系， 从而导致代码难以维护 需要实现诸如： 有效期、终止线程数、 传递请求全局变量之类的功能

# context 机制 
    context的产生 正是因为goroutine的管理问题 golang从1.7之后引入context 相互调用goroutine之间通过传递context变量 保持关联 这样在不用暴露各个goroutine内部实现细节的前提下， 有效地控制各个goroutine的运行。通过传递context就可以追踪groutine 调用树 并且调用树之间传递通知和元数据
    虽然goroutine之间是平行的，没有继承关系，但是Context设计成是包含父子关系的，这样可以更好的描述goroutine调用之间的树型关系。

# context 定义是什么样子的
    ```
    type Context interface {
        Deadline()(dealine time.Time, ok bool)
        Done() <-chan struct{}
        Err() error
        Value(key interface{})interface{}
    }
    ```
    context包里的方法是线程安全的 可以被多个线程使用
    当Context被canceled或是timeout Done返回一个被close的channel
    在Done的channel被关闭后 Err代表被关闭的原因 如果存在
    Deadline 返回Context关闭的时间 
    如果存在Value返回与key相关的值

# Context使用
    step1 创建context 的根结点
    ```
    func Background() Context \\ 此方法创建的ctx 不能被取消 没有值 也没有过期时间 通常是在主协程或者第一个处理Request的协程中
    ```
    step2 创建下层context节点
    1 父节点context可以主动通过调用cancel 方法取消字节点context
    2 子节点context 只能被动等待
    3 父节点context 自身一旦被取消 如期上节点cancel 旗下所有的字节点context均会自动被取消
    ```
    func handler() {
        fmt.Println("handler start ...")
        // 创建继承Background 的子节点Context
        ctx, cancel := context.WithCancel(context.Background())
        go do(ctx)
        cancel()
        time.Sleep(5 * time.Second)
        fmt.Println("handler end...", time.Now())
    }

    func do(ctx context.Context) {
        i := 1
        for {
            time.Sleep(1 * time.Second)
            select {
            case <-ctx.Done():
                fmt.Println("done", time.Now())
                return
            default:
                fmt.Printf("work %d seconds: %v \n", i, time.Now())
            }
            i++
        }
    }

    // 主协程 调用cancel 取消子协程
    func main() {
        fmt.Println("main start")
        handler()
        fmt.Println("main end....")
    }

    ```

# context是如何实现的

context的存储和查询 上下文像是一个树 每个节点都存储 一个key/value对 withvalue（）保存一个key/value 它将父context嵌入到子context 并在节点中保存了key/value 会从当前的context中查询 如果查询不到 会递归查询父级context中的数据
备注：context中的上下文数据不是全局的，它只查询本节点及父节点们的数据，不能查询兄弟节点的数据。

cannel()实现

cancelCtx结构体中children保存它的所有子canceler， 当外部触发cancel时，会调用children中的所有cancel()来终止所有的cancelCtx。done用来标识是否已被cancel。当外部触发cancel、或者父Context的channel关闭时，此done也会关闭。

对于超时调用cancel(), 是因为timerCtx 中存储了一个超时时间，等到超时间到期之后，会主动调用cancel()。



参考

https://segmentfault.com/a/1190000017872359
https://www.sohamkamani.com/blog/golang/2018-06-17-golang-using-context-cancellation/
https://studygolang.com/articles/23740#reply0


