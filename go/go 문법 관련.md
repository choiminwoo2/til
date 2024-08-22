# 다른 언어와 다른 GO의 문법 정리

## 1. go 패키지 사용시 유의점. package와 import가 붙어 있다면 EOF 에러가 발생합니다.
```go
package main
import "fmt"

func main() {
    fmt.Println("Hello, World!")
}

```

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}

```

## 2. Go는 reselt 타입을 미리 정하고 반환이 가능합니다.

```go
package main

import "fmt"

func split(sum int) (x, y int){
	x = sum * 4 / 9
	y = sugom - x
	return
}

func main() {
	fmt.Println(split(17))
	//result
	//7 10
}
```

