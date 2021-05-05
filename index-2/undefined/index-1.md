## 배열

변수는 하나의 값만 넣을 수 있지만 배열은 여러개의 값을 넣어 사용할 수 있습니다. 배열의 가장 앞에 있는 원소의 번호는 1이 아니라 0입니다. 첫번째 원소에 접근하지 위해서는 0 인덱스와 대괄호를 사용합니다. 마지막 원소는 인덱스 -1과 대괄호를 사용합니다.

-튜플_은 리스트처럼 요소를 일렬로 저장하지만, 안의 요소를 변경,추가,삭제를 할 수 없습니다. 읽기 전용 리스트라 할 수 있습니다.

_딕셔너리_는 연관된 값을 묶어서 저장하는 자료형 입니다. {}중괄호안에 키:값 형식으로 저장합니다. 사전에서 단어 찾듯이 값을 가져올 수 있습니다.



### 배열의 길이와 배열 원소의 접근  


배열의 데이터가 많을 경우 배열 원소의 길이를 알려주는 함수를 사용합니다. len()

list = [ 1,10,15,2 ] 일때

list의 1번째 원소는 1 (인덱스 번호는 0)

list의 1번째 원소는 10 (인덱스 번호는 1)

list의 1번째 원소는 15 (인덱스 번호는 2)

list의 1번째 원소는 2 (인덱스 번호는 3 ,혹은 -1)


### 슬라이싱 : 배열 원소의 일정 부분만 가져오기

배열의 원소 중 일부분만 가져와서 사용하는 경우나 전체 데이터를 여러부분으로 나누어서 사용할 경우 사용하는 방법입니다. 
슬라이싱할 처음 위치와 마지막 위치를 정해주면 그 사이 값을 가져옵니다.
```
print(list1[2:6])   #list1 배열의 인덱스 2번부터 6번 앞까지의 데이터 출력 요청
print(list1[2:])    #list1 배열의 인덱스 2번부터 마지막까지의 데이터 출력 요청
print(list1[:6])    #list1 배열의 처음부터 인덱스 6번부터 앞까지의 데이터 출력 요청
print(list1[:-1])   #list1 배열의 처음부터 인덱스 마지막 앞까지의 데이터 출력 요청
```

### range를 사용해서 리스트 만들기  

*  리스트 = list( range(횟수) )
*  리스트 = list( range(시작,끝) )
*  리스트 = list( range(시작,끝,증가폭) )

```
list_rg1 = list(range(11))   
list_rg2 = list(range(5,12))
list_rg3 = list(range(-4,5,2))
list_rg4 = list(range(20,-1,-1))
list_rg5 = list('hello world')

print("list_rg1은" , list_rg1)
print("list_rg2은" , list_rg2)
print("list_rg3은" , list_rg3)
print("list_rg4은" , list_rg4)
print("list_rg5은" , list_rg5)
```
### 요소의 값 할당하기,삭제하기

```list_rg5 = list('hello world')
list_rg5[0] = 'H'

print("list_rg5의 0번째 요소 대문자로 수정" , list_rg5)

del list_rg5[5]
print("list_rg5의 5번째 요소 삭제" , list_rg5)
```
colab으로 실습하기 [https://colab.research.google.com/drive/1hcaetTRU7Yre6mOI3zysmCUtf7hzIiGP?usp=sharing](https://colab.research.google.com/drive/1hcaetTRU7Yre6mOI3zysmCUtf7hzIiGP?usp=sharing)
