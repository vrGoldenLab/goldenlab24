# 공공데이터 활용

* 데이터 분석 
  `문제 정의` - `데이터정의` - `데이터 수집` - `데이터 전처리` - `데이터 시각화` 

## 1. 서울시 온도로 데이터 분석 
* 문제 정의 - 내가 살고 있는 지역의 온도 변화. 봄이 짧아지고 있나?
* 데이터 정의 - 어떤 데이터가 필요할까? 연도별 데이터로 분석가 필요!!
* 데이터 수집 - 기상청 공공데이터를 찾아봅시다

## 2. 데이터 수집 
* 기상자료개방포털(기상청): [https://data.kma.go.kr/](https://data.kma.go.kr/)
* 기상자료개방포털 > 기후통계분석 > 기온분석 메뉴 사용
* 검색 조건을 입력한 후 검색
* csv 파일로 다운로드
* 데이터 파일을 필요한 형태로 정제
  * 엑셀에서 다운로드 파일 열기
    <center><img src="https://github.com/vrGoldenLab/goldenlab24/blob/master/gdata/images/172.png" width="500" height="300"></center>    
  * 불필요한 부분 삭제  
  * 헤더 수정  
  
    ![173](https://github.com/vrGoldenLab/goldenlab24/blob/master/gdata/images/173.png) 
  * 파일형식을 csv utf-8(쉼표로 분리)로 선택하여 다른이른으로 저장합니다.
    <center><img src="https://github.com/vrGoldenLab/goldenlab24/blob/master/gdata/images/176.png" width="600" height="150"></center>  
  * 구글드라이브에 업로드  
      
## 3. 데이터 확인   
* colab 에서 데이터 파일 불러오기    
  `import pandas as pd`    
  `df = pd.read_csv('파일경로/파일명.csv')`    
  `df`    
* colab 폴더에서 파일명을 더블클릭 하면 데이터 내용을 볼 수 있습니다.   
 ![183](https://github.com/vrGoldenLab/goldenlab24/blob/master/gdata/images/183.png)  
## 4. pandas 데이터 정보 확인  
* head() : 불러온 데이터 상위 n행을 출력합니다. 빈 채로 출력하면 디폴트 5개를 출력합니다.  

  <img src="https://github.com/vrGoldenLab/goldenlab24/blob/master/gdata/images/187.png" width="300" height="200">   
  
  <img src="https://github.com/vrGoldenLab/goldenlab24/blob/master/gdata/images/188.png" width="300" height="500"> 
* describe() : 컬럼 별 통계량을 출력합니다.    
  ![192](https://github.com/vrGoldenLab/goldenlab24/blob/master/gdata/images/192.png)  
* info() : 행과 열의 크기, 컬럼명, 컬럼을 구성하는 값의 자료형 등을 출력합니다.

  <center><img src="https://github.com/vrGoldenLab/goldenlab24/blob/master/gdata/images/193.png" width="300" height="300"></center>  
  
   Null 값(결측치)이 포함된 것을 알 수 있습니다.  
* isnull( ) : 빈 값에 True를 출력합니다.  
  <center><img src="https://github.com/vrGoldenLab/goldenlab24/blob/master/gdata/images/197.png" width="500" height="300"></center> 
*  isnull( ).sum( ) : 컬럼 별 빈 값 개수를 출력합니다.  
  <center><img src="https://github.com/vrGoldenLab/goldenlab24/blob/master/gdata/images/198.png" width="500" height="150"></center>   

* mean( )함수로 해당 컬럼의 평균값을 구할 수 있습니다.  
  <center><img src="https://github.com/vrGoldenLab/goldenlab24/blob/master/gdata/images/199.png" width="500" height="150"></center> 


