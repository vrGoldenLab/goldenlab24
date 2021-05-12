# FOR문 

## 1. 다양한 for문의 사용
```
a = [(1,2), (3,4), (5,6)]
for (first, last) in a:
     print(first + last)
```
a 리스트의 요솟값이 튜플이기 때문에 각각의 요소가 자동으로 (first, last) 변수에 대입됩니다.

## 2. for문의 응용  
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

## 3. for문과 continue  
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
## 4. for문과 함께 자주 사용하는 range 함수
for문은 숫자 리스트를 자동으로 만들어 주는 range 함수와 함께 사용하는 경우가 많습니다.
시작 숫자와 끝 숫자를 지정하려면 range(시작 숫자, 끝 숫자) 형태를 사용하는데, 이때 끝 숫자는 포함되지 않습니다.  
```
sum1 = 0 
for i in range(1, 11): 
     sum1 = sum1 + i 
 
print(sum1)
```
## 5. for와 range를 이용한 구구단
for와 range 함수를 사용하면 소스 코드 단 4줄만으로 구구단을 출력할 수 있습니다. 
```
for i in range(2,10):        # for문1
    for j in range(1, 10):   # for문2
         print(i*j, end=" ") 
    print('') 
```
## 6. 리스트 컴프리헨션


`파이썬에서는 컴프리헨션이라는 문법을 지원합니다.`  

`컴프리헨션은 패턴이 있는 list, dictionary, set을 보다 간단하게 작성할 수 있도록 지원합니다.` 

리스트 컴프리헨션은 for문에서 반복되는 변수를 콜론(:)다음에 줄을 바꿔 들여쓰기하는것이 아니라, for문앞에 작성합니다.  
컴프리헨션에서 사용한 x는 for문 내부에서 append메소드에 인자로 넣은 변수 n과 같습니다.

* 기존 1부터 10까지 정수를 순서대로 가지고 있는 리스트를 생성하는코드
   
```
numbers = []
for n in range(1, 10+1):
    numbers.append(n)
```
* 리스트 컴프리헨션으로 1부터 10까지 정수를 순서대로 가지고 있는 리스트를 생성하는코드
```
[x for x in range(10)]
```
* 2의 배수를 10개 가지고 있는 리스트를 컴프리헨션
     ```
     [ 2*x for x in range(1, 10+1) ]
    ```
## 7. 조건 걸기
만약 1부터 10까지 숫자중 짝수만 순차적으로 들어있는 리스트를 생성하는 코드는 다음과 같습니다.
```
even_numbers = []
for n in range(1, 10+1):
    if n % 2 == 0:
        even_numbers.append(n)
```
## 7. 리스트 컴프리헨션에도 조건을 설정
컴프리헨션은 if 키워드를 지원합니다. 이때 if키워드는 for문 다음에 위치해야 합니다. 짝수를 담는 리스트 컴프리헨션은 다음과 같이 작성할 수 있습니다. 
`[x for x in range(1, 10+1) if x % 2 == 0]`
## 8. 중복 표현
컴프리헨션은 내부에서 for 키워드와 if키워드를 몇번이고 반복할 수 있습니다.
#### for
저녁으로 먹을 메뉴 쌈밥, 치킨, 피자 중 하나와 후식으로 먹을 사과, 아이스크림, 커피 를 정할때 가능한 경우에 수를 뽑는 코드를 컴프리헨션으로 표현하면 다음과 같이 작성할 수 있습니다.
```
[ (x, y) for x in ['쌈밥', '치킨', '피자'] for y in ['사과', '아이스크림', '커피']]
```
출력 결과 
```
[('쌈밥', '사과'),
 ('쌈밥', '아이스크림'),
 ('쌈밥', '커피'),
 ('치킨', '사과'),
 ('치킨', '아이스크림'),
 ('치킨', '커피'),
 ('피자', '사과'),
 ('피자', '아이스크림'),
 ('피자', '커피')]
```
2가지 선택지도 추가
```
[ (x, z, y) for x in ['쌈밥', '치킨', '피자'] for y in ['사과', '아이스크림', '커피'] for z in ['배달 시키기', '가서 먹기']]
```

for문 변경
```
for x in ['쌈밥', '치킨', '피자']:
    for y in ['사과', '아이스크림', '커피']:
        for z in ['배달 시키기', '가서 먹기']:
            print(x, z, y)
``` 
#### IF문 중복
if문 또한 중복해서 작성해서 여러 조건을 걸 수 있습니다.
```
[ x for x in range(10) if x < 5 if x % 2 == 0 ]
```  
## 8. 컴프리헨션
리스트 컴프리헨션은 다른 자료구조로도 확장이 되었습니다.  
리스트를 만들때 사용했던 컴프리헨션문법을 중괄호를({}) 이용해서 한다면 set comprehension이 됩니다.  
`[ x+y for x in range(10) for y in range(10) ]`  
`{ x+y for x in range(10) for y in range(10) }`  
중괄호를 이용하면서, 동시에 key: value 의 형태로 내용을 채운다면 dictionary comprehension이 되어, dict를 만들 수 있습니다.  
```
students = ['철수', '영희', '길동', '순희']
 { student: 0 for student in students }
```
dict comprehension을 이용해서 기존에 dict데이터를 새롭게 변경할수도 있습니다.  
```
scores = {'철수': 50, '영희': 80, '길동': 90, '순희': 60, '전학생': 100}
scores = { name: score for name, score in scores.items() if name != '전학생'}
print(scores)
```

# while 조건반복
조건이 참인 동안 계속 반복합니다.
while 문 내부에서 조건이 변경 하여 반복을 종료합니다.
```
a = 0
while a < 5:
    a += 1
    print('while 반복 수',a)
```
## 1. 여러 가지 선택지 중 하나를 선택해서 입력
```
prompt = """
1. Add
2. Del
3. List
4. Quit
Enter number: """

number = 0
while number != 4:
    print(prompt)
    number = int(input())
```
## 2. while문 강제로 빠져나가기
while문은 조건문이 참인 동안 계속해서 while문 안의 내용을 반복적으로 수행한다. 하지만 강제로 while문을 빠져나가고 싶을 때가 있다.  
while 반복을 강제로 멈추게 하는 것이 바로 break문이다.
```
coffee = 10
money = 300
while money:
     print("돈을 받았으니 커피를 줍니다.")
     coffee = coffee -1
     print("남은 커피의 양은 %d개입니다." % coffee)
     if coffee == 0:
         print("커피가 다 떨어졌습니다. 판매를 중지합니다.")
         break
```
예제를 완성해 보세요
```
coffee = 10
while True:
    money = int(input("돈을 넣어 주세요: "))
```
## 3. while문의 맨 처음으로 돌아가기
while문 안의 문장을 수행할 때 입력 조건을 검사해서 조건에 맞지 않으면 while문을 빠져 나갑니다. 그런데 프로그래밍을 하다 보면 while문을 빠져나가지 않고 while문의 맨 처음(조건문)으로 다시 돌아가게 만들고 싶은 경우 사용하는 것이 바로 continue문입니다.

1부터 10까지의 숫자 중에서 홀수만 출력하는 것을 while문을 사용해서 작성
```
a = 0
while a < 10:
     a = a + 1
     if a % 2 == 0: continue
     print(a)
```
## 4. 무한 루프
```
while True:
     print("Ctrl+ M + I 를 눌러야 while문을 빠져나갈 수 있습니다.")
```

> **colab 코딩연습:** 
> [https://colab.research.google.com/drive/1-mcLjFHDGz3gDW32XJ-T2XZSuZgcQQZc?usp=sharing](https://colab.research.google.com/drive/1-mcLjFHDGz3gDW32XJ-T2XZSuZgcQQZc?usp=sharing) 
>  [https://colab.research.google.com/drive/14LOQjVMWef_WV4jx3HAfaDpDFG5TuLxf?usp=sharing](https://colab.research.google.com/drive/14LOQjVMWef_WV4jx3HAfaDpDFG5TuLxf?usp=sharing) 

