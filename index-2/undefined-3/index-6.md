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
2.함수 키워드 return  
함수를 호출할 때 결과값을 반환합니다.

3.복수의 매개변수 구성
4.복수의 return 값 사용 가능
5.튜플,딕셔너리로 매개변수 받기
7.변수의 유효범위
 함수내부에서 생성된 변수는 함수밖에서 사용할 수 없습니다.
 외부에서 사용할 시에는 global을 사용합니다. 
8.객체 고유의 함수 활용
 문자열이나 리스트 등도 스스로 사용할 수 있는 함수가 있습니다.
 이를 메소드(Method)라고 합니다.  
 메소드도 함수이므로 호출하는 방식은 같으나 누가 호출하는지를 명시해야 합니다.


> **colab 코딩연습:** [https://colab.research.google.com/drive/1U0JXeHcd2cBpGOUaRyrDnHPLqq82xUio?usp=sharing](https://colab.research.google.com/drive/1U0JXeHcd2cBpGOUaRyrDnHPLqq82xUio?usp=sharing) 
