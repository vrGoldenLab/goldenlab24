# **데이터 이해하기**

* 정보 (information)을 얻기 위한 재료
* 데이터 혹은 자료라고 이야기하며 구체적으로 이야기 할 때는 값(value) 라고 합니다.   
        신체검사시 키,몸무게,시력 등의 구체적인 특성이 value  
        이 값을 모아 '2021년 신체검사 결과'로 만들면 data  
        신장을 체중으로 나누어 비만도 위험군을 선별하면 information
        
## variable   

* 변수 - 값을 저장하는 공간   
* 변수명 - 값을 저장하는 공간의 이름

## 변수와 관계된 주요 작업 

* 변수를 생성(declaration)해 값 저장하기(assignment)
* 변수를 호출해(call)하고 값 참조(reference) 

```
cal_test = 10*10+10/10 # 계산값을 변수명 cal_text에 저장, 변수 생성과 값저장을 동시에 수행
print(cal_test) #변수 num1을 호출해 참조하여 출력
```
## 변수명 객체 이름 정하기 기준  

객체 - 파이썬을 구성하는 모든 요소  
*   알파벳,숫자,공백을 표현하기 위한 _
*   객체명은 첫문자로 숫자를 사용할 수 없다
*   혼동하기 쉬운 문자 변수는 사용하지 않는것이 좋다.   
            'l'(소문자 엘),I(대문자 아이), O(대문자 오),o(소문자 오) 등
*   파이썬이 사용하는 객체명(키워드)는 사용할 수 없다

> 'False', 'None', 'True', 'and', 'as', 'assert', 'break', 'class',    
> 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for','from',    
> 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or','pass',   
> 'raise', 'return', 'try', 'while', 'with', 'yield'

## 파이썬 표준 작명 기준  

*   snake_case: 모든 단어를 소문자로 구성하고 단어 사이를 _로 구분  
*   CamelCase: 단어의 첫 문자를 대문자로 나머지는 소문자로 공백없이 
*   mixedCase: CamelCase와 같으나 객체명 첫글자는 소문자 사용

기준참조[https://www.python.org/dev/peps/pep-0008/#id34](https://www.python.org/dev/peps/pep-0008/#id34)


## 1.숫자형 
정수: 소숫점이 없는 숫자.자료형명 int
실수: 소숫점이 있는 숫자. 자료형명 float
```
a = 1
b = 1.0
c = 00.00310
d = .554
e = 15.
print(a,b,c,d,e,sep='   ')
print(a*b,c/d,(e-3)*d,sep='   ')

# 실수값에 영향이 없는 0은 제거된다.
# 산술연산자 +,-,*,/ 사용 가능
# 나눗셈을 제외한 정수간 계산의 결과값은 정수,정수와 실수 간 계산값은 실수
```
### 산술연산자

*  사칙연산자 +, -, * 
*  제곱을 나타내는 **  
*  나머지를 산출하는 % (Modulus),   
*  나누기에 소숫점 이하를 버리는 // 연산자(Floor Division) 
 
### 비교연산자  

* 관계연산자로도 불리운다
* 등호(==), 같지 않음(!=), 부등호(<, >, <=, >=) 등이 있다.

```
#제자리 연산:변수에서 값을 꺼낸 연산 후 그 결과를 원래의 변수에 다시 저장 
num1 = 100
num1 = num1 + 100
num1 += 100 
print(num1)
```
```
# 제자리 연산자
num2 = 100
num3 = 200
num2 += num3   # num2 = num2 + num3
print(num2)
num2 -= num3   # num2 = num2 - num3
print(num2)
num2 *= num3   # num2 = num2 * num3
print(num2)
```
## 2.문자열

### 문자열은 텍스트의 기본 자료형

문자를 사슬(string)처럼 나영한 값, 자료형명 str  
변수명이나 함수명과 구분하기 위해 따옴표로 열고 닫아 생성합니다.

문자열 내의 특수키  

\'   => '
\"   => "
\\   => \
\n   => 줄바꿈(newline), enter
\t   => 줄맞춤(intent),tap  

```
# '''로 문자열을 열고 닫을때
# \n없이 enter로 줄바꿈,\',\"없이 따옴표 사용 가능
print('''{
    마크다운 전환: ctrl + m m 
    코드로 전환: ctrl + m y 
    " 사용 가능  " '  '
}''')
```  
### 문자열에서 사용되는 함수  

* join : 문자열을 원하는 글자로 더한다.
* split : 문자열을 원하는 글자로 나눈다.
* strip : 문자열 앞뒤의 공백을 지운다. 문자열 내부의 공백은 지우지 않는다.
* replace : 문자열의 특정 글자를 다른 글자로 바꾼다.
* in : 문자열 안에 해당 글자가 있는지 확인
* not in : 문자열 안에 해당 글자가 없는지 확인 
* count : 특정 글자가 문자열에 몇번 사용되었는지 확인 
* find : 문자열에서 특정 글자의 위치정보 확인
* capitalize : 문자열의 첫 글자를 대문자로 변환
* lower : 모든 글자를 소문자로 변환
* upper: 모든 글자를 대문자로 변환
* starstwith : 해당 문자열이 특정 글자로 시작되는지 확인
* endswith : 해당 문자열이 특정 글자로 끝나늕 확인

## 3. bool 
주어진 조건 안에서 참,거짓을 판단해서 결과를 담는 자료형 값 True,False  
### 논리연산자

* 조건식과 조건식을 연결하는 연산자 
        논리합 => a and b : a나 b 모두 참일때만 참 
        논리곱 => a or b : a나 b 중 하나만 참이어도 참
        부정   => not a : a가 참이면 거짓,거짓이면 참

> colab 코딩 실습: [https://colab.research.google.com/drive/1vldvHtlau8-_RByxLpMbd2LwXNJiNzGO?usp=sharing](https://colab.research.google.com/drive/1vldvHtlau8-_RByxLpMbd2LwXNJiNzGO?usp=sharing)




