---
title :  "[Swift] 옵셔널 추출"
date :   2022-01-28 18:51 +0900
categories: [Programming, Swift]
tags: [swift, Xcode, Programming, iOS]
---

> 본 게시물은 '스위프트 프로그래밍(3판)'의 8장 옵셔널을 정리하며 작성하는 게시글입니다.  
> 아래 작성된 코드는 [yagom님 swift 기본 문법](https://github.com/yagom/swift_basic.git)의 코드를 참고했습니다.

  

옵셔널 추출이란, 옵셔널에 들어있는 값을 사용하기 위해 꺼내오는 것 !
---

## 1. 강제 추출 Forced Unwrapping
---
옵셔널 강제 추출은 옵셔널의 값을 추출하는 가장 간단하지만 가장 위험한 방법이다.  

런타임 오류가 일어날 가능성이 가장 높고, 옵셔널을 만든 의미가 무색해지는 방법이기도 하기 때문이다.  

```swift
var myName: String? = "gaanii"

var gaanii: String = myName!

myName = nil
gaanii = myName!

if myName != nil {
    print("My name is \(myName!)")
} else {
    print("myName == nil")
}
```
옵셔널의 값을 강제 추출하려면 옵셔널 값의 뒤에 `느낌표(!)`를 붙여주면 값을 강제로 추출하여 반환하게 된다.

만약 강제 추출 시 옵셔널에 값이 없다면, 즉 nil이라면 런타임 오류가 발생한다.  

런타임 오류의 가능성을 항상 내포하기 때문에 옵셔널 강제 추출 방식을 사용하는 것을 지양해야 한다.  


## 2. 옵셔널 바인딩 Optional Binding
---
옵셔널 바인딩은 옵셔널에 값이 있는지 확인할 때 사용한다.  

만약 옵셔널에 값이 있다면 옵셔널에서 추출한 값을 일정 블록 안에서 사용할 수 있는 상수나 변수로 할당해서 옵셔널이 아닌 형태로 사용할 수 있도록 해준다.  

옵셔널 바인딩은 if - let 방식을 사용한다.  
### 1개의 옵셔널 값 추출
```swift
var myName: String? = "gaanii"

// 옵셔널 바인딩을 통하여 임시 상수를 할당한다.
// 임시 상수는 if 구문을 실행하는 블록 안쪽에서만 사용할 수 있다.  
// 즉, if 블록 밖에서는 사용할 수 없고, else 블록에서도 사용할 수 없다.
if let name = myName {
    print("My name is \(name)")
} else {
    print("myName == nil")
}
// my name is gaanii

// 옵셔널 바인딩을 통하여 임시 변수를 할당한다.
// 상수로 사용하지 않고 변수로 사용하고 싶다면 if var를 사용한다.
if var name = myName {
    name = "galamgwi"
    print("My name is \(name)")
} else {
    print("myName == nil")
}
// my name is galamgwi
```  

### 여러 개의 옵셔널 값의 추출 
```swift
var myName: String? = "gaanii"
var yourName: String? = nil

if let name = myName, let friend = yourName {
    print("We are friend! \(name) & \(friend)")
}

yourName = "Hwan"

if let name = myName, let friend = yourName {
    print("We are friend! \(name) & \(friend)")
}
// We are friend! gaanii & Hwan
```

## 3. 암시적 추출 옵셔널 Implicitly Unwrapped Optionals
---
### 사용 방법
암시적 추출 옵셔널을 사용하려면 타입 뒤에 `느낌표(!)`를 사용하면 된다.  

### 사용 이유
때때로 nil을 할당하고 싶지만, 옵셔널 바인딩으로 매번 값을 추출하기 귀찮거나 로직상으로 nil 때문에 런타임 오류가 발생하지 않을 것 같다는 확신이 들때 nil을 할당해줄 수 있는 옵셔널이 아닌 변수나 상수가 있으면 좋을 건데, 이때 사용하는 것이 암시적 추출 옵셔널이다.

### 사용 예시
```swift
var myName: String! = "gaanii"
print(myName)
myName = nil

// 암시적 추출 옵셔널도 옵셔널이므로 바인딩 사용 가능 
if let name = MyName {
    print("My name is \(name)")
} else {
    print("myName은 nil")
}
```

암시적 추출 옵셔널로 지정된 타입은 일반 값처럼 사용 가능하고, 옵셔널이기 때문에 nil도 할당 가능하다.  

하지만 nil이 할당되어 있을 때 접근을 시도하면 런타임 오류가 발생한다.  