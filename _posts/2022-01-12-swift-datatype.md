---
title :  "[Swift] 데이터 타입 기본"
date :   2022-01-12 20:34 +0900
categories: [Programming, Swift]
tags: [swift, Xcode, Programming]
---

> 본 게시물은 '스위프트 프로그래밍(3판)'의 3장 데이터 타입 기본을 정리하며 작성하는 게시글입니다.  
> 아래 작성된 코드는 [yagom님 swift 기본 문법](https://github.com/yagom/swift_basic.git)의 코드를 참고했습니다.
> 
## 데이터 타입(자료형)이란 
- 프로그램 내에서 다뤄지는 데이터의 종류를 의미합니다.
- 스위프트의 기본 데이터 타입은 **구조체를 타입의 기반**으로 삼아 스위프트의 다양한 기능(익스텐션, 제네릭 등)을 두루 사용하여 구현되어 있습니다.
- 스위프트의 모든 데이터 타입의 이름은 첫 글자가 대문자로 시작하는 **대문자 카멜케이스**를 사용합니다. 


## Int & UInt
**정수 타입**을 의미한다. (현재는 기본적으로 Int는 64비트 정수형, UInt는 64비트 양의 정수형)  
<span style="background-color:#fff5b1">Int</span>는 +, -. 즉 부호가 있는 정수를 뜻하며, 이 중 - 부호를 포함하지 않는 0을 포함한 양의 정수는 <span style="background-color:#fff5b1">UInt</span>로 표현한다.

각각 데이터 타입의 최댓값/최솟값은 max와 min 프로퍼티로 알아볼 수 있다.
```swift
var someInt:Int = -100
// someInt = -100.1     // 컴파일 오류 발생, 자료형이 다르다.
```

```swift
var someUInt:UInt = 100
// someUInt = -100      // 컴파일 오류 발생, UInt에 음수를 넣을 수 없다.
// someUInt = someInt   // 컴파일 오류 발생, Int와 UInt의 자료형은 엄연히 다르다.
```

## Bool
**불리언 타입**을 의미한다.  
불리언 타입은 참(true) 또는 거짓(false)만 값으로 가진다.     
```swift
var someBool: Bool = true
someBool = false
// someBool = 0         // 컴파일 오류 발생
// someBool = 1         // 컴파일 오류 발생
```

## Float & Double
부동소수점을 사용하는 실수며 **부동소수 타입**이라고 한다. 흔히 말하는 소수점 자리가 있는 수를 말한다.  
부동소수 타입은 정수 타입보다 훨씬 넓은 범위의 수를 표현할 수 있고,   
스위프트에는 64비트의 부동소수를 표현하는 <span style="background-color:#fff5b1">Double</span>와 32비트의 부동소수를 표현하는 <span style="background-color:#fff5b1">Float</span>가 있다.  

64비트 환경에서는 Double은 최소 15자리의 십진수를 표헌할 수 있는 반면에, Floatsms 6자리의 숫자까지만 표현이 가능하다. 필요에 따라 둘 중하나를 선택하여 사용하면 되는데, 대부분은 Double을 사용하길 권장한다.

```swift
var someFloat:Float = 3.14
somefloat = 3

var someDouble:Double = 3.14
someDouble = 3
// someDouble = someFloat   // 컴파일 오류 발생
```

> 스위프트 4.2 버전부터 임의의 수를 만드는 random(in: ) 메소드가 추가되었다.  
> 정수(Int, UInt), 실수(Float, Double) 모두 임의의 수를 만들 수 있다.  


## Character
말 그대로 **문자**를 의미한다.   
단어, 문장과 같은 문자의 집합이 아닌 단 하나의 문자를 의미한다.   
스위프트는 유니코드 9 문자를 사용하기때문에 영어는 물론, 유니코드에서 지원하는 모든 언어 및 특수기호 등을 사용할 수 있다.(심지어, 스위프트 코드를 작성할 때도 유니코드 문자를 모두 사용할 수 있다.)
```swift
var someCharacter:Character = "🇰🇷"
someCharacter = "😄"
someCharacter = "가"
someCharacter = "A"
// someCharacter = "하하하" // 컴파일 오류발생, Character는 단 하나의 문자만을 의미하기 때문이다.
```

## String
문자의 나열, 즉 **문자열**을 의미한다.  
Character와 마찬가지로 유니코드를 사용하고, 값의 앞뒤에 큰따옴표("")를 사용하여 표현한다.
```swift
var someString: String = "하하하 😄 "
someString = someString + "웃으면 복이와요"
print(someString)             // 하하하 😄 웃으면 복이와요

// someString = someCharacter // 컴파일 오류발생, Character와 String은 다른 데이터 타입이다.
```
  

여러줄을 가지는 문자열을 사용하고싶다면 큰따옴표 세 개를 사용하면 된다.  
반드시 겹따옴표 세 개인 줄(첫줄과 끝줄)에서 줄 바꿈을 하지 않으면 오류가 발생한다.  
```swift
someString = """
안녕하세요
저는 개발자가 되고싶은
가람쥐입니다!
"""

// 아래와 같은 경우 오류가 발생한다.
someString = """오류
발생"""
```
  

스위프트에는 문자열 내에서 일정 기능을 하는 특수문자(제어문자)가 존재한다.  
모두 백슬래시에 특정한 문자를 조합하여 사용하며, 가장 많이 쓰이는 특수문자는 아래 표와 같다.

|특수문자|설명|
|------|------|
|\n|줄바꿈 문자|
|\&#92;|문자열 내에서 백슬래시를 표현하고자 할 때 사용|
|\&#34;|문자열 내에서 큰따옴표를 표현하고자 할 때 사용|
|\t|탭 문자. 키보드의 탭키를 눌렀을 때와 같은 효과|
|\0|문자열이 끝났음을 알리는 null 문자|

  

## Any, AnyObject, nil
<span style="background-color:#fff5b1">Any</span>는 모든 데이터 타입을 사용할 수 있다는 뜻이다.  
변수 또는 상수의 데이터 타입이 Any로 지정되어있다면 그 변수 또는 상수에는 어떤 종류의 데이터 타입이든지 상관없이 할당 가능하다.  

<span style="background-color:#fff5b1">AnyObject</span>는 Any보다 조금 한정된 의미를 가지며, 클래스의 인스턴스만 할당할 수 있다. 이 내용은 추후 업로드할 게시물에서 설명하겠다. 
```swift
var someVar: Any = "gaanii"     // Any로 선언된 변수에는 문자열도
someVar = 23                    // 정수도
someVar = 166.9                 // 실수, 또는 어떤 타입의 값도 할당 가능
```

```swift
class SomeClass {}
var someAnyObject: AnyObject = SomeClass()

someAnyObject = 123.12          // 컴파일 오류발생, 클래스의 인스턴스가 아니기 때문
```
> 하지만 Any와 AnyObject는 되도록 사용하지 않는 편이 좋다.  
> 타입에 엄격한 스위프트의 특성 상 위와 같은 데이터 타입으로 선언된 변수의 값을 가져다 쓰려면 매번 타입 확인 및 변환을 해줘야 하는 불편함이 존재하며, 예기치 못한 오류의 위험을 증가시킨다.

<span style="background-color:#fff5b1">nil</span>은 특정 타입이 아니라 **없음**을 의미하는 스위프트의 키워드이다.  
즉, 변수 또는 상수에 값이 들어있지 않고 비어있음을 의미하고, 다른 언어에서의 'NULL', 'Null'< 'null' 등과 유사한 표현이다.  
nil을 다루는 방법은 추후 업로드 할 옵셔널 파트에서 다루게 된다.