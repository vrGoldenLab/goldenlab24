# 기본적인 사용법

\(v1.0\)

Colab을 사용하기 위해 먼저 TensorFlow가 어떻게 동작하는지를 이해해 봅시다.  
## Colab 서버 스펙 확인

```python


아래의 코드는 한줄씩 셀에서 실행하기 바란다. 쥬피터 노트북의 셀은 출력결과가 여러개인 경우 맨 마지막의 OutputStream 결과가 남으므로 이전 출력결과를 확인할 수 없기 때문이다. 일반적인 .py파일 작성과는 다르게 .ipynb파일의 경우 가급적 하나의 셀에 많은 코드를 작성하지 않는것이 좋다.

!cat /etc/issue.net
!cat /proc/meminfo
!cat /proc/cpuinfo
!df -h
!nvidia-smi
!python --version
!ls

* 파일처리

%%writefile  test.py
print('hello world!')

# test.py 실행시키기
%run test.py

from google.colab import files
# 브라우저에 다운로드 됨을 확인할 수 있다.
files.download('test.py')

# [Cancel upload] 버튼을 클릭하여 잠시 멈춘 후 파일선택 버튼을 클릭하면 PC 내 파일을 선택할 수 있는 다이얼로그 창이 뜬다.
# 리턴값을 받는 변수인 myupload라는 이름의 디렉토리가 생성된다.
myupload = files.upload()
*구글드라이브 연동


import os
print(os.getcwd())
!ls

# 실행시 등장하는 URL을 클릭하여 허용해주면 인증KEY가 나타난다. 복사하여 URL아래 빈칸에 붙여넣으면 마운트에 성공하게된다.
from google.colab import drive
drive.mount('./MyDrive')

# 마운트된 내 드라이브를 확인해보자
!ls

# 해당 드라이브로 이동 
# 내 드라이브는 원격서버가 아니라 로컬서버로 간주하므로 명령어 실행시 앞단에 !를 붙이지 않는다.
cd MyDrive/My Drive

# 내드라이브의 전체 목록이 나타난다.
ls

# 특정파일을 가져오고 싶은 경우 다음과 같이 접근한다.
import pandas as pd
df = pd.read_csv("./MyDrive/test/test.csv")
```
