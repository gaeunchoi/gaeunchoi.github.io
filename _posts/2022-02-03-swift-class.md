---
title :  "[Swift] 구조체와 클래스"
date :   2022-02-03 19:22 +0900
categories: [Programming, Swift]
tags: [swift, Xcode, Programming, iOS]
---

> 본 게시물은 '스위프트 프로그래밍(3판)'의 9장 구조체와 클래스를 정리하며 작성하는 게시글입니다.  
> 아래 작성된 코드는 [yagom님 swift 기본 문법](https://github.com/yagom/swift_basic.git)의 코드를 참고했습니다.


## 구조체
---
### 1. 개념  
   하나의 `새로운 사용자 정의 데이터 타입`이라고 말할 수 있다.  

### 2. 정의  
   `struct` 키워드를 사용하여 정의할 수 있다.  
   ```swift
   struct 구조체이름 {
       /* 프로퍼티와 메서드들 */
   }

   // 구조체 예시 
   struct Student {
       var name: String
       var `class`: String     // 키워드도 `로 묶어주면 사용 가능 
   }
   ```

### 3. 구조체 인스턴스 생성 및 초기화
   구조체 정의 후에, 인스턴스를 생성하고 초기화하고자 할 때는 기본적으로 생성되는 멤버와이즈 이니셜라이저를 사용한다.  

   인스턴스가 생성되고 초기화된 후 프로퍼티 값에 접근하고 싶다면 `마침표(.)`를 사용하면 된다.  

   구조체를 `상수 let`으로 선언하면 인스턴스 내부 프로퍼티 값은 변경 불가능하고,  
   `변수 var`로 선언하면 값을 변경할 수 있다.
   ```swift
   // 프로퍼티 이름(name, age)으로 자동 생성된 이니셜라이저를 사용하여 구조체 생성 
   var gaaniiInfo: Student = Student(name: "gaanii", class: "swift")
   gaaniiInfo.class = "ML/DL"
   gaaniiInfo.name = "galamgwi"
   ```


## 클래스 
---
### 1. 개념
개념은 구조체와 동일하다.  다른 부분은 아래에서 설명 !  

### 2. 정의
`class` 키워드를 사용하여 정의할 수 있다.  

클래스 정의 방법은 구조체와 매우 흡사하지만, 여기엔 가장 크게 다르다고 볼 수 있는 `상속`이 존재한다.

클래스는 상속받을 수 있기 때문에 상속받을 때는 클래스 이름 뒤에 `콜론(:)`을 써주고 부모클래스 이름을 명시한다.(상속은 추후에 다룬다.)  

```swift
class 클래스 이름 {
    /* 프로퍼티와 메서드들 */
}

class 클래스 이름: 부모클래스 이름 {
    /* 프로퍼티와 메서드들 */
}

// 클래스 예시
class Student {
    var name: String
    var `class`: String = "Swift"
}
```

### 3. 클래스 인스턴스의 생성 및 초기화
