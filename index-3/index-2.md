# fastpages에서 블로그 시작하기
Github Pages를 활용하여 기술블로그를 운영하기 위해서는 몇 가지 난관이 있습니다. 
자료를 찾아보면 주로 Jekyll, Hugo, Hexo, Gatsby.JS 와 같이 낯설고 어려운 프레임워크을 사용해야 합니다.  
커스터마이징을 하거나 기능을 추가하기 위해서는 html, CSS 또는 NodeJS 같은 프레임워크를 알아야 합니다.  
그래서 간단하고 쉬운 플랫폼이 시간을 절약해 주기도 합니다.
심플하게 기본만 딱 하는 테마로 fastpages가 있습니다.

## 장점
* 기존의 방식과 같이 markdown(.md) 파일로 블로그 포스트를 작성할 수 있습니다.
* jupyter notebook(.ipynb) 파일까지도 그대로 블로그 포스트로 변환해 줍니다.
* word 파일까지도 블로그 포스트로 변환해 줍니다.
* 다른 프레임워크 기반 명령어가 따로 필요 없이, 그저 add, commit, push 명령어만으로 포스트를 간편하게 업데이트할 수 있습니다. 
나머지는 Github Action을 배포과정 알아서 진행하기 때문입니다.

## 만들기 

1. fastpages 블로그용 레포지토리 생성
 fastpages 공식 레포지토리에서 Use this template 버튼을 클릭하고 새로운 레포지토리를 생성합니다. 
 이때, 레포지토리의 이름은 아무것이나 정해되 상관 없되, {계정명}.github.io는 피해야 합니다.  

2. 새로운 Pull Request가 자동으로 생성
 “Initial Setup”이라는 새로운 Pull Request가 자동으로 생성된 것을 확인할 수 있습니다.  

3. PR 가이드  
* this utility (새탭으로 열기) 에서 prive key와 public 키를 생성합니다. 이때, 옵션은 RSA와 4069를 선택 후 “Generate SSH-Keys” 버튼을 클릭합니다.  
* 두번째 주어진 링크에서 새 “New repository secret” 버튼을 클릭합니다. 
 Value 입력 칸에 앞서 생성한 Private key 전체를 복사하여 붙여넣습니다. Name 입력 칸에는 `SSH_DEPLOY_KEY`라고 입력하고 저장합니다.   
* 세번째 링크에서는 “Add deploy key” 버튼을 클릭합니다.  
앞서 생성한 Public key를 복사하여 붙여넣습니다. 이름은 아무렇게나 지정해도 된다고 합니다. 그리고 제일 아래 `Allow write access` 박스를 꼭 체크합니다.  
* PR을 merge합니다. 이후 fastpages 블로그가 배포되는 과정은 Github actions에서 아래와 같이 확인할 수 있습니다.    

4. 완료  
 완료되면, {github username}.github.io/{레포지토리 이름} 에서 fastpages 기반의 블로그가 배포되었음을 확인할 수 있습니다.

---

## fastpages를 통해서 블로그를 작성하기 위해서는 다음 파일들에 대해서 알아두어야 합니다. 
* _config.yml: 블로그의 이름, Latex사용 여부, 미리보기 여부, 태그 보여주기 여부 등을 설정할 수 있는 파일입니다. 
자신의 SNS계정 버튼도 추가할 수 있고, description, pagination의 갯수 등의 사항들도 설정할 수 있습니다.  
* index.html: 블로그 메인 페이지에 보여지는 컨텐츠를 작성하는 파일입니다.   
* _pages/about.md: 블로그의 자기소개 페이지 About페이지의 내용을 작성하는 파일입니다. markdown 포맷으로 작성하면 됩니다.  
* 포스트를 저장하는 디렉토리는 다음 종류에 따라 달라지므로 디렉토리를 구분해서 작성하시면 됩니다. (_notebooks/ , _posts/ , _word/ , images/ )

##  YYYY-mm-dd-{아무 이름} 형태로 작성되어야 fastpages가 이를 인식하고 파일을 html로 변환합니다.  


