# 머릿말



### **1. Colab이란?**

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



구글의 CPU, RAM, GPU를 사용해서 Jupiter Notebook과 같은 환경을 구성

Colaboratory는 Google 리서치팀에서 개발한 제품입니다.

Colab을 사용하면 누구나 브라우저를 통해 임의의 Python 코드를 작성하고 실행할 수 있습니다.

Colab은 특히 머신러닝, 데이터 분석 및 교육에 적합합니다.

Colab은 설정 없이도 사용 가능한 호스팅 Jupyter 메모장 서비스로, GPU를 포함한 컴퓨팅 리소스를 무료로 제공합니다.

#### colab 주의 사항

* 구글 계정 필요
* 최대 세션 유지 시간 존재\(12시간\)
* 세션이 종료되면 결과값,데이터 모두 삭제
* 소스코드는 구글 드라이브에 저장



깃허브의 주소는 [https://github.com/tensorflowkorea/tensorflow-kr](https://github.com/tensorflowkorea/tensorflow-kr) 입니다.

깃북의 주소는 [https://tensorflowkorea.gitbooks.io/tensorflow-kr](https://tensorflowkorea.gitbooks.io/tensorflow-kr) 입니다.

깃허브의 작업 방법에 대해서는 [블로그 포스팅](https://tensorflowkorea.wordpress.com/2016/06/01/텐서플로우-문서-한글화/)을 참고해 주세요.

감사합니다.

## 번역 및 마크다운 참고사항

### 번역 범위

현재 텐서플로우는 버전이 빠르게 변하고 있어서 API 문서가 자주 변경됩니다. 따라서 가능하시면 api\_docs 폴더 이외의 다른 문서를 먼저 번역하는 것이 합리적으로 생각됩니다. 각 폴더별 번역 진행 상황은 [@hunkim](https://github.com/hunkim) 님께서 작업해 주신 [progress.md](https://github.com/vrGoldenLab/goldenlab24/tree/d859d22cada0135c05e5d5250453b38ae07fadcc/progress.md) 파일을 참고해 주세요. api\_docs 문서를 제외하고 번역이 완료되면 몇명이서 전체 번역을 다듬으려고 합니다. 이 때 필요한 자원봉사자를 페이스북 텐서플로우 그룹을 통해 신청받으려고 합니다.

### 버전 관리 안내

텐서플로우 버전이 업데이트 되면서 번역된 문서 간의 버전 차이가 있을 수 있습니다. master 브랜치에는 v0.9의 영문 문서가 들어가 있습니다. 그리고 master 브랜치외에 r0.9, r0.10 두개의 브랜치가 추가 되었습니다. 각각 v0.9, v0.10의 영문 문서가 담겨 있습니다. 두개의 브랜치를 비교하면서 기 번역된 문서를 업데이트 하거나 새로운 번역 문서를 추가할 수 있습니다.

master 브랜치의 번역 문서는 아래와 같이 번역된 버전을 제목 아래에 적어 주십시요. 만약 버전이 적혀있지 않을 경우에는 v0.9로 간주합니다.

```text
# 순환 신경망(Recurrent Neural Networks)
(v0.9)
```

### 아래 pip-installation의 경우처럼 페이지내 이동을 위해서 네임드 앵커 태그가 없이 사용만 되는 경우가 있습니다.

```text
*  [Pip 설치](#pip-installation): 이 방식으로 텐서플로우를 설치하거나 업그레이드할 때는
   이 전에 작성했던 파이썬 프로그램에 영향을 미칠 수 있습니다.
```

이럴 때에는 pip-installation 이 가리키는 위치에 네임드 앵커 태그를 넣어주시면 됩니다.

```text
...
<a id="pip-installation"></a>
## Pip Installation
...
```

