---
title :  "[Swift] 데이터 타입 고급"
date :   2022-01-12 21:34 +0900
categories: [Programming, Swift]
tags: [swift, Xcode, Programming]
---

> 본 게시물은 '스위프트 프로그래밍(3판)'의 4장 데이터 타입 고급을 정리하며 작성하는 게시글입니다.  
> 아래 작성된 코드는 [yagom님 swift 기본 문법](https://github.com/yagom/swift_basic.git)의 코드를 참고했습니다.

## 타입 별칭
스위프트에서 기본으로 제공하는 데이터 타입이든, 사용자가 임의로 만든 데이터 타입이든 이미 존재하는 데이터 타입의 임의로 다른 이름(별칭)을 부여할 수 있다. 그런 다음 기본 타입 이름과 이후에 추가한 별칭을 모두 사용할 수 있다. >> C언어 구조체에서의 typedef를 생각하면 될 것 같다.
```swift
typealias MyInt = Int
typealias YourInt = Int
typealias MyDouble = Double

let age: MyInt = 11
var year: YourInt = 2000

// MyInt도, YourInt도 이름은 다르지만 사실 같은 Int이기 때문에 같은 타입으로 취급
year = age

let month: Int = 8                  // 기존의 타입 이름도 사용 가능 
let percentage: MyDouble = 99.9     // Int 외에 다른 자료형도 모두 별칭 사용 가능 
```


## 튜플 Tuple
프로그래머 마음대로 만드는 타입으로 `지정된 데이터의 묶음`이라고 표현할 수 있다.  
C언어에서 원시 구조체의 형태와 가깝고, Python의 튜플과 유사하다.  

튜플은 타입 이름이 따로 존재하지 않는다. 일정 타입의 나열만으로 튜플 타입을 생성해줄 수 있다.
```swift
// String, Int, Double 타입을 갖는 튜플 
var person: (String, Int, Double) = ("gaanii", 23, 166.8)

// 인덱스를 통해 값을 빼 올 수 있다.
print("이름: \(person.0), 나이: \(person.1), 신장: \(person.2))

// 인덱스를 통해 값을 할당할 수도 있다. 
person.1 = 100
person.2 = 180.2
```

  
위 코드에서는 튜플의 각 요소를 이름 대신 숫자로 표현하기 때문에 간편해 보일 수 있지만, 차후 타인이 코드를 볼 때 각 요소가 어떤 의미가 있는지 인지하기 어렵기 때문에 아래 코드와 같이 튜플의 요소마다 이름을 붙여주는것이 좋다.   
```swift
// String, Int, Double 타입을 갖는 튜플 
var person: (name: String, age: Int, height: Double) = ("gaanii", 23, 166.8)

// 요소 이름을 통해 값을 빼 올 수 있다.
print("이름: \(person.name), 나이: \(person.age), 신장: \(person.height)")

// 요소 이름을 통해 값을 할당할 수도 있으며, 인덱스를 통해서도 가능하다.
person.age = 99
person.2 = 180.2
```

또, 튜플에는 타입 이름에 해당하는 키워드가 없어 불편함을 겪을 수 있는데, 이때 타입 별칭을 사용하여 조금 더 깔끔하고 안전하게 코드를 작성할 수 있다. 아래 코드를 참고하자.
```swift
typealias PersonTuple = (name: String, age: Int, height: Double)

let gaanii: PersonTuple = ("gaanii", 23, 166.8)
let mrstone: PersonTuple = ("stone", 26, 167.1)
```


## 컬렉션형
스위프트는 튜플 외에도 많은 수의 데이터를 묶어서 저장하고 관리할 수 있는 컬렉션 타입을 제공한다.   
컬렉션 타입에는 `배열 Array`, `딕셔너리 Dictionary`, `세트 Set` 등이 있다.

`let` 키워드를 사용해 상수로 선언하면 변경 불가능, `var` 키워드를 사용해 변수로 선언하면 변경 가능을 의미한다.

1. 배열 Array  
   같은 타입의 데이터를 일렬로 나열한 후 순서대로 저장하는 형태의 컬렉션 타입이다.  
   각기 다른 위치에 같은 값이 들어갈 수 있다.  
   

   실제로 배열을 사용할 때는   
   - `Array` 키워드와 `타입 이름`의 조합으로 사용
   - 대괄호로 값을 묶어 Array 타입임을 표현 
   - 빈 배열은 이니셜라이저 또는 리터럴 문법을 통해 생성 
    
    ```swift
    // 빈 Int Array 생성
    var integers: Array<Int> = Array<Int>()

    // 같은 표현
    var integers: Array<Int> = [Int]()
    var integers: Array<Int> = []
    var integers: [Int] = Array<Int>()
    var integers: [Int] = [Int]()
    var integers: [Int] = []
    var integers = [Int]()
    ```
    - `isEmpty` 프로퍼티로 비어있는 배열인지 확인 가능하다.
    - `count` 프로퍼티로 배열에 몇 개의 요소가 존재하는지 알 수 있다.
    - 배열의 각 요소에 인덱스를 통해 접근할 수 있으며, 인덱스는 0부터 시작한다.  
    - 잘못된 인덱스로 접근하려고 하면 익셉션 오류 Exception Error가 발생한다.  
    - 맨 처음과 맨 마지막 요소는 `first`와 `last` 프로퍼티를 통해 가져올 수 있다.  
    - `firstIndex(of:)` 메소드를 이용하면 해당 요소의 인덱스를 알아낼 수 있다. 이 메소드의 경우 중복된 요소가 있다면 제일 먼저 발견된 요소의 인덱스를 반환한다.  
    - 맨 뒤에 요소를 추가하고 싶다면 `append(-:)` 메소드를 사용한다.
    - 중간에 요소를 삽입하고 싶다면 `insert(_:at:)` 메소드를 사용한다.
    - 요소를 삭제하고 싶다면 `remove(_:)` 메소드를 사용하고, 메소드를 사용하면 해당 요소가 삭제된 후 반환된다.  



2. 딕셔너리 Dictionary  
   요소들이 순서 없이 키와 값의 쌍으로 구성되는 컬렉션 타입이다.  
   딕셔너리 안에는 키가 하나이거나 여러 개일 수 있지만, 하나의 딕셔너리 안의 키는 같은 이름을 중복해서 사용할 수 없다.  

   딕셔너리는 `Dictionary 키워드`와 `키의 타입`, `값의 타입 이름`의 조합으로 써준다.  
   대괄호로 키와 값의 타입 이름의 쌍을 묶어 딕셔너리 타입임을 표현한다.   
   ```swift
    // Key가 String 타입이고 Value가 Any인 빈 Dictionary 생성
    var anyDictionary: Dictionary<String, Any> = [String: Any]()

    // 같은 표현
    var anyDictionary: Dictionary <String, Any> = Dictionary<String, Any>()
    var anyDictionary: Dictionary <String, Any> = [:]
    var anyDictionary: [String: Any] = Dictionary<String, Any>()
    var anyDictionary: [String: Any] = [String: Any]()
    var anyDictionary: [String: Any] = [:]
    var anyDictionary = [String: Any]()
    ```

      
    딕셔너리는 각 값에 키로 접근할 수 있는데, 딕셔너리 내부에서 키는 유일해야 하며, 값은 유일하지 않다.  
    딕셔너리는 배열과 다르게 딕셔너리 내부에 없는 키로 접근해도 오류가 발생하지 않고, 이 경우 nil을 반환한다.  
    특정 키에 해당하는 값을 제거하려면 `removeValue(forKey:) 메소드를 사용한다.
    ```swift
    // 키에 해당하는 값 할당
    anyDictionary["someKey"] = "value"
    anyDictionary["anotherKey"] = 100

    print(anyDictionary) // ["someKey": "value", "anotherKey": 100]

    // 키에 해당하는 값 변경
    anyDictionary["someKey"] = "dictionary"
    print(anyDictionary) // ["someKey": "dictionary", "anotherKey": 100]

    // 키에 해당하는 값 제거
    anyDictionary.removeValue(forKey: "anotherKey")
    anyDictionary["someKey"] = nil
    print(anyDictionary) // [:]
    ```


3. 세트 Set  
    같은 타입의 데이터를 순서 없이 하나의 묶음으로 저장하는 형태의 컬렉션 타입이다.  
    세트 내의 값은 모두 유일한 값, 즉 중복된 값이 존재하지 않기 때문에, **순서가 중요하지 않거나 각 요소가 유일한 값이어야 하는 경우**에 사용한다.
      
    세트는 `Set 키워드`와 `타입 이름`의 조합으로 써준다.  
    배열과 마찬가지로 대괄호로 값들을 묶어 세트 타입임을 표현하지만, 배열과 달리 축약형(Array<Int>를 [Int]로 축약하는 것과 같은)이 없다.  
    ```swift
    // 빈 Int Set 생성
    var integerSet: Set<Int> = Set<Int>()
    integerSet.insert(1)
    integerSet.insert(100)
    integerSet.insert(99)
    integerSet.insert(99)
    integerSet.insert(99)

    print(integerSet)             // [100, 99, 1]
    print(integerSet.contains(1)) // true
    print(integerSet.contains(2)) // false

    integerSet.remove(100)
    integerSet.removeFirst()

    print(integerSet.count)       // 1
    ```

    세트는 자신 내부의 값들이 모두 유일함을 보장하므로, 집합관계를 표현하고자 할 때 유용하게 쓰일 수 있다.  
    아래 코드는 세트를 활용한 집합 연산을 보여준다.  
    ```swift
    // Set는 집합 연산에 꽤 유용합니다
    let setA: Set<Int> = [1, 2, 3, 4, 5]
    let setB: Set<Int> = [3, 4, 5, 6, 7]

    // 합집합
    let union: Set<Int> = setA.union(setB)
    print(union) // [2, 4, 5, 6, 7, 3, 1]

    // 합집합 오름차순 정렬
    let sortedUnion: [Int] = union.sorted()
    print(sortedUnion) // [1, 2, 3, 4, 5, 6, 7]

    // 교집합
    let intersection: Set<Int> = setA.intersection(setB)
    print(intersection) // [5, 3, 4]

    // 차집합
    let subtracting: Set<Int> = setA.subtracting(setB)
    print(subtracting) // [2, 1]
    ```
