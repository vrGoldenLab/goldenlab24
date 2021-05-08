# 형변환

각기 다른 데이터 타입이라도 그 부분들에 대해서 특정 연상등의 조합이 이루어질 수도 있습니다. 이때 형변환이 필요합니다. 

## 처리 
* 문자열,숫자열  
int() - 정수형으로 바꿈   
float() - 실수형으로 바꿈   
str() - 문자열로 바꿈   
hex() - 16진수로 바꿈   
oct() - 8진수로 바꿈   
bin() - 2진수로 바꿈   

* 복합형  
tuple() - 튜플로 변환   
list() - 리스트로 변환   
set() - Set형으로 변환 
* 문자열을 슬라이싱하여 숫자형으로 변환  
데이터 전처리시 많이 사용합니다.
```
text_data = '가격:12000원'
price_data = text_data[3:8]
print(price_data,type(price_data))

#계산을 위해 숫자형 변환하여 매출액을 계산 
price_data = float(price_data)
print('단가',price_data, '주문수량',2, '매출액' , price_data*2, type(price_data))
```
#### 문자가 있는 data의 숫자형변환은 오류 발생 
```
#형변환 오류
int(text_data) #문자가 있는 data의 숫자형변환은 오류 발생
```
### 형변환으로 중복 제거
리스트나 튜플을 집합으로 형변환하여 중복값을 제거하고 원래의 리스트나 튜플로 재변환
```
#형변환으로 중복 제거

b = (1,2,3,3,3,3,4,4,5,6,6,7,8,9,11)
print(b)
b = set(b)
print(b)
b = tuple(b)
print(b)
```
### 객체를 bool로 형변환 - bool()
data type별로 비어 있는 값은 False,데이터가 존재하면 True


> **colab 코딩연습:** [https://colab.research.google.com/drive/1SfUHB1VT-hvU-0L0X75Urr8rWyBBhxVu?usp=sharing](https://colab.research.google.com/drive/1SfUHB1VT-hvU-0L0X75Urr8rWyBBhxVu?usp=sharing) 
