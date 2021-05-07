# 조건문

특정 조건일 때 코드를 실행하는 문법합니다.
다양한 상황에 대처할 때 사용합니다.
```
if 조건:   
        작업1     
else:      
        작업2     
```
```
a = 5
b = 4
if a % b == 0:
   print(f'{a}는 {b}로 나누어 떨어집니다')
else:
    print(f'{a}는 {b}로 나머지가 {a % b} 입니다')
```
## 조건 처리
* and, or, not  
조건을 판단하기 위해 사용하는 다른 연산자로는 and, or, not이 있습니다.  
각각의 연산자는 다음처럼 동작합니다.

* 연산자   
x or y :x와 y 둘중에 하나만 참이어도 참
x and y :x와 y 모두 참이어야 참
not x :x가 거짓이면 참

* x in s, x not in s  
in,not in 뒤의 리스트나 튜플, 문자열 중에 포함 여부를 참,거짓으로 반환

* pass
조건문의 참, 거짓에 따라 실행할 행동을 정의할 때, 아무런 일도 하지 않도록 설정

## elif 
조건이 여러개 일때 if 다음에 오능 조건처리시에 사용합니다. 단독으로 사용하지는 못하고 if문과 같이 사용할 수 있습니다.
```
If <조건문>:
  <작업1> 
  <작업2>
  ...
elif <조건문>:
  <작업1>
  <작업2>
  ...
elif <조건문>:
  <작업1>
  <작업2>
  ...
...
else:
  <작업1>
  <작업2>
 ... 
 ```
 ### 사용 예시
 ```
 x = 30
 
if x == 10:             # x가 10일 때
    print('10입니다.')
elif x == 20:           # x가 20일 때
    print('20입니다.')
else:                   # 앞의 조건식에 모두 만족하지 않을 때
    print('10도 20도 아닙니다.')
```    
> **colab 코딩연습:** [https://colab.research.google.com/drive/1-mcLjFHDGz3gDW32XJ-T2XZSuZgcQQZc?usp=sharing](https://colab.research.google.com/drive/1-mcLjFHDGz3gDW32XJ-T2XZSuZgcQQZc?usp=sharing) 
 
