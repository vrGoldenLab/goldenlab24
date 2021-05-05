### 1.주사위 빈도수 사전 만들기
```
* 주사위 수 리스트 만들기 (1에서 6까지의 주사위 수를 30번 반복) 
        import random 
        주사위수 빈 리스트 생성
       #반복:
        for in range(30):
           #주사위 리스트에 1~6의 무작위 수를 추가합니다.
            주사위수리스트명.append(random.randint(1,6))

        주사위수별 발생 횟수를 딕션어리로 작성합니다. 
        key는 주사위값으로 ,value는 주사위리스트명.count(값)을 넣습니다.
        주사위수를 입력받아 30번 중 몇 번 나왔는지 횟수를 출력합니다.
```

```
import random
t_list = []
r_count = 10
for i in range(r_count):
    t_list.append(random.randint(1,6))
print(t_list)
#---------------------------------------------------------------------
t_dict = {'1':t_list.count(1),'2':t_list.count(2),'3':t_list.count(3),
          '4':t_list.count(4),'5':t_list.count(5),'6':t_list.count(6)}
print(t_dict)
a = input('주사위 수를 입력하세요')
#b = int(a) 
print(f'{r_count}번 주사위를 던져 {a}이 나온 횟수는 {t_dict[a])}번 입니다')
```
> colab 작성: [https://colab.research.google.com/drive/15klrTP1tGukmKEsn0BJXaV-esE_XomsC?usp=sharing](https://colab.research.google.com/drive/15klrTP1tGukmKEsn0BJXaV-esE_XomsC?usp=sharing)  
>
> 과제 제출 설문지: [https://docs.google.com/forms/d/e/1FAIpQLSe9lTRW_YWo5CeBO55Vtw9FMnIrsrvCScCv-MzbhbNUAT-56A/viewform](https://docs.google.com/forms/d/e/1FAIpQLSe9lTRW_YWo5CeBO55Vtw9FMnIrsrvCScCv-MzbhbNUAT-56A/viewform)

