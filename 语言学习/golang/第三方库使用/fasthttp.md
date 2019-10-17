# fasthttp

fasthttp 是Go的一款不同于标准库的net/http 的http实现 性能可达到 标准库的10倍 

net/http 的实现 是一个连接 新建一个goroutine fasthttp 是利用一个worker 服用goroutine 减轻runtime 调度goroutine的压力
net/http 解析的请求数据很多事放在map[string]string 或 map[string][]string 有不必要的[]byte 到string 转换 是可以规避的
net/http 解析 HTTP 请求每次生成新的 *http.Request 和 http.ResponseWriter; fasthttp 解析 HTTP 数据到 *fasthttp.RequestCtx，然后使用 sync.Pool 复用结构实例，减少对象的数量
fasthttp 会延迟解析 HTTP 请求中的数据，尤其是 Body 部分。这样节省了很多不直接操作 Body 的情况的消耗
但是因为 fasthttp 的实现与标准库差距较大，所以 API 的设计完全不同。使用时既需要理解 HTTP 的处理过程，又需要注意和标准库的差别。

step 安装fasthttp 1 
``` go get -u github.com/valyala/fasthttp ```

get 请求 
```status, resp, err := fasthttp.Get(nil, url)
	if err != nil {
		fmt.Println("请求失败:", err.Error())
		return
	}
	if status != fasthttp.StatusOK {
		fmt.Println("请求没有成功:", status)
		return
	}
	fmt.Println(string(resp)) ```

post请求 
``` 
args := &fasthttp.Args{}
	args.Add("name", "xiaoming")
	args.Add("age", "22")

	status, resp, err := fasthttp.Post(nil, url, args)
	if err != nil {
		fmt.Println("请求失败:", err.Error())
		return
	}

	if status != fasthttp.StatusOK {
		fmt.Println("请求没有成功:", status)
		return
	}

	fmt.Println(string(resp))
 ```
 请求
 ```
 req := &fasthttp.Request{}
 req.SetRequestURI("http://XXXX")
 req.SetBody(body)
 req.Header.SetContentType("application/xml")
 req.Header.SetMethod(method)
 resp := &fasthttp.Response{}
 client := &fasthttp.Client{}
 if err := client.Do(req, resp); err != nil {
	logger.Error("请求失败:", err.Error())
	return nil, err
 }
 ```