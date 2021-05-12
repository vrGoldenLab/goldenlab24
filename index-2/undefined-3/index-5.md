# 반복문

## * 다양한 for문의 사용
```
a = [(1,2), (3,4), (5,6)]
for (first, last) in a:
     print(first + last)
```
a 리스트의 요솟값이 튜플이기 때문에 각각의 요소가 자동으로 (first, last) 변수에 대입됩니다.

## * for문의 응용  
`"총 5명의 학생이 시험을 보았는데 시험 점수가 60점이 넘으면 합격이고 그렇지 않으면 불합격이다. 합격인지 불합격인지 결과를 보여 주시오."`
```
marks = [90, 25, 67, 45, 80]
number = 0 
for i in marks: 
    number = number +1 
    if i >= 60: 
        print("%d번 학생은 합격입니다." % number)
    else: 
        print("%d번 학생은 불합격입니다." % number)
```
학생에게 번호를 붙여 주기 위해 number 변수
점수 리스트 marks에서 차례로 점수를 꺼내어 i 라는 변수에 대입
for문이 한 번씩 수행될 때마다 number는 1씩 증가  

## * for문과 continue
while문에서 살펴본 continue문을 for문에서도 사용할 수 있습니다.  
for문 안의 문장을 수행하는 도중에 continue문을 만나면 for문의 처음으로 돌아가게 됩니다.
```
marks = [90, 25, 67, 45, 80]

number = 0 
for i in marks: 
    number = number +1 
    if i < 60:
        continue 
    print("%d번 학생 축하합니다. 합격입니다. " % number)  
```  
## * for문과 함께 자주 사용하는 range 함수
for문은 숫자 리스트를 자동으로 만들어 주는 range 함수와 함께 사용하는 경우가 많습니다.
시작 숫자와 끝 숫자를 지정하려면 range(시작 숫자, 끝 숫자) 형태를 사용하는데, 이때 끝 숫자는 포함되지 않습니다.  
```
sum1 = 0 
for i in range(1, 11): 
     sum1 = sum1 + i 
 
print(sum1)
```
## * for와 range를 이용한 구구단
for와 range 함수를 사용하면 소스 코드 단 4줄만으로 구구단을 출력할 수 있습니다. 
```
for i in range(2,10):        # for문1
    for j in range(1, 10):   # for문2
         print(i*j, end=" ") 
    print('') 

## * 리스트 컴프리헨션
리스트 컴프리헨션은 for문에서 반복되는 변수를 콜론(:)다음에 줄을 바꿔 들여쓰기하는것이 아니라, for문앞에 작성합니다.  
컴프리헨션에서 사용한 x는 for문 내부에서 append메소드에 인자로 넣은 변수 n과 같습니다.    

1부터 10까지 정수를 순서대로 가지고 있는 리스트를 생성하는코드
    * 기존
```
numbers = []
for n in range(1, 10+1):
    numbers.append(n)
```
    * 리스트 컴프리헨션
```
[x for x in range(10)]
```
    * 2의 배수를 10개 가지고 있는 리스트를 컴프리헨션
     ```
     [ 2*x for x in range(1, 10+1) ]
    ```

## while 조건반복
조건이 참인 동안 계속 반복합니다.
while 문 내부에서 조건이 변경 하여 반복을 종료합니다.
```
a = 0
while a < 5:
    a += 1
    print('while 반복 수',a)
```


> **colab 코딩연습:** [https://colab.research.google.com/drive/1-mcLjFHDGz3gDW32XJ-T2XZSuZgcQQZc?usp=sharing](https://colab.research.google.com/drive/1-mcLjFHDGz3gDW32XJ-T2XZSuZgcQQZc?usp=sharing) 
