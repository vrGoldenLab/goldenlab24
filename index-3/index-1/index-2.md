# open API 
표준 웹 프로토콜을 이용하여 프로그램 개발에 사용할 수 있는 공개 API 입니다.  
일반적으로 현실 세계에 있는 실제 데이터를 수집한 단체에서 개발자들이 개발하는 응용에서 사용할 수 있게 제공하고 있습니다.  
이러한 OPEN API에서는 웹 쿼리로 검색 질의를 보내면 XML 문서 형태로 결과를 보내는 것이 일반적입니다.

## 파이썬을 이용한 Naver Open API 활용하기 – 시작하기(도서 검색) 
Naver 검색 API를 이용하여 도서를 검색하는 간단한 콘솔 응용을 제작  
### 1. 등록  
1. 네이버 개발자센터에서  상단 Application 메뉴를 선택하고 팝업된 애플리케이션 등록을 선택하세요.   
2. 애플리케이션 이름을 정하고 사용 API 중에서 검색을 선택하세요.
3. 환경추가에서 WEB설정을 선택하시고 웹 서비스 URL을 입력하세요.
4. 만약 웹 서비스 URL을 소유하고 있는 것이 없다면 http://sample.co.kr로 입력합니다.
5. 등록하기 버튼을 클릭합니다.
6. Open API를 사용하기 위해 발급한 ClientID와 ClientSecret을 확인할 수 있습니다.
7. 네이버 개발자 센터의 [Document]=>서비스 API [검색]을 선택하세요.
8. Open API는 XML 출력포멧 혹은 JSON 출력포멧으로 결과를 제공하고 있는데 이번 게시글에서는 json 출력포멧을 이용할 것입니다. 요청 URL 주소를 기록해 두세요.

### 2. 사용 
1. urllib.request를 임포트
2. 애플리케이션의 클라이언트 ID와 secret을 변수에 설정
```
#애플리케이션 클라이언트 id 및 secret
client_id = "[자신의 client id]"
client_secret = "[자신의 client secret]"
``` 
  3. 도서 검색 url과 옵션을 설정하세요.
  ```
url = "https://openapi.naver.com/v1/search/book.json"
option = "&display=3&sort=count"
```   
  4. 사용자로부터 입력받은 질의를 쿼리 문자열에 맞게 변환하세요.
```
query = "?query="+urllib.parse.quote(input("질의:"))
```
  5. 도서 검색 url과 검색 질의 및 옵션을 하나의 쿼리 문자열로 설정합니다.
```
url_query = url + query + option
```
  6. Open API에 검색 요청을 위한 개체를 설정합니다.
  검색 요청을 위해 쿼리 문자열을 입력 인자로 Request 개체를 생성한 후에 클라이언트 id와 클라이언트 secret을 헤더에 추가합니다.
  ```
#Open API 검색 요청 개체 설정
request = urllib.request.Request(url_query)
request.add_header("X-Naver-Client-Id",client_id)
request.add_header("X-Naver-Client-Secret",client_secret)
```
  7. 검색을 요청하고 검색 결과의 내용을 얻어와서 화면에 출력합니다.
```
#검색 요청 및 처리
response = urllib.request.urlopen(request)
rescode = response.getcode()
```
  8. 검색 요청한 결과가 200이면 정상적으로 성공한 것입니다.
```
if(rescode == 200):
 
    response_body = response.read()
 
    print(response_body.decode('utf-8'))
 
else:
 
    print("Error code:"+rescode)
```



네이버 책 검색 결과를 출력해주는 REST API [https://developers.naver.com/docs/search/book/](https://developers.naver.com/docs/search/book/)
