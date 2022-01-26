---
title :  "[컴퓨터알고리즘 4주차 과제] Swing을 이용한 자판기 팀프로젝트"
date :   2020-04-15 18:30 +0900
categories: [INU, Computer algorithm]
tags: [algorithm, java]
---

## Vending Machine 제작

1. Swing을 이용한 GUI 제작
   - JFrame, JLabel, JButton, ImageIcon, JTextfield, JOptionPane 등을 사용하여 사용자 인터페이스 구현
   
   ![사용자 인터페이스 구현](/assets/img/data/GUI.png)

2. Event 구현  
   1. -/+ 버튼 클릭  
    - JTextfield인 total_out에 총액 더하고 빼준거 set해주기  
    - 수량이 0일때 - 버튼 클릭 시 setEnabled false 설정
     
    2. 계산 버튼 클릭
    - 입력한 금액이 총액보다 작을때 잔액부족 팝업 
    - 위 조건만 아니면 그리디 알고리즘으로 잔돈 반환
  
3. 추가 수정사항 
   1. [수정] 수량을 -/+ 버튼만으로 조절하는게 아니라 입력할 수 있게 해볼까 ..
   2. [수정] ~~처음 시작할때 -버튼 setEnabled false 설정해주기~~
