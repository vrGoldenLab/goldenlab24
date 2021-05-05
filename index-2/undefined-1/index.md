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



