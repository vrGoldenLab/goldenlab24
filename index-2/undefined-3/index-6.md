# 함수 
함수는 대부분의 프로그래밍 언어에서 지원하는 기능으로, 하나의 큰 프로그램을 여러 부분으로 나누어주기 때문에 같은 함수를 여러 상황에서 여러 차례 호출할 수 있으며 일부분을 수정하기 쉽다는 장점을 가집니다.

## 구조
어떤 루틴에서 함수를 호출한다. 이때 함수가 가지는 특정 변수에 값을 전달하기도 하며, 이 특정 변수를 매개변수(parameter), 전달되는 값을 인자(argument)합니다.
함수가 호출되어 계산을 수행합니다.
함수가 종료되고 실행 흐름이 원래의 루틴으로 돌아옵니다.
경우에 따라서는 함수가 계산하여 반환된 값(반환값, return value)을 원래의 루틴에서 사용하기도 합니다.

## 장점 
* 하나의 큰 프로그램을 여러 부분으로 분리함으로써 구조적 프로그래밍이 가능합니다.
* 같은 코드를 계속 쓰지 않음으로써 프로그램의 용량을 줄일 수 있고, 다른 부분이나 다른 프로그램에서 같은 코드를 사용할 수 있습니다.
* 함수의 기능과 내부 구현을 분리할 수 있습니다.

## 1. 파이썬에서 함수 구현
1.함수 정의 키워드 def()
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
2.함수 키워드 return  
함수를 호출할 때 결과값을 반환합니다.
```
def reapple():
       a= 'apple'
       return a
text1 = reapple()
```
3.복수의 매개변수 구성  
```
def calcu1(a,b): #2개의 매개변수
       c = a + b 
       return c
print(calcu1(10,8.7))  #2개의 인수 전달 
```
4.복수의 return 값 사용 가능
```
def calcu2(a,b): #2개의 매개변수
       result1 = a + b 
       result2 = a - b 
       result3 = a / b 
       result4 = a * b 
       return result1,result2,result3,result4
print(calcu2(10,8.7))  #2개의 인수 전달     
```
2개의 인수, 4개의 return값 사용 예 
```
def calcu3(a,b): #2개의 매개변수

       result1 = a + b 
       result2 = flat(a - b)
       result3 = a / b 
       result4 = a * b 
       return result1,result2,result3,result4
r1,r2,r4,r4 = (calcu2(10,8.7))  #2개의 인수 전달 4개의 변수로 반환   
```
5.튜플,딕셔너리로 매개변수 받기
```
def t_print(x, y, *rest):        # 인수앞에 * 추가
    print(x, y, rest)
t_print(1,2,3,4,5,6,7,8)
```
```
def d_print(**dic) :
    for key, value in dic.items() :
        print(f"{key} : {value}")

dic1 = {'a' :1, 'b':2, 'c':3}
d_print(**dic1)
``` 
7.변수의 유효범위
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
8.객체 고유의 함수 활용
 문자열이나 리스트 등도 스스로 사용할 수 있는 함수가 있습니다.
 이를 메소드(Method)라고 합니다.  
 메소드도 함수이므로 호출하는 방식은 같으나 누가 호출하는지를 명시해야 합니다.
 ```
 t1 = 'aaa'
t2 = 'bbbbb'
print(t1.upper())
print(t2.title())
```
9. 언패킹 사용하기
인수를 순서대로 넣을 때는 리스트나 튜플을 사용할 수 있습니다.  
`*(애스터리스크)`를 붙여서 함수에 넣어서 사용합니다.  
`함수(*리스트)`  
`함수(*튜플)`  
함수의 매개변수 개수와 리스트의 요소 개수는 같아야 합니다.  
```
def print_numbers(a, b, c):
    print(a)
    print(b)
    print(c)
    
x = [10, 20, 30]
print_numbers(*x)
```
10. 가변 인수 함수 만들기   
같은 함수에 인수 한 개를 넣을 수도 있고, 열 개를 넣을 수도 있습니다.  또는, 인수를 넣지 않을 수도 있습니다.  

다음과 같이 가변 인수 함수는 매개변수 앞에 `*`를 붙여서 만듭니다.
같은 함수에 인수 한 개를 넣을 수도 있고, 열 개를 넣을 수도 있습니다. 또는, 인수를 넣지 않을 수도 있습니다.  

다음과 같이 가변 인수 함수는 매개변수 앞에 `*`를 붙여서 만듭니다.  
```
def print_numbers(*args):
    for arg in args:
        print(arg)
print_numbers(10)
print_numbers(10, 20, 30, 40)        
```
`print_numbers` 함수에 숫자를 넣어서 호출해봅니다.넣은 숫자 개수만큼 출력되는 것을 확인할 수 있습니다.
리스트(튜플) 언팩킹도 사용할 수 있습니다.
```
x = [10]
print_numbers(*x)

y = [10, 20, 30, 40]
print_numbers(*y)
```
고정인수와 가변 인수 함께 사용 예
```
def print_numbers(a, *args):
    print(a)
    print(args)

print_numbers(1) # 1,()
print_numbers(1, 10, 20) # 1, (10,20)
print_numbers(*[10, 20, 30]) # 10,(20,30)
```
def print_numbers`(*args, a)`:처럼 `*args`가 고정 매개변수보다 앞쪽에 오면 안 됩니다. 매개변수 순서에서 `*args`는 반드시 가장 뒤쪽에 와야 합니다.

11. 키워드 인수 사용  
키워드 인수는 말 그대로 인수에 이름(키워드)을 붙이는 기능입니다.  
키워드=값 형식으로 사용합니다.
```
def personal_info(name, age, address):
    print('이름: ', name)
    print('나이: ', age)
    print('주소: ', address)
personal_info(name='홍길동', age=30, address='서울시 용산구 이촌동')
personal_info(age=30, address='서울시 용산구 이촌동', name='홍길동')
```
키워드 인수를 사용하면 인수의 순서를 맞추지 않아도 키워드에 해당하는 값이 들어갑니다.  

12. 키워드 인수 딕션너리 언팩킹
`**x`처럼 딕셔너리를 언패킹하면 딕셔너리의 값들이 함수의 인수로 들어갑니다.
```
def personal_info(name, age, address):
    print('이름: ', name)
    print('나이: ', age)
    print('주소: ', address) 
x = {'name': '홍길동', 'age': 30, 'address': '서울시 용산구 이촌동'}
personal_info(**x) 
personal_info(**{'name': '홍길동', 'age': 30, 'address': '서울시 용산구 이촌동'})
```
딕셔너리 변수 대신 딕셔너리 앞에 바로 `**`를 붙여도 동작은 같습니다.  
매개변수 이름, 개수가 다른 딕셔너리를 넣으면 에러가 발생합니다.

13. 키워드 인수를 사용하는 가변 인수 함수 만들기  
매개변수 앞에 `**`를 붙여서 만듭니다.    
함수를 만들 때 괄호 안에 `**kwarg`s와 같이 매개변수 앞에 `**`를 붙입니다. 함수 안에서는 for로 kwargs.items()를 반복하면서 print로 값을 출력합니다. 
매개변수 이름은 관례적으로 keyword arguments를 줄여서 kwargs로 사용합니다. 특히 이 kwargs는 딕셔너리라서 for로 반복할 수 있습니다.
```
def personal_info(**kwargs):
    for kw, arg in kwargs.items():
        print(kw, ': ', arg, sep='')
personal_info(name='홍길동')
personal_info(name='홍길동', age=30, address='서울시 용산구 이촌동')
x = {'name': '홍길동'}
personal_info(**x)
y = {'name': '홍길동', 'age': 30, 'address': '서울시 용산구 이촌동'}
personal_info(**y)
```
보통 `**kwargs`를 사용한 가변 인수 함수는 다음과 같이 함수 안에서 특정 키가 있는지 확인한 뒤 해당 기능을 만듭니다.  
```
def personal_info(**kwargs):
    if 'name' in kwargs:    # in으로 딕셔너리 안에 특정 키가 있는지 확인
        print('이름: ', kwargs['name'])
    if 'age' in kwargs:
        print('나이: ', kwargs['age'])
    if 'address' in kwargs:
        print('주소: ', kwargs['address'])
```
14. 매개변수에 초깃값 지정하기  
인수를 생략시 함수의 매개변수에 초깃값을 지정합니다.  
```
def personal_info(name, age, address='비공개'):
   print('이름: ', name)
   print('나이: ', age)
   print('주소: ', address)  
personal_info('홍길동', 30)   
```
`초깃값을 지정할 때 한 가지 주의할 점`:초깃값이 지정된 매개변수 다음에는 초깃값이 없는 매개변수가 올 수 없습니다.  

## 2. 파이썬에서 함수 재귀 호출  
함수 안에서 함수 자기자신을 호출하는 방식  
재귀호출은 일반적인 상황에서는 잘 사용하지 않지만 알고리즘을 구현할 때 매우 유용합니다. 
1. 재귀호출 사용  
```
def hello():
    print('Hello, world!')
    hello()
 
hello()
```
파이썬에서는 최대 재귀 깊이(maximum recursion depth)가 1,000으로 정해져 있습니다.  최대 재귀 깊이를 초과하면 RecursionError가 발생합니다.  
2. 재귀호출에 종료 조건  
```
def hello(count):
    if count == 0:    # 종료 조건을 만듦. count가 0이면 다시 hello 함수를 호출하지 않고 끝냄
        return
    
    print('Hello, world!', count)
    
    count -= 1      # count를 1 감소시킨 뒤
    hello(count)    # 다시 hello에 넣음
 
hello(5)    # hello 함수 호출
```
3. 재귀호출을 사용하여 팩토리얼을 구현  
팩토리얼은 1부터 n까지 양의 정수를 차례대로 곱한 값이며 !(느낌표) 기호로 표기합니다.  
n과 반환된 결괏값을 곱하여 다시 반환하는 과정을 반복합니다.  
```
def factorial(n):
    if n == 1:      # n이 1일 때
        return 1    # 1을 반환하고 재귀호출을 끝냄
    return n * factorial(n - 1)    # n과 factorial 함수에 n - 1을 넣어서 반환된 값을 곱함
 
print(factorial(5))
```
4. 재귀호출로 회문 판별  

```
def is_palindrome(word):
    if len(word) < 2:
        return True
    if word[0] != word[-1]:
        return False
    return is_palindrome(word[1:-1])
print(is_palindrome('hello'))
print(is_palindrome('level'))
```
첫번째 문자와 마지막 문자가 같으면 
is_palindrome 함수에는 word[1:-1]처럼 현재 문자열의 두 번째 문자부터 뒤에서 두 번째 문자까지만 잘라서 다시 넣어줍니다.  

문자열이 회문인지 판단할 때는 종료 조건이 두 가지입니다.  
* if word[0] != word[-1]:와 같이 첫 번째 문자와 마지막 문자가 다를 때는 False를 반환합니다.  
* if len(word) < 2:로 글자가 하나일 때 재귀호출을 끝내고 True를 반환  
`if len(word) < 2:`는 `if word[0] != word[-1]:`보다 먼저 와야 합니다. 그렇지 않으면 글자가 하나도 없는데도 word[0]과 word[-1]에 접근하여 에러가 발생하게 됩니다.   

## 3. 파이썬에서 람다 표현식  
람다 표현식은 함수를 간편하게 작성할 수 있어서 다른 함수의 인수로 넣을 때 주로 사용합니다.  
1. 람다 표현식으로 함수 만들기  
```
# 숫자를 받은 뒤 10을 더해서 반환하는 함수   
def plus_ten(x):
    return x + 10
plus_ten(1)  
# plus_ten 함수를 람다 표현식으로 작성   (lambda 매개변수들: 식)
plus_ten1 = lambda x: x + 10  
plus_ten1(1)
```
2. 람다 표현식 자체를 호출  
다음과 같이 람다 표현식을 ( )(괄호)로 묶은 뒤에 다시 ( )를 붙이고 인수를 넣어서 호출합니다.   
```
(lambda x: x + 10)(1)  
```
3. 람다 표현식 안의 변수  
람다 표현식 안에서는 새 변수를 만들 수 없습니다.  
반환값 부분은 변수 없이 식 한 줄로 표현할 수 있어야 합니다. 변수가 필요한 코드일 경우에는 def로 함수를 작성하는 것이 좋습니다.  
```
# (lambda x: y = 10; x + y)(1) 오류 
y = 10
(lambda x: x + y)(1) # 정상
```
4. 람다 표현식을 인수로 사용  
람다 표현식을 사용하는 이유는 함수의 인수 부분에서 간단하게 함수를 만들기 위해서 입니다.  
```
def plus_ten(x):
    return x + 10
list(map(plus_ten, [1, 2, 3]))  
```
map을 사용할 때 map(str, [1, 2, 3])와 같이 자료형 int, float, str 등을 넣었습니다. plus_ten처럼 함수를 직접 만들어서 넣어도 됩니다.
```
 list(map(lambda x: x + 10, [1, 2, 3]))
```
5. 람다 표현식에 조건부 표현식 사용  
map을 사용하여 리스트 a에서 3의 배수를 문자열로 변환
```
a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
list(map(lambda x: str(x) if x % 3 == 0 else x, a))
# list(map(lambda x: str(x) if x % 3 == 0, a)) # 오류 
```
람다 표현식에서 if를 사용했다면 반드시 else를 사용해야 합니다. 다음과 같이 if만 사용하면 문법 에러가 발생하므로 주의해야 합니다.  

lambda 매개변수들: 식1 if 조건식1 else 식2 if 조건식2 else 식3
```
a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
list(map(lambda x: str(x) if x == 1 else float(x) if x == 2 else x + 10, a))
```
별로 복잡하지 않은 조건인데도 알아보기가 힘듭니다. 이런 경우에는 함수에서 if, elif, else를 사용하는 것이 좋습니다. 
```
def f(x):
    if x == 1:
        return str(x)
    elif x == 2:
        return float(x)
    else:
        return x + 10
a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
list(map(f, a))         
```
6. map에 객체를 여러 개 사용  
map은 리스트 등의 반복 가능한 객체를 여러 개 넣을 수도 있습니다
```
a = [1, 2, 3, 4, 5]
b = [2, 4, 6, 8, 10]
list(map(lambda x, y: x * y, a, b))
```
7. filter 사용하기  
filter에 지정한 함수의 반환값이 True일 때만 해당 요소를 가져옵니다. ```
def f(x):
   return x > 5 and x < 10
a = [8, 3, 2, 10, 15, 7, 1, 9, 0, 11]
list(filter(f, a))
```
```
람다 표현식 `lambda x: x > 5 and x < 10`을 filter에 넣어서 5보다 크면서 10보다 작은 수를 가져오도록 만들었습니다.
```
a = [8, 3, 2, 10, 15, 7, 1, 9, 0, 11]
list(filter(lambda x: x > 5 and x < 10, a))  
```


> **colab 코딩연습:** [https://colab.research.google.com/drive/1U0JXeHcd2cBpGOUaRyrDnHPLqq82xUio?usp=sharing](https://colab.research.google.com/drive/1U0JXeHcd2cBpGOUaRyrDnHPLqq82xUio?usp=sharing) 
