# 딕셔너리  
* 대응 관계를 나타내는 자료형
* 딕셔너리는 Key와 Value를 한 쌍으로 갖는 자료형
Key와 Value의 쌍 여러 개가 { }로 둘러싸여 있습니다. 각각의 요소는 Key : Value 형태로 이루어져 있고 쉼표(,)로 구분합니다.  
{Key1:Value1, Key2:Value2, Key3:Value3, ...}  
주민번호 : 이름 같이 자료를 순차적으로 검색하는 것이 아니라 key으로 대은 관계인 value값을 가져올 수 있습니다.

### 특징 
리스트나 튜플, 문자열은 읽어올 때 인덱싱이나 슬라이싱 기법 중 하나를 사용. 
딕셔너리는 Key를 사용해서 Value를 구합니다. Key의 Value를 얻기 위해서는 딕셔너리변수이름[Key]를 사용합니다.
```
city = {'한국':'서울','중국':'베이징','미국':'워싱턴'}
print(city['한국'])

personal_list = {'나이':29,'phone':'010-1111-2222','이름':'강단','주소':'서울시'}
print(personal_list['이름'],' ',personal_list['나이'],'세',' ',personal_list['주소'])
```
### 주의사항
중복되는 Key 값을 설정해 놓으면 하나를 제외한 나머지 것들이 모두 무시됩니다.  
Key에 리스트는 쓸 수 없습니다. 하지만 튜플은 Key로 쓸 수 있습니다.  

### 딕셔너리 관련 함수들
* keys()
딕셔너리의 Key만을 모아서 dict_keys 객체를 돌려줍니다.
* values()
딕셔너리의 value만을 모아서 dict_values 객체를 돌려줍니다.
* items()
Key, Value 쌍을 dict_items로 반환합니다.
* get()
key값으로 value 읽음
딕션너리[key] 읽기와 동일하나 key가 없는 경우 디폴트값 반환(디폴트가 없으면 None)
* in
안에 해당 key가 있는지 bool값으로 반환
* clear()
딕셔너리 모두 지우기


> **colab 코딩연습:** [https://colab.research.google.com/drive/1SfUHB1VT-hvU-0L0X75Urr8rWyBBhxVu?usp=sharing](https://colab.research.google.com/drive/1SfUHB1VT-hvU-0L0X75Urr8rWyBBhxVu?usp=sharing) 
