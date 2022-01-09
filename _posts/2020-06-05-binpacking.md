---
title :  "[컴퓨터알고리즘 12주차 OJS] 통 채우기(Bin Packing)"
date :   2020-06-05 00:15 +0900
categories: [Computer_algorithm, OJS]
tags: [algorithm, java]
math: true
---


## 통 채우기 문제   
우선, Fit이라는 인터페이스를 통해서 기본 틀을 만들어준 후 First, Next, Best, Worst Fit에서 Fit을 상속받아 메소드 오버라이딩을 통해 코드를 구현하였다.  
Fit은 다음과 같이 정의되었다.  
```java
import java.util.ArrayList;

public interface Fit {
    public void fit(ArrayList<Bin> arr, Item item);
}
```  
  

1. First Fit, 최초 적합  
   첫 번째 통부터 차례로 살펴보며 가장 먼저 여유가 있는 통에 새 물건을 넣는다.  
   결과는 다음과 같이 나온다.  
   ![FirstFit](/assets/img/data/FirstFit.png)  

   ```java
   import java.util.ArrayList;

    public class FirstFit implements Fit {
        @Override
        public void fit(ArrayList<Bin> arr, Item item) {
            for (int i=0; i<arr.size(); i++) {
                Bin bin = arr.get(i);
                if(bin.check(item)) {
                    bin.update(item);
                    return;
                }
            }

            Bin b = new Bin();
            b.update(item);
            arr.add(b);
        }
    }
   ```  
<br/>

2. Next Fit, 다음 적합
   직전에 물건을 넣은 통에 여유가 있으면 새 물건을 넣는다.  
   결과는 다음과 같이 나온다.  
   ![NextFit](/assets/img/data/NextFit.png)   
   ```java
   import java.util.ArrayList;

    public class NextFit implements Fit{
        @Override
        public void fit(ArrayList<Bin> arr, Item item) {
            Bin bin = new Bin();
            if(arr.size() == 0){
                bin.update(item);
                arr.add(bin);
            }
            else {
                bin = arr.get((arr.size())-1);

                if(bin.check(item))
                    bin.update(item);
                else {
                    Bin b = new Bin();
                    b.update(item);
                    arr.add(b);
                }
            }

        }
    }
   ```    
<br/>

3. Best Fit, 최선 적합  
   기존의 통 중에서 새 물건이 들어가면 남는 부분이 가장 적은 통에 새 물건을 넣는다.  
   결과는 다음과 같이 나온다.  
   ![BestFit](/assets/img/data/BestFit.png)  
   ```java
   import java.util.ArrayList;

    public class BestFit implements Fit {
        @Override
        public void fit(ArrayList<Bin> arr, Item item) {
            Bin bin = new Bin();
            
            if(arr.size() == 0){
                bin.update(item);
                arr.add(bin);
                return;
            }
            else {
                int min = 10;
                for (int i = 0; i < arr.size() ; i++) {
                    bin = arr.get(i);
                    if(bin.check(item)) {
                        if (min > bin.remainCapacity - item.weight) min = i;
                    }
                }

                // 다 돌았는데 넣을 곳이 없었다 ? 그러면 통 새로 만들어서 넣어주기
                if(min == 10) {
                    bin = new Bin();
                    bin.update(item);
                    arr.add(bin);
                }
                // min의 값이 바뀌었다면 어딘가에 얘를 최선으로 넣었다는거지
                else {
                    bin = arr.get(min);
                    bin.update(item);
                }
            }
        }
    }
    ```
<br/>

4. Worst Fit, 최악 적합
   기존의 통 중에서 새 물건이 들어가면 남는 부분이 가장 큰 통에 새 물건을 넣는다.  
   결과는 다음과 같이 나온다.  
   ![WorstFit](/assets/img/data/WorstFit.png)
   ```java
   import java.util.ArrayList;

    public class WorstFit implements Fit {
        @Override
        public void fit(ArrayList<Bin> arr, Item item) {
            Bin bin = new Bin();

            if(arr.size() == 0){
                bin.update(item);
                arr.add(bin);
                return;
            }
            else {
                int max = -1;
                for (int i = 0; i < arr.size() ; i++) {
                    bin = arr.get(i);
                    if(bin.check(item)) {
                        if (max < bin.remainCapacity - item.weight) max = i;
                    }
                }

                // 다 돌았는데 넣을 곳이 없었다 ? 그러면 통 새로 만들어서 넣어주기
                if(max == -1) {
                    bin = new Bin();
                    bin.update(item);
                    arr.add(bin);
                }
                // max의 값이 바뀌었다면 최악으로 들어갈 곳을 찾았다는거지
                else {
                    bin = arr.get(max);
                    bin.update(item);
                }
            }
        }
    }
    ```  
