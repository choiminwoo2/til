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

## 3. Go의 반복문은 다른 언어와 같지만 선언 부에 소괄호를 사용하지 않습니다.

```go
package main

import "fmt"

func main() {
    sum := 0
    for i := 0; i < 10; i++ {
        sum += i
    }
    fmt.Println(sum)
}
```

## 4. Go에서는 while문 대신 for {} 로 무한 루프를 선언합니다.

```go
package main

import "fmt"

func main() {
    for {
    }
}
```


