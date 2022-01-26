---
title :  "[컴퓨터알고리즘 3주차 과제] Strassen Algorithm 알아보기"
date :   2020-04-07 12:30 +0900
categories: [INU, Computer algorithm]
tags: [algorithm, java]
math: true
---

컴퓨터알고리즘 개인 과제인 Strassens Algorithm 조사내용입니다.

Markdown에서의 수식작성은 [위키백과:Tex 문법](https://ko.wikipedia.org/wiki/%EC%9C%84%ED%82%A4%EB%B0%B1%EA%B3%BC:TeX_%EB%AC%B8%EB%B2%95#%EC%9C%84,_%EC%95%84%EB%9E%98,_%EC%A0%84%EC%B9%98,%ED%9B%84%EC%B9%98_%EC%B2%A8%EC%9E%90) 참고  


## Strassen Algorithm (슈트라센 알고리즘)

선형대수학에서 슈트라센 알고리즘은 독일의 수학자 폴커 슈트라센(Volker Strassen)이 1969년에 개발한 행렬 곱셈 알고리즘이다.  
정의에 따라 n×n 크기의 두 행렬을 곱하면 O($n^3$)의 시간이 소요되지만 이 알고리즘은 대략 O($n^{2.807}$)의 시간이 소요된다.

### 알고리즘 설명  

$A$와 $B$를 체 $F$에 대한 정사각행렬이라고 하자.   두 행렬의 곱 C는 다음과 같다.  

$$C=AB \qquad\qquad A, B, C \in F^{2^n \times 2^n}$$
   
만약 $A$와 $B$가 $2^n \times 2^n$ 꼴의 크기가 아니라면 먼저 모자라는 행과 열을 0으로 채운다. 이 경우 행렬 곱셈이 끝난 뒤 행렬에서 필요한 부분만 다시 잘라 내야 한다.
   
이제 A, B, C를 같은 크기의 정사각행렬 네 개로 나눈다.

$$ A=\begin{bmatrix}
        A_{1,1} & A_{1,2}\\
        A_{2,1} & A_{2,2}
        \end{bmatrix}, 
    B = \begin{bmatrix}
        B_{1,1} & B_{1,2}\\
        B_{2,1} & B_{2,2}
        \end{bmatrix}, 
    C = \begin{bmatrix}
        C_{1,1} & C_{1,2}\\
        C_{2,1} & C_{2,2}
        \end{bmatrix}
$$

이때,  

$$ A_{i, j}, B_{i, j}, C_{i, j} \in F^{2^{n-1} \times 2^{n-1}}$$  


따라서 다음이 성립한다.

$$C_{1,1} = A_{1,1}B_{1,1} + A_{1,2}B_{2,1}$$
  
$$C_{1,2} = A_{1,1}B_{1,2} + A_{1,2}B_{2,2}$$
  
$$C_{2,1} = A_{2,1}B_{1,1} + A_{2,2}B_{2,1}$$
  
$$C_{2,2} = A_{2,1}B_{1,2} + A_{2,2}B_{2,2}$$

이 과정에서는 필요한 연산의 수가 줄어 들지 않는다. 여전히 $C_{i,j}$행렬을 계산하려면 여덟 번의 곱셈과 네 번의 덧셈이 필요하다.

이제 다음과 같은 행렬을 정의한다.

$$M_1 := (A_{1,1} + A_{2,2})(B_{1,1} + B_{2,2})$$  

$$M_2 := (A_{2,1} + A_{2,2})B_{1,1}$$
  
$$M_3 := A_{1,1}(B_{1,2} - B_{2,2})$$
  
$$M_4 := A_{2,2}(B_{2,1} - B_{1,1})$$
  
$$M_5 := (A_{1,1} + A_{1,2})B_{2,2}$$
  
$$M_6 := (A_{2,1} - A_{1,1})(B_{1,1} + B_{1,2})$$
  
$$M_7 := (A_{1,2} - A_{2,2})(B_{2,1} + B_{2,2})$$

이 $M_k$ 행렬들은 $C_{i,j}$ 행렬을 표현하는 데 쓰이는데, 이 행렬들을 계산하는 데는 일곱 번의 곱셈(각 변수마다 한 번씩)과 10번의 덧셈이 필요하다. 이제 $C_{i,j}$ 행렬은 다음과 같이 표현할 수 있다.

$$C_{1,1} = M_1 + M_4 - M_5 + M_7$$  

$$C_{1,2} = M_3 + M_5$$
  
$$C_{2,1} = M_2 + M_4$$
  
$$C_{2,2} = M_1 - M_2 + M_3 + M_6$$


이 과정에서는 곱셈이 사용되지 않기 때문에, 전체 곱셈을 일곱 번의 곱셈과 18번의 덧셈으로 처리할 수 있다. 큰 행렬에 대해서는 행렬의 곱셈이 덧셈보다 더 많은 시간을 필요로 하기 때문에 덧셈을 더 하는 대신 곱셈을 덜 하는 것이 전체적으로 더 효율적이다.

이 과정을 재귀적으로 반복할 경우 총 $7 \cdot n^{\log_{2}7} - 6 \cdot n^2$ 번의 연산이 필요하다. $\log_{2} 7$ = $2.807 \cdots$ 이므로 전체 수행 시간은 약 O($n^{2.807}$)이다.

실제로 n이 작을 경우 정의에 따라 행렬 곱셈을 하는 경우가 빠를 수도 있기 때문에, 보통 작은 n에 대해서는 일반적인 방법으로 곱셈을 하도록 구현한다.

슈트라센 알고리즘은 속도에 비해 수치 안정성이 떨어지는 것으로 알려져 있다. 두 행렬 $A$와 $B$를 곱한 결과를 $C$라 할 때, 실제 오차인 $\lVert C - AB \rVert$는 $27n^2u\lVert A \rVert \lVert B \rVert + O(u^2)$ 보다 작음이 알려져 있다. 이는 일반적인 행렬 곱셈보다 더 큰 오차이다. 

아래 코드는 Google에 `Strassen Algorithm java`를 검색하면 나오는 소스코드이다. 혼자 짜보려다 실패해서 아래 코드를 따라쳐 이해하며 만들었다 ... 길어보이긴 하지만 생각보다 어렵진않다.
```java
import java.util.Scanner;
 
/** Class Strassen **/
public class Strassen
{
    /** Function to multiply matrices **/
    public int[][] multiply(int[][] A, int[][] B)
    {        
        int n = A.length;
        int[][] R = new int[n][n];
        /** base case **/
        if (n == 1)
            R[0][0] = A[0][0] * B[0][0];
        else
        {
            int[][] A11 = new int[n/2][n/2];
            int[][] A12 = new int[n/2][n/2];
            int[][] A21 = new int[n/2][n/2];
            int[][] A22 = new int[n/2][n/2];
            int[][] B11 = new int[n/2][n/2];
            int[][] B12 = new int[n/2][n/2];
            int[][] B21 = new int[n/2][n/2];
            int[][] B22 = new int[n/2][n/2];
 
            /** Dividing matrix A into 4 halves **/
            split(A, A11, 0 , 0);
            split(A, A12, 0 , n/2);
            split(A, A21, n/2, 0);
            split(A, A22, n/2, n/2);
            /** Dividing matrix B into 4 halves **/
            split(B, B11, 0 , 0);
            split(B, B12, 0 , n/2);
            split(B, B21, n/2, 0);
            split(B, B22, n/2, n/2);
 
            /** 
              M1 = (A11 + A22)(B11 + B22)
              M2 = (A21 + A22) B11
              M3 = A11 (B12 - B22)
              M4 = A22 (B21 - B11)
              M5 = (A11 + A12) B22
              M6 = (A21 - A11) (B11 + B12)
              M7 = (A12 - A22) (B21 + B22)
            **/
 
            int [][] M1 = multiply(add(A11, A22), add(B11, B22));
            int [][] M2 = multiply(add(A21, A22), B11);
            int [][] M3 = multiply(A11, sub(B12, B22));
            int [][] M4 = multiply(A22, sub(B21, B11));
            int [][] M5 = multiply(add(A11, A12), B22);
            int [][] M6 = multiply(sub(A21, A11), add(B11, B12));
            int [][] M7 = multiply(sub(A12, A22), add(B21, B22));
 
            /**
              C11 = M1 + M4 - M5 + M7
              C12 = M3 + M5
              C21 = M2 + M4
              C22 = M1 - M2 + M3 + M6
            **/
            int [][] C11 = add(sub(add(M1, M4), M5), M7);
            int [][] C12 = add(M3, M5);
            int [][] C21 = add(M2, M4);
            int [][] C22 = add(sub(add(M1, M3), M2), M6);
 
            /** join 4 halves into one result matrix **/
            join(C11, R, 0 , 0);
            join(C12, R, 0 , n/2);
            join(C21, R, n/2, 0);
            join(C22, R, n/2, n/2);
        }
        /** return result **/    
        return R;
    }
    /** Funtion to sub two matrices **/
    public int[][] sub(int[][] A, int[][] B)
    {
        int n = A.length;
        int[][] C = new int[n][n];
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                C[i][j] = A[i][j] - B[i][j];
        return C;
    }
    /** Funtion to add two matrices **/
    public int[][] add(int[][] A, int[][] B)
    {
        int n = A.length;
        int[][] C = new int[n][n];
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                C[i][j] = A[i][j] + B[i][j];
        return C;
    }
    /** Funtion to split parent matrix into child matrices **/
    public void split(int[][] P, int[][] C, int iB, int jB) 
    {
        for(int i1 = 0, i2 = iB; i1 < C.length; i1++, i2++)
            for(int j1 = 0, j2 = jB; j1 < C.length; j1++, j2++)
                C[i1][j1] = P[i2][j2];
    }
    /** Funtion to join child matrices intp parent matrix **/
    public void join(int[][] C, int[][] P, int iB, int jB) 
    {
        for(int i1 = 0, i2 = iB; i1 < C.length; i1++, i2++)
            for(int j1 = 0, j2 = jB; j1 < C.length; j1++, j2++)
                P[i2][j2] = C[i1][j1];
    }    
    /** Main function **/
    public static void main (String[] args) 
    {
        Scanner scan = new Scanner(System.in);
        System.out.println("Strassen Multiplication Algorithm Test\n");
        /** Make an object of Strassen class **/
        Strassen s = new Strassen();
 
        System.out.println("Enter order n :");
        int N = scan.nextInt();
        /** Accept two 2d matrices **/
        System.out.println("Enter N order matrix 1\n");
        int[][] A = new int[N][N];
        for (int i = 0; i < N; i++)
            for (int j = 0; j < N; j++)
                A[i][j] = scan.nextInt();
 
        System.out.println("Enter N order matrix 2\n");
        int[][] B = new int[N][N];
        for (int i = 0; i < N; i++)
            for (int j = 0; j < N; j++)
                B[i][j] = scan.nextInt();
 
        int[][] C = s.multiply(A, B);
 
        System.out.println("\nProduct of matrices A and  B : ");
        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < N; j++)
                System.out.print(C[i][j] +" ");
            System.out.println();
        }
 
    }
}
```

```console
Enter order n :
4

Enter N order matrix 1
2 3 1 6
4 0 0 2
4 2 0 1
0 3 5 2

Enter N order matrix 2 
3 0 4 3
1 2 0 2
0 3 1 4
5 1 3 2
 
Product of matrices A and  B :
39 15 27 28
22 2 22 16
19 5 19 18
13 23 11 30
```
