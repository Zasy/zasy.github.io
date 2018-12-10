---
title: Go装饰器模式教程
date: 2018-10-22 10:57:21
tags: Go
---

对于某类确定的问题，使用装饰器模式是一个完美的解决方案。

#### 理解装饰器模式

> **Decorators** essentially allow you to wrap existing functionality and append or prepend your own custom functionality on top.
>
> 装饰器允许你包裹现存的函数功能并且在外层追加自己的函数。

在Go语言中，function被当作基类对象，这就意味着你可以将函数当作变量进行传递。一个例子：

```go
package main

import (
	"fmt"
	"time"
)

func myFunc() {
	fmt.Println("Hello World")
	time.Sleep(1*time.Second)
}

func main(){
	fmt.Printf("Type: %T\n", myFunc)
}
```

**这表明函数可以被传递，作为调用的实参**，接下来扩展一下我们的函数并且添加一个coolFunc()函数，这个函数令一个函数作为它的参数。

```go
package main

import (
"fmt"
"time"
)

func myFunc() {
	fmt.Println("Hello World")
	time.Sleep(1*time.Second)
}


func coolFunc(a func()){
	a()
}

func main(){
	fmt.Printf("Type: %T\n", myFunc)

	coolFunc(myFunc)
}
```

函数作为参数传递给`coolFunc`函数运行`a()`

这里有必要添加一个抽象层去包裹`myFunc`

#### 一个简单的装饰器实例

使用一个简单的实例来给代码实例添加值。添加一些额外的log来观察一下部分函数的开始时间和结束时间

```go
package main

import (
	"fmt"
	"time"
)

func myFunc() {
	fmt.Println("Hello World")
	time.Sleep(1 * time.Second)
}

func coolFunc(a func()) {
	fmt.Printf("Starting function execution: %s\n", time.Now())
	a()
	fmt.Printf("End of function execution: %s\n", time.Now())
}

func main() {
	fmt.Printf("Type: %T\n", myFunc)
	coolFunc(myFunc)
}
```

#### 现实的例子

这里实现一个简单的http web server 并且装饰我们的节点。这样我们可以验证是否来的请求有特定的header set。

这里我们可以添加一个简单的认证装饰器函数，这个函数可以检查过来的请求头部是否被验证过。

```go
package main

import (
	"fmt"
	"log"
	"net/http"
)

func isAuthorized(endpoint func(http.ResponseWriter, *http.Request)) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request){
        fmt.Println("Checking to see if Authorized header set...")
        
        if val, ok := r.Header["Authoried"]; ok {
            fmt.Println(val)
            if val[0] == "true"{
                fmt.Println("Header is set! We can serve content!")
                endpoint(w, r);
            }
        }else {
            fmt.Println("Not Authorized!!")
            fmt.Fprintf(w, "Not Authorized!!")
        }
    })
}

func homePage(w http.ResponseWriter, r *http.Request) {
	fmt.Println("Endpoint Hit: homePage")
	fmt.Fprintf(w, "Welcome to the HomePage!")
}

func handleRequests() {
    http.HandleFunc("/", isAuthorized(homePage))
    // if we want to decotator more function
    http.HandleFunc("/new", isAuthrized(newEndPoint))
    
	log.Fatal(http.ListenAndServe(":8081", nil))
}

func main() {
	handleRequests()
}
```

在正式的进入到http的处理文件之前，对处理函数进行装饰，使主处理函数在装饰函数的合理位置运行。

通俗的理解，给处理函数进行了必要的装饰。从代码复用的角度来说，装饰器，将一些可以抽象出来的必要的组件抽象出来，并将所要装饰的函数作为参数传递进去，起到装饰器添加的装饰的作用后，再运行传入的函数

[装饰器]: https://tutorialedge.net/golang/go-decorator-function-pattern-tutorial/	"Go Decorator Function Pattern Tutorial"

