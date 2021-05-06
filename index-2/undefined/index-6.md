# import 사용법  

파이썬에서는 다양한 분야의 처리를 위한 기능을 제공합니다.
프로그램에서 자주 사용하는 기능을 가져와 사용해 보도록 하겠습니다. 

`모듈(module)` 이란
모듈이란 함수나 변수 또는 클래스를 모아 놓은 파일입니다.
모듈은 다른 파이썬 프로그램에서 불러와 사용할 수 있습니다. 파이썬 스크립트를 작성할 때마다 매번 비슷한 클래스와 함수를 작성한다면 코드도 길어지고 중복되는 부분이 생깁니다. 이런 경우에는 공통되는 부분을 빼내서 모듈과 패키지로 만들면 됩니다. 이후에는 코드를 다시 만들지 않고 모듈과 패키지만 가져와서 사용하면 편리합니다.

`모듈(module)`은 변수, 함수, 클래스 등을 모아 놓은 스크립트 파일이고, `패키지(package)`는 여러 모듈을 묶은 것입니다. 모듈은 간단한 기능을 담을 때 사용하며, 패키지는 코드가 많고 복잡할 때 사용합니다. 즉, 패키지는 기능들이 모듈 여러 개로 잘게 나누어져 있고, 관련된 모듈끼리 폴더에 모여 있는 형태입니다.

캘린더 기능

## 1. 모듈 import 방법
```
import 모듈명 # 모듈 불러오기
import 모듈명 as 별칭 # 별칭으로 모듈 불러오기
from 패키지명 import 모듈명  # 원하는 모듈만 특정해서 불러오기
from 모듈명 import 함수명  # 원하는 함수만 특정해서 불러오기 
```
```
from math import ceil
a = ceil(-3.14) #결과는 -3
b = ceil(3.14) #결과는 4
# import math #math 모듈을 먼저 import해야 한다.
#math.ceil(-3.14) #결과는 -3
#math.ceil(3.14) #결과는 4
print(a,b)
```
## 2. 캘린더 기능  
month(): 함수에 인수로 년,월을 입력하여 호출하면 캘린더 데이터(문자열)반환  
isleap(): 함수에 인수로 년도를 입력하면 bol을 반환  
```
import calendar  # calendar 모듈 import
print(calendar.month(2021,5)) # 달력 년월을 지정 출력
```
```
import calendar  # calendar 모듈 import
print(calendar.isleap(2021)) # 윤년 여부 출력
```
## 3. 날짜와 시간  

어떤 언어를 사용하든지 프로그래밍을 하면서 날짜와 시간 처리는 피하기 어려운 부분입니다. 파이썬은 내장 모듈인 datetime을 통해서 어떻게 날짜와 시간 데이터를 처리를 지원하고 있습니다.

* today(): 프로그램을 실행한 시점의 날찌와 시간을 반환  
* now(): 실행 시점의 날짜와 시간을 반환. 초값에는 소수점 이하값 포함  
* timezone(): datetime 내장 모듈의 timezone 클래스는 시간대를 표현하기 위해서 사용   
timezone 클래스의 생성자는 UTC 기준으로 시차를 표현하는 timedelta 객체를 인자로 받아 timezone 객체를 생성해줍니다.  
한국은 UTC 기준으로 9시간이 빠르므로 다음과 같이 timezone 객체를 생성할 수 있습니다.  
```
from datetime import timedelta, timezone
# timezone 클래스의 생성자는 UTC 기준으로 시차를 표현
tzinfo=timezone(timedelta(hours=9))
print(datetime.date.today(tzinfo)))
print(datetime.datetime.now(tzinfo))
now_str = datetime.datetime.now(tzinfo)
print(now_str.hour)
print(now_str.minute)
print(now_str.second)
```
참고 자료 [https://docs.python.org/3/library/datetime.html](https://docs.python.org/3/library/datetime.html)  

### 경과한 날짜 수 확인 임의의 날짜에서 다른 임의의 날짜까지의 경과일 계산  
```
import datetime 

date1 = datetime.date.today()
date2 = datetime.date(2000,1,1)
print(date1-date2)
```

## 4. random 모듈
파이썬의 random 모듈은 랜덤 숫자를 생성 뿐만 아니라 다양한 랜덤 관련 함수를 제공합니다.  
우선 random 모듈을 사용하려면 임포트해야 합니다.

import random

### random() 함수  
0부터 1사이의 랜덤 실수를 리턴합니다.  
random.random() # Random float x, 0.0 <= x < 1.0

### uniform() 함수  
2개의 숫자 사이의 랜덤 실수를 리턴합니다.  
random.uniform(1, 10) # Random float x, 1.0 <= x < 10.0

### randint() 함수  
2개의 숫자 사이의 랜덤 정수를 리턴합니다. (2번째 인자로 넘어온 정수도 범위에 포함시킴)  
random.randint(1, 10) # Integer from 1 to 10, endpoints included

### randrange() 함수
range(start, stop, step) 함수로 만들어지는 정수 중에 하나를 랜덤하게 리턴합니다.  
random.randrange(0, 101, 2) # Even integer from 0 to 100

### choice() 함수  
랜덤하게 하나의 원소를 선택합니다.   
random.choice('abcdefghij') # Choose a random element random.choice('가위','바위','보')

## <실습link>
#### colab으로 실습하기: [https://colab.research.google.com/drive/1hcaetTRU7Yre6mOI3zysmCUtf7hzIiGP?usp=sharing](https://colab.research.google.com/drive/1hcaetTRU7Yre6mOI3zysmCUtf7hzIiGP?usp=sharing)

