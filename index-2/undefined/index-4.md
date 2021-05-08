# 반복문 while  

## 1. while 명령어 뒤에 오는 조건이 참일 동안 반복

while 반복문은 조건식으로만 동작하고 반복 수행문에 조건에 영향을 주는 변화식이 들어갑니다.  
for는 반복할 횟수가 정해졌을때 while은 반복할 횟수가 정해지지 않았을 때 사용합니다.  
중첩 반복은 테이블 형태의 데이터를 다룰 때 사용합니다.  
```
x = 0                   #변수 x에 초기값 0을 넣습니다
while x < 15:           #while 조건식 - 변수x가 15보다 작을 경우 반복 
  print('Hello world', x)  #반복처리 코드
  x += 1                #조건 변화 처리 - 반복시 x를 1씩 증가합니다
```
## 2. break, continue로 반복문 제어  

break는 for와 while의 반복을 중단합니다.  
continue는 반복을 유지한 상태에서 코드 실행만 건너뛰는 역할을 합니다.    
```
x = 0          #초기값
while True:    #무한루프
  print (x)   
  x += 1       #변수x를 1씩 증가
  if x == 10:  #변수 x가 10일 때
    break      #반복문을 끝내고 while 문을 벗어남
```
## <실습link>  

#### colab으로 실습하기: [https://colab.research.google.com/drive/1hcaetTRU7Yre6mOI3zysmCUtf7hzIiGP?usp=sharing](https://colab.research.google.com/drive/1hcaetTRU7Yre6mOI3zysmCUtf7hzIiGP?usp=sharing)

