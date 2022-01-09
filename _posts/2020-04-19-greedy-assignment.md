---
title :  "[컴퓨터알고리즘 5주차 OJS] 탐욕 알고리즘(Greedy) - Programmers 문제"
date :   2020-04-19 01:30 +0900
categories: [Computer_algorithm, OJS]
tags: [algorithm, java]
---


## 탐욕 알고리즘 Greedy Algorithm  

### Programmers 코딩테스트 연습 탐욕법 문제 - 단속카메라 
    
**문제 설명**  
고속도로를 이동하는 모든 차량이 고속도로를 이용하면서 단속용 카메라를 한 번은 만나도록 카메라를 설치하려고 합니다. 고속도로를 이동하는 차량의 경로 routes가 매개변수로 주어질 때, 모든 차량이 한 번은 단속용 카메라를 만나도록 하려면 최소 몇 대의 카메라를 설치해야 하는지를 return 하도록 solution 함수를 완성하세요.  

**제한사항**
- 차량의 대수는 1대 이상 10,000대 이하입니다.
- routes에는 차량의 이동 경로가 포함되어 있으며 routes[i][0]에는 i번째 차량이 고속도로에 진입한 지점, routes[i][1]에는 i번째 차량이 고속도로에서 나간 지점이 적혀 있습니다.
- 차량의 진입/진출 지점에 카메라가 설치되어 있어도 카메라를 만난것으로 간주합니다.
- 차량의 진입 지점, 진출 지점은 -30,000 이상 30,000 이하입니다.  
  
**입출력 예시**  
```console
Input :-20,15, -14,-5, -18,-13, -5,-3  
Output: 2
```  

**입출력 예시 설명**  
-5 지점에 카메라를 설치하면 첫 번째, 두 번째, 네 번째 차량이 카메라를 만납니다.  
-15 지점에 카메라를 설치하면 첫 번째, 세 번째 차량이 카메라를 만납니다.

**풀이**  
![풀이과정](/assets/img/greedy_solution_2.jpg)  

```java
import java.util.*;

public class greedy {
    public int solution(int[][] routes) {
        int cnt = 0, position = -30001;

        // 람다식 사용
        Arrays.sort(routes, (a, b) -> Integer.compare(a[1], b[1]));

        // route[0]은 진입지점, route[1]은 진출지점
        for (int[] route : routes) {
            if (position < route[0]) {
                position = route[1];
                cnt++;
            }
        }
    return cnt;
    }
}
```  

  
   
