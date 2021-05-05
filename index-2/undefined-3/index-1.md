# 집합

\(v0.9\)

## 소개

집합(set)은 파이썬 2.3부터 지원하기 시작한 자료형으로, 집합에 관련된 것을 쉽게 처리하기 위해 만든 자료형입니다.
집합 자료형은 다음과 같이 set 키워드를 사용해 만들 수 있습니다.

## 특징

* 중복을 허용하지 않습니다.
* 순서가 없습니다(Unordered).
* 집합은 여러 원소를 ,로 구분하고 { }로 여닫아 생성합니다.
* 하나의 집합에 여러 자료형을 담아 저장할 수 있습니다.
* 집합은 리스트와 집합을 원소로 저장할 수 없습니다.
* 집합은 +,*를 사용할 수 없습니다
* 자료형명은 set

리스트나 튜플은 순서가 있기(ordered) 때문에 인덱싱을 통해 자료형의 값을 얻을 수 있지만 set 자료형은 순서가 없기(unordered) 때문에 인덱싱으로 값을 얻을 수 없습니다. 이는 딕셔너리와 비슷합니다. 딕셔너리 역시 순서가 없는 자료형이라 인덱싱을 지원하지 않습니다. 
만약 set 자료형에 저장된 값을 인덱싱으로 접근하려면 다음과 같이 리스트나 튜플로 변환한후 해야 합니다.  
중복을 허용하지 않는 set의 특징은 자료형의 중복을 제거하기 위한 필터 역할로 종종 사용하기도 합니다.  


```
set1 = {"1", 3, 5, (1,3)}
set1
``` 
1. set 합집합  
set의 합집합은 | 연산자와 union함수를 이용  
파이썬의 합집합도 수학의 합집합 연산과 동일한 기능 
set 요소와 또 다른 set 요소를 합하여 새로운 set을 반환  
이때 중복되는 요소는 삭제

2. set 교집합   
set의 교집합은 & 연산자와 intersection 함수를 이용.   
수학의 교집합과 동일한 연산. 
공통적인 요소만을 포함한 새 set을 반환.

3. set 차집합  
set의 차집합은 - 연산자와 difference 함수를 이용.  
수학의 차집합과 동일한 연산.   
다른 set이 가지고 있는 요소를 빼고 새 set을 반환.

```
set3 = {1,2,3,4,5,6,7}
set4 = {4,5,6,7,8,9,10,11,12}

# 합집합
print(set3 | set4)
print(set3.union(set4))

# 교집합
print(set3 & set4)
print(set3.intersection(set4))

# 차집합 - set4에에서 set3의 원소를 뺀 원소
print(set4 - set3)
print(set4.difference(set3))

# 대칭차집합 - 교집합을 뺀 합집합
print(set3 ^ set4)
```
```
#반환값이 bool인 집헙 연산
#진부분 집합 
set5 = {2,3,4,5}
print(set3>set5) #set5의 모든 원소가 set3에 존재하고 set3과 set5는 같지않다
print(set3<set5) #set3의 모든 원소가 set5에 존재하고 set3과 set5는 같지않다  
#부분 집합 
print(set3>=set5) #set5의 모든 원소가 set3에 존재
print(set3<=set5) #set3의 모든 원소가 set5에 존재
```
## 집합자료형 관련 함수

1개값 추가 add
여러개 값 추가 update
특정값 제거 remove


> **colab 코딩연습:** [https://colab.research.google.com/drive/1SfUHB1VT-hvU-0L0X75Urr8rWyBBhxVu?usp=sharing](https://colab.research.google.com/drive/1SfUHB1VT-hvU-0L0X75Urr8rWyBBhxVu?usp=sharing) 
