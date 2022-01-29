---
title :  "[Swift] 옵셔널"
date :   2022-01-28 16:35 +0900
categories: [Programming, Swift]
tags: [swift, Xcode, Programming, iOS]
---

> 본 게시물은 '스위프트 프로그래밍(3판)'의 8장 옵셔널을 정리하며 작성하는 게시글입니다.  
> 아래 작성된 코드는 [yagom님 swift 기본 문법](https://github.com/yagom/swift_basic.git)의 코드를 참고했습니다.

## 옵셔널 개념
---
단어 뜻 그대로 '선택적인', 즉 값이 `있을 수도, 없을 수도 있음`을 나타내는 표현이다.  
이는 변수나 상수 등에 꼭 값이 있다는 것을 보장할 수 없다. 즉 변수 또는 상수의 값이 nil일 수도 있다'는 것을 의미한다.  


## 옵셔널 사용
---
```swift
// var myName: Optional<String> 처럼 옵셔널을 명확히 써줄 수도 있다 
// 하지만 물음표를 붙여주는 것이 조금 더 편하고 읽기 쉽기 때문에 굳이 긴 표현을 사용하지 않는다.
var myName: String? = "gaanii"

print(myName)       // Optional("gaanii")

myName = nil
print(myName)       // nil
```
nil은 옵셔널로 선언된 곳에서만 사용될 수 있다.  

옵셔널 변수 또는 상수 등은 데이터 타입 뒤에 `물음표(?)`를 붙여 표현한다.

옵셔널 타입의 값을 print 함수를 통해 출력하면 Optional("gaanii") 라고 출력되지만, 앞으로는 주석 표현을 간단히 하기 위해 Optional()을 생략하고 표기할 것이다.  


## 옵셔널 사용 이유
---
### 1. 명시적 표현
- nil의 가능성을 코드만으로 표현이 가능하다.
- 문서/주석 작성 시간을 절약해준다.

### 2. 안전한 사용
- 전달받은 값이 옵셔널이 아닌 경우, nil 체크를 하지 않고 사용 가능하다.
- 예외 상황을 최소화하는 안전한 코딩을 할 수 있다.


## 옵셔널 정의
---
### 열거형
연관된 항목들을 묶어서 표현할 수 있는 타입을 말한다.  

이 자료형은 배열이나 딕셔너리 같은 타입과 다르게 프로그래머가 정의해준 항목 값 외에는 추가/수정이 불가하다.  

열거형 각 항목이 원시 값(Raw Value)이라는 형태로 (정수, 실수, 문자 타입 등의) 실제 값을 가질 수도 있다.  


### 옵셔널 정의
```swift
public enum Optional<Wrapped> : ExpressibleByNilLiteral {
    case none
    case some(Wrapped)
    
    public init(_ some: Wrapped)
    // 중략 ...
}

let optionalValue: Optional<Int> = nil
let optionalValue: Int? = nil
```
위 코드에서 확인가능한 것은 다음과 같다.  
- 옵셔널은 제네릭이 적용된 열거형이다.
- ExpressibleByNilLiteral 프로토콜을 따른다.(아직 배우지 않은 내용)
- 옵셔널이 값을 갖는 케이스와 그렇지 못한 케이스 두 가지로 정의되어 있다.
- 즉, nil일때는 none 케이스, 값이 있는 경우는 some 케이스(연관값 Wrapped)가 된다.
- 값이 옵셔널이라는 열거형의 방패막에 보호되어 래핑되어 있는 모습이다.  
