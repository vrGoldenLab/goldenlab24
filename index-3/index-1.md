# 깃허브와 COLAB 연동하기

## 1. 깃허브 REPOSITORY를 주소 복사
Clone하기 위한 깃허브 repository의 url을 복사합니다.  
깃허브 repository 우측 초록색 code 버튼을 클릭한 후 url을 복사합니다.  

## 2. 드라이브 마운트(Drive Mount)   
이제 colab 페이지를 하나 열고 내 드라이브와 연동해봅시다.
colab의 좌측 폴더 모양을 누르면 드라이브가 마운트됩니다.
또는 아래의 명렬어를 코드셀에서 실행합니다.
```
from google.colab import drive
drive.mount('/content/drive')
```
코랩을 이용할 때 항상 습관적으로 먼저 실행해주어야 하는 드라이브 마운트 기능! 코랩 사이트 내 드라이브 버튼을 누르면 위 코드가 자동으로 뜨게 됩니다.   

## 3. 드라이브 경로로 이동
다음으로 소스 코드를 받아올 경로로 이동합니다.
```
cd "/content/drive/My Drive/작업폴더"
```
## 4. git clone 
복사된 url을 colab 코드셀에서 다음과 같은 clone 명령어를 입력합니다. 
```
!git clone url주소 
```

## 5. 드라이브 데이터 확인
구글 드라이브 폴더에 데이터가 잘 들어가 있는지 확인합니다.

### 이 방법을 알아둔다면, 로컬에서 클론하고 다시 드라이브로 옮길 필요 없이 코랩으로 실행하고픈 코드를 바로 바로 드라이브에 불러올 수 있습니다. 

## < colab 실습 >
깃허브와 colab 클론: [https://colab.research.google.com/drive/1gGpXU4X7IDk-J7Bog7d0xY3kbF8ZbDud?usp=sharing](https://colab.research.google.com/drive/1gGpXU4X7IDk-J7Bog7d0xY3kbF8ZbDud?usp=sharing)
