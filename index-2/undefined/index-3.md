## 6. 함수

* 함수는 대부분의 프로그래밍 언어에서 지원하는 기능으로, 하나의 큰 프로그램을 여러 부분으로 나누어주기 때문에 같은 함수를 여러 상황에서 여러 차례 호출할 수 있으며 일부분을 수정하기 쉽다는 장점을 가집니다.  

#### 6-1. 구조 
* 어떤 루틴에서 함수를 호출한다. 이때 함수가 가지는 특정 변수에 값을 전달하기도 하며, 이 특정 변수를 매개변수(parameter), 전달되는 값을 인자(argument)합니다.
* 함수가 호출되어 계산을 수행합니다.
* 함수가 종료되고 실행 흐름이 원래의 루틴으로 돌아옵니다.
*  경우에 따라서는 함수가 계산하여 반환된 값(반환값, return value)을 원래의 루틴에서 사용하기도 합니다. 
#### 6-2. 장점 
* 하나의 큰 프로그램을 여러 부분으로 분리함으로써 구조적 프로그래밍이 가능합니다.
* 같은 코드를 계속 쓰지 않음으로써 프로그램의 용량을 줄일 수 있고, 다른 부분이나 다른 프로그램에서 같은 코드를 사용할 수 있습니다.
* 함수의 기능과 내부 구현을 분리할 수 있습니다.
#### 6-3. 파이썬에서 함수 구현
* 함수 정의 키워드 def()  
```
def 함수명(매개변수);
    함수가 수행할 일
    return 함수가 반환할 객체
```
```
def doubler(a):  # 함수,매개변수 정의
    print( a * 2)
doubler(11)      # 함수 호출
```
* 함수 키워드 return 
* 함수를 호출할 때 결과값을 반환한다.
            
```
def reapple():
    a= 'apple'
    return a
text1 = reapple()

```
* 복수의 매개변수 구성 
```
def calcu1(a,b): #2개의 매개변수
    c = a + b 
    return c
print(calcu1(10,8.7))  #2개의 인수 전달     
```
* 복수의 return값
```
def calcu2(a,b): #2개의 매개변수
    result1 = a + b 
    result2 = a - b 
    result3 = a / b 
    result4 = a * b 
    return result1,result2,result3,result4
print(calcu2(10,8.7))  #2개의 인수 전달  튜플로 반환   
r1,r2,r4,r4 = (calcu2(10,8.7))  #2개의 인수 전달 4개의 변수로 반환  
```
* 튜플로 매개변수 받기 *
```
def t_print(x, y, *rest):        # 인수앞에 * 추가
    print(x, y, rest)
t_print(1,2,3,4,5,6,7,8)
```
* 딕셔너리로 매개변수 받기 **
```
# 방법 1
def d_print(**dic) :
    for key, value in dic.items() :
        print(f"{key} : {value}")

dic1 = {'a' :1, 'b':2, 'c':3}
d_print(**dic1)
```
* 변수의 유효범위
       함수내부에서 생성된 변수는 함수밖에서 사용할 수 없습니다.
       외부에서 사용할 시에는 global을 사용합니다.
```
def a_test():
    obj = 10
obj = 20
a_test()
print('1',obj)

def b_test():
    global obj
    obj = 10
obj = 20
b_test()
print('2',obj)

```
* 객체 고유의 함수 활용
       문자열이나 리스트 등도 스스로 사용할 수 있는 함수가 있습니다.
       이를 메소드(Method)라고 합니다.  
       메소드도 함수이므로 호출하는 방식은 같으나 누가 호출하는지를 명시해야 합니다.
```
t1 = 'aaa'
t2 = 'bbbbb'
print(t1.upper())
print(t2.title())
```
colab으로 실습하기: [https://colab.research.google.com/drive/1hcaetTRU7Yre6mOI3zysmCUtf7hzIiGP?usp=sharing](https://colab.research.google.com/drive/1hcaetTRU7Yre6mOI3zysmCUtf7hzIiGP?usp=sharing)

