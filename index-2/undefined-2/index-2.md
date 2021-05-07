## 슬라이싱 

> 일렬로 들어있는 원소 여럿을 한꺼번에 필요할 때 사용합니다.
> 원하는 원소의 시작 순서와 끝 순서를 특정해서 사용합니다.

```
print('t_liat1',t_list1)
print('*'* 60)

print('t_list1[0:3] ',t_list1[0:3])

print('t_list1[1:]  ',t_list1[1:])

print('t_list1[:5]  ',t_list1[:5])

print('t_list1[2:4] ',t_list1[2:4])

print('t_list1[-4:7]',t_list1[-4:7])
```

### 튜플 일정 간격으로 슬라이싱

```
t_list3 = t_list[0:8:2]
t_list4 = t_list[1:8:2]

print(t_list3,'*',t_list4)

print(t_list3 + t_list4)

print(t_list4 * 2)
```

> **colab 코딩연습:** [https://colab.research.google.com/drive/1SfUHB1VT-hvU-0L0X75Urr8rWyBBhxVu?usp=sharing](https://colab.research.google.com/drive/1SfUHB1VT-hvU-0L0X75Urr8rWyBBhxVu?usp=sharing) 
