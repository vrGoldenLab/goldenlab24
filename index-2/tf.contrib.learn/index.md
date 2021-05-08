# 코딩 연습

\(v1.0\)

단순 테이블이 있는 웹페이지를 크롤링 예제입니다.  
몇 줄의 코드로 데이터를 가져오는 것이 가능합니다.  
코드를 복사해서 코랩에서 실행시켜 봅니다.   

```
# 필요한 라이브러리를 불러옵니다.
import pandas as pd

# 위키백과 한국인구
url ='https://ko.wikipedia.org/wiki/%EB%8C%80%ED%95%9C%EB%AF%BC%EA%B5%AD%EC%9D%98_%EC%9D%B8%EA%B5%AC'
# pandas.read_html 함수에 url을 인자로 전달하고 살행한 결과를 테이즐에 지정
table = pd.read_html(url)
len(table)
```
```
# 테이블 내용 확인하기

df = table[0]
df.shape
df.head()
```


## 추가적인 자료

* pandas 는 데이터 조작 및 분석을 위해 Python 프로그래밍 언어로 작성된 소프트웨어 라이브러리 입니다[https://en.wikipedia.org/wiki/Pandas_(software)] (https://en.wikipedia.org/wiki/Pandas_(software))

* colab 으로 실습 [https://colab.research.google.com/drive/1T_eQbKQI0M1YenLzxZ0zPlBYhVw_rreD?usp=sharing](https://colab.research.google.com/drive/1T_eQbKQI0M1YenLzxZ0zPlBYhVw_rreD?usp=sharing)
