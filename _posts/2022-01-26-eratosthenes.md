---
title :  "[Algorithm] 에라토스테네스의 체"
date :   2022-01-26 18:05 +0900
categories: [Study, Algorithm]
tags: [python, algorithm, prime number]
---

# 에라토스테네스의 체 Sieve of Eratosthenes


## 소수
---
1과 자기 자신 이외의 자연수로는 나눌 수 없는 자연수  
  
  

## 소수 판별 알고리즘을 단순하게 생각해보면 
---
아래 코드는 1부터 100 사이의 소수를 판별하는 파이썬 코드이다.  

```python
n = 100

def isPrime(n):
    if n < 2:
        return False
    
    for i in range(2, n):
        if n % i == 0:
            return False
    
    return True

for i in range(n+1):
    if(isPrime(i)):
        print(i)
```

  
## 에라토스테네스의 체 
---
위 코드는 brute force의 방식이라고 볼 수 있다.  
한 개의 소수를 구할 때는 꽤 괜찮은 방법이라고 볼 수 있지만, N부터 M까지 범위의 모든 소수를 구할 때는 효율적인 방법이 아니다.  
그래서 주어진 범위 내에서 소수를 구할 때 사용하는 것이 에라토스테네스의 체이다.  
  
이 방법은 주어진 범위에서 합성수를 지우는 방식으로 소수를 조금 더 빠르게 찾는 방법이다.  
![에라토스테네스의체](/assets/img/algorithm/Sieve_of_Eratosthenes_animation.gif)  
  
위 알고리즘은 다음 과정을 통해 진행된다.  
1. 2부터 소수를 구하고자 하는 구간의 모든 수를 나열한다. 위 그림에서 회색 사각형으로 두른 수들이 여기에 해당한다.
2. 2는 소수이므로 오른쪽에 2를 쓴다.(빨간색)
3. 자기 자신을 제외한 2의 배수를 모두 지운다.
4. 남아있는 수 가운데 3은 소수이므로 오른쪽에 3을 쓴다.(초록색)
5. 자기 자신을 제외한 3의 배수를 모두 지운다.
6. 남아있는 수 가운데 5는 소수이므로 오른쪽에 5를 쓴다.(파란색)
7. 자기 자신을 제외한 5의 배수를 모두 지운다.
8. 위 과정을 반복하면 구하는 구간의 모든 소수가 남는다.
  
위 알고리즘을 파이썬으로 구현하면 다음과 같다.  
```python
def prime_list(n):
    # 에라토스테네스의 체 리스트를 초기화: n개의 요소를 우선 True로 설정한다(소수로 간주)
    sieve = [True] * n

    # n의 최대 약수는 sqrt(n) 이하이므로 i = sqrt(n)까지 for문으로  확인한다.
    for i in range(2, int(n ** 0.5)):
        if sieve[i] == True:                # i가 소수인 경우 
            for j in range(i+i, n, i):      # 자기 자신을 제외한 i의 배수를 모두 False로 설정
                sieve[j] = False

    # sieve에서 True인 값만 list형식으로 리턴
    return [i for i in range(2, n) if sieve[i] == True]
```