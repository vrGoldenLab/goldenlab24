# 모듈과 패키지 
`참고자료`: [https://docs.python.org/ko/3/tutorial/modules.html](https://docs.python.org/ko/3/tutorial/modules.html)

모듈(module) : 각종 변수, 함수, 클래스를 담고 있는 파일이다. 특정 기능을 .py 파일 단위로 작성한 것입니다.

패키지(package) : 여러 모듈을 묶은 것이다. 패키지는 모듈에 네임스페이스(namespace, 이름공간)를 제공합니다.

파이썬 표준 라이브러리(Python Standard Library, PSL) : 파이썬에 기본으로 설치된 모듈과 패키지, 내장 함수등이 있습니다.

## 1. import로 모듈 가져오기
모듈을 여러 개 가져올 때는 모듈을 콤마로 구분합니다.

`import 모듈  
import 모듈1, 모듈2  
모듈.변수  
모듈.함수()  
모듈.클래스()`
