# 마크다운(Markdown) 사용하기  

  특수기호와 문자를 이용한 매우 간단한 구조의 문법을 사용
  웹에서 보다 빠르게 컨텐츠를 작성
  일반 텍스트로 서식이 있는 문서를 작성하는 데 사용되며, 일반 마크업 언어에 비해 문법이 쉽고 간단한 것이 특징이다.
  HTML과 리치 텍스트(RTF) 등 서식 문서로 쉽게 변환되기 때문에 응용 소프트웨어와 함께 배포되는 README 파일이나 온라인 게시물 등에 많이 사용된다.

  마크다운 위키백과 [https://ko.wikipedia.org/wiki/%EB%A7%88%ED%81%AC%EB%8B%A4%EC%9A%B4](https://ko.wikipedia.org/wiki/%EB%A7%88%ED%81%AC%EB%8B%A4%EC%9A%B4)  

1. 제목 표시 

  * 큰제목
  ```
     This is a Title
     ================
  ```
     This is a Title
     ================
 
 * 작은 제목
 ```
    This is a Title
    -----------------
 ```
    This is a Title 
    -----------------
    
* 말머리 표기  
```
  # This is a H1
  ## This is a H2
  ### This is a H3
  #### This is a H4
  ##### This is a H5
  ###### This is a H6  
``` 
  # This is a H1
  ## This is a H2
  ### This is a H3
  #### This is a H4
  ##### This is a H5
  ###### This is a H6  

2. 블록
```
  > This is a first blockqute.
  >    > This is a second blockqute.
  >    >    > This is a third blockqute. 
```
  > This is a first blockqute.
  >    > This is a second blockqute.
  >    >    > This is a third blockqute.  
 
3.  순서 있는 목록  

 > 숫자와 점을 사용
```
    1. 첫번째
    2. 두번째
    3. 세번째
```   
    1. 첫번째
    2. 두번째
    3. 세번째
```
첫번째
두번째
세번째
```
첫번째
두번째
세번째
 

4. 순서없는 목록
    글머리 기호: *, +, - 지원
```
* 빨강
 * 녹색
   * 파랑
 
+ 빨강
 + 녹색
   + 파랑
 
- 빨강
   - 녹색
    - 파랑
```
* 빨강
 * 녹색
   * 파랑
 
+ 빨강
 + 녹색
   + 파랑
 
- 빨강
   - 녹색
    - 파랑

5.  구분선 

```
* * *
 
***
 
*****
 
- - -
--------------------------------------
``` 
* * *
 
***
 
*****
 
- - -
--------------------------------------  

6.  링크
```
[링크 텍스트](https://)   
[Google](https://google.com, "google link") 
```
[링크 텍스트](https://)   
[Google](https://google.com, "google link") 

7.  줄바꿈
  * 3칸 이상 띄어쓰기( )를 하면 줄이 바뀐다.