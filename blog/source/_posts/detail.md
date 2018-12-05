---
title: 常见面试问题—细节篇
date: 2018-10-19 11:27:11
tags: 细节
---

1. 什么是RESTful架构：

　　（1）每一个URI代表一种资源；

　　（2）客户端和服务器之间，传递这种资源的某种表现层；

　　（3）客户端通过四个HTTP动词，对服务器端资源进行操作，实现"表现层状态转化"。

2. **状态转化（State Transfer）**
   1. **GET用来获取资源**
   2. **POST用来新建资源（也可以用于更新资源）**
   3. **PUT用来更新资源**
   4. **DELETE用来删除资源**

3. 适配器模式

   将一个类的接口，转换成客户期望的另一个接口，适配器让原本接口不兼容的类可以合作无间

   针对接口编程的具体实现，例如：将类的接口对外的接口

4. Go的接口是什么

   1. 接口提供了一种方式来说明对象的行为

   2. 接口定义了一组方法，但是这些方法不包含(实现代码)：它们没有被实现。接口内也不能包含变量。

      ```go
      type Namer interface {
          Method1(param_list) return_type
          Method2(param_lsit) return_type
          ...
      }
      ```

      接口的名字由方法名加`[e]r`后缀组成

   3. 类型不需要显示声明它实现了某个接口：接口被隐式的实现。多个类型可以实现同一个接口。
   4. 实现某个接口的类型可以有其他的方法
   5. 一个类型可以实现多个接口
   6. 接口类型可以包含一个实例的引用，改实例的类型实现了此接口（接口是动态类型）

   ```go
   package main
   
   import "fmt"
   
   type Shaper interface {
       Area() float32
   }
   
   type Square struct {
       side float32
   }
   
   type (sq *Square) Area() float32 {
       return sq.side * sq.side
   }
   
   func main(){
       sq1 := new(Square)
       sql.side = 5
       
       var areaIntf Shaper
       areaIntf = sq1
       
       // shorter, without separate declaration
       // areaIntf := Shaper(sq1)
       // or even:
       // areaIntf := sq1
       fmt.Printf("The square has area: %f\n", areaIntf.Area())    
   }
   ```

   7. 接口变量中包含了接受者实例的值和指向对应方法表的指针
   8. 多态的go版本， interface相当于一个函数能力的表格，实现了表格里的函数的实例可以被赋值给改接口的实例，接口实例运行时，就按照表格中记录的接口实现的方法的地址去调用具体的实现。这个和多态的理解是一样的：同一个类型在不同的实例上似乎表现不同的行为
   9. 也可以以一种稍微不同的方式来使用接口这个词：从某个类型的角度来看，它的接口指的是：它的所有的导出方法，只不过没有显示地为这些导出方法额外定一个接口而已

5. 死锁的必要条件
   1. 互斥
   2. 占有且等待
   3. 不可抢占
   4. 循环等待
6. 避免死锁的方法
   1. 破坏占有且等待条件 (一次申请所有资源，不然阻塞)
   2. 破坏不可抢占条件 (不能申请资源被阻塞时，自己的资源需要被释放，被抢占)
   3. 破坏循环等待条件 (必须按一定的顺序申请资源)

7. 

