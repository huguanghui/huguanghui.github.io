---
title: 译文_C?Go?Cgo
reward: true
date: 2019-01-01 21:03:17
description:
categories:
- 文档
tags:
- Go语言
---

# C?Go?Cgo

    2011/03/17

## 引言

Go中的Cgo工具让Go包可以调用C代码.在Go源码中使用特定的格式,cgo可以将Go和C文件组合成一个单一的Go包.

举个例子,下面的Go包中有调用C的random和srandom组成的Random和Seed两个函数.

```go
package rand

/*
#include <stdlib.h>
*/
import "C"

func Random() int {
    return int(C.random())
}

func Seed(i int) {
    C.srandom(C.uint(i))
}
```

下面我们来从import状态开始分析一下发生些什么情况.

1. rand包import "C".
    你在Go的标准库中是无法找到"C"对应的包的.这是因为C是一个"伪包".此处的C伪包是一个C代码的参考,被cgo工具解析.

2. rand包中包含了C包中的4个调用. C.random, C.srandom, C.uint(i)转换和import状态

3. Random函数调用C标准库中的random函数,返回了一个结果.在C中, random返回得是C类型中的long,所有cgo会把这个类型
   写成C.long.如果想在包外使用这个参数,必须要转换成Go的参数类型.使用一个普通的Go类型转换

    ```go
    func Random() int {
        return int(C.random())
    }
    ```

    等价下面使用临时变量转换

    ```go
    func Random() int {
        var r C.long = C.random()
        return int(r)
    }
    ```

4. Seed函数相反.它获取到一个Go中int类型,将它转换成C中的unsigned int类型,再把转换后的参数传入C的srandom函数中.

    ```go
    func Seed(i int) {
        C.srandom(C.uint(i))
    }
    ```

    注意: cgo知道unsigned int类型是C.uint类型.

5. 这个例子中我们还没有分析import状态行上的注释

   ```go
    /*
    #include <stdlib.h>
    */
    import "C"
   ```

   Cgo可以识别这个注释.任何以#cgo开始后面接有空格字符的行将会被移除.这些行变成了cgo的指令.在编译这个包中C部分的代码
   时,剩余行会变成头部分.在这个例子中,这些行就是#include,也可以是任何的C代码.当编译包中的C部分时,#cgo指令对于编辑器和链接器提供标识.

   这里还有一个限制条件:如果你的程序中使用了任何一个//export指令,在注释上的C代码将只会包含声明,没有定义.你可以使用//export指令让Go函数能访问到C代码.

   #cgo和//export指令可以在cgo文档中查看.

## Strings 和 things

不像Go, C没有一个明确的string类型.在C中字符串使用以'\0'表示符结尾的字符数组.

Go和C中的字符串转换使用C.CString, C.GoString, 和C.GoStringN函数.这些转换就是对一个字符传数据的一个拷贝.

下面这个例子是实现了一个Print函数,将字符串使用C中stdio库的fputs显示到标准输出.

```go
package print

// #include <stdio.h>
// #include <stdlib.h>
import "C"
import "unsafe"

func Print(s string) {
    cs := C.CString(s)
    C.fputs(cs, (*C.FILE)(C.stdout))
    C.free(unsafe.Pointer(cs))
}
```

Go的内存管理器无法知道C代码的内存分配.当我们使用C.CString创建一个C的字符串时,必须要记得在适当的位置使用C.free进行释放.

调用C.CString返回了一个指向字符数组开始地方的指针,所以在这个函数退出前,我们要将它转换成unsafe.Pointer和使用C.free使用
内存.在cgo程序中处理内存释放的一个惯用方法是在分配内存后立即使用defer去释放.Print可以改写成

```go
func Print(s string) {
    cs := C.CString(s)
    defer C.free(unsafe.Pointer(cs))
    C.fputs(cs, (*C.FILE)(C.stdout))
}
```

## 编译cgo包

编译cgo包和编译其他包一样,使用go build或go install.go工具识别import "C"自动使用cgo去编译对应的文件

## cgo的其他资源

    [cgo commond](https://golang.org/cmd/cgo/)
    [cgo example](https://golang.org/misc/cgo/)

    如果想了解cgo的内部工作原理,可以看下cgocall.go文件.