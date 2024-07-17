---
draft: false
date: 2024-04-01
categories:
  - Golang
authors:
  - junho
---

- [go.dev/wiki](https://go.dev/wiki/)

<!-- more -->

## Learn Golang

```sh
# fmt 라이브러리만 사용할때는 go run 파일명.go 실행 가능
# thrid party 라이브러리 사용 시 에는

docker run --rm -it golang:1.18
apt-get update && apt-get install vim -y
echo $GOPATH
  /go
```

```sh
# GOPATH 가 아닌 디렉토리에서 실행 /root/TestApp
# fmt 라이브러리만 사용하므로 정상 실행
mkdir -p ~/TestApp && cd ~/TestApp

# main.go 작성 후 실행 성공!
go run main.go

cat > main.go
package main
import (
    "fmt"
    "github.com/Pallinder/go-randomdata"
)
func main(){
    fmt.Println("Running the TestApp")
    fmt.Println(randomdata.SillyName())
}

go run main.go

# 외부 라이브러리 사용 시 It complains about not finding the package because :
#  1.GOPATH밖 2.패키지 다운로드 안했기 떄문
#  no required module provides package github.com/Pallinder/go-randomdata:
#  go.mod file not found in current directory or any parent directory;
#  use go module to fix this
# Go모듈을 사용하여 해결

# go mod init /root/TestApp
# go.mod 파일 생성

cd hellogo/cookbook
go mod init github.com/jnuho/jnuho.github.io/hellogo/cookbook


# go.mod에 현재 module 정의 외에는 별 내용 없음
# go build 실행 하여 디펜던시를 다운받아야 함
cat go.mod
  module github.com/jnuho/jnuho.github.io/hellogo/TestApp
  go 1.18

# 디펜던시 다운로드. 다른 버전 사용하고자 하면,
# go.mod 파일 수정 후 go build 재실행
go build

# `go mod tidy` fetch all the dependencies that you need for testing in your module.
go mod tidy

# go mod why -m <module>
# find out where any of your dependencies are used (consumed)
go mod why -m golang.org/x/text

# 특정 버전의 패키지 사용
# 디폴트 : latest
go get github.com/bwmarrin/discordgo@v0.20.3

cat go.mod
  require github.com/bwmarrin/discordgo v0.203

go get github.com/bwmarrin/discordgo@latest

# 빌드 하기 전 go.mod 파일 필요
# go build 커멘드로 실행 파일 생성
go build
```

- Vscode > Extension > Go

```sh
### CREATE MODULE ###
cd goproject/calculator
# MODULE_NAME should ideally be on the web
go mod init github.com/jnuho/jnuho.github.io/goproject/calculator
cat go.mod

### CREATE PACKAGE ###
# e.g. two packages
mkdir operations display
# to use 'format.go' inside 'simple.go', use:
# import "github.com/jnuho/jnuho.github.io/goproject/calculator/display"
touch operations/simple.go
touch display/format.go

### COMMIT AND PUSH TO REPO ###
```

```go
### USE ABOVE PACKAGES ###
# mkdir simplego && cd simplego
# cat > main.go
package main

import "github.com/jnuho/jnuho.github.io/goproject/calculator/operations"

func main() {
}
```

```sh
# look through import statements
# and downloads all missing packages/dependencies
# 외부 패키지 다운로드
go mod tidy

cat go.mod
```

- 프로그래밍 언어
  - 어셈블리어 vs. 고수준 언어
    - 어셈블리어는 코드와 기계어가 1:1 매칭이지만 고수준언어 코드는 실행하려며 기계어로 변환 필요
    - 각각의 고수준 언어는 컴파일러 있음 e.g. C 컴파일러, Go 컴파일러
  - 정적 컴파일 언어 vs. 동적 컴파일 언어
    - 미리 컴파일(파른 속도) vs. 사용할때 컴파일(속도 희생, 여러 OS 범용성 뛰어남)
    - Go는 저적 컴파일 언어로, 다양한 플랫폼에 맞도록 실행 파일을 따로 만들어야 함
  - 약 타입 언어 vs. 강 타입 언어
    - Go는 강 타입 언어.

- 가비지 컬렉터 유무
  - 자동 메모리 해제 처리 하여 메모리 관련 문제 적음
  - CPU를 사용하므로 성능 저하 단점


- 코드 실행 단계
  - 폴더생성
  - .go 파일생성 및 작성
  - Go 모듈 생성 (.mod 생성: 모듈명,Go버전,필요패키지 목록 등 정보)
  - 빌드 (`go build`)
    - GOOS GOARCH 환경변수 조정하여 다른 OS및 아키텍쳐에서 실행가능한 파일 생성 가능
    - e.g. `GOOS=linux GOARCH=amd64 go build`
  - 실행

- Go1.16버전 부터 Go 모듈 사용이 기본이 됨
  - 모듈은 패키지 종속성 관리 등 패키지 관리 시스템 역할
  - `Ver < 1.16`: 모든 Go코드는 $GOPATH/src 아래
  - `Ver >= 1.16`: 모든 Go코드는 Go모듈 아래
    - `go mod init MODULE_NAME`으로 Go모듈 생성
    - 모듈이름은 유니크해야 함; GitHub 저장소 주소를 활용하거나 URL을 모듈 이름으로 사용


이름| 설명| 값의 범위
--|--|--
uint8 | 1바이트 부호 없는 정수 | 0~255
uint16 | 2바이트 부호 없는 정수 | 0~65535
uint32 | 4바이트 부호 없는 정수 | 0~4294...95
uint64 | 8바이트 부호 없는 정수 | 0~1844...615
int8 | 1바이트 부호 있는 정수 | -128~127
int16 | 2바이트 부호 있는 정수 | -32768~32767
int32 | 4바이트 부호 있는 정수 | -214...648~214..647
int64 | 8바이트 부호 있는 정수 | -922....808 ~ 922..807
float32 | 4바이트 실수 | IEEE~754 32비트 실수
float64 | 8바이트 실수 | IEEE~754 64비트 실수 (`a:=3.14` will default to float64 type)
complex64 | 8바이트 복소수(진수,가수) | 진수와 가수 범위는 float32 범위와 같음
complex128 | 16바이트 복소수(진수,가수) | 진수와 가수 범위는 float64 범위와 같음
byte | uint8의 별칭 1바이트 데이터 나타낼때 사용 | 0~255 rune | int32별칭 UTF-8로 문자하나 나타낼때 사용 | -214..648~214..647, (`myChar := 'a' will default to rune)`
int |  32비트 컴퓨터에서 int32. 64비트 컴퓨터에서 int64 |
uint |  32비트 컴퓨터에서 uint32. 64비트 컴퓨터에서 uint64 |


- 그외 타입
  - boolean
  - 문자열
  - 배열
  - 슬라이스
  - 구조체
  - 포인터
  - 함수타입
  - 인터페이스
  - 맵
  - 채널

- 타입별 기본값

타입 | 기본값
--|--
모든정수타입 (int8, int16, int32, int64, uint8, uint16, uint32, uint64, int, uint, byte, rune) | 0
모든 실수 타입 (float32, float64, complex64, complex128) | 0.0
불리언 | false
문자열 | "" (빈문자열)
그외 | nil (정의되지 않은 메모리 주소를 나타내는 Go 키워드)


- 디폴트 데이터타입

```go
package main
import (
  "fmt"
  "reflect"
)
func main() {
  // int
  fmt.Println(reflect.TypeOf(10))

  // float64
  fmt.Println(reflect.TypeOf(3.1415))

  // string
  fmt.Println(reflect.TypeOf("LaLaLalla"))

  // bool
  fmt.Println(reflect.TypeOf(true))

  // int32: (rune타입 : 4-byte int32 타입과 별칭)
  fmt.Println(reflect.TypeOf('A'))
}
```


- 변수선언 형태

```go
package main

import "fmt"

func main() {
  var a int = 3
  var b int // 타입별 기본값으로 대체 (초깃값 생략)
  var c = 4 // 우변값의 타입으로 대체 (타입생략)
  d := 5    // 우변값의 타입으로 대체 (var 키워드와 타입 생략)

  fmt.Println(a, b, c ,d)
}
```


### 6.연산자

- numericOperator.go

```go
package main

import (
  "fmt"
)

func main(){
  var x int32 = 7
  //var y float32 = 3.14

  fmt.Println(x + 1)
  fmt.Println(x - 1)
  fmt.Println(x * 1)
  fmt.Println(x / 1)
  fmt.Println(x % 1)

  fmt.Println(x & 1)
  fmt.Println(x | 1)
  fmt.Println(x ^ 1)
  fmt.Println(x &^ 1)

  fmt.Println(x << 1)
  fmt.Println(x >> 1)
}
```

- compOperator.go

```go
package main

import (
  "fmt"
)

func main(){
  var x int32 = 7
  var y float32 = 3.14

  fmt.Println(x == y)
  fmt.Println(x != y)
  fmt.Println(x * y)
  fmt.Println(x < y)
  fmt.Println(x > y)
  fmt.Println(x <= y)
  fmt.Println(x >= y)

}
```

- operationErr1.go
  - 컴퓨터는 2진수로만 표현-> 실수 표현시 오차발생 (e.g. 0.376 != 2^-2 + 2^-3+ ...)
  - 서로 다른 값이 오차에 의해 같다고 나오는 현상 테스트
  - epsilon 값을 정의하여 두 값의 차이가 해당 값보다 작으면 equal처리
- operationErr2.go
  - 비트표현시 '지수부+실수부' 중 가장 오른쪽 비트 하나차이 이내이면 같다고 판단
  - 마지막 비트가 1만큼 차이 나는지 확인
    - `func Nextafter(x,y float64) (r float64)`
    - x에서 y를향 해서 1비트 조정 (+ or - 한 값을 반환)

```go
package main

import (
  "fmt"
  "math"
)

const epsilon = 0.000001

func equal(a, b float64) bool {
  diff := math.Abs(a-b)

  if diff <= epsilon {
    return true
  } else {
    return false
  }

}

func main() {
  var a float64 = 0.1
  var b float64 = 0.2
  var c float64 = 0.3

  fmt.Printf("%0.18f + %0.18f = %0.18f\n", a, b, a+b)
  fmt.Printf("%0.18f == %0.18f : %v\n", c, a+b, equal(a+b,c))

  a= 0.0000000000004
  b= 0.0000000000002
  c= 0.0000000000007

  fmt.Printf("%g == %g : %v\n", c, a+b, equal(a+b,c))

}
```

- operationErr2.go


```go

package main

import (
  "fmt"
  "math"
)

func equal(a, b float64) bool {
  return math.Nextafter(a,b) == b
}

func main() {
  var a float64 = 0.1
  var b float64 = 0.2
  var c float64 = 0.3

  fmt.Printf("%0.18f + %0.18f = %0.18f\n", a, b, a+b)
  fmt.Printf("%0.18f == %0.18f : %v\n", c, a+b, equal(a+b,c))

  a= 0.0000000000004
  b= 0.0000000000002
  c= 0.0000000000007

  fmt.Printf("%g == %g : %v\n", c, a+b, equal(a+b,c))
}
```

- operationErr3.go


```go

package main

import (
  "fmt"
  "math/big"
)

func main() {
  a, _ :=  new(big.Float).SetString("0.1") // a
  b, _ :=  new(big.Float).SetString("0.2") // b
  c, _ :=  new(big.Float).SetString("0.3") // c

  d := new(big.Float).Add(a,b) // a+b
  fmt.Println(a, b, c, d)
  fmt.Println(c.Cmp(d)) // 0: equals (정밀도 높음)
}
```

- 논리 연산자
  - `|| && !`


- 대입연산자
  - `a,b =3,4`
  - `a,b = b,a`
  - `a=10 b=a`

- 증감연산자
  - `a++ a-- += -=`
  - `a++` 는 값을 반환하지 않음!

- 연산자 우선순위

### 7.함수


```go
package main
import "fmt"

func factorial(n int) int {

  if n <= 1  {
    return 1
  } else {
    return n * factorial(n-1)
  }
}

func main() {

  fmt.Println(factorial(5))
}
```

### 8.상수


```go
const Pig int = 0
const Cow int = 1
const Chicken int = 2

const PI = 3.14
const PI2 float64 = 3.14

// iota로 간편하게 열거값 사용 하기
// 1씩증가. 소괄호 벗어나면 다시 초기화 됨
const (
  Red   int = iota // 0
  Blue  int = iota // 1
  Green int = iota // 2
)

// const를 소괄호()로 묶고 iota 사용하면
// 0부터 1씩 차례로 증가하며 값이 초기화 됨
const (
  C1 uint = iota + 1 // 1 = 0 + 1
  C2                 // 2 = 1 + 1
  C3                 // 3 = 2 + 1
)

const (
  BitFlag1 uint = iota + 1 // 1 = 1 << 0
  BitFlag2                 // 2 = 1 << 1
  BitFlag3                 // 4 = 1 << 2
  BitFlag4                 // 8 = 1 << 3
)

func PrintAnimal(animal int) {
  if animal == Pig {
    fmt.Println("꿀")
  } else if animal == Cow {
    fmt.Println("음메")
  } else if animal == Chicken {
    fmt.Println("꼬끼오")
  }

}

func main() {
  PrintAnimal(Pig)
  PrintAnimal(Cow)
  PrintAnimal(Chicken)

  var a int = PI * 100
  // var b int = PI2 * 100 // ERROR!
  fmt.Println(a)
  // fmt.Println(b)

  fmt.Println(C1)
  fmt.Println(C2)
  fmt.Println(C3)

  fmt.Println(BitFlag1)
  fmt.Println(BitFlag2)
  fmt.Println(BitFlag3)
}
```


### 9.if조건문

```go
  // 초기문을 실행하고 그 결과를 확인할때 조건문 사용
  if 초기문; 조건문 {
    // 초기문의 결과를 확인하는 목적으로 활용가능
  }
```


### 10.switch문

```
// From A Tour of Go
Go only runs the selected case, not all the cases that follow.
In effect, the break statement that is needed at the end of each case
in those languages is provided automatically in Go.
Another important difference is that Go's switch cases need not be constants,
and the values involved need not be integers.
```

```go
package main

import "fmt"


type ColorType int

const (
  Red ColorType = iota // 1
  Blue                 // 2
  Yellow                 // 3
  Green                 // 4
)

func SelectColor(color ColorType) {
  switch color {
    case Red:
      fmt.Println("Red!!!rrrr")
    case Blue:
      fmt.Println("Blue!!!bbb")
    case Yellow:
      fmt.Println("Yellow!!!")
    case Green:
      fmt.Println("Greeen!!!ggg")
  }
}

func main() {
  mycolor := Red
  fmt.Println(mycolor)

}

```

### 11.for문

```go
// label사용은 지양 - 혼동 올 수 있음
func find45(a int) (int, bool) {
  for b := 1; b < 10; b++ {
    if b*a == 45 {
      return b, true
    }
  }
  return 0, false
}

func main() {
  a := 1
  b := 0
  found := false

  for ; a <= 9; a++ {
    // Like for, the if statement can start with a short statement to execute before the condition.
    if b, found = find45(a); found {
      break
    }
  }

  fmt.Printf("%d * %d = %d\n", a, b, a*b)
}
```

```go
package main

import (
  "fmt"
  "math"
)

func pow(x, n, lim float64) float64 {
  // Like for, the if statement can start with a short statement to execute before the condition.
  if v := math.Pow(x, n); v < lim {
    return v
  }
  return lim
}

func main() {
  fmt.Println(
    pow(3, 2, 10),
    pow(3, 3, 20),
  )
}
```


- continue, break

```go
package main

import (
  "bufio"
  "fmt"
  "os"
)

func main() {
  stdin := bufio.NewReader(os.Stdin)

  for {
    // 입력 된 값이 변수에 저장되기 전에 버퍼에 저장
    // 숫자는 number에 저장되고 
    // 숫자 + 
    fmt.Print("숫자를 입력하세요: [-1로 종료]")
    var number int
    _, err := fmt.Scanln(&number)

    if err != nil {
      fmt.Println("숫자가 아닙니다!")

      //키보드 버퍼 비움
      stdin.ReadString('\n')
      continue
    }

    fmt.Printf("입력 하신 숫자는 %d 입니다.", number)

    if number%2 == 0 {
      fmt.Printf("입력 하신 숫자는 짝수, %d, 입니다.\n", number)
    } else if number%2 == 1 {
      fmt.Printf("입력 하신 숫자는 홀수, %d, 입니다.\n", number)
    } else if number == -1 {
      fmt.Printf("for문 종료\n")
      break
    }
  }
}
```


### 12.배열 array

- array copy

```go
package main

import (
  "fmt"
)

func main() {
  a := [5]int{1,2,3,4,5}
  b := [5]int{500,400,300,200,100}

  // a
  for i,v := range a {
    fmt.Printf("a[%d] = %d\n", i, v)
  }

  // b
  fmt.Println()
  for i, v := range b {
    fmt.Printf("b[%d] = %d\n", i, v)
  }

  b = a

  // a가 복사된 b
  fmt.Println()
  for i,v := range b {
    fmt.Printf("b[%d] = %d\n", i, v)
  }
}
```


- multi-array

```go
package main

import (
  "fmt"
)

func main() {
  a := [2][5] int {
    {1,2,3,4,5},
    {6,7,8,9,10},
    // 행바뀜 있을때는 마지막에 , 필요
    // 행바뀜없는 inline 일때는 필요 없음 e.g. { {...},{.., 9,10} }
  }

  for _, arr := range a {
    for _, v := range arr {
      fmt.Print(v, "")
    }
    fmt.Println()
  }
}
```

### 13.구조체 struct


- 컴퓨터가 데이터에 효과적으로 접근하고자, 메모리를 일정 크기 간격으로 정렬
  - 64비트 컴퓨터의 경우 8바이트 단위로 정렬 되어 있는게 효율적
  - int32, float64필드가 있는 구조체의 경우 12바이트(4+8) 가 아닌 16바이트(8+8) 할당
  - 순서를 float64, int32로 하면 12바이트(8+4)
  - 불필요한 메모리 낭비를 줄이려면 작은 크기 필드값을 앞에 배치
  - 패딩: 메모리 정렬을 위해서 필드간 간격을 띄움

```go
package main

import (
  "fmt"
  "unsafe"
)


type User struct {
  A int32 // 4바이트
  B float64 // 8바이트
}

type User2 struct {
  A int8    // 1바이트
  B int     // 8바이트
  C int8    // 1바이트
  D int     // 8바이트
  E int8    // 1바이트
}

type User3 struct {
  A int8    // 1바이트
  C int8    // 1바이트
  E int8    // 1바이트
  B int     // 8바이트
  D int     // 8바이트
}

func main() {
  user := User {34, 97.5}
  // 12바이트가 아닌 16바이트 출력 : 메모리정렬
  // 변수시작주소를 변구크기의 배수로 맞춤
  fmt.Println("user size : ", unsafe.Sizeof(user))

  user2 := User2{1,2,3,4,5}
  fmt.Println("user2 size : ", unsafe.Sizeof(user2))

  user3 := User3{1,2,3,4,5}
  fmt.Println("user3 size : ", unsafe.Sizeof(user3))

}
```

### 14.포인터

```go
func main() {
  var a int = 500
  var p *int

  p = &a

  fmt.Printf("p의 값: %p\n", p) // 메모리 주솟값
  fmt.Printf("p가 가리키는 메모리의 값: %d\n", *p) // p가 가리키는 메모리의 값 *p == a

  *p = 100 // p가 가리키는 메모리의 값 변경
  fmt.Printf("===p가 가리키는 메모리의 값 변경->100===\n")
  fmt.Printf("a의 값: %d\n", a) // a값 변화 확인 *p == a

  var p2 *int = &a
  fmt.Printf("p2도 a를 가리키는 *int 포인터 입니다: \n\tp2= %p, *p2=%d, &a=%p\n", p2,*p2, &a)
}
```


- `==` 연산으로 포인터가 같은 메모리 공간 가리키는지 확인가능


```go
func main() {
  var a int = 10
  var b int = 20

  var p1 *int = &a
  var p2 *int = &a
  var p3 *int = &b

  fmt.Printf("p1 == p2 : %v\n", p1==p2)
  fmt.Printf("p2 == p3 : %v\n", p2==p3)


  // 포인터의 기본값 nil
  var p *int
  if p != nil {
    fmt.Println("포인터 p는 유효한 메모리 공간을 가리킴")
  } else {
    fmt.Println("포인터 p == nil 어떤 메모리 공간도 가리키고 있지 않음")
  }

  // 포인터는 변수대입 또는 함수 인수전달 시 메모리 공간을 적게 사용하면서 사용 가능
}
```


```go
package main

import (
  "fmt"
)

type Data struct {
  value int
  data [200]int
}

// 호출할때마다 Data 구조체 크기만큼의 메모리 복사되고 그 값을 변경함
// 전달받은 변수의 값은 변경 안됨.
// 메모리를 매번 복사하기 때문에 많이 호출 시 성능저하
func ChangeDataNotWorking(arg Data) {
  // 매개'변수' arg 데이터 변경 안됨...
  arg.value = 999
  arg.data[100] = 999
}

func ChangeData(arg *Data) {
  // 매개'변수' arg 데이터 변경
  arg.value = 999
  arg.data[100] = 999
}

func main() {
  // 인스턴스: 메모리에 할당된 '데이터의 실체'
  // 포인터를 이용하여 인스턴스에 접근

  // 인스턴스는 언제사라지나?
  // 메모리에 데이터 할당되고 사라지지 않으면 메모리고갈-> 메모리 해제 Gc가 담당
  // Garbage Collector에 의해 일정 간격으로 메모리에서 쓸모없는 데이터 청소 (인스턴스 등)
  // 생성된 변수 (인스턴스) 메모리는 함수 종료시 사라짐
  // 1.인스턴스는 메모리에 생성된 데이터의 실체
  // 2.포인터를 이용해서 인스턴스를 가리키게 할 수 있음
  // 3.함수 호출 시 포인터 인수를 통해서 인스턴스를 입력받고, 그값을 변경할 수 있게 됨
  // 4.쓸모 없어진 인스턴스는 가비지 컬렉터가 자동으로 지워줌

  // Data 인스턴스 생성
  var data Data
  
  // p: 새로운 Data인스턴스가 생성된 것이 아닌, 기존에 있던 data 인스턴스를 가리키는 포인터 변수
  var p *Data = &data

  fmt.Printf("p.value = %d\n", p.value)
  fmt.Printf("data.value = %d\n", data.value)

  ChangeData(&data)

  // 0->999 확인
  fmt.Printf("p.value = %d\n", p.value)
  fmt.Printf("data.value = %d\n", data.value)

  // 인스턴스 하나만 생성하고 포인터 3개가 하나의 인스턴스 가리킴
  var p1 *Data = &Data{}
  var p2 *Data = p1
  var p3 *Data = p1

  // initial value
  fmt.Println(*p1)

  fmt.Printf("주솟값1 = %p\n", p1)
  fmt.Printf("주솟값2 = %p\n", p2)
  fmt.Printf("주솟값3 = %p\n", p3)

  // 포인터 초기화 방법
  // & 사용한 초기화 방법:
  //    포인터 값을 별도의 변수로 선언하지 않고 초기화 하는 방법
  // new  사용한 초기화 방법
  //    new 초기화 방법은 내부 필드값 초기화는 안됨
  //    & 사용한 초기화 방법과 동일 &Data{} == new(Data)
  //    & 사용한 초기화 방법은 내부 필드값도 초기화 가능 p1 := &Data{3,4}
  p4 := &Data{}
  ChangeData(p4)
  p5 := new(Data)
  ChangeData(p5)

  // var p6 Data
  p6 := Data{}
  ChangeData(&p6)

  fmt.Printf("주솟값4 = %p\n", p4)
  fmt.Printf("p4.value = %d\n", p4.value)
  fmt.Printf("p4.value = %d\n", p4.value)

  fmt.Printf("주솟값5 = %p\n", p5)
  fmt.Printf("p5.value = %d\n", p5.value)
  fmt.Printf("p5.value = %d\n", p5.value)

  fmt.Printf("주솟값6 = %p\n", &p6)
  fmt.Printf("p6.value = %d\n", p6.value)
  fmt.Printf("p6.value = %d\n", p6.value)
}
```


- 스택 메모리 : 힙메모리 영역보다 훨씬 효율적이지만, 함수 내부에서만 사용 가능
- 힙 메모리 : 함수외부로 공개되는 메모리 공간 할당 시, 힙 메모리 영역에서 할당

```go
package main

import "fmt"

type User struct{
  Name string
  Age int
}

func NewUser(name string, age int) *User{
  var u = User{name, age}
  return &u
}

func main() {
  userPointer := NewUser("AAA", 23)
  fmt.Println(userPointer)
  fmt.Printf("userPointer: %v has an address: %p\n", userPointer, userPointer)
}
```

```
* C/C++에서는 malloc() 호출하여 힙메모리 공간 할당
* java에서는 클래스타입을 힙에, 기본타입을 스택에 할당
* Go언어는 탈출검사(escape analysis)로 인스턴스(instance)를 스택메모리 또는 힙메모리 중 어느 메모리에 할당 할 지 결정
* 함수외부로 공개되는 인스턴스의 경우 함수가 종료 되어도 사리지지 않음
  Suppose, we define a public method that returns 내부에서 생성된 객체
  원래, 함수 내부에서 선언된 변수는 함수가 종료되면 사라집니다.
  Go.언어에서는 탈출검사에서 u 변수의 인스턴스가 함수 외부로 공개되는 것을 분석해내서,
  u를 스택 메모리가 아닌 힙메모리에서 할당하게됨. 함수가 종료 되어도 메모리에서 사라지지 않음
  (GC가 해당 객체를 분별 할 수 있음)


* Go언어 스택 메모리는 계속 증가되는 동적 메모리 풀.
*    일정한 크기를 갖는 C/C++언어와 비교해도 메모리 효율성 높고,
*   재귀 호출때문에 스택 메모리 고갈문제는 발생 X
```


### 15.문자열

```go
s1 := "Hello string variable!"
s2 := `Special \t characters \t\t \n inside backticks are ignored\n
  backticks also ignores new lines
  line3
  line4
  line5`

fmt.Println(s1)
fmt.Println(s2)
```

- rune타입 : 4-byte int32타입과 별칭
  - `type rune int32`

```go
  // 문자 하나를 표현하는데 rune 타입 사용
  // UTF-8은 1~3바이트
  // 알파벳 문자열크기 =1, 한글 문자열 크기 = 3
  var c rune = '한'

  fmt.Printf("%T\n", c) // 타입 출력 : int32
  fmt.Println(c)        // int32(rune) 형식 값 출력
  fmt.Printf("%c\n", c) // 문자출력

  // 12 = (1*3) +  (3*3)
  a := "abc가나다"
  fmt.Println(len(a))


  // string <-> []rune 타입 변환
  //     []rune(str)
  //     string([]rune{...})
  str := "Hello World!"
  // []rune{72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100}
  runes := []rune(str)

  fmt.Println(str)
  fmt.Println(runes)
  fmt.Println(string(runes))
  fmt.Println(len(runes))

  for _,v := range runes {
    fmt.Printf("타입: %T, 값: %d, 문자열: %c\n", v,v,v)
  }

  d := []byte(c)
  e := []rune(c)
  // [65 66 67 235 172 184 236 158 144 236 151 180]
  fmt.Println(d)
  // [65 66 67 47928 51088 50676]
  fmt.Println(e)

  // []byte and []rune are immutable, contrary to string
  d[5] = 23
  fmt.Println(string(d))
  e[3] = 244
  fmt.Println(string(e))

  // strng <-> []byte 변환
  // 모든 문자열은 1바이트 배열로 변환 가능
```

- Compare String

```go
  s1 := "Hello"
  s2 := "Hell"
  s3 := "Hello"

  fmt.Printf("%s == %s, %v\n", s1, s2, s1 == s2)
  fmt.Printf("%s == %s, %v\n", s1, s3, s1 == s3)

  str1 := "BBB"
  str2 := "aaaaAAA"
  str3 := "BBAD"
  str4 := "ZZZ"

  fmt.Printf("%s > %s, %v\n", str1, str2, str1 > str1)
  fmt.Printf("%s <= %s, %v\n", str3, str4, str3 <= str4)
```


- string 끼리 대입하기
  - Data, Len 같은지 확인

```go
import (
  "fmt"
  "unsafe"
  "reflect"
)

func main() {
  str1 := "Hello World"
  str2 := str1


  // string -> unsafe.Pointer -> *reflect.StringHeader
  stringHeader1 := (*reflect.StringHeader) (unsafe.Pointer(&str1))
  stringHeader2 := (*reflect.StringHeader) (unsafe.Pointer(&str2))
  
  // 두 값이 같음
  fmt.Println(stringHeader1)
  fmt.Println(stringHeader2)
}
```


- string is immutable


```go
func main() {
  
  var str string = "Hello World"
  str= "How are you"
  // ERROR: string is immutable
  // str[2] = 'a'

  fmt.Println(str)

  var slice []byte = []byte(str)
  slice[2] = 'a'
  fmt.Printf("%s\n", slice)

  // str = string(slice)
  // fmt.Printf("%s\n", str)
}
```

### 16.패키지

- go build 로 실행 파일 만들때 go mod 필요

```sh
go mod init [패키지명]
go mod init 'github.com/jnuho/goproject'
# Go모듈에 필요한 패키지를 찾아서 다운로드, 필요한 패키지 정보를 go.mod, go.sum 파일에 적어줌
go mod tidy
cat go.mod
```


- 패키지 내 필드 외부 공개 여부
  - const, 변수, 함수, 별칭 타입


```sh
# ch16
#   ㄴ usepkg/usepkg.go
#   ㄴ usepkg/go.mod
#   ㄴ usepkg/go.sum
#     ㄴ custompkg/custompkg.go
cd 16-package/usepkg

# 퍼블릭 github 있는 경우
# go mod init github.com/reponame/16-package/usepkg
go mod init 16-package/usepkg
go mod tidy

# ch16
#   ㄴ ex16.2
#     ㄴ ex16.2.go
#     ㄴ publicpkg/publicpkg.go
cd 16-package/ex16.2
go mod init 16-package/ex16.2
go mod tidy
```

- 패키지 초기화
  - 전역변수 초기화
  - init() 호출 (매개변수, 반환값 없는 함수)

```go
package main

import (
  "fmt"
  "math/rand"

  // 겹치는 패키지 이름 별칭으로 묶기
  "text/template"
  htemplate "html/template"

  // 패키지를 사용하지는 않지만 부과효과 떄문에 import 하는 경우
  "database/sql"

  // 밑줄 _을 이용해서 init() 함수 호출
  // 밑줄 _ 이용하여 unused 에러 방지
  _ "github.com/mattn/go-sqlite3"
)

type Service struct {
  db *sql.DB
}

func main() {

  template.New("foo").Parse(`{{define "T"}}Hello`)
  htemplate.New("foo").Parse(`{{define "T"}}Hello`)

  fmt.Println(rand.Int())
}
```

- Go 모듈만들고, 외부 패키지 활용하기

```sh
cd 16-package/usepkg
go mod init 16-package/usepkg
mkdir custompkg
```

- `16-package/usepkg/custompkg/custompkg.go`

```go
package custompkg

import "fmt"

func PrintCustom() {
  fmt.Println("This is custom package!")
}
```


- `16-package/usepkg/usepkg.go`

```go
package main

import (
  "fmt"
  "16-package/usepkg/custompkg" // 모듈 내 패키지
  "github.com/guptarohit/asciigraph" // 외부 저장소 패키지
  "github.com/tuckersGo/musthaveGo/16-package/expkg"
)

func main() {
  custompkg.PrintCustom()
  expkg.PrintSample()

  data := []float64{3,4,5,6,9,7,5,8,5,10,2,7,2,5,6}
  graph := asciigraph.Plot(data)
  fmt.Println(graph)
}
```


- 패키지명과 패키지 외부 공개

```go
cd 16-package/ex16.2/publicpkg
cat publicpkg.go
  package publicpkg

  import "fmt"

  const (
    PI = 3.1415
    pi = 3.1415 // 외부에 공개되지 않음
  )

  var ScreenSize int = 1080 
  var screenHeight int // 외부에 공개되지 않음

  func PublicFunc() {
    const MyConst = 100 // 외부에 공개되지 않음 (대분자 변수라해도, 함수 내부에서 선언되었기 때문에 외부에 공개되지 않음)
    fmt.Println("This is a public function", MyConst)
  }

  func privateFunc() { // 외부에 공개되지 않음
    fmt.Println("This is a private function")
  }

  type MyInt int
  type myString string // 외부에 공개되지 않음

  type MyStruct struct {
    Age int
    name string // 외부에 공개되지 않음
  }

  func (m MyStruct) PublicMethod() {
    fmt.Println("This is a public method")
  }

  func (m MyStruct) privateMethod() { // 외부에 공개되지 않음
    fmt.Println("This is a private method")
  }

  type myPrivateStruct struct { // 외부에 공개되지 않음
    Age int
    name string
  }

  func (m myPrivateStruct) PrivateMethod() { // 외부에 공개되지 않음
    fmt.Println("This is a private method")
  }
```

```sh
cat 16-package/ex16.2
cat ex16.2.go
  package main

  import (
    "fmt"
    "16-package/ex16.2/publicpkg"
  )

  func main() {
    fmt.Println("PI: ", publicpkg.PI)
    publicpkg.PublicFunc()

    var myint publicpkg.MyInt = 10
    fmt.Println("myint:", myint)

    var mystruct = publicpkg.MyStruct{Age: 18}
    fmt.Println("mystrcut:", mystruct)
  }
```

- 패키지 임포트하면 다음 진행
  1. 전역변수 초기화
  2. 패키지에 init() 정의되어 있다면 호출
    - 만약 어떤 패키지의 초기화 함수인 init() 함수기능만 사용하길 원할 경우 밑줄 _ 로 임포트

```go
```

### 17. 랜덤숫자 맞추기 게임

```go
package main

import (
	"bufio"
	"fmt"
	"math/rand"
	"os"
	"time"
)

func Print(o ...interface{}) {
	fmt.Println(o...)
}

func InputIntValue(stdin *bufio.Reader) (int, error) {
	var n int
	fmt.Printf("Guess number (1~100): ")
	_, err := fmt.Scanln(&n)
	if err != nil {
		stdin.ReadString('\n')
	}
	return n, err
}

// Scanln reads a small piece of input (like a number or a word) until the first Enter key press (newline).
// stdin.ReadString reads the entire line of input (including spaces) until the Enter key press (newline).
// Remember, buffered streams help manage data flow,
// and Scanln and ReadString are like different ways of listening to your friend’s answers
// —either short and quick or long and detailed!
// => stdin is more explicit about handling buffering

// Both methods involve buffering, but Scanln abstracts it away for you.
// ReadString gives you more control over the buffering process.
func main() {
	// Seed random
	rand.New(rand.NewSource(time.Now().UnixNano()))

	stdin := bufio.NewReader(os.Stdin)
	guess := rand.Intn(100) + 1
	cnt := 1

	for {
		n, err := InputIntValue(stdin)
		if err != nil {
			fmt.Println("Only numbers are allowed")
		} else {
			if n == guess {
				fmt.Printf("\nYou're correct! %d was guessed in %d attempts!\n", guess, cnt)
				break
			} else if n < guess {
				fmt.Printf("it is bigger than %d\n", n)
			} else if n > guess {
				fmt.Printf("it is smaller than %d\n", n)
			}
			cnt++
		}
	}
}
```

### 18.슬라이스

- slice: 동적배열
  - 일반적인 배열 `var array [10]int`은 일정한 길이에서 늘어나지 않는 문제
  - 동적배열 슬라이스 : `var slice []int`

- [Slice Interview Questions](https://medium.com/@ninucium/go-interview-questions-part-2-slices-87f5289fb7eb)
    1. A slice is a reference data type. Inside there is a pointer to the first element of the slice. This factor is what determines how certain operations, even when performed on copies of the slice, can affect the original slice.
    2. A slice has a length, which describes the number of elements currently stored in the slice, and a capacity, which indicates how many elements can be added to this memory area.
    3. If the inequality len(x) + 1 <= cap(x) is not met when adding a new element, the slice expands into a new area of memory, and capacity doubles (until it reaches the size of 1024, after which they increase by 25% with each expansion).
    4. When you pass a slice as an argument to a function as a copy (not via a pointer), you should remember that the slice contains a pointer to the first element, which allows for modifications to the original slice.
    5. The length and capacity values are passed by copy. If you pass a slice to a function and then the same slice is modified elsewhere in the code (e.g., by adding a new element), it will not affect the length and capacity of the copied slice within the function.

```go
// 초기화 방법
var slice1 = []int{1,2,3} //len:3 cap: 3
var slice2 = []int{1, 5:2, 10:3} // [1 0 0 0 0 2 0 0 0 0 3]
var slice3 = make([]int, 3, 5) // len: 3 cap: 5

for i := 0; i<len(slice1); i++ {
  fmt.Print(slice1[i], " ")
}
for i,v := range slice1 {
  slice[i] = v*2
}
```

- 슬라이스 동작원리
  - func(arr [5]int) 배열 파라미터로 넘기면 전체 배열 COPY : array 요소들 변경 적용 X
  - func(slice []int) 슬라이스 파라미터 포인터까지 복제되므로: array 요소들 변경 적용 됨
    - **reallocation is expensive in terms of time and memory**

- Length: The length of a slice is the number of elements it currently contains. You can get the length of a slice using the built-in len() function.

- Capacity: The capacity of a slice represents the maximum number of elements it can hold without allocating additional memory. You can get the capacity of a slice using the built-in cap() function. Initially, a slice’s capacity is equal to its length, but it can grow as needed. For example:

- Performance

Understanding the difference between length and capacity is crucial for performance optimization. When appending elements to a slice, Go may need to allocate a new underlying array if the capacity is exceeded. This reallocation can be expensive in terms of time and memory.

- Avoiding Reallocation

If you know the expected size of your data, you can preallocate a slice with sufficient capacity to avoid frequent reallocations during appends. This can significantly improve performance. For example:

```go
// Preallocate a slice with capacity 100
myData := make([]int, 0, 100)

// Append elements to myData
// ...
// No reallocation needed as long as len(myData) < 100
```

- Example of a slice with `len=cap=0` and appending
  - When you create a slice without specifying an initial capacity (e.g., `[]int{}`),
  - Go initializes it with a default capacity of 0. However, as you append elements to the slice, Go dynamically manages its capacity.

1. **Dynamic Capacity Growth**:
   - When you append elements to a slice, Go automatically increases its capacity as needed.
   - Initially, the slice has a capacity of 0 (no underlying array).
   - As you append elements, Go allocates a new underlying array with a larger capacity
    - (usually double the current capacity).
   - The existing elements are copied to the new array, and the slice now points to the new array.

2. **Capacity Doubling and Beyond**:
   - Initially, the capacity doubles each time it exceeds the current capacity.
   - However, after a certain point (usually when the capacity reaches 1024 elements), Go switches to increasing the capacity by 25% instead of doubling.
   - This strategy balances memory usage and reallocation frequency.

3. **Example**:

```go
package main

import "fmt"

/**
Length: 1, Capacity: 1
Length: 2, Capacity: 2
Length: 3, Capacity: 4
Length: 4, Capacity: 4
Length: 5, Capacity: 8
Length: 6, Capacity: 8
Length: 7, Capacity: 8
Length: 8, Capacity: 8
Length: 9, Capacity: 16
Length: 10, Capacity: 16
*/
func main() {
    var s []int // Create an empty slice (capacity 0)
    for i := 0; i < 10; i++ {
        s = append(s, i)
        fmt.Printf("Length: %d, Capacity: %d\n", len(s), cap(s))
    }
}
```
In this example, observe how the capacity grows dynamically as elements are appended to the slice.

4. **Efficient Programming Tips**:
   - If you know the expected maximum size of your slice, consider preallocating capacity using `make` (e.g., `make([]int, 0, 100)`).
   - Avoid unnecessary reallocations by setting an initial capacity that accommodates your use case.
   - Be mindful of shared underlying arrays when creating multiple slices from the same array.

Go's dynamic capacity management ensures efficient memory usage while allowing you to work with slices without worrying about manual reallocation.


```go
type SliceHeader struct {
  Data uintptr  // 실제 배열을 가리키는 포인터
  Len int       // 요소개수
  Cap int       // 실제 배열의 길이
}
```


- 문제발생 CASE1

```go
package main
import "fmt"

func main() {
  slice1 := make([]int, 3, 5)
  slice2 := append(slice1, 4, 5)
	slice3 := append(slice2, 6)

  // len() cap()
  // slice1:  [0 0 0] 3 5
  fmt.Println("slice1: ", slice1, len(slice1), cap(slice1))
  // slice2:  [0 0 0 4 5] 5 5
  fmt.Println("slice2: ", slice2, len(slice2), cap(slice2))
  // slice3:  [0 0 0 4 5 6] 6 10
	fmt.Println("slice3: ", slice3, len(slice3), cap(slice3))

  // 문제1: slice1변경 시 둘다 바뀜
  slice1[1] = 100
  fmt.Println("After slice1[1]=100")
  fmt.Println("slice1: ", slice1, len(slice1), cap(slice1))
  fmt.Println("slice2: ", slice2, len(slice2), cap(slice2))
  fmt.Println("slice3: ", slice3, len(slice3), cap(slice3))

  // 문제2: slice1 append()하면 1,2 둘다 바뀌는데,
  // len에 따라 append 위치가 다름
  slice1 = append(slice1, 500)
  fmt.Println("After append(slice1, 500)")
  fmt.Println("slice1: ", slice1, len(slice1), cap(slice1))
  fmt.Println("slice2: ", slice2, len(slice2), cap(slice2))
}

// slice1:  [0 0 0] 3 5
// slice2:  [0 0 0 4 5] 5 5
// After slice1[1]=100
// slice1:  [0 100 0] 3 5
// slice2:  [0 100 0 4 5] 5 5
// After slice1 = append(slice1, 500)
// slice1:  [0 100 0 500] 4 5
// slice2:  [0 100 0 500 5] 5 5
```


- 문제발생 CASE2

```go
// cap이 다 찼을때, append() 하면
// 2배만큼 len 증가
package main
import "fmt"

func main() {
  // len=3 cap=3
  slice1 := []int{1,2,3}

  // cap=len으로 슬라이스 용량이 다 찬 상태에서
  //  append() 실행 시 cap*2만큼 용량(capacity) 증가
  //  cap: 3-> 6
  //  새로운 용량 (6)의 배열이 생성되면서,
  //  slice1과 slice2는 다른배열을 가리키게됨
  slice2 := append(slice1, 4, 5)
  fmt.Println("After slice2 := append(slice1, 4, 5) ")
  fmt.Println("slice1: ", slice1, len(slice1), cap(slice1))
  fmt.Println("slice2: ", slice2, len(slice2), cap(slice2))

  slice1[1] = 100
  fmt.Println("After slice1[1] = 100")
  fmt.Println("slice1: ", slice1, len(slice1), cap(slice1))
  fmt.Println("slice2: ", slice2, len(slice2), cap(slice2))

  slice1 = append(slice1, 500)
  fmt.Println("After slice1 = append(slice1, 500)")
  fmt.Println("slice1: ", slice1, len(slice1), cap(slice1))
  fmt.Println("slice2: ", slice2, len(slice2), cap(slice2))
}

// After slice2 := append(slice1, 4, 5) 
// slice1:  [1 2 3] 3 3
// slice2:  [1 2 3 4 5] 5 6
// After slice1[1] = 100
// slice1:  [1 100 3] 3 3
// slice2:  [1 2 3 4 5] 5 6
// After slice1 = append(slice1, 500)
// slice1:  [1 100 3 500] 4 6
// slice2:  [1 2 3 4 5] 5 6

```

- 슬라이싱

```go
package main

import "fmt"

func main() {
  array := [5]int{1,2,3,4,5}
  slice := array[1:2]


  // 슬라이싱 cap길이 = 시작인덱스 ~끝인덱스 까지의 길이
  //   여기에서는 cap = 시작인덱스 1부터 끝까지 길이 = 4
  fmt.Println("After slice := array[1:2]")
  fmt.Println("array: ", array)
  fmt.Println("slice: ", slice, len(slice), cap(slice))

  array[1] = 100
  fmt.Println("After array[1] = 100")
  fmt.Println("array: ", array)
  fmt.Println("slice: ", slice, len(slice), cap(slice))

  slice = append(slice, 500)
  fmt.Println("After slice = append(slice, 500)")
  fmt.Println("array: ", array)
  fmt.Println("slice: ", slice, len(slice), cap(slice))


  // IF 슬라이스 append를 배열 길이 5이상으로 실행하면
  // array는 그대로, slice는 동적으로 크기 증가: cap*2 용량 증가 및 len 증가
}


// After slice := array[1:2]
// array:  [1 2 3 4 5]
// slice:  [2] 1 4
// After array[1] = 100
// array:  [1 100 3 4 5]
// slice:  [100] 1 4
// After slice = append(slice, 500)
// array:  [1 100 500 4 5]
// slice:  [100 500] 2 4
```



- 슬라이스를 슬라이싱 하기

```go
package main

import "fmt"

func main() {
  slice1 := []int{1,2,3,4,5}
  fmt.Println("slice1: ", slice1, len(slice1), cap(slice1))

  // 중간
  slice2 := slice1[1:3]
  fmt.Println("slice1[1:3]: ", slice2, len(slice2), cap(slice2))

  // 처음부터 i까지
  slice3 := slice1[:3]
  fmt.Println("slice1[:3]: ", slice3, len(slice3), cap(slice3))

  // i부터 끝까지
  slice4 := slice1[1:]
  fmt.Println("slice1[1:]: ", slice4, len(slice4), cap(slice4))

  // 전체
  slice5 := slice1[:]
  fmt.Println("slice1[:]", slice5, len(slice5), cap(slice5))
}
// slice1:  [1 2 3 4 5] 5 5
// slice1[1:3]:  [2 3] 2 4
// slice1[:3]:  [1 2 3] 3 5
// slice1[1:]:  [2 3 4 5] 4 4
// slice1[:] [1 2 3 4 5] 5 5
```




- 슬라이스 복제 (서로 다른 배열 가리키도록)

```go
package main
import "fmt"

func main() {
  slice1 := []int{1,2,3,4,5}

  // 복제
  slice2 := make([]int, len(slice1))
  for i,v := range slice1 {
    slice2[i] = v
  }
  fmt.Println("After slice1-> slice2 복제(for문)")
  fmt.Println("slice1", slice1, len(slice1), cap(slice1))
  fmt.Println("slice2", slice2, len(slice2), cap(slice2))

  // slice1,2는 서로 다른 배열 가리키므로 slice1의 배열만 반영
  slice1[1] = 100
  fmt.Println("After slice1[1] = 100")
  fmt.Println("slice1", slice1, len(slice1), cap(slice1))
  fmt.Println("slice2", slice2, len(slice2), cap(slice2))
}

// After slice1-> slice2 복제(for문)
// slice1 [1 2 3 4 5] 5 5
// slice2 [1 2 3 4 5] 5 5
// After slice1[1] = 100
// slice1 [1 100 3 4 5] 5 5
// slice2 [1 2 3 4 5] 5 5
```

- 슬라이스 복제 (append()로 코드개선)

```go
package main
import "fmt"

func main() {
  slice1 := []int{1,2,3,4,5}
  slice2 := append([]int{}, slice1...)
  fmt.Println("After slice2 := append([]int{}, slice1...)")
  fmt.Println("slice1", slice1, len(slice1), cap(slice1))
  fmt.Println("slice2", slice2, len(slice2), cap(slice2))
}
```




- 슬라이스 복제 (copy()로 코드개선)
  - `func copy(dest, src []Type) int`

```go
package main
import "fmt"

func main() {
  slice1 := []int{1,2,3,4,5}
  slice2 := make([]int, 3, 10) // len:3, cap:10
  slice3 := make([]int, 10) // len:10, cap:10

  // 3개만 복사됨
  cnt1 := copy(slice2, slice1)
  // 5개 복사됨
  cnt2 := copy(slice3, slice1)

  fmt.Println("slice2: ", cnt1, slice2)
  fmt.Println("slice3: ", cnt2, slice3)


  // 같은 cap, len으로 복제하려면:
  // for문으로 실행 하거나
  // copy이용
  slice2 = make([]int, len(slice1))
  copy(slice2, slice1)
  fmt.Println("slice2: ", slice2)
}

// slice2:  3 [1 2 3]
// slice3:  5 [1 2 3 4 5 0 0 0 0 0]
```



- 슬라이스 요소 삭제
  1. 삭제한 요소 인덱스 이후를 1칸씩 당기고, 마지막 요소 슬라이싱 기능으로 제거
  2. 또는 append() 조합으로 요소삭제 후 reassign


- 방법 1. 한칸씩 당기는 작업: for문

```go
package main
import "fmt"

func main() {
  slice1 := []int{1,2,3,4,5}
  del := 2

  for i:=del; i<len(slice1)-1; i++ {
    slice1[i] = slice1[i+1]
  }
  slice1 = slice1[:len(slice1)-1]

  fmt.Printf("After slice1[%d] is deleted: %v  %d %d\n", del, slice1, len(slice1), cap(slice1))
```

- 방법 2. append() 활요

```go
package main
import "fmt"

func main() {
  slice1 := []int{1,2,3,4,5}
  del := 2
  
  slice1 = append(slice1[:del], slice1[del+1:]...)

  fmt.Println("slice1: ", slice1, len(slice1), cap(slice1))
}
```


- 슬라이스 요소 추가
  1. 추가한 요소 인덱스 이후를 1칸씩 밀기: for문
  2. 또는 append() 조합으로 요소추가 후 reassign


- 방법 1. 한칸씩 미는 작업: for문
  - len+1이 되지만 cap*2 가 됨!

```go
package main
import "fmt"
func main() {
  slice1 := []int{1,2,3,4,5}
  add := 2
  slice1 = append(slice1, 0)


  for i:= len(slice1)-1 ; i > add; i-- {
    slice1[i] = slice1[i-1]
  }
  slice1[add] = 100
  slice1 = slice1[:len(slice1)]

  // slice1 [1 2 100 3 4 5] 6 10
  fmt.Println("slice1", slice1, len(slice1), cap(slice1))
}
```

- 방법 2. append() 활용

```go
package main
import "fmt"
func main() {
  slice1 := []int{1,2,3,4,5}
  add := 2
  slice1 = append(slice1[:add], append([]int{100}, slice1[add:]...)...)

  // slice1 [1 2 100 3 4 5] 6 10
  fmt.Println("slice1", slice1, len(slice1), cap(slice1))
}
```



- 슬라이스 요소 (int형) 정렬

```go
package main
import (
  "fmt"
  "sort"
)
func main() {
  slice := []int{5, 1, 2, 3, 4}

  sort.Ints(slice)
  fmt.Println(slice)
}
```

- 구조체 타입 슬라이스 정렬
  - 구조체를 Sort()로 정렬 하려면 '구조체 리스트' 대해 Len(), Less(), Swap() 메소드 구현필요
  - 구조체리스트 = `[]구조체`

```go
package main
import (
  "fmt"
  "sort"
)

type Student struct {
  Name string
  Age int
}

type Students []Student

func (s Students) Len() int {
  return len(s)
}

func (s Students) Less(i, j int) bool {
  return s[i].Age < s[j].Age
}

func (s Students) Swap(i, j int) {
  s[i], s[j] = s[j], s[i]
}

// 구조체 정렬 시 필요한 정의 메소드
// Len(), Less(), Swap()
func main() {
  // 슬라이스안에 {"A", 1} 선언시
  // 구조체 type 명 생략
  slice := []Student {
    {"B", 2},
    {"C", 9},
    {"A", 1},
    {"D", 5},
  }

  sort.Sort(Students(slice))
  fmt.Println(slice)
}
```


### 19.메소드

- `func (r Rabbit) info() int`
  - 리시버: `(r Rabbit)`
  - 메소드명: `info`

- 메소드와 함수의 구분: '소속'
  - 함수는 어디에도 속하지 않지만, 메소드는 리시버에 속함
  - 리시버를 통해 해당 메소드의 소속 명시
  - 메소드를 통해 object와 기능을 묶을 수 있음
- 응집도 높힘
- 객체지향 (절차중심 -> 관계중심)
  - 클래스 상속은 지원 X, 메소드와 인터페이스 O

```go
package main
import "fmt"

type account struct {
  balance int
}

func withdrawFunc(a* account, amount int) { // 일반함수 표현
  a.balance -= amount
}

func (a *account) withdrawMethod(amount int) { // 메소드 표현
  a.balance -= amount
}

func main() {
  a := &account{100}

  withdrawFunc(a, 30)
  a.withdrawMethod(30)

  fmt.Printf("%d \n", a.balance)
}
```


- 별칭 리시버 타입
  - int 타입도 별칭을 통해 리시버로 기능할 수 있음

```go
package main
import "fmt"

// 사용자 정의 별칭 타입
type myInt int

func (a myInt) add(b int) int {
  return int(a) + b
}

func main() {
  var a myInt = 10 // myInt타입변수
  res := a.add(30)
  fmt.Println("myInt + 30 = ", res)

  var b int = 20
  myInt(b)
}
```


- 객체지향: 절차중심 -> 관계중심
  - Student 는 단순히 이름,나이정보를 가지고 있는 데이터가 아니라,
  - 과목을 등록하고, 리포트를 보내는 기능이 추가된 객체(Object)가 됨.

```go
type Student struct {
  FirstName string
  LastName string
  Age int
}

// Student 구조체에 속하는 메소드들
func (s *Student) EnrollClass(c *Subject) {
  // ...
}

func (s *Student) SendReport(p *Professor, r *Report) {
  // ...
}
```

- 포인터 메소드 vs 값타입 메소드

```go
package main
import "fmt"

type account struct {
  balance int
  firstName string
  lastName string
}

// 1. 포인터타입 메소드
func (a1 *account) withdrawPointer(amount int) {
  a1.balance -= amount
}

// 2. 값타입 메소드
func (a2 account) withdrawValue(amount int) {
  a2.balance -= amount
}

// 3. 변경된 값을 반환하는 값 타입 메소드
//  값타입 메소드를 보완하지만, 메모리의 복사가 여러번 일어나 메모리 비효율적
func (a3 account) withdrawReturnValue(amount int) account {
  a3.balance -= amount
  return a3
}

func main() {
  var mainA *account = &account{100, "Joe", "Park"}

  mainA.withdrawPointer(30)
  fmt.Println(mainA)

  // 고언어에서는 (*mainA).withdrawValue(30) 와 같음
  // 복사가 일어나므로 mainA에 변경값 반영안됨
  mainA.withdrawValue(30)
  fmt.Println(mainA)

  mainB := mainA.withdrawReturnValue(30)
  fmt.Println(mainB)
}
```



### 20.인터페이스

- 인터페이스 중괄호 블록안에 메서드 집합 정의시 유의사항:

1. 메소드는 반드시 메소드명이 있어야 함
2. 매개변수와 반환이 다르더라도 이름이 같은 메소드 있을 수 없음
3. 인터페이스에서는 메소드 구현 포함 X

- 추상화
  - 내부동작을 감춰서 서비스를 제공하는 쪽과 사용하는 쪽 모두에게 자율르 주는 방식
  - 구체화된 객체가 아닌 인터페이스만 가지고 메서드 호출 가능.
  - 코드 수정없이 필요에 따라 구체화된 객체를 바꿔서 사용할 수 있음.
  - 프로그램의 변경요청에 유연하게 대처 가능.
- 덕테이핑 - 서비스 사용자 중심 코딩
  - 구조체 타입이 인터페이스를 구현한다는걸 명시할 필요 없음

1. 포함된 인터페이스
2. 빈 인터페이스
3. 인터페이스 기본값

- Interface as parameter

// NOTE
// In Go, interfaces are already reference types.
// When you pass an interface as an argument, you’re effectively passing a reference\
// to the underlying concrete type that implements the interface.
// Even if you pass an interface by value (without a pointer),
// it behaves like a reference because it points to the actual implementation.
// func SendBook(parcel string, sender Sender) {}


```go
package main

import "fmt"

type Stringer interface {
	String() string
}

type Student struct {
	Name string
	Age  int
}

func (s *Student) String() string {
	return fmt.Sprintf("안녕, 나는 %d살, %s라고 해", s.Age, s.Name)
}

func main() {
	student := &Student{"Jake", 9}
  // 인터페이스를 이용하면 메서드 구현을 포함한 구체적인 객체(concrete object)가 아닌,
  // 추상화된 객체(e.g. stringer 변수)로 상호작용 할 수 있습니다.
  // Student타입 객체는 String()메서드를 포함하기 때문에,
  // stringer에 student를 대입 할 수 있다. (abstract away)
	var stringer Stringer // 인터페이스의 기본값은 nil (e.g. stringer == nil)
  stringer = student

	fmt.Printf("%s\n", stringer.String())
}
```


- 우편업체 fedex.FedexSender, koreaPost.PostSender

1. FedexSender

```go
// github.com/tuckersGo/musthaveGo/ch20/fedex
package fedex
import "fmt"

type FedexSender struct {
}

func (f *FedexSender) Send(parcel string) {
  fmt.Printf("Fedex에서 %s를 보냅니다.\n", parcel)
}
```

2. PostSender

```go
// github.com/tuckersGo/musthaveGo/ch20/koreaPost
package koreaPost
import "fmt"

type PostSender struct{
}

func (p *PostSender) Send(parcel string) {
  fmt.Printf("Post우편에서 %s를 보냅니다.\n", parcel)
}
```


- 인터페이스 없이 사용

```go
package main

import (
  "fmt"
  "github.com/tuckersGo/musthaveGo/ch20/fedex"
  "github.com/tuckersGo/musthaveGo/ch20/koreaPost"
)

func SendFedexParcel(parcel string, f *fedex.FedexSender) {
  f.Send(parcel)
}

func SendKoreaPostParcel(parcel string, p *koreaPost.PostSender) {
  p.Send(parcel)
}

func main() {
  f := &fedex.FedexSender{}
  p := &koreaPost.PostSender{}

  // f.Send("fedex parcel")
  // p.Send("koreaPost parcel")
  SendFedexParcel("fedex parcel", f)
  SendKoreaPostParcel("koreaPost parcel", p)
}
```

- 인터페이스 사용
  - 두개 struct 타입이 기능을 공유하되 implemntation이 조금 다름


```go
package main
import (
  "fmt"
  "github.com/tuckersGo/musthaveGo/ch20/fedex"
  "github.com/tuckersGo/musthaveGo/ch20/koreaPost"
)

type Sender interface {
  Send(parcel string)
}

// In Go, interfaces are already reference types.
// When you pass an interface as an argument, you’re effectively passing a reference\
// to the underlying concrete type that implements the interface.
// Even if you pass an interface by value (without a pointer),
// it behaves like a reference because it points to the actual implementation.
func SendBook(parcel string, sender Sender) {
  sender.Send(parcel)
}

func main() {
  f := &fedex.FedexSender{}
  p := &koreaPost.PostSender{}

  SendBook("fedex소포", f)
  SendBook("koreaPost소포", p)
}


- 덕타이핑
  - FedexSender, PostSender에 implements Sender라는 명시를 하지 않아도
  - Sender인터페이스 의 Send() 메소드만 정의했다면 자동으로 duckTyping 됨

- 서비스 사용자 중심 코딩
  - Sender 인터페이스를 서비스 제공자인 Fedex나 Post가 아닌 패키지를 이용하는 쪽에서 만듦
  - 덕타이핑에서는 인터페이스 구현 여부를 타입선언에서 하는게 아니라, 인터페이스가
  - 사용될 때, 해당 타입이 인터페이스에 정의된 메서드를 포함했는지 여부로 결정
  - 서비스 제공자가 인터페이스를 정의할 필요없이, 구체적인 객체만 제공하고,
  - 서비스 이용자가 필요에 따라 그때그떄 인터페이스를 정의해서 사용할 수 있음
```

```go
// A회사: B,C회사의 제품 성능 비교하고자 함
//    A회사가 직접 Database 인터페이스 정의하여
//    TotalTime 함수 사용하도록 구현
// 구조체 BDatabase, CDatabase가 달라서
// 한 함수의 인수로 쓸수 없기때문에, Database 인터페이스 정의
//    Database 인터페이스를 매개변수로 사용 (reference to address)
//    (In Go, interfaces are already reference types!)
func TotalTime(db Database) int {
  db.Get()
  db.Set()
  return ?
}

func Compare() {
  BDB := &BDatabase{}
  CDB := &CDatabase{}

  if TotalTime(BDB) < TotalTime(CDB) {
    fmt.Println("B회사 제품이 더 빠름")
  } else {
    fmt.Println("C회사 제품이 더 빠름")
  }
}

// 덕타이핑을 지원하지 않는다면
//    B 인터페이스 정의, C 인터페이스 정의하여
//    고객에게 알려줘야하는 불편함
//    또한, C에게 B인터페이스를 지원하도록 요청 해야함
//  덕타이핑을 활용하면, 인터페이스 지원여부를 사용하는 쪽에서 판단
```


1. 포함된 인터페이스


```go
package main

type Reader interface {
  Read()(n int, err error)
  Close() error
}

type Writer interface {
  Write()(n int, err error)
  Close() error
}

type ReadWriter interface {
  Reader
  Writer
}
// 1 Read() Write() Close() 포함 타입
//    => Reader, Writer, ReadWriter 모두 사용가능
// 2 Read() Close() 포함 타입
//    => Reader만 사용 가능
// 3 Write Close() 포함 타입
//    => Writer만 사용 가능
// 4 Read() Write() 포함 타입
//    => Close()없기 떄문에 3개 interface 모두 사용 불가능
```

2. 빈 인터페이스

- `interface{}`는 메서도를 가지고 있지 않은 빈 인터페이스
  - 가지고 있어야할 메서드가 하나도 없기 때문에 모든 타입이 빈인터페이스로 쓰일 수 있음
  - 어떤값이든 받을 수 있는 함수, 메소드, 변숫값을 만들 떄 사용



- 빈 인터페이스를 인수로 받기

```go
package main
import "fmt"


type Student struct{
  Age int
}

func PrintVal(v interface{}) {

  switch t:= v.(type) {
    case int:
      fmt.Printf("v is int %d\n", int(t))
    case float64:
      fmt.Printf("v is float64 %f\n", float64(t))
    case string:
      fmt.Printf("v is string %s\n", string(t))
    case []int:
      fmt.Printf("v is []int Slice %T:%v", t, t)
    case [5]int:
      fmt.Printf("v is [5]int Array %T:%v", t, t)
    default:
      fmt.Printf("Not supported type %T:%v\n", t, t)
  }
}

func main() {
  PrintVal(10)
  PrintVal(3.14)
  PrintVal("Hello")
  PrintVal(Student{15})

  arr := [5]int{1,2,3,4,5}
  slice := arr[2:]
  PrintVal(arr)
  PrintVal(slice)
}
```


3. 인터페이스 기본 값 nil

```go
package main

type Attacker interface {
  Attack()
}

func main() {
  var att Attacker // 인터페이스 기본값은 nil입니다.
  att.Attack()     // att가 nil이기 때문에 런타임 에러가 발생합니다.
}
```


- 인터페이스 변환 하기

1. 구체화된 다른 타입으로 타입 변환
  - 인터페이스를 본래의 구체화된 타입으로 복원할 때
  - 인터페이스 변수 a 를 ConcreteType 타입으로 변환하여, ConcreteType 변수 t 생성하여 대입

```go
var a Interface
t := a.(ConcreteType)
```

```go
package main
import "fmt"

type Stringer interface {
  String() string
}

// Student 구조체가  Stringer 인터페이스 구현
//    String()메소드 정의되어 있기 때문
type Student struct {
  Age int
}

func (s *Student) String() string {
  return fmt.Sprintf("학생 나이는: %d\n", s.Age)
}

// 인터페이스 -> 구현체 타입으로 변환
// Stringer -> *Student
func PrintAge(stringer Stringer) {
  // 특정 구현체 타입으로 변환
  // PrintAge의 매개변수로 어떤 타입이 들어온지 알수 없기 때문에 
  s := stringer.(*Student)
  fmt.Printf("Age: %d\n", s.Age)
  // fmt.Println(stringer.String())
}

func main() {
  s := &Student{100}
  PrintAge(s)
}
```

- 컴파일 에러
  - 인터페이스 변수를 구체화된 타입으로 변환 하려면
  - 해당 타입이 인터페이스 메서드 집합을 포함하고 있어야함, 그렇지 않은 경우 컴파일 에러

```go
type Stringer interface {
  String() string
}

type Student struct {
}

func main() {
  var Stringer stringer
  stringer.(*Student) // 컴파일 에러
}

```


- 런타임 에러
  - go build는 되지만, 실행 중 에러 발생

```go
package main
import "fmt"

type Stringer interface {
  String() string
}

type Student struct {
}

func (s *Student) String() string {
  return "Student"
}

type Actor struct {
}

func (a *Actor) String() string {
  return "Actor"
}

func ConvertType(stringer Stringer) {
  student := stringer.(*Student)
  fmt.Println(student)
}

func main() {
  actor := &Actor{}

  // 런타임 에러:
  // Actor -> Student 타입 에러!!!
  //  panic: interface conversion: main.Stringer is *main.Actor, not *main.Student
  ConvertType(actor)
}
```

2. 다른 인터페이스로 변환
  - 구체화된 타입 뿐아니라, 다른 인터페이스로도 변환 가능
  - `AInterface -> ConcreteType <- BInterface`

```go
var AInterface = ConcreteType{}
b := a.(BInterface)
```


```go
package main
import "fmt"

type Reader interface {
  Read()
}

type Closer interface {
  Close()
}

type File struct {
}

func (*f File) Read() {
}

func ReadFile(reader Reader) {
  c := reader.(Closer)
  // ERROR! 발생!
  // reader 인터페이스변수는 File타입을 가리키고 있고,
  // File 타입은 Close() 메서드를 포함하고 있지 않기 때문에 에러발생
  c.Close()
}

func main() {
  file := &File{}

  // ERROR!
  ReadFile(file)
}
```

- 타입 변환 성공 여부 반환

```go
package main
import (
  "fmt"
  "os"
)

type Reader interface {
  Read()
}

type Closer interface {
  Close()
}

type File struct {
}

func (f *File) Read() {
}

func ReadFile(reader Reader {
  if c, ok := reader.(Closer); ok {
    c.Close()
  }
}

func main() {
  f := &File{}
  ReadFile(f)
}
```


### 21.함수고급편

- 매개변수 `...` 키워드 사용


```go
package main
import "fmt"

func sum(nums ...int) int {
  sum := 0

  fmt.Printf("nums 타입: %T\n", nums)
  for _,v := range nums {
    sum += v
  }
  return sum
}

func PrintT(args ...interface{}) {
  for _,arg := range args {
    switch f := arg.(type) {
      case int:
        val := arg.(int)
        fmt.Println(val, int(f))
        fmt.Println(val == int(f))
        // Print로직
      case float64:
        val := arg.(float64)
        fmt.Println(val == float64(f))
      case string:
        val := arg.(string)
        fmt.Println(val == string(f))
    }
  }
}

func main() {
  fmt.Println(sum(1,2,3,4,5))
  fmt.Println(sum(10,20))
  fmt.Println(sum())

  PrintT(1,3.14, "abc")

}

```


- `defer` 지연 실행
  - 함수가 종료되기 직전에 실행해야하는 코드에 사용
    - 파일이나 소캣 핸들 처럼 OS 내부 자원을 사용하는 경우
    - 내부 자원 이기 떄문에, 반드시 쓰고나서 OS에 되돌려 줘야함.
    - 내부 자원/메모리 고갈을 막기 위함.

```go
package main

import (
	"fmt"
	"os"
)

// 1->2->3->4
// 파일에 Hello World를 씁니다.
// 파일을 닫았습니다.
// 반드시 호출됩니다.
func main() {
	f, err := os.Create("test.txt") // 파일 생성
	if err != nil {
		fmt.Println("Failed to create a file")
		return
	}
	defer fmt.Println("반드시 호출됩니다.") // 4
	defer f.Close() // 3
	defer fmt.Println("파일을 닫았습니다.") // 2

	fmt.Println("파일에 Hello World를 씁니다.") //1
	fmt.Fprintln(f, "Hello, World!") // 파일에 텍스트를 씁니다.
}
```

- 함수타입 변수
  - 함수 시작지점을 가리키는 프로그램 카운터 있음 e.g. 1번라인, 2번라인...
  - 함수 시작지점은 숫자로 표현되며, 가리키는 값을 함수포인터라고 함
  - 함수 타입은 함수정의로 표현 e.g. `func (int, int) int`
  - 함수 alias 지정가능
    - `type opFunc func (int, int) int`
    - `type CollectorOption func(*Collector)`
  - 함수리터럴 (lambda; 익명함수)
    - 함수리터럴 외부변수를 자동으로 리터럴 함수 내부상태로 가져와 저장 ('capture') : 값복사가 아닌 참조형태로 가져옴

```go
package main

import "fmt"

func add(a, b int) int {
  return a + b
}

func mul(a, b int) int {
  return a * b
}

type opFunc func(int, int) int

func getOperator(op string) opFunc {
  if op == "+" {
    return add
  } else if op == "*" {
    return mul
  } else {
    return nil
  }
}

func main() {
  // var opFnc func(int,int) int = getOperator("*")
  opFnc := getOperator("*")

  res := opFnc(2, 9)
  fmt.Println("2*9 = ", res)
}

```

- 함수 리터럴
  - 다른 언어 에서는 lambda; 익명 함수

```go
package main
import "fmt"

func getOperator(operator string) func(int, int) int {
  if operator == "*" {
    return func(a, b int) int {
      return a * b
    }
  } else if operator == "+" {
    return func(a, b int) int {
      return a + b
    }
  } else {
    return nil
  }
}

func main() {
  fn := getOperator("*")
  a, b := 3,4
  fmt.Printf("%d x %d = %d\n", a,b, fn(a,b))
}
```


- 함수리터럴 내부 상태
  - 함수 내부에서 사용 되는 외부 변수는 자동으로 함수 내부 상태로 저장 됨

```go
package main
import "fmt"
func main() {
  i := 0

  // 함수
  f := func() {
    i += 10
  }

  i++
  f()
  fmt.Println(i)
}
```


- 함수 리터럴 내부상태 주의점
  - 캡쳐: 함수 리터럴 외부 변수를 내부로 가져옴
  - 다만 캡쳐는 복사가 아닌 참조 형태로 가져옴



```go
package main
import "fmt"

func CaptureLoop() {
  // make slice of functions with length 3
  f := make([]func(), 3)
  fmt.Println("CaptureLoop")

  // i 가 복사되는것이 아닌 참조되기 떄문에
  for i :=0; i< len(f); i++ {
    f[i] = func() {
      // 캡쳐할 떄 캡쳐하는 순간의 i값(1,2,3)이
      // 복제 되는 것이 아니라, 변수가 참조로 캡쳐되므로
      // i가 최종적으로 3이 되었을떄
      // i를 참조하는 f[0], f[1], f[2]는 모두 i=3를 참조하게 됨
      fmt.Println(i)
    }
  }

  for i :=0; i< len(f); i++ {
    f[i]()
  }
}


func CaptureLoop2() {
  // make slice of functions with length 3
  f := make([]func(), 3)
  fmt.Println("CaptureLoop2")

  // i 가 복사되는것이 아닌 참조되기 떄문에
  for i :=0; i< len(f); i++ {
    v := i
    f[i] = func() {
      // 캡쳐할 떄 캡쳐하는 순간의 i값(1,2,3)이
      // 복제 되는 것이 아니라, 변수가 참조로 캡쳐되므로
      // i가 최종적으로 3이 되었을떄
      // i를 참조하는 f[0], f[1], f[2]는 모두 i=3를 참조하게 됨
      fmt.Println(v)
    }
  }

  for i :=0; i< len(f); i++ {
    f[i]()
  }
}

func main() {
  // 3 3 3
  CaptureLoop()
  // 1 2 3
  CaptureLoop2()
}
```


- 파일 핸들을 내부 상태로 사용하는 예

```go
package main
import (
  "os"
  "fmt"
)

type Writer func(string)

func writeHello(writer Writer) {
  writer("Hello World")
}

func main() {
  f, err := os.Create("test.txt")
  if err != nil {
    fmt.Println("Failed to create a file")
    return
  }

  defer f.Close()

  writeHello(func (msg string) {
    // 함수리터럴 외부 변수 f사용
    fmt.Fprintf(f, msg)
  })
}
```

### 22.자료구조

- 리스트
  - 리스트 구현하는 구조체 코드

```go
type Element struct {
  Value interface{}
  Next *Element
  Prev *Element
}
```

- golang standard library `container`
- https://pkg.go.dev/container
  - `container/heap`
  - `container/list`
  - `container/ring`

- Slices (golang's idiomatic datatype) vs. `container/list` standard library
  - Slices are generally more efficient due to their contiguous memory layout and dynamic resizing strategy.
  - (Doubly) Linked lists (from container/list) have additional overhead due to memory allocation and pointer traversal.
  - Use slices for most scenarios unless you specifically need a doubly-linked list.

1. 리스트 `container/list`
  - 스탠다드 라이브러리

```go
// Element
func (e *Element) Next() *Element
func (e *Element) Prev() *Element

// List
// Package list implements a doubly linked list.
func New() *List
func (l *List) Back() *Element
func (l *List) Front() *Element
func (l *List) Init() *List
func (l *List) InsertAfter(v any, mark *Element) *Element
func (l *List) InsertBefore(v any, mark *Element) *Element
func (l *List) Len() int
func (l *List) MoveAfter(e, mark *Element)
func (l *List) MoveBefore(e, mark *Element)
func (l *List) MoveToBack(e *Element)
func (l *List) MoveToFront(e *Element)
func (l *List) PushBack(v any) *Element
func (l *List) PushBackList(other *List)
func (l *List) PushFront(v any) *Element
func (l *List) PushFrontList(other *List)
func (l *List) Remove(e *Element) any
```

- 리스트 기본 사용법

```go
package main
import (
  "container/list"
  "fmt"
)

func main() {
  // PushBack, PushFront returns Pointer to newly insertedElement
  // 1 4
  //    1 <- e1
  //    4 <- e4
  v := list.New()
  e4 := v.PushBack(4)
  e1 := v.PushFront(1)

  v.InsertBefore(3, e4)
  v.InsertAfter(2, e1)

  for e := v.Front(); e != nil; e= e.Next() {
    fmt.Print(e.Value, " ")
  }
  fmt.Println()

  // 역순
  for e := v.Back(); e != nil; e = e.Prev() {
    fmt.Print(e.Value, " ")
  }
}
```

- 배열,슬라이스 vs. 리스트
  - 요소삽입 : O(N) vs. O(1)
  - 요소삭제 : O(N) vs. O(N)
  - 요소접근 : O(1) vs. O(N)
    - 배열시작주소 + (인덱스*타입크기)

- 큐
  - Not a standard library: use `container/list` to custom implement
  - First In First Out

```go
package main

import (
  "fmt"
  "container/list"
)

// list.List : Doubly Linked List!
//    .PushBack(n)
//    .Front()
//        front = .Front()
//    .Remove(front)
type Queue struct {
  v *list.List
}

func (q *Queue) Push(val interface{}) {
  q.v.PushBack(val)
}

func (q *Queue) Pop() interface{} {
  front := q.v.Front()
  if front != nil {
    return q.v.Remove(front)
  }
  return nil
}

func NewQueue() *Queue {
  return &Queue{ list.New()}
}

func main() {
  queue := NewQueue()

  for i :=1; i<=4; i++ {
    queue.Push(i)
  }

  v := queue.Pop()
  for v != nil {
    fmt.Print(v, " ")
    v = queue.Pop()
  }
  fmt.Println()
}
```

- 스택
  - Not a standard library: use `container/list` to custom implement
  - First In Last Out

```go
package main

import (
  "fmt"
  "container/list"
)

type Stack struct {
  v *list.List
}

func (s *Stack) Push(val interface{}) {
  s.v.PushBack(val)
}

func (s *Stack) Pop() interface{} {
  back := s.v.Back()
  if back !=nil {
    return s.v.Remove(back)
  }
  return nil
}

func NewStack() *Stack {
  return &Stack{ list.New() }
}

func main() {
  stack := NewStack()
  for i:=1; i<=4; i++ {
    stack.Push(i)
  }

  val := stack.Pop()
  for val != nil {
    fmt.Print(val , " ")
    val = stack.Pop()
  }
}
```

2. 링 `container/ring`
  - 스탠다드 라이브러리

```go
func New(n int) *Ring
func (r *Ring) Do(f func(any))
func (r *Ring) Len() int
func (r *Ring) Link(s *Ring) *Ring
func (r *Ring) Move(n int) *Ring
func (r *Ring) Next() *Ring
func (r *Ring) Prev() *Ring
func (r *Ring) Unlink(n int) *Ring
```

```go
package main

import (
  "fmt"
  "container/ring"
)

func main() {
  r := ring.New(5)
  n := r.Len()

  for i:=0; i< n; i++ {
    r.Value = 'a' + i
    r = r.Next()
  }

  for i :=0; i<n; i++ {
    fmt.Printf("%c", r.Value)
    r = r.Next()
  }
  fmt.Println()

  for i :=0; i<n; i++ {
    fmt.Printf("%c", r.Value)
    r = r.Prev()
  }
}
```

- 맵
  - 같은입력이 들어오면 같은값이 나옴
  - 입력범위는 무한, 결과는 특정범위

```go
package main
import "fmt"

func main() {
  m := make(map[string]string)
  m["이하나"] = "A100"
  m["송하나"] = "A101"
  m["박하나"] = "A102"
  m["최하나"] = "A103"

  s := "송하나"
  fmt.Print(s, ": ")
  fmt.Println(m[s])
}
```

- 요소 삭제와 없는 요소 확인

```go
package main
import "fmt"
func main() {
  m := make(map[int]int)
  m[1] = 0
  m[2] = 1
  m[3] = 2

  // delete(맵, key값)
  delete(m, 3)
  delete(m, 4) // 없는요소 삭제시도

  v, ok := m[3]
  fmt.Println(v, ok) // 삭제된 요소값 출력

  v, ok = m[1]
  fmt.Println(v, ok) // 존재하는 요소값 출력


  // 맵 순환하기
  for k, v := range m {
    fmt.Printf("Key: %d, Value: %d\n", k, v)
  }
}
```

- 배열,슬라이스 vs. 리스트 vs. 맵
  - 삽입 : O(N) vs. O(1) vs. O(1)
  - 삭제 : O(N) vs. O(N) vs. O(1)
  - 접근 : O(1) vs. O(N) vs. O(1) 키로 접근
    - 배열시작주소 + (인덱스*타입크기)

- 맵이 추가,삭제,읽기에서 속도가 빠른이유: 해쉬함수

`|배열, 슬라이스| 리스트| 맵
--|--|--|--
추가| O(N) | O(1) | O(1)
삭제| O(N) | O(1) | O(1)
읽기| O(1)-인덱스로 접근 | O(N)-인덱스로 접근 | O(1)-키로 접근


- 맵의 원리 - 해시함수는 다음 3가지 특징을 만족 해야한다
  1. 같은 입력 -> 같은 결과
  2. 다른 입력 -> (되도록) 다른 결과 (`in general` different result)
  3. 입력값의 범위는 무한대, 결과는 특정 범위를 갖는다.
    - e.g. `f(x) = sign(x)`: 삼각함수는 계산이 복잡해서, 주로 Mod를 씀
    - e.g. `f(x) = Mod(x, 10)` does `x % 10` operation
      - 나머지 연산은 계산이 빠르고, 결과값의 범위와 간격 조절 쉬움
    - 배열로 구현시 같은 해시값(인덱스)에 1개의 값만 맵핑
    - m[hash(23)] m[hash(33)] 해시충돌
      - 이 문제는 배열안에 리스트 저장하여 해결가능
    - 해시함수는 요소개수와 상관없이 고정된 시간을 갖는 함수이므로 맵이 읽기,쓰기에서 O(1)의 시간


- 해시로 맵 만들기
  - 해시충돌은 인덱스마다 리스트에 충돌되는 값들 전부 저장하여 해결한다
  - 해시 함수는 암호화, 비트코인 등에서 광범위하게 쓰임

```go
package main
import "fmt"

const M = 10

// returns in range of 0,1,...9
func hash(d int) int {
  return d % M
}

func main() {
  m := [M]int{}
  m[hash(23)] = 10
  m[hash(33)] = 10 // 덮어 씌워짐 (해시충돌)
  m[hash(259)] = 50

  // Prints:
  // m[hash(23)] = 10
  // m[hash(33)] = 10
  // m[hash(259)] = 50
  fmt.Printf("m[hash(23)] = %d\n", m[hash(23)])
  fmt.Printf("m[hash(33)] = %d\n", m[hash(33)])
  fmt.Printf("m[hash(259)] = %d\n", m[hash(259)])
}
```


### 23.에러 핸들링

- 에러 반환

```go
package main

import (
  "bufio"
  "fmt"
  "os"
)

const filename string =  "data.txt"

// 파일에서 한줄 읽기
func ReadFile(filename string) (string, error) {
  file, err := os.Open(filename)
  if err != nil {
    return "", err
  }
  defer file.Close()

  rd := bufio.NewReader(file)
  line, _ := rd.ReadString('\n')
  return line, nil
}

func WriteFile(filename, line string) error {
  file, err := os.Create(filename)
  if err != nil {
    return err
  }
  defer file.Close()
  _, err = fmt.Fprintln(file, line)
  return err
}

func main() {
  line, err := ReadFile(filename)
  if err != nil {
    err = WriteFile(filename, "This is WriteFile")
    if err !=nil {
      fmt.Println("파일 생성에 실패했습니다.", err)
      return
    }
    line, err = ReadFile(filename)
    if err !=nil {
      fmt.Println("파일 읽기에 실패 했습니다.", err)
      return
    }
  }

  fmt.Println("파일내용: ", line)
}
```


- 사용자 에러 반환
  - `fmt.Errorf()` 사용 또는
  - `func New(text string) error` 에러 생성하여 반환 가능

```go
import errors
errors.New("에러 메시지")
```

```go
package main

import (
  "fmt"
  "math"
)

func Sqrt(f float64) (float64, error) {
  if f <0 {
    return 0, fmt.Errorf("제곱근은 양수여야 합니다. f:%g", f)
  }
  return math.Sqrt(f), nil
}

func main() {
  sqrt, err := Sqrt(-2)
  if err != nil {
    fmt.Printf("에러: %v\n", err)
    return
  }
  fmt.Printf("Sqrt(-2)=%v\n", sqrt)
}
```

- 에러 타입

```go
type error interface {
  Error() string
}
```

```go
package main

import "fmt"

// Error() 메소드 있는 error 인터페이스를 구현
type PasswordError struct {
  Len int
  RequireLen int
}

func (err PasswordError) Error() string {
  return "암호 길이가 짧습니다."
}

func RegisterAccount(name, password string) error {
  if len(password) < 8 {
    return PasswordError{len(password), 8}
  }
  return nil
}

func main() {
  err := RegisterAccount("myID", "myPw")
  if err != nil {
    if errInfo, ok := err.(PasswordError); ok {
      fmt.Printf("%v Len: %d RequiredLen: %d\n", errInfo, errInfo.Len, errInfo.RequireLen)
    }
  } else {
    fmt.Println("회원 가입됐습니다.")
  }
}
```

- 에러 랩핑
  - 에러를 감싸서 새로운 에러 만들기
  - 예를들어, 파일을 읽을떄 에러 뿐 아니라, 몇번째 줄에서 에러발생했는지 등 정보 담을 에러 필요

```go
// As finds the first error in err's chain that matches target,
// and if one is found, sets target to that error value
// and returns true. Otherwise, it returns false.
//    type any = interface{}
func As(err error, target any) bool
func As(err error, target interface{}) bool

// Reader is the interface that wraps the basic Read method.
// Read reads up to len(p) bytes into p.
// It returns the number of bytes read (0 <= n <= len(p)) and any error encountered. 
type Reader interface {
  Read(p []byte) (n int, err error)
}

// NewReader returns a new Reader reading from s.
// It is similar to bytes.NewBufferString but more efficient and read-only.
func NewReader(s string) *Reader

// NewScanner returns a new Scanner to read from r.
// The split function defaults to ScanLines.
func NewScanner(r io.Reader) *Scanner


// Split sets the split function for the Scanner.
// The default split function is ScanLines.
func (s *Scanner) Split(split SplitFunc)

// ScanWords is a split function for a Scanner that returns
// each space-separated word of text, with surrounding spaces deleted.
// It will never return an empty string.
// The definition of space is set by unicode.IsSpace.
func ScanWords(data []byte, atEOF bool) (advance int, token []byte, err error)
```



```go
//ch23/ex23.4/ex23.4.go
package main

import (
  "bufio"
  "errors"
  "fmt"
  "strconv"
  "strings"
)

func MultipleFromString(str string) (int, error) {
  scanner := bufio.NewScanner(strings.NewReader(str)) // ❶ 스캐너 생성
  scanner.Split(bufio.ScanWords)                      // ❷ 한 단어씩 끊어읽기

  pos := 0
  a, n, err := readNextInt(scanner)
  if err != nil {
    return 0, fmt.Errorf("Failed to readNextInt(), pos:%d err:%w", pos, err) // ➏ 에러 감싸기
  }

  pos += n + 1
  b, n, err := readNextInt(scanner)
  if err != nil {
    return 0, fmt.Errorf("Failed to readNextInt(), pos:%d err:%w", pos, err)
  }
  return a * b, nil
}

// 다음 단어를 읽어서 숫자로 변환하여 반환합니다.
// 변환된 숫자, 읽은 글자수, 에러를 반환합니다.
func readNextInt(scanner *bufio.Scanner) (int, int, error) {
  if !scanner.Scan() { // ❸ 단어 읽기
    return 0, 0, fmt.Errorf("Failed to scan")
  }
  word := scanner.Text()
  number, err := strconv.Atoi(word) // ❹ 문자열을 숫자로 변환
  if err != nil {
    return 0, 0, fmt.Errorf("Failed to convert word to int, word:%s err:%w", word, err) // ➎ 에러 감싸기
  }
  return number, len(word), nil
}

func readEq(eq string) {
  rst, err := MultipleFromString(eq)
  if err == nil {
    fmt.Println(rst)
  } else {
    fmt.Println(err)
    var numError *strconv.NumError
    if errors.As(err, &numError) { // ➐ 감싸진 에러가 NumError인지 확인
      fmt.Println("NumberError:", numError)
    }
  }
}
func main() {
  readEq("123 3")
  readEq("123 abc")
}
```


- 패닉
  - 문제 발생 시점에 즉시 종료
  - 파라미터 메시지 표시 후 호출 순서 나타내는 콜스택 표시 (에러 발생경로 확인 가능)

- 패닉 생성
  - `func panic(interface{})`

```go
// panic(42)
// panic("Error message")
// panic(fmt.Errorf("Error object"))
// panic(SomeType{SomeData})
package main
import "fmt"

func divide(a,b int) {
  if b==0 {
    panic("b가 0일 수 없습니다")
  }
  fmt.Printf("%d /%d= %d\n",a,b, a/b )
}

func main() {
  divide(3,6)
  divide(6,3)
  divide(3,0)
}
```

- 패닉 전파 그리고 복구
  - 패닉 발생 후 종료 대신 복구
  - 함수호출 순서 : main-> f->g-> h()
  - 패닉전파 순서(h() 패닉발생):  g->f->main()
  - main()에서 복구 되지 않으면 프로그램 종료됨
  - recover()로 복구하여 계속 진행 가능
  - recover() 호출된 시점에 panic 전파 중이면 패닉객체 반환, 아니면 nil 반환

```go
//ch23/ex23.6/ex23.6.go
package main

import "fmt"

func f() {
  fmt.Println("f() 함수 시작")
  defer func() { // ❹ 패닉 복구
    if r := recover(); r != nil {
      fmt.Println("panic 복구 -", r)
    }
  }()

  g() // ❶ g() -> h() 순서로 호출
  fmt.Println("f() 함수 끝")
}

func g() {
  fmt.Printf("9 / 3 = %d\n", h(9, 3))
  fmt.Printf("9 / 0 = %d\n", h(9, 0)) // ❷ h() 함수 호출 - 패닉
}

func h(a, b int) int {
  if b == 0 {
    panic("제수는 0일 수 없습니다.") // ❸ 패닉 발생!!
  }
  return a / b
}

func main() {
  f()
  fmt.Println("프로그램이 계속 실행됨") // ➎ 프로그램 실행 지속됨
}
```

- recover() 결과
  - `func recover() interface{}`

```go
if r, ok := recover().(net.Error); ok {
  fmt.Println("r is net.Error type")
}
```

### 24.고루틴과 동시성 프로그래밍
### 25.채널과 컨텍스트

- [Concurrency](golang_concurrency)


### 26.단어검색 프로그램 만들기

- 와일드카드
  - * : 0개이상 문자
  - ? : 1개 문자
- `os.Args []string` 변수와 실행 인수
  - Args는 os 패키지의 전역변수로 각 실행인수가 []string 슬라이스에 담김
  - 첫번째 항목으로 실행 명령이 들어감
  - 두번쨰 부터 입력한 인수들이 차례로 들어감
    - `find word filepath`
      - os.Args[0] : find
      - os.Args[1] : word
      - os.Args[2] : filepath

- 파일 핸들링

```go
// 파일열기
func Open(name string) (*File, error)

// 파일 목록가져오기 (slice)
func Glob(pattern string) (matches []string, err error)
filepaths, err := filepath.Glob("*.txt")

// 파일 내용 한줄 씩 읽기
func NewScanner(r io.Reader) *Scanner

type Scanner
  func (s *Scanner) Scan() bool
  func (s *Scanner) Text() string
```


- 단어 포함여부 검사
  - `func Contains(s, substr string) bool`


- 실행 인수 읽고 파일목록 가져오기
  - 단어프로그램 실행파일 만들기 :
  - cd 26-search-word-project/ex26.1
  - touch ex26.1.go
  - go mod init 26-search-word-project/ex26.1
  - go mod tidy
  - go build
  - ex26.1 word ex*
  - 찾으려는 단어 : word
  - 찾으려는 파일 리스트 :
  -   ex26.1.exe
  -   ex26.1.go

```go
package main

import (
  "fmt"
  "os"
  "path/filepath"
)

func main() {
  if len(os.Args) < 3 {
    fmt.Println("2개 이상의 실행 인수가 필요합니다. ex) ex26.1 word filepath")
    return
  }

  // 실행인수 가져오기
  //  찾으려는 단어
  word := os.Args[1]
  //  검색할 파일리스트 (슬라이스)
  files := os.Args[2:]
  fmt.Println("- 찾으려는 단어: ", word)
  PrintAllFiles(files)
}

// 파일리스트 및 에러 반환
func GetFileList(path string) ([]string, error) {
  return filepath.Glob(path)
}

// 찾은 파일리스트 출력
func PrintAllFiles(files []string) {
  fmt.Println("- 찾으려는 파일 리스트")
  for _, path := range files {
    filelist, err := GetFileList(path)
    if err != nil {
      fmt.Println("파일경로가 잘못되었습니다. err:", err, "path:", path)
      return
    }

    for _, name := range filelist {
      fmt.Println(name)
    }
  }
}
```

- 파일을 열어서 라인 읽기
  - 파일을 열고 bufio 패키지의 NewScanner()로 스캐너를 만들어, 파일내용을 한단어씩 읽기

```go
package main

import (
  "bufio"
  "fmt"
  "os"
)

func main() {
  PrintFile("hamlet.txt")
}

// 파일을 읽어서 출력
func PrintFile(filename string) {
  file, err := os.Open(filename) // 파일 열기
  if err != nil {
    fmt.Println("파일을 찾을 수 없습니다.", filename)
    return
  }

  defer file.Close() // 함수 종료전 파일 닫기

  scanner := bufio.NewScanner(file) // 스캐너를 생성해서 한줄 씩 읽기
  for scanner.Scan() {
    fmt.Println(scanner.Text())
  }
}
```

- 파일 검색 프로그램 완성 하기

```go
//ch26/ex26.3/ex26.3.go

/**
cd 26-search-word-project/ex26.3
go mod init 26-search-word-project/ex26.3
go mod tidy
go build
./ex26.3 word *.txt
*/

package main

import (
  "bufio"
  "fmt"
  "os"
  "path/filepath"
  "strings"
)

// 찾은 라인 정보
type LineInfo struct { // ❶ 찾은 결과 정보
  lineNo int
  line   string
}

// 파일 내 라인 정보
type FindInfo struct {
  filename string
  lines    []LineInfo
}

func main() {
  if len(os.Args) < 3 {
    fmt.Println("2개 이상의 실행 인수가 필요합니다. ex) ex26.3 word filepath")
    return
  }

  word := os.Args[1] // ❷ 찾으려는 단어
  files := os.Args[2:]
  findInfos := []FindInfo{}
  for _, path := range files {
    // ❸ 파일 찾기
    findInfos = append(findInfos, FindWordInAllFiles(word, path)...)
  }

  for _, findInfo := range findInfos {
    fmt.Println(findInfo.filename)
    fmt.Println("--------------------------------")
    for _, lineInfo := range findInfo.lines {
      fmt.Println("\t", lineInfo.lineNo, "\t", lineInfo.line)
    }
    fmt.Println("--------------------------------")
    fmt.Println()
  }
}

func GetFileList(path string) ([]string, error) {
  return filepath.Glob(path)
}

func FindWordInAllFiles(word, path string) []FindInfo {
  findInfos := []FindInfo{}

  filelist, err := GetFileList(path) // ❶ 파일 리스트 가져오기
  if err != nil {
    fmt.Println("파일 경로가 잘못되었습니다. err:", err, "path:", path)
    return findInfos
  }

  for _, filename := range filelist { // ❷ 각 파일별로 검색
    findInfos = append(findInfos, FindWordInFile(word, filename))
  }
  return findInfos
}

func FindWordInFile(word, filename string) FindInfo {
  findInfo := FindInfo{filename, []LineInfo{}}
  file, err := os.Open(filename)
  if err != nil {
    fmt.Println("파일을 찾을 수 없습니다. ", filename)
    return findInfo
  }
  defer file.Close()

  lineNo := 1
  scanner := bufio.NewScanner(file) // ❸ 스캐너를 만듭니다.
  for scanner.Scan() {
    line := scanner.Text()
    if strings.Contains(line, word) { // ❹ 한 줄씩 읽으면 단어 포함 여부 검색
      findInfo.lines = append(findInfo.lines, LineInfo{lineNo, line})
    }
    lineNo++
  }
  return findInfo
}
```

- 개선하기 (고루틴, 채널)
  - 파일개수가 늘어나도 빨리조회 되도록
  - 파일별로 작업을 할당하고 작업이 완료되면, 채널을 이용하여 결과 수집

```go
package main

import (
  "fmt"
  "os"
  "path/filepath"
  "bufio"
  "strings"
)

type LineInfo struct {
  lineNo int
  line string
}

type FindInfo struct {
  filename string
  lines []LineInfo
}

/**
cd 26-search-word-project/ex26.4
go mod init 26-search-word-project/ex26.4
go mod tidy
go build
./ex26.4 word *.txt
*/



func GetFileList(path string) ([]string, error) {
  return filepath.Glob(path)
}

func FindWordInAllFiles(word, path string) []FindInfo {
  findInfos := []FindInfo{}

  filelist, err := GetFileList(path)
  if err != nil {
    fmt.Println("파일경로가 잘못되었습니다. err:", err, "path:", path)
    return findInfos
  }

  ch := make(chan FindInfo)
  cnt := len(filelist)
  recvCnt := 0

  for _,filename := range filelist {
    go FindWordInFile(word, filename, ch)
  }

  for findInfo := range ch {
    findInfos = append(findInfos, findInfo)
    recvCnt++
    if recvCnt == cnt {
      // all received
      break
    }
  }
  return findInfos
}

func FindWordInFile(word, filename string, ch chan FindInfo) {
  findInfo := FindInfo{filename, []LineInfo{}}

  file, err := os.Open(filename)
  if err != nil {
    fmt.Println("파일을 찾을 수 없습니다. ", filename)
    ch <- findInfo
    return
  }
  defer file.Close()

  scanner := bufio.NewScanner(file)

  lineNo := 1
  for scanner.Scan() {

    line := scanner.Text()
    if strings.Contains(line, word) {
      findInfo.lines = append(findInfo.lines, LineInfo{lineNo, line})
    }
    lineNo++
  }

  ch <- findInfo
}


func main() {
  if len(os.Args) < 3 {
    fmt.Println("2개 이상의 실행 인수가 필요합니다. ex) ex26.1 word filepath")
    return
  }

  findInfos := []FindInfo{}
  word := os.Args[1]
  files := os.Args[2:]

  for _, path := range files {
    findInfos = append(findInfos, FindWordInAllFiles(word, path)...)
  }

  for _, findInfo := range findInfos {
    fmt.Println(findInfo.filename)
    fmt.Println("=====")
    for _, lineInfo := range findInfo.lines {
      fmt.Println(lineInfo.lineNo, "\t", lineInfo.line)
    }
    fmt.Println("=====")
  }
}
```


### 27.객체지향원칙 SOLID

- 단일 책입원칙
- 개방-폐쇄 원칙
- 라스코프 치환 원칙
- 인터페이스 분리 원칙
- 의존 관계 역전 원칙


```go
```


### 28.테스트와 벤치마크

- _test.go 작성
- testing 패키지 임포트
- `func TestXxxx(t *testing.T)` 형태이어야 함
  - ex28.1.go
  - ex28_1_test.go

```sh
# gcc 관련 에러
sudo apt install build-essential
go mod init ex28.1
go mod tidy

# 테스트 전부 실행
go test

# 일부 테스트만 실행
go test -run 테스트명
go test -run TestSquare1

```

```go
// ex28.1.go
package main

import "fmt"

func square(x int) int {
  return x*x
}

func main() {
  fmt.Printf("9 * 9 = %d\n", square(9))
}
```

- 테스트 돕는 외부 패키지

```go
import "github.com/stretchr/testify/assert"

// func Equal(t TestingT, expected, actual interface{}, msgAndArgs ...interface{}) bool
// func NotEqual(t TestingT, expected, actual interface{}, msgAndArgs ...interface{}) bool
// func Greater(t TestingT, e1 interface{}, e2 interface{}, msgAndArgs ...interface{}) bool
// func Nil(t TestingT, object interface{}, msgAndArgs ...interface{}) bool
// func NotNilf(t TestingT, object interface{}, msg string, args ...interface{}) bool
//    NotNilf asserts that the specified object is not nil.
//    assert.NotNilf(t, err, "error message %s", "formatted")
```

```go
// ex28_1_test.go
package main

import (
  "testing"
  "github.com/stretchr/testify/assert"
)

func TestSquare1(t *testing.T) {
  rst := square(9)
  if rst != 81 {
    t.Errorf("square(9) should return 81, but returned %d\n", rst)
  }
}

func TestSquare2(t *testing.T) {
  rst := square(3)
  if rst != 9 {
    t.Errorf("square(3) should return 9, but returned %d\n", rst)
  }
}

func TestSquare3(t *testing.T) {
  // func New(t TestingT) *Assertions
  assert := assert.New(t)

  // 테스트 함수 호출
  // func (a *Assertions)Equal(expected, actual interface{}, msgAndArgs ...interface{}) bool
  assert.Equal(81, square(9),"9^2 = 81 결과가 나와야 함")
  assert.Equal(9, square(3),"3^2 = 9 결과가 나와야 함")

  // 또는 assert.New(t) 사용하지 않고
  // assert.Equal(t, 49, square(7),"7^2 = 49 결과가 나와야 함")
}
```

- mock(테스트용 목업)과 suite(테스트 시작과 종료) 패키지 제공
  - mock 패키지: 모듈행동을 가장하는 mockup 객체 제공
    - 온라인 기능 테스트 시 하위영역인 네트워크 기능까지 테스트 힘들때, 네트워크 객체 가장한 목업 객체 만들때 유용
  - suite 패키지: 테스트 준비 작업이나 종료 후 뒤처리 작업
    - 시작전 임시파일 생성
    - 종료 후 생성한 임시파일 삭제

- 테스트 주도 개발 - TDD
  - 블랙박스 테스트 : 제품내부 오픈하지 않은 상태로 사용자 입장에서 테스트 (QA 담당)
  - 화이트박스 테스트 : 내부코드 검증 - unit test
    - `코드작성 -> [테스트-코드수정] -> 완성`

- 벤치마크
  - 코드 성능 검사 : testing 패키지에서 제공
  - _test.go 작성
  - testing 패키지 임포트
  - `func BenchmarkXxxx(b *testing.B)` 형태 여야 함
  - `go test -bench .`


```sh
# 47035 vs 9.346 nanosecond
go test -bench .
  goos: linux
  goarch: amd64
  pkg: ex28.2
  cpu: Intel(R) Core(TM) i7-6700HQ CPU @ 2.60GHz
  BenchmarkFibonacci1-8              24924             47035 ns/op
  BenchmarkFibonacci2-8           125435312                9.346 ns/op
  PASS
  ok      ex28.2  3.810s
```

```go
// ex28.2.go
package main

import "fmt"

func fibonacci1(n int) int {
  if n < 0 {
    return 0
  }
  if n < 2 {
    return n
  }
  return fibonacci1(n-1) + fibonacci1(n-2) // ❶ 재귀 호출
}

func fibonacci2(n int) int {
  if n < 0 {
    return 0
  }
  if n < 2 {
    return n
  }
  one := 1
  two := 0
  rst := 0
  for i := 2; i <= n; i++ { // ❷ 반복문
    rst = one + two
    two = one
    one = rst
  }
  return rst
}

func main() {
  fmt.Println(fibonacci1(7))
  fmt.Println(fibonacci2(7))
}
```

```go
// ex28_2_test.go
package main

import (
  "testing"
  "github.com/stretchr/testify/assert"
)


func TestFibonacci1(t *testing.T) {
  assert := assert.New(t)
  assert.Equal(0, fibonacci1(-1), "fibonacci1(-1) should be 0")
  assert.Equal(0, fibonacci1(0), "fibonacci1(0) should be 0")
  assert.Equal(1, fibonacci1(1), "fibonacci1(1) should be 1")
  assert.Equal(2, fibonacci1(3), "fibonacci1(2) should be 2")
  assert.Equal(233, fibonacci1(13), "fibonacci1(13) should be 233")
}

func TestFibonacci2(t *testing.T) {
  assert := assert.New(t)
  assert.Equal(0, fibonacci2(-1), "fibonacci1(-1) should be 0")
  assert.Equal(0, fibonacci2(0), "fibonacci1(0) should be 0")
  assert.Equal(1, fibonacci2(1), "fibonacci1(1) should be 1")
  assert.Equal(2, fibonacci2(3), "fibonacci1(2) should be 2")
  assert.Equal(233, fibonacci2(13), "fibonacci1(13) should be 233")
}

func BenchmarkFibonacci1(b *testing.B) {
  // b.N만큼 반복
  for i := 0; i < b.N; i++ {
    fibonacci1(20)
  }
}

func BenchmarkFibonacci2(b *testing.B) {
  // b.N만큼 반복
  for i := 0; i < b.N; i++ {
    fibonacci2(20)
  }
}
```

### 29.Go언어로 만드는 웹서버

- HTTP는 인터넷에서 데이터를 주고받는 통신 프로토콜
  - 비연결성 특징 : 클라이언트와 서버가 계속 연결 되어 있지 않고, 응답 후 연결을 끊어버림
  - 그래서 이전 상태 정보나 현재 통신 상태가 남아 있지 않습니다.
  - 자원 낭비를 줄일 수 있지만, 클라이언트의 상태를 유지 할 수 없는 단점
  - cookie, session 사용하면 상태 정보 유지 할 수 있음
    - cookie: '클라이언트'에서 데이터를 저장/관리하여 상태를 유지하는 기술
    - session: '서버'에서 데이터를 저장/관리하여 상태를 유지하는 기술
- HTTPS는 HTTP의 암호화 통신버전. 통신내용을 암호화 하므로 더 안전
- Go 언어를 이용해 만든 웹서버는 뛰어난 성능을 자랑함


- HTTP 웹서버 만들기
  - net/http 패키지로 웹서버 만들 수 있음

- 핸들러 등록 : HTTP 요청 URL 수신됐을때 그걸 처리하는 함수
  - HandleFunc() 함수 등록: URL 해당 경로 호출 시 함수 호출
  - http.Handler 인터페이스 구현한 객체 등록. 이 객체의 인터페이스인 ServeHTTP() 호출

```go
func IndexPathHandler(w http.ResponseWriter, r *http.Request) { ...  }
// "/" 요청 시 IndexPathHandler 호출
http.HandleFunc("/", IndexPathHandler)
```

- http 패키지의 Request 구조체

```go
type Request struct {
  // GET, POST, PUT, DELETE
  Method string

  UL *url.URL

  Proto string
  ProtoMajor int
  ProtoMinor int
  Header header

  Body io.ReadCloser
}
```

- 웹서버 시작
  - 각 경로에 대한 핸들러 등록을 마치고, 웹서버 시작

```go
// addr: HTTP 요청 수신 주소 (포트포함)
// handler: nil 이면 디폴트 핸들러
//    패키지 함수인 hattp.HandleFunc()로 핸들러 함수 등록 시 인자에 nil 전달
//    또는 새로운 핸들러 인스턴스를 두번쨰 인수로 전달 가능 (ServeMux 인스턴스 이용)
func ListenAndServe(addr string, handler Handler) error
```

```go
package main

import (
  "fmt"
  "net/http"
)

func main() {
  // http패키지 함수인 HandleFunc로 핸들러 함수 등록할 때는
  // ListenAndServe 두번째 인수에 nil 전달 해야함!
  // 두번째 인수 nil 전달 시, DefaultServeMux 사용-> http.HandleFunc() 호출하여 등록된 핸들러 사용
  // "/" 경로로 HTTP 요청을 받으면 함수 리터럴 func(w,r){...} 실행!
  http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
      // 출력 스트림에 값을 쓰는 함수
      // 지정한 출력 스트림 w에 "Hello World" 출력
      // http.ResponseWriter에 값을 쓰면, HTTP 응답으로 전송 됨
      fmt.Fprint(w, "Hello World")
  })

  // 웹서버 실행
  http.ListenAndServe(":3000", nil)
}
```


- HTTP 동작원리
  - https://goldenrabbit.co.kr:3000 호출
  - 웹 브라우저는 DNS(domain name system)에 도메인에 해당하는 IP 주소를 요청
  - 웹브라우저 goldenrabbit.co.kr->DNS
  - DNS ip주소 -> 웹브라우저
  - IP주소:목적지(컴퓨터), 포트: 해당 컴퓨터 내 데이터 수신 가능한 창구 (0~65535)
  - 웹서버란? 특정 포트에서 대기하며 사용자의 HTTP요청에 HTTP응답을 전송하는 서버 (응답은 일반적으로 HTMl 문서)


- HTTP 쿼리인수 사용하기
  - HTTP 요청에 포함된 쿼리 인수를 읽고 사용 가능
  - http://localhost?id=1&name=abcd

```go
package main

import (
  "fmt"
  "net/http"
  "strconv"
)

func barHandler(w http.ResponseWriter, r *http.Request) {
  values := r.URL.Query() // 쿼리인수 가져오기
  name := values.Get("name") // 특정 키 값이 있는지 확인
  if name == "" {
    name = "World"
  }

  id, _ := strconv.Atoi(values.Get("id")) // id값을 가져와서 int형 타입 변환
  fmt.Fprintf(w, "Hello %s! id: %d", name, id)
}


// http://localhost:3000/bar?name=Lalalala&id=123
func main() {
  http.HandleFunc("/bar", barHandler)
  http.ListenAndServe(":3000", nil)
}
```

- ServeMux 인스턴스 이용하기
  - ListenAndServe 두번째 인수 nil -> DefaultServeMux가 http.HandleFunc() 패키지함수 호출. 다양한 기능 추가 어려움
  - ServeMux 인스턴스 생성하여 사용
    - http.HandleFunc()는 DefaultServeMux에 핸들러를 등록하는 반면
    - mux.HandleFunc()는 생성한 ServeMux 인스턴스에 핸들러를 등록 함
    - Mux (multiplexer 약자): 여러 입력 중 하나를 선택해서 반환 하는 디지털 장치

```go
package main
import (
  "fmt"
  "net/http"
)

func main() {
  mux := http.NewServeMux()
  mux.HandleFunc("/", func(w http.ResponseWriter, r *http.Request){
      fmt.Fprint(w, "Hello World")
  })
  mux.HandleFunc("/bar", func(w http.ResponseWriter, r *http.Request){
      fmt.Fprint(w, "Hello Bar")
  })

  http.ListenAndServe(":3000", mux)
}
```

- 파일서버
  - 이미지 데이터를 직접 가져오지 않고 src에 경로만 담고 있음
  - 웹브라우저는 다시 필요한 이미지 데이터를 HTTP 요청을 통해 가져옴
  - 이미지 요청을 받은 웹서버는 이미지 경로에 해당하는 데이터를 반환 하여 이미지 표시
  - 대신에 '/static' 폴더의 파일 제공하는 파일 서버 생성

```html
<!-- ch29/ex29.4/test.html -->
<html>
<body>
<img src="https://golang.org/lib/godoc/images/footer-gopher.jpg"/>
<h1>이것은 Gopher 이미지입니다.</h1>
</body>
</html>
```


```go
package main
import "net/http"

// http://localhost:3000/gopher.jpg
func main() {
  http.Handle("/", http.FileServer(http.Dir("static")))
  http.ListenAndServe(":3000", nil)
}
```

- 특정 경로에 있는 파일 읽어오기
  - http://localhost:3000/static/gopher.jpg 호출

```go
package main
import "net/http"

func main() {
  // http://localhost:3000/gopher.jpg
  // http.Handle("/", http.FileServer(http.Dir("static")))

  // http.StripPrefix로 URL에서 /static/을 제거 해줌
  // http://localhost:3000/static/gopher.jpg 출력
  http.Handle("/static/", http.StripPrefix("/static/", http.FileServer(http.Dir("static"))))
  http.ListenAndServe(":3000", nil)
}
```

```html
<!-- ch29/ex29.4/test.html -->
<html>
<body>
<img src="http://localhost:3000/static/gopher.jpg"/>
<h1>이것은 Gopher 이미지입니다.</h1>
</body>
</html>
```


- 웹서버 테스트 코드 만들기

```go
// ex29.5/ex29.5.go
package main

import (
  "fmt"
  "net/http"
)

func MakeWebHandler() http.Handler {
  mux := http.NewServeMux()
  mux.HandleFunc("/", func(w http.ResponseWriter, r *http.Request){
      fmt.Fprint(w, "Hello World")
  })
  mux.HandleFunc("/bar", func(w http.ResponseWriter, r *http.Request){
      fmt.Fprint(w, "Hello Bar")
  })
  return mux
}

func main() {
  http.ListenAndServe(":3000", MakeWebHandler())
}
```

```go
// ex29.5/ex29_5_test.go
package main

import (
  "io"
  "net/http"
  "net/http/httptest"
  "testing"
  "github.com/stretchr/testify/assert"
)


func TestIndexHandler(t *testing.T) {
  assert := assert.New(t)

  res := httptest.NewRecorder()
  req := httptest.NewRequest("GET", "/", nil) // '/' 경로 테스트

  mux := MakeWebHandler()
  mux.ServeHTTP(res, req)

  assert.Equal(http.StatusOK, res.Code) // Code 확인
  data, _ := io.ReadAll(res.Body)    // 데이터를 읽어서 확인
  assert.Equal("Hello World", string(data))
}

func TestBarHandler(t *testing.T) {
  assert := assert.New(t)

  res := httptest.NewRecorder()
  req := httptest.NewRequest("GET", "/bar", nil) // '/bar' 경로 테스트

  mux := MakeWebHandler()
  mux.ServeHTTP(res, req)

  assert.Equal(http.StatusOK,res.Code)
  data, _ := io.ReadAll(res.Body)
  assert.Equal("Hello Bar", string(data))
}
```


- JSON 데이터 전송

```json
{
  "Name":"abc",
  "Age": 16,
  "Score": 87
}
```

```go
// ex29.6/ex29.6.go
package main

import (
  "fmt"
  "net/http"
  "encoding/json"
)

type Student struct {
  Name string
  Age int
  Score int
}

func StudentHandler(w http.ResponseWriter, r *http.Request) {
  student := Student{"Abc", 18, 87}
  data, _ := json.Marshal(student)
  w.Header().Add("content-type", "application/json")
  w.WriteHeader(http.StatusOK)
  fmt.Fprint(w, string(data))
}

func MakeWebHandler() http.Handler {
  mux := http.NewServeMux()
  mux.HandleFunc("/student", StudentHandler)
  mux.HandleFunc("/", func(w http.ResponseWriter, r *http.Request){
      fmt.Fprint(w, "Hello World")
  })
  return mux
}

func main() {
  http.ListenAndServe(":3000", MakeWebHandler())
}
```

```go
// ex29.6/ex29_6_test.go
package main

import (
  "io"
  "net/http/httptest"
  "net/http"
  "testing"
  "encoding/json"
  "github.com/stretchr/testify/assert"
)

func TestIndexHandler(t *testing.T) {
  assert := assert.New(t)

  res := httptest.NewRecorder()
  req := httptest.NewRequest("GET", "/", nil) // '/' 경로 테스트

  mux := MakeWebHandler()
  mux.ServeHTTP(res, req)

  assert.Equal(http.StatusOK, res.Code)
  data, _ := io.ReadAll(res.Body)
  assert.Equal("Hello World", string(data))
}

func TestJsonHandler(t *testing.T) {
  assert := assert.New(t)

  res := httptest.NewRecorder()
  req := httptest.NewRequest("GET", "/student", nil) // '/student' 경로 테스트

  mux := MakeWebHandler()
  mux.ServeHTTP(res, req)

  assert.Equal(http.StatusOK, res.Code)
  student := &Student{}

  // res.Body 파싱 -> Student 타입
  err := json.NewDecoder(res.Body).Decode(student)
  assert.Nil(err) // 결과 확인
  assert.Equal("Abc", student.Name)
  assert.Equal(18, student.Age)
  assert.Equal(87, student.Score)
}
```

- HTTPS 웹서버 만들기
  - HTTP는 모든 요청이 평문(일반 문자열)
  - HTTPS는 요청과 응답을 공개키 암호화 방식을 사용해서 암호화한 프로토콜
    - 패킷이 암호화 되기 때문에 스니핑 해도 내용 알 수 없음

- 공개키 암호화 방식
  - 공개키, 비밀키 두가지 키 생성하여 클라이언트에 공개키, 서버에 비밀키 비공개 상태로 보관
  - 클라이언트가 HTTPS 요청 보낼 때 공개키로 암호화, 서버가 비밀키로 복호화: 비대칭 암호화 방식
    - 참고: Khan Academy Lecture, "칸 아카데미 공개키"

- 인증서와 비밀키 생성
  - 인증서는 인증기관에서 발급해야 하지만 개인 프로젝트에서는 셀프인증
  - openssl로 인증서 발급

```sh
# rsh:2048 방식으로 키 localhost.key 와 인증파일 localhost.csr 생성
# localhost.key는 절대 외부에 공개되지 않도록 별도 저장소에 저장 (웹서버 로컬 파일 시스템 저장 권장 X, 일정주기 교체 권장)
openssl req -new -newkey rsa:2048 -nodes -keyout localhost.key -out localhost.csr

# .csr 인증파일을 기관에 제출해서 .crt 인증서 생성
# x509 알고리즘으로 1년짜리 인증서 발급
# 개인정보를 수집하고 외부로 공개되는 사이트는 반드시 인증기관을 통해 인증받은 인증서 사용하도록 법적 강제되어있음
openssl x509 -req -days 365 -in localhost.csr -signkey localhost.key -out localhost.crt
```

```go
package main
import (
  "fmt"
  "log"
  "net/http"
)

func main() {
  http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
      fmt.Fprint(w, "Hello World")
  })

  err := http.ListenAndServeTLS( ":3000", "localhost.crt", "localhost.key", nil)
  if err != nil {
    log.Fatal(err)
  }
}
```

### 30.Restful API 서버 만들기


1. gorilla/mux 같은 RESTful API 웹서버 제작 도와주는 패키지 설치
2. RESTful API에 맞춰서 Web handler 함수 생성
3. RESTful API를 테스트하는 테스트 코드 생성
4. 웹 브라우저로 데이터 조회

- HTTP 메서드: GET, POST, PUT, PATCH, DELETE
  - GET /students 전체 학생 데이터 반환
  - GET /students/id 아이디에 해당하는 학생 데이터 반환
  - POST /students 새로운 학생 등록
  - PUT /students/id 아이디 해당 학생 데이터 변경
  - DELETE /students/id 아이디 해당 학생 데이터 삭제


- RESTful API 특징
  1. 자기 표현적인 URL
  2. 메서드로 행위 표현 : URL과 메서드 조합으로 데이터 조작 정의
  3. 서버/클라이언트 구조
    - 데이터 제공자 / 데이터 사용자
  4. 무상태 statless: 서버는 클라이언트 상태 유지 X
  5. 캐시 처리 cacheable: 더 쉽게 캐쉬정책 적용하여 성능 개선 가능


- gorilla/mux 패키지 설치

```sh
go get -u github.com/gorilla/mux
```

- GET "/students" 학생 리스트 조회
- GET "/student/{id:[0-9]+}" 학생 조회
- POST "/students" 학생 등록
- DELETE "/student/{id:[0-9]+}" 학생 삭제

```go
// ex30.1/ex30.1.go
package main

import (
  "encoding/json"
  "net/http"
  "sort"
  "strconv"

  "github.com/gorilla/mux"
)

type Student struct {
  Id int
  Name string
  Age int
  Score int
}

/**
  Student 리스트를 Id 기준정렬하기 위한, Id 정렬 인터페이스 정의
*/
type Students []Student

func (s Students) Len() int {
  return len(s)
}

func (s Students) Swap(i, j int) {
  s[i], s[j] = s[j], s[i]
}

func (s Students) Less(i, j int) bool {
  return s[i].Id < s[j].Id
}

var students map[int]Student
var lastId int

func GetStudentListHandler(w http.ResponseWriter, r *http.Request) {
  list := make(Students, 0) // 학생 목록을 Id로 정렬
  for _, student := range students {
    list = append(list, student)
  }
  sort.Sort(list)

  w.WriteHeader(http.StatusOK)
  w.Header().Set("Content-Type", "application/json")

  json.NewEncoder(w).Encode(list) // JSON 포맷으로 변경
}

func GetStudentHandler(w http.ResponseWriter, r *http.Request) {
  vars := mux.Vars(r)
  id, _ := strconv.Atoi(vars["id"])
  student, ok := students[id]

  if !ok {
    w.WriteHeader(http.StatusNotFound)
    return
  }
  w.WriteHeader(http.StatusOK)
  w.Header().Set("Content-Type", "application/json")
  json.NewEncoder(w).Encode(student)
}

func PostStudentHandler(w http.ResponseWriter, r *http.Request) {
  var student Student
  err := json.NewDecoder(r.Body).Decode(&student) // JSON 데이터 변환
  if err != nil {
    w.WriteHeader(http.StatusBadRequest)
    return
  }

  lastId++  // id를 증가시킨 후 앱에 등록
  student.Id = lastId

  students[lastId] = student
  w.WriteHeader(http.StatusCreated)
}

func DeleteStudentHandler(w http.ResponseWriter, r *http.Request) {
  vars := mux.Vars(r)
  id, _ := strconv.Atoi(vars["id"])
  _, ok := students[id]
  if !ok {
    w.WriteHeader(http.StatusNotFound) // id 해당 학생 없으면 에러
    return
  }
  delete(students, id)
  w.WriteHeader(http.StatusOK) // 삭제 성공 시, StatusOK 반환
}

func MakeWebHandler() http.Handler {
  mux := mux.NewRouter() // gorilla/mux 생성

  /** 새로운 핸들러 등록 */
  mux.HandleFunc("/students", GetStudentListHandler).Methods("GET") // 학생 리스트 조회
  mux.HandleFunc("/student/{id:[0-9]+}", GetStudentHandler).Methods("GET") // 학생 한명 조회
  mux.HandleFunc("/students", PostStudentHandler).Methods("POST") // 학생 등록
  mux.HandleFunc("/student/{id:[0-9]+}", DeleteStudentHandler).Methods("DELETE") // 학생 삭제

  students = make(map[int]Student)
  students[1] = Student{1, "zzz", 10, 77}
  students[2] = Student{2, "aaa", 20, 88}
  students[3] = Student{3, "ccc", 30, 99}
  students[4] = Student{4, "bbb", 40, 50}
  lastId = 4

  return mux
}

func main() {
  http.ListenAndServe(":3000", MakeWebHandler())
}
```

```go
// ex30.1/ex30_1_test.go
package main

import (
  "encoding/json"
  "net/http"
  "net/http/httptest"
  "testing"
  "strings"

  "github.com/stretchr/testify/assert"
)

func TestJsonHandler(t *testing.T) {
  assert := assert.New(t)

  res := httptest.NewRecorder()
  req := httptest.NewRequest("GET", "/students", nil) // '/students' 경로 테스트

  mux := MakeWebHandler()
  mux.ServeHTTP(res, req)

  assert.Equal(http.StatusOK, res.Code)
  var list []Student
  err := json.NewDecoder(res.Body).Decode(&list)
  assert.Nil(err)
  assert.Equal(4, len(list))
  assert.Equal("zzz", list[0].Name)
  assert.Equal("aaa", list[1].Name)
}

func TestJsonHandler2(t *testing.T) { 
  assert := assert.New(t)

  var student Student
  mux := MakeWebHandler()
  res := httptest.NewRecorder()
  req := httptest.NewRequest("GET", "/student/1", nil) // id=1 학생 조회

  mux.ServeHTTP(res, req)
  assert.Equal(http.StatusOK, res.Code)
  err := json.NewDecoder(res.Body).Decode(&student)
  assert.Nil(err)
  assert.Equal("zzz", student.Name)


  res = httptest.NewRecorder()
  req = httptest.NewRequest("GET", "/student/2", nil) // id=2 학생 조회
  mux.ServeHTTP(res, req)
  assert.Equal(http.StatusOK, res.Code)
  err = json.NewDecoder(res.Body).Decode(&student)
  assert.Nil(err)
  assert.Equal("aaa", student.Name)
}

func TestJsonHandler3(t *testing.T) { 
  assert := assert.New(t)

  var student Student
  mux := MakeWebHandler()
  res := httptest.NewRecorder()
  req := httptest.NewRequest("POST", "/students",
    // 새로운 학생 데이터 등록
    strings.NewReader(`{"Id":0, "Name": "nnnn", "Age": 15, "Score": 78}`),
  )

  mux.ServeHTTP(res, req)
  assert.Equal(http.StatusCreated, res.Code)

  res = httptest.NewRecorder()
  req = httptest.NewRequest("GET", "/student/5", nil)
  // 추가된 학생 데이터
  mux.ServeHTTP(res, req)
  assert.Equal(http.StatusOK, res.Code)
  err := json.NewDecoder(res.Body).Decode(&student)
  assert.Nil(err)
  assert.Equal("nnnn", student.Name)
}

func TestJsonHandler4(t *testing.T) { 
  assert := assert.New(t)

  mux := MakeWebHandler()
  res := httptest.NewRecorder()
  req := httptest.NewRequest("DELETE", "/student/1", nil)

  // DELETE 요청
  mux.ServeHTTP(res, req)
  assert.Equal(http.StatusOK, res.Code)

  res = httptest.NewRecorder()
  req = httptest.NewRequest("GET", "/students", nil)
  mux.ServeHTTP(res, req)

  assert.Equal(http.StatusOK, res.Code)
  var list []Student
  err := json.NewDecoder(res.Body).Decode(&list)
  assert.Nil(err)
  assert.Equal(3, len(list))
  assert.Equal("aaa", list[0].Name)
}
```

### 31.TODO리스트 웹사이트 만들기

- 프론트엔드(HTML, Javascript) <-> 백엔드(Go 웹 서버)
- gorilla/mux 이외에 urfave/negroni 와 unrolled/render 패키지 사용

1. RESTful API에 맞춰 서비스 정의
2. Todo 구조체 정의
3. RESTful API에 맞춰 각 핸들러 정의
4. HTML 작성
5. Javascript 작성
6. 웹브라우저 동작 확인


- urfave/negroni 설치
  - 자주 사용하는 웹 핸들러를 제공하는 패키지
    - 로그기능
    - panic 복구 기능
    - 파일 서버 기능

```sh
go get github.com/urfave/negroni
```

```go
mux := MakeWebHandler() // 우리가 만든 핸들러
n := negroni.Classic()  // negroni 기본 핸들러
n.UseHandler(mux) // 우리가 만든 핸들러를 감쌈

err := http.ListenAndServe(":3000", n) // negroni 기본 핸들러가 동작함
```

- unrolled/render 설치
  - 웹서버 응답을 구현하는데 유용한 패키지.
  - 서버응답으로 HTML, JSON, TEXT 같은 포맷 간단히 사용가능

```sh
go get github.com/unrolled/render
```

```go
// JSON. 포맷으로 변환하여 응답
r := render.New()
r.JSON(w, http.StatusOK, map[string]string{"hello": "json"})
```

- 웹 서버 만들기
  - GET /todos 리스트조회
  - POST /todos 등록
  - PUT /todos/id 업데이트
  - DELETE /todos/id 삭제

```sh
cd 30-restful/ex31.1
go mod init ex31.1
go mod tidy
go build
./ex31.1
  2022/07/27 16:02:13 Started App
```

```go
// ex31.1/ex31.1.go
package main

import (
  "encoding/json"
  "log"
  "net/http"
  "sort"
  "strconv"

  "github.com/gorilla/mux"
  "github.com/unrolled/render"
  "github.com/urfave/negroni"
)


var rd *render.Render

// 할일 정보 담는 Todo 구조체
type Todo struct {
  ID int `json:"id,omitempty"`    // JSON 포맷으로 변환 옵션
  Name string `json:"name"`
  Completed bool `json:"completed,omitempty"`
}

var todoMap map[int]Todo
var lastID int = 0

type Todos []Todo

func (t Todos) Len() int {
  return len(t)
}

func (t Todos) Swap(i, j int) {
  t[i], t[j] = t[j], t[i]
}

func (t Todos) Less(i, j int) bool {
  return t[i].ID < t[j].ID
}

func GetTodoListHandler(w http.ResponseWriter, r *http.Request) {
  list := make(Todos, 0)
  for _, todo := range todoMap {
    list = append(list, todo)
  }
  sort.Sort(list)  // ID 기준 정렬
  rd.JSON(w, http.StatusOK, list)  // JSON 포맷으로 반환

  // w.WriteHeader(http.StatusOK)
  // w.Header().Set("Content-Type", "application/json")
  // json.NewEncoder(w).Encode(list) // JSON 포맷으로 변경
}

func PostTodoHandler(w http.ResponseWriter, r *http.Request) {
  var todo Todo
  err := json.NewDecoder(r.Body).Decode(&todo)
  if err != nil {
    log.Fatal(err)
    w.WriteHeader(http.StatusBadRequest)
    return
  }
  lastID++
  todo.ID = lastID
  todoMap[lastID] = todo
  rd.JSON(w, http.StatusCreated, todo)
}

type Success struct {
  Success bool `json:"Success"`
}

func RemoveTodoHandler(w http.ResponseWriter, r *http.Request) {
  vars := mux.Vars(r)
  id, _ := strconv.Atoi(vars["id"])
  if _, ok := todoMap[id]; ok {
    delete(todoMap, id)
    rd.JSON(w, http.StatusOK, Success{true})
  } else {
    rd.JSON(w, http.StatusNotFound, Success{false})
  }
}

func UpdateTodoHandler(w http.ResponseWriter, r *http.Request) {
  var newTodo Todo
  err := json.NewDecoder(r.Body).Decode(&newTodo)
  if err != nil {
    log.Fatal(err)
    w.WriteHeader(http.StatusBadRequest)
    return
  }

  vars := mux.Vars(r)
  id, _ := strconv.Atoi(vars["id"])
  if todo, ok := todoMap[id]; ok {
    todo.Name = newTodo.Name
    todo.Completed = newTodo.Completed
    rd.JSON(w, http.StatusOK, Success{true})
  } else {
    rd.JSON(w, http.StatusBadRequest, Success{false})
  }
}

func MakeWebHandler() http.Handler {
  todoMap = make(map[int]Todo)

  mux := mux.NewRouter() // gorilla/mux 객체 생성

  mux.Handle("/", http.FileServer(http.Dir("public")))
  mux.HandleFunc("/todos", GetTodoListHandler).Methods("GET")
  mux.HandleFunc("/todos", PostTodoHandler).Methods("POST")
  mux.HandleFunc("/todos/{id:[0-9]+}", RemoveTodoHandler).Methods("DELETE")
  mux.HandleFunc("/todos/{id:[0-9]+}", UpdateTodoHandler).Methods("PUT")
  return mux
}

func main() {
  rd = render.New()
  m := MakeWebHandler()
  n := negroni.Classic()
  n.UseHandler(m)

  log.Println("Started App")
  err := http.ListenAndServe(":3000", n)
  if err != nil {
    panic(err)
  }
}
```

- 프론트엔드 만들기
  - ex31.1/public/index.html
  - ex31.1/public/todo.js
  - ex31.1/public/todo.css


- 3티어 웹
  - 프론트엔드-백엔드-데이터베이스

- 웹 배포 방법
  - 로컬에 띄우는 서버 한계
    1. 도메인이 없음 (e.g. https://13.125.141.84  https://mytodolist.com)
    2. 고정된 공개 IP가 없음
      - IPv4는 고정된것이 아닌 공유기나 ISP에서 컴퓨터에 임시할당한 주소이고, 공개된 주소도 아님
      - 공유기 네트워크 안쪽에서만 유효함
  - 개인 PC는 고정 IP가 없음
  - 고정된 공개 IP주소를 얻으려면 공개 IP 대역을 이미 획득한 인터넷 호스팅업체로부터 호스팅 받아야함
  - IaaS, PaaS: aws,gcloud,azure (유료)
  - Heroku(무료) Paas: 간단한 명령어로 웹서버 배포 가능

- 클라우드 서비스 유형
  - IaaS : infrastructure as a service
  - PaaS : 머신성능 선택 및 서버 실행간편화. 서버 세부조정 어려움
  - SaaS : e.g. 구글드라이브, 구글문서도구


- 헤로쿠로 배포하기
  - heroku.com 가입
  - CLI 설치
    - https://devcenter.heroku.com/articles/heroku-cli
    - `curl https://cli-assets.heroku.com/install.sh | sh`
    - `heroku version`

```sh
# 모듈 생성
mkdir todo && cd $_
touch ex31.1.go
mkdir public
go mod init todo
go build

git init
heroku login
heroku create
```

- 웹서버 수정
  - 헤로쿠에서 웹서버 배포하려면 port등 일부 수정 필요
  - Procfile 생성 및 내용 입력

```go
func main() {
  rd = render.New()
  m := MakeWebHandler()
  n := negroni.Classic()
  n.UseHandler(m)

  log.Println("Started App")
  port := os.Getenv("PORT") // 헤로쿠서버에서 환경변수 PORT 가져오기
  // err := http.ListenAndServe(":3000", n)
  err := http.ListenAndServe(":" + port, n) // port를 이용해서 웹 서버 실행
  if err != nil {
    panic(err)
  }
}
```

```sh
cd todo
cat > Procfile
  web: bin/todo
```

- 깃 커밋

```sh
# .gitignore
cat > .gitignore
  *.exe

git add .
git status
git commit -m 'first commit of todo'
git push heroku master

heroku open
```

- go build 크로스 플랫폼

```sh
GOOS=windows GOARCH=amd64 go build
```

- Linux 환경배포

```sh
# 로컬
zip -r public.zip public/
scp public.zip root@{ip}:/root
scp demo root@{ip}:/root

# 원격
mkdir goapp && cd $_
unzip public.zip -d goapp
cp /root/demo /goapp
./demo &

# http://{ip}:3000/
# 서버 
```




## golang http server

```
Q) what's the best practice for golang to store aws credentials 
A) When it comes to storing AWS credentials in a Go application,
the best practice is to use the AWS SDK for Go's built-in credential chain.
The credential chain allows you to specify multiple ways to provide AWS credentials,
including environment variables, shared credential files, and IAM roles.
The SDK will automatically search for and use the first set of valid credentials it finds in the chain.

Here's an example of using the credential chain in a Go application:
```


```go
package main

import (
    "fmt"

    "github.com/aws/aws-sdk-go/aws"
    "github.com/aws/aws-sdk-go/aws/session"
    "github.com/aws/aws-sdk-go/service/s3"
)

func main() {
    // Create a new session using the default configuration
    sess := session.Must(session.NewSessionWithOptions(session.Options{
        SharedConfigState: session.SharedConfigEnable,
    }))

    // Create a new S3 client using the session
    svc := s3.New(sess)

    // List all buckets in the account
    result, err := svc.ListBuckets(nil)
    if err != nil {
        panic(err)
    }

    // Print the name of each bucket
    for _, bucket := range result.Buckets {
        fmt.Println(*bucket.Name)
    }
}
```

```
In this example, we create a new session using the session.NewSessionWithOptions function
and specifying SharedConfigEnable as the SharedConfigState option.
This tells the SDK to use the default configuration file and environment variables to find AWS credentials.

If you need to use a specific set of credentials or a different configuration file,
you can specify those options in the session.NewSessionWithOptions function. For example:
```

- This would create a session with the specified profile ("my-profile") and region ("us-west-2").

```go
sess := session.Must(session.NewSessionWithOptions(session.Options{
    Config: aws.Config{
        Region: aws.String("us-west-2"),
    },
    Profile: "my-profile",
}))
```


### Stack vs. Heap

- https://medium.com/@denniswon/a-practical-guide-to-memory-allocation-in-go-3e7aca6b449a
  - Variables whose addresses are taken become candidates for allocation on the heap.
  - Memory allocation in Go follows escape analysis, where variables local to a function are typically allocated on the stack. However, if the compiler cannot prove that a variable is not referenced after the function returns, it allocates the variable on the heap to avoid dangling pointer errors.

- Variables in Go can be allocated either on the stack or the heap:
  - Stack: Local variables (like function arguments or temporary values) are usually allocated on the stack. This memory is fast to allocate and deallocate.
  - Heap: Dynamic memory (like slices, maps, and large data structures) is allocated on the heap. This memory is managed by the garbage collector and is slower to allocate and deallocate.

- Both stdout and stderr use memory from the stack or heap, depending on how they are accessed.




### Userspace vs. Kernal space

https://stackoverflow.com/questions/1739799/doesnt-the-fact-that-go-and-java-use-user-space-thread-mean-that-you-cant-real

In Go, the term **userspace** refers to the part of a program that runs in user mode, as opposed to kernel mode.

1. **Kernel Mode vs. User Mode**:
   - When a computer runs an operating system, it operates in two primary modes:
     - **Kernel Mode**: In this mode, the operating system's kernel (core) has direct access to hardware resources (CPU, memory, devices). It can execute privileged instructions and manage system resources.
     - **User Mode**: In this mode, regular application code (user programs) runs. User-mode processes don't have direct access to hardware; they rely on the kernel for system calls (e.g., file I/O, networking, process management).

2. **Userspace in Go**:
   - In the context of Go programming, **userspace** specifically refers to the part of your Go program that runs in user mode.
   - When you write Go code, most of it runs in userspace. This includes your application logic, data processing, and interactions with libraries.
   - Userspace code interacts with the Go runtime, which manages memory, goroutines, garbage collection, and other runtime features.

3. **Examples**:
   - When you create a Go program that reads a file, processes data, and sends an HTTP request, all those actions happen in userspace.
   - However, if your Go program needs to perform low-level tasks (e.g., interacting directly with hardware, managing memory pages), it might need to make system calls to the kernel (enter kernel mode).

4. **WireGuard-Go Example**:
   - An interesting example related to userspace is **WireGuard-Go**.
   - WireGuard is a modern VPN protocol, and WireGuard-Go is an implementation of WireGuard in Go.
   - When you run WireGuard-Go, it creates a virtual network interface (like `wg0`) entirely in userspace.
   - Instead of relying on a kernel module (which is faster but requires administrative privileges), WireGuard-Go manages the VPN interface purely in userspace.
   - You can use it by running:
     ```
     $ wireguard-go wg0
     ```
     This command creates the interface and forks into the background.

5. **Pros and Cons of Userspace**:
   - **Advantages**:
     - Portability: Userspace code is more portable across different platforms (Linux, macOS, Windows, etc.).
     - Flexibility: Userspace programs can be written in any language (including Go) without requiring kernel-specific code.
   - **Disadvantages**:
     - Performance: Userspace operations are generally slower than kernel-mode operations due to the overhead of system calls.
     - Privileges: Some tasks (e.g., managing network interfaces) require kernel-level access, which userspace programs lack.

In summary, userspace in Go refers to the part of your program that runs outside the kernel, handling application logic and interactions with libraries. WireGuard-Go is an excellent example of userspace networking! 🚀¹⁵

(1) WireGuard/wireguard-go - GitHub. https://github.com/WireGuard/wireguard-go.
(2) GitHub - google/netstack: IPv4 and IPv6 userland network stack. https://github.com/google/netstack.
(3) examples module - github.com/cilium/ebpf/examples - Go Packages. https://pkg.go.dev/github.com/cilium/ebpf/examples.
(4) Golang 1.18 workspaces 尝鲜 - 掘金. https://juejin.cn/post/7087207256126652429.
(5) Get familiar with workspaces - The Go Programming Language. https://go.dev/blog/get-familiar-with-workspaces.
(6) undefined. https://git.zx2c4.com/wireguard-go.
