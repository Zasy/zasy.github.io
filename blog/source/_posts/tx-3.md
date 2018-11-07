---
title: regex in Golang -线上回滚日记 3
date: 2018-06-22 01:34:35
tags: 
- regex
- going
---

## regexp 包

上几节的内容中对正则有了初步的了解。只有不断的训练才会加深印象，当项目中碰到时，才可以有余力去完成项目中的挑战。

* 简单模式： 使用`Match`方法便可：

  ```go
  ok, _ := regexp.Match(pat, []byte(searchIn))
  ```

* 使用Compile方法，返回Regexp对像，匹配符合模式的字符串对象，指定re对象的方法


### example

```go
package main

import (
   "strconv"
   "regexp"
   "fmt"
)

func main() {
   SearchIn := "John: 2578.34 William: 4567.23 Steve: 5632.18"
   pat := "[0-9]+.[0-9]+"

   f := func(s string) string {
      v, _ := strconv.ParseFloat(s, 32)
      return strconv.FormatFloat(v*2, 'f', 2, 32)
   }

   if ok, _ := regexp.Match(pat, []byte(SearchIn)); ok {
      fmt.Println("Match Found!")
   }

   re, _ := regexp.Compile(pat)

   str := re.ReplaceAllString(SearchIn, "##.#")
   fmt.Println(str)
   str2 := re.ReplaceAllStringFunc(SearchIn, f)
   fmt.Println(str2)

}
```