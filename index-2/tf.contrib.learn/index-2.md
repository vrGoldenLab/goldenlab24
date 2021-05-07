# Colab Turtle

\(v1.0\)

터틀 그래픽스(Turtle graphics) 모듈을 사용해서 간단한 그림을 그려보겠습니다.  
터틀은 어린이 및 초보자가 파이썬을 쉽게 배울 수 있도록 만든 모듈인데, 거북이가 기어가는 모양대로 그림을 그린다고 해서 터틀이라고 합니다.  
터틀은 그림을 그리는 모듈이므로 Windows, 리눅스, macOS 그래픽 환경에서만 동작합니다.  

* 터틀 명령어 링크: [https://python.flowdas.com/library/turtle.html](https://python.flowdas.com/library/turtle.html)

코랩에서는 그래픽을 사용하기 위한 colab turtle 라이브러리를 사용해야 합니다.
```
!pip3 install ColabTurtle
from ColabTurtle.Turtle import *
import ColabTurtle.Turtle as a
```
1. 그리기 이동
* 화면을 새로 고침
* 색을 파랑으로 변경
* 앞으로 100만큼 이동
* 오른쪽으로 45도 회전
* 색을 빨강으로 변경
* 앞으로 50만큼 이동

```
a.initializeTurtle(initial_speed=5) 
a.color('blue')
a.forward(100)
a.right(45)
a.color('red')
a.forward(50)
```
* colab 사용실습: [https://colab.research.google.com/drive/1Yq-JOQxNfNMMkfXWL1vRVBlQav-7QeKo?usp=sharing](https://colab.research.google.com/drive/1Yq-JOQxNfNMMkfXWL1vRVBlQav-7QeKo?usp=sharing)
