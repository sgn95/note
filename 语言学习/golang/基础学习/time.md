# time 包

定时任务

一个三秒的定时器
timer := time.NewTimer(3 * time.Second)
Rest

用于重置定时器

该方法返回一个bool类型的值

Stop

用来停止定时器

该方法返回一个bool类型的值，如果返回false，说明该定时器在之前已经到期或者已经被停止了,反之返回true。


time.After函数， 表示多少时间之后，但是在取出channel内容之前不阻塞，后续程序可以继续执行

鉴于After特性，其通常用来处理程序超时问题

time.Afterfunc函数
```
package main

import (
    "fmt"
    "time"
)
func main(){
    var t *time.Timer

    f := func(){
        fmt.Printf("Expiration time : %v.\n", time.Now())
        fmt.Printf("C`s len: %d\n", len(t.C))
    }

    t = time.AfterFunc(1*time.Second, f)
    //让当前Goroutine 睡眠2s，确保大于内容的完整
    //这样做原因是，time.AfterFunc的调用不会被阻塞。它会以一部的方式在到期事件来临执行我们自定义函数f。
    time.Sleep(2 * time.Second)
}
```
转自 https://www.kancloud.cn/digest/batu-go/153534
