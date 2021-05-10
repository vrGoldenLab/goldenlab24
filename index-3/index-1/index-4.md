# 웹 크롤링 혹은 웹 스크래핑 

`웹 크롤링`이란 컴퓨터 소프트웨어 기술로 웹 사이트들에서 원하는 정보를 추출하는 것을 의미합니다.  
`웹 크롤러`란 인터넷에 있는 웹페이지를 방문해서 자료를 수집하는 일을 하는 프로그램을 말합니다.  

이때 한 페이지만 방문하는 것이 아니라 그 페이지에 링크되어 있는 또 다른 페이지를 차례대로 방문하고 이처럼 링크를 따라 웹을 돌아다니는 모습이 마치 거미와 비슷하다고 해서 `스파이더`라고 부르기도 합니다.  

웹은 기본적으로 HTML 형태로 되어 있습니다.  
해당 정보가 HTML 형태로 어떻게 보여지는지도 '페이지 소스 보기' 또는 '개발자 검사' 로 볼 수 있습니다.  
이런 소스들은 보통 개발자들이 어떤 정형화된 규칙으로 관리하고 있습니다. 이런 `규칙을 분석해서 우리가 원하는 정보들만 뽑아오는 것`을 웹 크롤링 작업이라고 할 수 있습니다. 

## 1. 네이버 크롤링  
* SSR방식은 server-side rendering입니다. 다시 말해, 사용자가 서버에 url을 통해서 request를 보내게 되면 서버에서 구성 요소가 rendering되어 html파일을 그려서 주는 것입니다.  
* CSR방식은 client-side rendering입니다. 이 방식은 서버에서 html을 구성해서 바로 주는것이 아닙니다.  
document를 불러온 사용자측에서 javascript코드를 통해서 엘리먼트의 형식으로 css정보를 나중에 외부 소스로 받는 방식입니다.  
javascript코드를 통해서 html을 사용자가 구성한다는 것입니다.  

1. 일반적인 경우의 크롤링 (SSR) - 네이버 뉴스스탠드, 네이버 웹툰 크롤링  
크롤링을 하기 위해서는 라이브러리가 필요합니다. 가장 기본적인, 웹페이지의 정보를 요청하는 request 라이브러리입니다.    
웹페이지는 사용자에게 html(text)의 형태로 제공되고 따라서, 우리가 정의한 response를 text로 받아올 수 있습니다.   
```
import requests		# requests 라이브러리를 import해온다

# 네이버 메인 페이지를 get method를 통해서 받아온다
response = requests.get('https://www.naver.com') 
print(response.text)
```
2. beautifulsoup이라는 라이브러리를 이용  
위에서 정렬하지 않고 받아온 데이터를 우리가 실질적으로 볼 수 있는 데이터별로 정렬해봅시다.  
아래는 네이버 메인 페이지 중에서 뉴스 스탠트 페이지를 가져오는 코드입니다.  
```
from bs4 import BeautifulSoup as bs

soup = bs(response.text, "html.parser")
presses = soup.select('.thumb_area .thumb') #뉴스를 가져옴
for press in presses:
  print("- Soup 객체: ", press)
  print("- Attrs: ", press.attrs)
  print("- Select One: ", press.select_one("img.news_logo"))
  print("- Attribute: ", press.select_one("img.news_logo").get("src"), press.select_one("img.news_logo").get("alt"))
  print("- Text: ", press.text)
  print()    
```  
  * presses = soup.select('.thumb_area .thumb') 라는 코드를 잘 보면 중요한 사실 두 개를 알 수 있습니다.
    equest와 beautifulsoup를 이용한 크롤링은 css 속성(class, id)를 토대로 정보를 받아옵니다.  
    .thumb_area와 .thumb는 뉴스 스탠드의 클래스 명이다. 이 css속성(attributes, attrs)을 select메서드 뒤에 적어서  
    '네이버'라는 페이지에서 .thumb라는 속성을 가진 요소들을 가져올 수 있게 되는 것입니다. 그래서 출력된 결과값의 - Attrs 내용을 보면  
    class: thumb라고 명시되어있습니다.
  * soup.select는 리스트의 형태로 저장됩니다.  
    바로 밑에 있는 for press in presses는 presses라는 리스트에 있는 엘리먼트 press 각각에 대한 내용을 지정한다는 의미입니다.  
    따라서 우리는 따로 presses의 형태를 지정해주지 않았지만, 리스트의 형태로 반환된다는 것을 알 수 있습니다.   
    
## 2. 네이버 웹툰을 크롤링  
해당 URL에 들어가서 웹툰의 이미지를 클릭해보면, wt_viewer라는 클래스 안에 img형태로 업로드 되어 있다는 것을 알 수 있습니다. 
```
import requests
from bs4 import BeautifulSoup as bs
#사신소년 95화
URL = 'https://comic.naver.com/webtoon/detail.nhn?titleId=730656&no=95&weekday=tue'

res = requests.get(URL)
soup = bs(res.text, 'html.parser')
cut_list = soup.select('.wt_viewer img')
print(cut_list)
```
우리가 볼 수 있는 이미지로 바꾸기 위해서는 ipyplot 모듈이 필요합니다.  
`image_src_list = [cut.get('src') for cut in cut_list]` 는 cut_list에 저장된 cut들마다 src 요소를 get 메서드로 가져옴을 의미합니다.  
그리고 설치하고 불러온 ipyplot을 이용하면 다음과 같이 잘 출력됩니다. 
```
!pip install ipyplot

import ipyplot

image_src_list = [cut.get('src') for cut in cut_list]
print(image_src_list)

ipyplot.plot_images(image_src_list, img_width=100)
```
## 3. CSR방식의 크롤링 - 네이버 스포츠 크롤링  
앞서 소개한 csr방식을 확인하기 위해서 네이버 스포츠 페이지를 크롤링. 
```
URL = "https://sports.news.naver.com/kbaseball/news/index.nhn?isphoto=N&type=latest"
res = requests.get(URL)
soup = bs(res.text, "html.parser")
soup.select("#news_List ul li")
```
네이버 야구의 최신 기사를 가져오기 위해서 css속성이 id=news_List임을 확인했고, 그 하위 태그인 ul 안에 있는 li를 뽑아오는 코드이다.   
그런데 이 코드를 실행하면 빈 리스트가 리턴됩니다.   

해결 방안은 2가지가 있습니다.   
방법1>  
네트워크상에서 데이터를 가져오는 부분을 찾아서 가져오는 방법    
방법2>   
가상의 브라우저를 띄워서 실제 사용자 측에서의 렌더링을 기다린 후 데이터를 가져오는 방법    
  
1. 네트워크상에서 데이터를 가져오는 부분을 찾아서 가져오는 방법    
  * 야구의 최신 기사들을 최신순/인기순을 전환했을 때 새롭게 전송되는 데이터가 우리가 크롤링하고자 하는 야구의 최신 기사 목록입니다. 
  * 인터넷 도구에서 네트워크 탭을 누른 다음 최신순/인기순을 전환해보니 일부분만 새롭게 로드되는 것을 확인할 수 있습니다. 
  * 이 부분을 드래그 하고 밑에 나온 정보를 확인하니, gif와 png등 이미지가 아닌 "xhr"형식의 데이터가 발생한 것을 확인할 수 있습니다.  
  * xhr타입의 데이터의 이름을 우클릭하고 copy-copy as cURL(bash)를 클릭하면 cURL데이터가 복사됩니다. 
  *  이렇게 복사된 cURL 데이터를 파이썬의 requests로 바꿔주는 사이트가 있습니다. `curl.trillworks.com/` 
  이 사이트에 접속해서 curl command에 우리가 복사한 정보를 넣으면 자동으로 Pyton requests로 변환되는데, 
  변환된 requests를 다시 복사해서 코드로 실행시키면 됩니다.  
  
 2. 가상의 브라우저를 띄워서 실제 사용자 측에서의 렌더링을 기다린 후 데이터를 가져오는 방법    
  * selenium 라이브러리가 추가로 필요  
  * 가상 환경을 아래에서 생성하는데에 필요한 요소 설치 

```
!pip install selenium
!apt-get update
!apt install chromium-chromedriver
```
```
from selenium import webdriver

# colab에서 selenium을 돌리기 위한 옵션들
chrome_options = webdriver.ChromeOptions()
chrome_options.add_argument('--headless')
chrome_options.add_argument('--no-sandbox')
chrome_options.add_argument('--disable-dev-shm-usage')
```
```
driver = webdriver.Chrome("chromedriver", options=chrome_options)
driver.get("https://search.naver.com/search.naver?where=image&sm=tab_jum&query=%EB%82%98%EC%84%B1%EB%B2%94")
driver.page_source
```
   * 이미지가 총 몇 장이나 리턴되는지를 알아보기 위한 코드
```
images = driver.find_elements_by_css_selector('.photo_bx .thumb img')
print(images)
print(len(images))
```
   * 이미지를 사진의 형태로 받기 위해서 코드
```
from IPython.core.display import display, HTML

display(HTML(driver.page_source))
```
   * for문으로 PAGE_DOWN을 0.5초 간격으로 총 20번을 실행 PAGE_DOWN이 브라우저에서 스크롤을 내리는 것과 같은 역할. 만약 이 상태에서 한 번 더 같은 코드를 실행하게 되면 아래의 250이라는 숫자가 또 바뀔 것입니다.
수치가 누적되는데, 이미지의 종류에 따라서 일정한 패턴으로 수가 늘어나는 것은 아니다. 이미지 숫자는 500을 넘지 않는데, 이는 네이버 이미지 페이지에서 스크롤을 끝까지 내린다고 가정하더라도 한 번에 500개까지의 이미지만을 보여주기 때문입니다.
```
from selenium.webdriver.common.keys import Keys
import time

body = driver.find_element_by_css_selector('body')

for i in range(20):
    body.send_keys(Keys.PAGE_DOWN)
    time.sleep(0.5)

images = driver.find_elements_by_css_selector('.photo_bx .thumb img')
print(images)
print(len(images))
```
   * 이미지를 사진의 형태로 리스트 작성
```
img_src_list = [img.get_attribute("src") for img in images]
# print(img_src_list)
ipyplot.plot_images(img_src_list, img_width=100, max_images=len(img_src_list))
```

