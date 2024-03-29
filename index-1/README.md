# colab 시작하기

## **1. Colab이란?**
* 구글 클라우드 기반의 무료 개발 환경 서비스 
* 환경 설정 및 실행까지 매우 빠른 환결
* 딥러닝 실행이 가능한 고사양 환경 제공
* Jupyter Notebook 환경 제공
* 대부분의 패키지들이 이미 설치된 환경 
* 여러 사용자와 동시에 사용 가능
* PC,태블릿,모바일 상관없이 인터넷 브라우저만 있으면 사용 가능
* 목차나 Markdown 미리보기 등 다양한 기능 제공
* 구글 드라이브와 연동
* Git,Github와 쉽게 연동  
   
### 구글에서 만든 Colaboratory는 클라우드 기반의 개발환경  
``` 
구글의 CPU, RAM, GPU를 사용해서 Jupiter Notebook과 같은 환경을 구성
Colaboratory는 Google 리서치팀에서 개발한 제품입니다.
Colab을 사용하면 누구나 브라우저를 통해 임의의 Python 코드를 작성하고 실행할 수 있습니다.  
Colab은 특히 머신러닝, 데이터 분석 및 교육에 적합합니다. 
Colab은 설정 없이도 사용 가능한 호스팅 Jupyter 메모장 서비스로, GPU를 포함한 컴퓨팅 리소스를 무료로 제공합니다.  
```

### colab 주의 사항  
  
* 구글 계정 필요
* 최대 세션 유지 시간 존재(12시간)
* 세션이 종료되면 결과값,데이터 모두 삭제
* 소스코드는 구글 드라이브에  저장 


## **2. Colab 연결하기**

*   구글 드라이브로 이동
*   구글 드라이브내 마우스 오른쪽 클릭(새로만들기) -> 연결할 앱 더보기   

*   colab을 검색하여 설치합니다 
*   다시 구글 드라이브로 돌아가 마우스 오른쪽버튼을 클릭(새로만들기)하면 Google Colaboratory를 확인 할 수 있습니다.  
  

## **3. GPU,TPU 사용하기**  
런타임 유형 변경(Change runtime type) 필요  
None : CPU만 사용  
GPU:하드웨어 가속으로 GPU(graphics processing unit)사용  
TPU:하드웨어 가속으로 TPU(Tensor Processing Unit)사용
COLAB 상단 선택메뉴 중 런타임 -> 런타임 유형 변경에서 사용합니다.
하드웨어 가속기 -> GPU,TPU 선택 후 저장하면 됩니다.
클라우드 환경이고 구글의 무료 자원을 사용하기 때문에 GPU,TPU를 무한정 사용할 수는 없습니다. Keras나 Tensorflow등을 사용할 때 사용합니다.

## **4. Google `Drive`와 연결**
### Drive Mount

* 방법 1  
좌측의 메뉴에서 폴더 모양을 선택   
드라이브 마운트 버튼을 클릭합니다.  
노트북이 google 드라이브 파일에 엑세스 허용 질문에 드라이브 연결을 선택합니다.  
본인의 Google Drive 경로로 이동합니다.    
 
* 방법 2
구글드라이브 마운트 명령어를 입력합니다.  
```
from google.colab import drive
drive.mount('/content/drive')
```

명령어 실행 후 화면에 표시된 링크로 접속합니다.  
연결할 구글 아이디로 로그인을 하고 허용을 누릅니다  
드라이브 마운트 허용코드를 복사합니다 (화면 코드옆 복사버튼 사용)  
Authorization Code 입력 부분에 붙여넣기 후 엔터를 치면 연결됩니다  

## **5.코랩 `단축키`**(ctrl+m,h)

*   선택된 셀을 실행 : Ctrl + Enter
*   선택된 셀을 실행 후 다음 셀로 포커스 이동 : Shift + Enter
*   실행 후 다음줄로 이동 : Alt + Enter
*   선택모드에서 화살표 방향키 : 셀 포커스를 위 아래로 움직일 수 있음
*   마크다운으로 전환 : Ctrl + M M
*   코드로 전환 : Ctrl + M Y
*   저장 : Ctrl + S
*   코드셀에 줄번호 부여 : Ctrl + M L
*   바로 윗줄에 셀 생성 : Ctrl + M A
*   바로 아랫줄에 셀 생성 : Ctrl + M B
*   셀 삭제 : Ctrl + M D
*   셀 병합 : (shift를 누른 상태에서 병합을 원하는 셀들을 한번에 다중 선택 후), Shift + M
*   셀 분할 : (분기를 원하는 부분에 커서를 지정 후), Ctrl + Shift + -
*   코드가 오래 실행되어 멈추고 싶은경우 : Ctrl+ M + I

## **`6.Jupyter Notebook`** 

* IPython Shell 브라우저 기반 그래픽 인터페이스
* 파이썬과 IPython문장 실행
* 서식 있는 텍스트와 정적/동적 시각화, 수학 공식 표현  

  `.ipynb` 확장자를 가진 파일은 주피터 노트북 파일입니다. 이 책은 일반적인 파이썬 스크립트(`.py`)대신 주피터 노트북을 사용합니다. 
    주피터 노트북은 데이터 분석 프로젝트에서 아주 잘 맞습니다. 
    코드와 실행 결과, 그래프, 수식을 포함한 막다운(Markdown) 문서를 모두 한 파일에 저장할 수 있습니다!



 
## Recommended Next Steps

* [파이썬 다운로드 및 설치](os_setup.md)
* [기본적인 사용법](basic_usage.md)
* [파이썬](https://www.python.org/)


