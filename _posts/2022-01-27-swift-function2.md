---
title :  "[Swift] 함수 고급"
date :   2022-01-27 15:12 +0900
categories: [Programming, Swift]
tags: [swift, Xcode, Programming]
---

> 본 게시물은 '스위프트 프로그래밍(3판)'의 7장 함수를 정리하며 작성하는 게시글입니다.  
> 아래 작성된 코드는 [yagom님 swift 기본 문법](https://github.com/yagom/swift_basic.git)의 코드를 참고했습니다.

## 매개변수와 전달인자
---
매개변수는 함수를 정의할 때 외부로부터 받아들이는 전달 값의 이름을 의미한다.  
전달인자(Argument), 혹은 인자는 함수를 실제로 호출할 때 전달하는 값을 의미한다.  
```swift
   func hello(name: String) -> String {
       return "Hello \(name)!"
   }

   let helloJenny: String = hello(name: Jenny)
   print(helloJenny)        // Hello Jenny!
```  
위 코드에서 hello(name:)함수에서 매개변수는 name이고, 실제 사용 시 전달받는 값인 "Jenny"가 전달인자에 해당한다.  


## 매개변수 이름과 전달인자 레이블 
---
아래 코드를 살펴보자.  
```swift
func sayHello(myName: String, yourName: String) -> String {
    return "Hello \(yourName)! I'm \(myName)"
}

print(sayHello(myName: "gaanii", yourName: "Hwan"))     // Hello Hwan! I'm gaanii
```  
위 코드에서 함수를 호출할 때 myName과 yourName이라는 **매개변수 이름**을 사용했다.  
여기서 매개변수 이름과 더불어 **전달인자 레이블**을 지정해줄 수 있다.  


전달인자 레이블은 함수 외부에서 매개변수의 역할을 좀 더 명확히 할 수 있다.  이를 사용하려면 함수 정의에서 매개변수 이름 앞에 한칸을 띄운 후 전달인자 레이블을 지정한다.  
```swift
func 함수이름(전달인자1 레이블 매개변수1 이름: 매개변수1 타입 ...) -> 반환타입 {
    /* 실행구문 */
    return 반환 값
}

// from과 to라는 전달인자 레이블을 사용하며
// myName과 name이라는 매개변수 이름이 있는 sayHello 함수 
func sayHello(from myName: String, to name: String) -> String {
    return "Hello \(name)! I'm \(myName)"
}

print(sayHello(from: "gaanii", to: "Hwan"))     // Hello Hwan! I'm gaanii
```
함수 내부에서 전달인자 레이블을 사용할 수 없으며 함수를 호출할 때는 매개변수 이름을 사용할 수 없다.  

전달인자 레이블을 사용하고 싶지 않다면 와일드카드 식별자인 `_`를 사용하면 된다. 아래 코드에서 확인할 수 있다.  
```swift
func sayHello(_ name: String, _ times: Int) -> String {
    var result: String = ""

    for _ in 0 .. < times {
        result += "Hello \(name)!" + " "
    }

    return result
}

print(sayHello("gaanii", 2))    // Hello gaanii! Hello gaanii!
```


## 매개변수 기본값 
---
매개변수마다 기본값을 지정할 수 있다.  즉 매개변수가 전달되지 않으면 기본값을 사용한다는 것이다.  

매개변수 기본값이 있는 함수는 함수를 중복 정의한 것처럼 사용할 수 있다.  
```swift
func sayHello(_ name: String, _ times: Int = 3) -> String {
    var result: String = ""

    for _ in 0 .. < times {
        result += "Hello \(name)!" + " "
    }

    return result
}

print(sayHello("Hwan"))

print(sayHello("gaanii", 2))    // Hello gaanii! Hello gaanii!
```  
sayHello(: times:) 함수의 times 매개변수에 기본값을 3으로 주면 times 매개변수를 넘겨주지 않아도 times 값을 3으로 설정해 함수가 동작한다.  

times 매개변수의 전달 값을 2로 설정하여 넘겨주면 전달 값을 반영하여 두 번 출력한다.  

## 가변 매개변수
---
매개변수로 몇개의 값이 들어올지 모를 때, 가변 매개변수를 사용할 수 있다.  

가변 매개변수는 0개 이상(0개 포함)의 값을 받아올 수 있으며, 가변 매개변수로 들어온 값은 배열처럼 사용 가능하다.  

함수마다 가변 매개변수는 하나만 가질 수 있다.  
```swift
func sayHelloToFriends(me: String, friends names: String...) -> String {
    var result: String = ""

    for friend in names {
        result += "Hello \(friends)" + " " 
    }

    result += "I'm " + me + "!"
    return result
}

print(sayHelloToFriends(me: "gaanii", friends:"Hwan", "Stone", "Hwi", "Ko"))
// Hello Hwan! Hello Stone! Hello Hwi! Hello Ko! I'm gaanii!

prinnt(sayHelloToFriends(me: "gaanii"))
// I'm gaanii!
```
함수의 전달인자로 값을 전달할 때는 보통 값을 복사해서 전달한다.  

값이 아닌 참조를 전달하려면 입출력 매개변수를 사용한다.  

입출력 매개변수의 전달 순서는 다음과 같다.  

1. 함수를 호출할 때, 전달인자의 값을 복사한다.
2. 해당 전달인자의 값을 변경하면 1에서 복사한 것을 함수 내부에서 변경한다.
3. 함수를 반환하는 시점에 2에서 변경된 값을 원래의 매개변수에 할당한다.

참조는 `inout` 매개변수로 전달될 변수 또는 상수 앞에 앰퍼샌드(&)를 붙여 표현한다.  

아래 코드에서 값 타입 매개변수와 참조 타입 매개변수의 사용을 비교하여 볼 수 있다.
```swift
var numbers: [Int] = [1, 2, 3]

func nonReferenceParameter(_ arr: [Int]) {
    var copiedArr: [Int] = arr
    copiedArr[1] = 1
}

func referenceParameter(_ arr: inout [Int]) {
    arr[1] = 1
}

nonReferenceParameter(numbers)
print(numbers[1])       // 2

referenceParameter(&numbers)    // 참조를 표현하기 위해 & 붙여줌 
print(numbers[1])       // 1
```
  
값 타입 데이터의 참조를 전달인자로 보내면 함수 내부에서 참조하여 원래 값을 변경한다(C 포인터와 유사)  

입출력 매개변수는 매개변수 기본값을 가질 수 없으며, 가변 매개변수로 사용될 수 없다.  

또한 상수는 변경될 수 없으므로 입출력 매개변수의 전달인자로 사용될 수 없다.
  
  
## 데이터 타입으로서의 함수 
---
스위프트의 함수는 일급 객체이므로 하나의 데이터 타입으로 사용할 수 있다. 방법은 아래와 같다.
```swift
(매개변수 타입의 나열) -> 반환타입
```  

### 함수타입의 사용
예시를 확인해보자.  
```swift
typealias CalculateTwoInts = (Int, Int) -> Int

func addTwoInts(_ a: Int, _ b: Int) -> Int {
    return a + b
}

func multiply TwoInts(_ a: Int, _ b: Int) -> Int {
    return a * b
}

// var mathFunction: (Int, Int) -> Int = addTwoInts와 동일한 표현
var mathFunction: CalculateTwoInts = addTwoInts

print(mathFunction(2, 5))       // 2 + 5 = 7

mathFunction = multiplyTwoInts
print(mathFunction(2, 5))       // 2 * 5 = 10
```
함수의 타입 표현에서는 반환 타입을 생략할 수 없다.  

함수를 데이터타입으로 사용할 수 있다 것은 함수를 전달인자로 받을 수도, 반환 값으로 돌려줄 수도 있다는 의미이다.  

### 전달인자로 함수를 전달받는 함수
```swift
func printMathResult(_ mathFunction: CalculateTwoInts, _ a: Int, _ b: Int) {
    print("Result: \(mathFunction(a, b))")
}

printMathResult(addTwoInts, 3, 5)       // Result: 8 
```


### 반환 값으로 함수를 반환하는 함수
```swift
func chooseMathFunction(_ toAdd: Bool) -> CalculateTwoInts {
    return toAdd ? addTwoInts : multiplyTwoInts
}

printMathResult(chooseMathFunction(true), 3, 5)     // Result: 8   
```
위 함수는 특정 조건에 따라 적절한 함수를 반환해주는 함수이다.