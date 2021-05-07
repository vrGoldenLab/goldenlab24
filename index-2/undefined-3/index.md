# 리스트

\(v1.0\)

## 특징 

> 리스트 생성시 튜플과 마찬가지로 원소는 ,로 구분하지만 [ ]을 사용합니다.
> 수,문자열,bool,리스트 데이터 타입이 모두 원소가 가능
> 하나의 원소도 list생성 가능 (원소뒤 , 필요없음)
> 인덱싱과 슬라이싱 가능
> +,*로 원소 처리

```
li_one = [0]
li_one
```
## 튜플과 차이

### 리스트는 원소의 추가,변경,삭제가 가능합니다.  

#### 인덱싱한 리스트에 값을 저장해 기존 원소 대체,추가,삭제 처리

* 인덱싱 원소 대체 
```
#리스트 인덱스 대체
list1 = ['월','화','수','목','금','토','일',7]
list1[0] = '월요일'
list1
```
* del을 사용한 인덱스 삭제

```
#리스트 인덱스 삭제
list1 = ['월','화','수','목','금','토','일',7]
del list1[7]
list1
```
```
#키워드 인덱스 삭제
list1 = ['월','화','수','목','금','토','일',7]
list1.remove('일') # '일' 삭제
list1
```
* insert를 이용한 인덱스 원소 추가
* 슬라이싱한 리스트에 값을 저장해 기존 원소 대체,추가,삭제

## 리스트의 함수

* reverse : 리스트를 거꾸로 뒤집는다. desc 정렬이 아님
* sort : 정렬, 기본값은 오름차순 정렬
* sort(reverse=True)
* sorted : 순서대로 정렬, 정렬된 리스트를 반환



> **colab 코딩연습:** [https://colab.research.google.com/drive/1SfUHB1VT-hvU-0L0X75Urr8rWyBBhxVu?usp=sharing](https://colab.research.google.com/drive/1SfUHB1VT-hvU-0L0X75Urr8rWyBBhxVu?usp=sharing) 


