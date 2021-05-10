# 모듈과 패키지 
`참고자료`: [https://docs.python.org/ko/3/tutorial/modules.html](https://docs.python.org/ko/3/tutorial/modules.html)

모듈(module) : 각종 변수, 함수, 클래스를 담고 있는 파일이다. 특정 기능을  파일 단위로 작성한 것입니다.

패키지(package) : 여러 모듈을 묶은 것이다. 패키지는 모듈에 네임스페이스(namespace, 이름공간)를 제공합니다.

파이썬 표준 라이브러리(Python Standard Library, PSL) : 파이썬에 기본으로 설치된 모듈과 패키지, 내장 함수등이 있습니다.

## 1. 모듈
### 1. import로 모듈 가져오기
모듈을 여러 개 가져올 때는 모듈을 콤마로 구분합니다.

`import 모듈`  

`import 모듈1, 모듈2`  

`모듈.변수`  

`모듈.함수() `  

`모듈.클래스()`

### 2. import as로 모듈 이름 지정하기  

`import 모듈 as 이름`

### 3. from import로 모듈의 일부만 가져오기  

* from import로 원하는 변수, 함수 , 클래스만 가져올 수 있습니다.
`from 모듈 import 변수`  
`from 모듈 import 변수, 함수, 클래스`  

* from import는 모듈의 모든 변수, 함수, 클래스를 가져올 수도 있습니다.
`from 모듈 import *`

* 뒤에 as를 붙여 원하는 이름을 지정할 수 있습니다.
`from 모듈 import 변수 as 이름`
`from 모듈 import 변수 as 이름1, 함수 as 이름2, 클래스 as 이름3`

### 4. 가져온 모듈 해제하기, 다시 가져오기  
* del로 해제하기
```
import math
del math
```
* importlib.reload로 다시 가져오기
```
import importlib
import math
importlib.reload(math)
```
## 2. 패키지 
### 1. import로 패키지 가져오기
* 모듈 가져오기에서 모듈 앞에 패키지. 만 적어주면 됩니다.

`import 패키지.모듈`
`import 패키지.모듈1, 패키지.모듈2`
`패키지.모듈.변수`
`패키지.모듈.함수()`
`패키지.모듈.클래스()`
* ipmport as로 패키지 모듈 이름 지정하기
`import 패키지.모듈 as 이름`



### 2. from import로 패키지의 모듈에서 일부만 가져오기
* 모듈 가져오기와 방법이 동일합니다.
`from 패키지.모듈 import 변수`  
`from 패키지.모듈 import 변수, 함수, 클래스`  

* 패키지의 모듈에서 모든 변수, 함수, 클래스를 가져오기
`from 패키지.모듈 import *`

* from import로 패키지의 모듈의 일부를 가져온 뒤 이름 지정하기
`from 패키지.모듈 import 변수 as 이름`  
`from 패키지.모듈 import 변수 as 이름, 함수 as 이름, 클래스 as 이름`





### 3. 파이썬 패키지 인덱스에서 패키지 설치하기
파이썬 표준 라이브러리(Python Standard Library, PSL) 이외에도 파이썬 패키지 인덱스(Python Package Index, PyPI)를 통해 다양한 패키지를 사용할 수 있습니다.  
명령만 입력하면 원하는 패키지를 인터넷에서 다운로드하여 설치해주며, 관련된 패키지(의존성)까지 자동으로 설치해주므로 편리합니다.  
* pip 설치하기
pip는 파이썬 패키지 인덱스의 패키지 관리 명령어입니다.  
리눅스와 macOS에서는 콘솔(터미널)에서 다음과 같은 방법으로 설치한다. (Windows용 파이썬에는 기본으로 내장되어 있다.)  
```
$ curl -O https://bootstrap.pypa.io/get-pip.py
$ sudo python3 get-pip.py
```
만약 리눅스에 curl이 설치되어 있지 않다면 설치해 줍니다.  
```
우분투 : $ sudo apt-get install curl
```
* pip로 패키지 설치하기  
pip install 패키지
`Windows : 명령 프롬프트(cmd)로 실행`
`리눅스, macOS : 콘솔(터미널)로 실행`
colab에서는 코드셀에서 입력해주면 됩니다.

* import로 패키지 가져오기  
파이썬 코드에서 패키지를 사용하기

`import 패키지`
```
>>> import requests                   # pip로 설치한 requests 패키지를 가져옴
>>> r = requests.get('http://www.google.co.kr')    # requests.get 함수 사용
>>> r.status_code # 결과값 200
```

## 3. 모듈 만들기
### 1. n의 거듭제곱을 구하는 모듈 square2 민들기  
`square2.py 파일명`  
`square2.ipynb 파일명`  
스크립트 파일에서 확장자를 제외하면 모듈 이름이 됨
```
base = 2          # 변수

def square(n):    # 함수
   return base ** n
```


### 2. 모듈 사용하기
`import 모듈`  
`모듈.변수`  
`모듈.함수()`  

* main 모듈을 실행하는 파일과 모듈 파일은 같은 폴더에 있어야 함
```
import square2               # import로 square2 모듈을 가져옴
 
print(square2.base)          # 모듈.변수 형식으로 모듈의 변수 사용
print(square2.square(10))    # 모듈.함수() 형식으로 모듈의 함수 사용
```


* from import로 변수, 함수 가져오기
from import로 변수와 함수를 가져온 뒤 모듈 이름을 붙이지 않고 사용할 수 있다.

`from 모듈 import 변수, 함수`
```
from square2 import base, square
print(base)
square(10)
```


### 3. 모듈에 클래스 작성하고 사용하기
```
class Person:    # 클래스
    def __init__(self, name, age, address):
        self.name = name
        self.age = age
        self.address = address

    def greeting(self):
        print('안녕하세요. 저는 {0}입니다.'.format(self.name))
```
`import 모듈`
`모듈.클래스()` 로 사용합니다.

main 프로그램에서
```
import person    # import로 person 모듈을 가져옴

# 모듈.클래스()로 person 모듈의 클래스 사용
maria = person.Person('마리아', 20, '서울시 서초구 반포동')
maria.greeting()
```
<실행 결과>
안녕하세요. 저는 마리아입니다.



### 4. from import로 클래스 가져오기
from import로 클래스를 가져온 뒤 모듈 이름을 붙이지 않고 사용할 수 있습니다.
from 모듈 import 클래스
```
from person import Person
maria = Person('마리아', 20, '서울시 서초구 반포동')
maria.greeting()
```





## 4. 모듈과 시작점 알아보기
`if __name__ == '__main__':  `
`    코드                    `
현재 스크립트 파일이 실행되는 상태를 파악하기 위해 사용합니다.

###  ` __name__`
`__name__`은 모듈의 이름이 저장되는 변수이며 import로 모듈을 가져왔을 때 모듈의 이름이 들어갑니다.   
하지만 파이썬 인터프리터로 스크립트 파일을 직접 실행했을 때는 모듈의 이름이 아니라 `'__main__'`이 들어갑니다.

import로 모듈을 가져오면 해당 스크립트 파일이 한 번 실행됩니다.
hello.ipynb의 `__name__` 변수에는 'hello'가 들어가고,
main.ipynb의 `__name__` 변수에는 `'__main__'`이 들어갑니다.

어떤 스크립트 파일이든 파이썬 인터프리터가 최초로 실행한 스크립트 파일의 `__name__`에는 `'__main__'`이 들어간다. 이는 `프로그램의 시작점`(entry point)이라는 뜻입니다. 

파이썬은 최초로 시작하는 스크립트 파일과 모듈의 차이가 없다. 그래서 `__name__` 변수를 통해 현재 스크립트 파일이 시작점인지 모듈인지 판단합니다.




## 5. 패키지 만들기 
모듈은 스크립트 파일이 한 개지만 패키지는 폴더(디렉터리)로 구성되어 있습니다.

프로젝트 폴더 안에 패키지 폴더를 만듭니다.
패키지 폴더 안에 `__init__.py` 파일을 저장한다.
패키지 폴더 안에 모듈 만듭니다.
`__init__.py` 파일의 내용은 비워 둘 수 있습니다.

### 패키지 사용하기  
스크립트 파일에서 패키지를 import해 사용한다.

`import 패키지.모듈`
`패키지.모듈.변수`
`패키지.모듈.함수()`
`패키지.모듈.클래스()`
`from 패키지.모듈 import 변수`
`from 패키지.모듈 import 함수`
`from 패키지.모듈 import 클래스`

## 6. 패키지에서 from import 응용하기

* import 패키지 형식으로 사용합니다. .(점)은 현재 패키지라는 뜻입니다.

`from . import 모듈`

그러려면 해당 패키지의 `__init__.py` 파일을 다음과 같이 수정해야 합니다.

  파이썬에서 __init__.py 파일은 폴더(디렉터리)가 패키지로 인식되도록 하는 역할도 하고, 이름 그대로 패키지를 초기화하는 역할도 합니다.   
  즉, import로 패키지를 가져오면 __init__.py 파일이 실 행되므로 이 파일에서 from . import 모듈 형식으로 현재 패키지에서 모듈을 가져오게 만들어야 합니다.  
  
`from . import 모듈1 `   # 현재 패키지에서 모듈1를 가져옴
`from . import 모듈2 `   # 현재 패키지에서 모듈2를 가져옴

  `__init__.py`에서 `from .모듈 import 변수, 함수, 클래스` 또는 `from .모듈 import * `형식으로 모듈을 가져오면 calcpkg 패키지의 네임스페이스에는 함수,변수,클래스가 들어갑니다.  
  따라서 모듈을 거치지 않고 패키지에서 함수를 바로 사용할 수 있습니다.


* from import로 패키지에 속한 모든 변수, 함수, 클래스 가져오기
패키지의 `__init__.py`파일에서 아래와 같이 작성해야 패키지를 가져오는 스크립트에서 패키지.함수() 형식으로 사용할 수 있습니다.

`from .모듈 import 변수, 함수, 클래스'  
`from .모듈 import *`


`from 패키지 import *` 이렇게 작성하면 __init__.py에서 모듈만 가져왔을 뿐 모듈 안의 함수는 가져오지 않아 에러가 발생합니다.


