---
title :  "[Swift] 함수 기본"
date :   2022-01-27 13:48 +0900
categories: [Programming, Swift]
tags: [swift, Xcode]
---

> 본 게시물은 '스위프트 프로그래밍(3판)'을 정리하며 작성하는 게시글입니다.


## 함수와 메서드 
---
함수와 메소드는 기본적으로 동일한 개념을 가진다.  
상황, 위치에 따라 다른 용어로 부르는 것인데 다음과 같이 구분할 수 있다.  
   - 구조체, 클래스, 열거형 등 특정 타입에 연관되어 사용되는 함수를 `메서드`  
   - 모듈 전체에서 전역적으로 사용할 수 있는 함수를 그냥 `함수`


## 함수 정의와 호출
---
스위프트의 함수는 재정의(오버라이드)와 중복 정의(오버로드)를 모두 지원합니다.  
따라서, 매개변수의 타입이 다르면 같은 이름의 함수를 여러개 만들 수 있고,  
매개변수의 개수가 달라도 같은 이름의 함수를 만들 수 있다.  

### 1. 함수 선언의 기본형태
   ```swift
   func 함수이름(매개변수1 이름:매개변수1 타입, 매개변수2 이름:매개변수2 타입, ...) -> 반환타입 {
       /* 실행 구문 */
       return 반환 값
   }


   // 예시 
   func hello(name: String) -> String {
       return "Hello \(name)!"
   }

   func introduce(name: String) -> String {
       // [return "제 이름은 " + name + "입니다"]와 같은 동작을 한다.
       "제 이름은 " + name + "입니다"
   }

   let helloJenny: String = hello(name: Jenny)
   print(helloJenny)        // Hello Jenny!
   print(introduceJenny)    // 제 이름은 Jenny입니다.
   ```

   기본적으로 함수의 이름과 매개변수(Parameter, 파라미터), 반환 타입(Return Type) 등을 사용하여 정의한다.   
   함수를 정의하는 키워드는 `func`이고, 반환타입을 명시하기 전에 `->`를 사용하여 어떤 타입이 반환될 것인지 명시해준다.  

   introduce 함수와 같이 함수 내부의 코드가 단 한줄의 표현이고, 그 표현의 결괏값의 타입이 함수의 반환 타입과 일치한다면 `return` 키워드를 생략해도 그 표현의 결괏값이 함수의 반환값이 될 수 있다.  
     

### 2. 반환 값이 없는 함수
   ```swift
    func 함수이름(매개변수1 이름 : 매개변수1 타입, 매개변수2 이름 : 매개변수2 타입, ...) -> Void {
        /* 실행 구문 */
        return 
    }

    // 예시
    func printMyName(name: String) -> Void {
        print(name)
    }

    // 반환값이 없는 경우 반환 타입(Void) 생략 가능함
    func printYourName(name: String) {
        print(name)
    }
   ```  

       
### 3. 매개변수가 없는 함수
   ```swift
    func helloWorld() -> String {
        return "Hello, World!"
    }

    print(helloWorld())     // Hello, world!
   ```
   함수에 매개변수가 필요 없다면 매개변수 위치를 공란으로 비워둔다.  

### 4. 매개변수와 반환값이 모두 없는 함수

   ```swift
    func 함수이름() -> Void {
        /* 함수 구현부 */
        return 
    }

    func hello() -> Void { print("hello") }


    func 함수이름(){
        return
    }

    func bye(){ print("bye") }
   ```  
   함수 구현이 짧은 경우는 가독성을 해치지 않는다면 줄바꿈을 하지 않고 한 줄에 표현해도 무관하다.  
   반환 값이 없는 경우, 반환 타입(Void)을 생략 가능하다.  
  
  
