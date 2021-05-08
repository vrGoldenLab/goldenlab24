# 정규 표현식 살펴보기

주민등록번호를 포함하고 있는 텍스트가 있다. 이 텍스트에 포함된 모든 주민등록번호의 뒷자리를 * 문자로 변경해 보자.
우선 정규식을 전혀 모르면 다음과 같은 순서로 프로그램을 작성해야 할 것이다.

정규식을 사용하면 다음처럼 훨씬 간편하고 직관적인 코드를 작성할 수 있습니다.
```
import re 

data = """
park 800905-1049118
kim  700905-1059119
"""

pat = re.compile("(\d{6})[-]\d{7}")
print(pat.sub("\g<1>-*******", data))
```
## 파이썬에서 정규 표현식을 지원하는 re 모듈
re.compile을 사용하여 정규 표현식(예제에서는 a-z)을 컴파일합니다.  
```
import re
p = re.compile('[a-z]+')

m = p.match("python") #  a-z 이므로 매치
print(m)
m = p.match("3 python") # 숫자 포함이므로 None
```

match()	문자열의 처음부터 정규식과 매치되는지 조사합니다.
search()	문자열 전체를 검색하여 정규식과 매치되는지 조사합니다.
findall()	정규식과 매치되는 모든 문자열(substring)을 리스트로 돌려줍니다.
finditer()	정규식과 매치되는 모든 문자열(substring)을 반복 가능한 객체로 돌려줍니다.  

## 자주 사용되는 정규식

* \d - 숫자와 매치, [0-9]와 동일한 표현식.
* \D - 숫자가 아닌 것과 매치, [^0-9]와 동일한 표현식.
* \s - whitespace 문자와 매치, [ \t\n\r\f\v]와 동일한 표현식. 맨 앞의 빈 칸은 공백문자(space)를 의미.
* \S - whitespace 문자가 아닌 것과 매치, [^ \t\n\r\f\v]와 동일한 표현식.
* \w - 문자+숫자(alphanumeric)와 매치, [a-zA-Z0-9_]와 동일한 표현식.
* \W - 문자+숫자(alphanumeric)가 아닌 문자와 매치, [^a-zA-Z0-9_]와 동일한 표현식. 


## Dot(.)
```
a.b
```
즉 a와 b라는 문자 사이에 어떤 문자가 들어가도 모두 매치된다는 의미이다.  

## 반복  *,+

## * \b
```
p = re.compile(r'\bclass\b')
print(p.search('no class at all'))  
```
<re.Match object; span=(3, 8), match='class'>  

\b는 단어 구분자(Word boundary)입니다. 보통 단어는 whitespace에 의해 구분됩니다.  
\bclass\b 정규식은 앞뒤가 whitespace로 구분된 class라는 단어와 매치됨을 의미합니다. 
따라서 no class at all의 class라는 단어와 매치됨을 확인할 수 있습니다.

```
print(p.search('the declassified algorithm'))
print(p.search('one subclass is'))
```
모두 매치되지 않고 none

## \B
\B 메타 문자는 \b 메타 문자와 반대의 경우입니다. 즉 whitespace로 구분된 단어가 아닌 경우에만 매치됩니다.
```
p = re.compile(r'\Bclass\B')
print(p.search('no class at all')) 
```
None
```
print(p.search('the declassified algorithm'))
```
<re.Match object; span=(6, 11), match='class'>
```
 print(p.search('one subclass is'))
```
None

## 그루핑
문자열이 계속해서 반복되는지 조사하는 정규식을 작성시 사용됩니다.  
그룹을 만들어 주는 메타 문자는 바로 ( )이다.
```
p = re.compile('(ABC)+')
m = p.search('ABCABCABC OK?')
print(m)
```
<re.Match object; span=(0, 9), match='ABCABCABC'>
```
print(m.group())
```
ABCABCABC

### 그룹을 사용하는 보다 큰 이유는 위에서 볼 수 있듯이 매치된 문자열 중에서 특정 부분의 문자열만 뽑아내기 위해서인 경우가 더 많습니다.
```
p = re.compile(r"\w+\s+\d+[-]\d+[-]\d+")
m = p.search("park 010-1234-1234")
```
\w+\s+\d+[-]\d+[-]\d+은 이름 + " " + 전화번호 형태의 문자열을 찾는 정규식입니다.

위 예에서 만약 ‘이름’ 부분만 뽑아내려 한다면 다음과 같이 할 수 있습니다.
```
p = re.compile(r"(\w+)\s+\d+[-]\d+[-]\d+")
m = p.search("park 010-1234-1234")
print(m.group(1))
```
#### park


\w+ 부분을 그룹 (\w+)으로 만들면 match 객체의 group(인덱스) 메서드를 사용하여 그루핑된 부분의 문자열만 뽑아낼 수 있습니다.

|group(인덱스)|	설명|
|:---:|:---:|
|group(0)|	매치된 전체 문자열|
|group(1)|	첫 번째 그룹에 해당되는 문자열|
|group(2)|	두 번째 그룹에 해당되는 문자열|
|group(n)|	n 번째 그룹에 해당되는 문자열|
```
p = re.compile(r"(\w+)\s+(\d+[-]\d+[-]\d+)")
m = p.search("park 010-1234-1234")
print(m.group(2))
```
#### 010-1234-1234
전화번호 부분을 추가로 그룹 (\d+[-]\d+[-]\d+)로 만들었습니다. 이렇게 group(2) 사용.
```
p = re.compile(r"(\w+)\s+((\d+)[-]\d+[-]\d+)")
m = p.search("park 010-1234-1234")
print(m.group(3))
```
### 010
위 예에서 볼 수 있듯이 (\w+)\s+((\d+)[-]\d+[-]\d+)처럼 그룹을 중첩되게 사용하는 것도 가능. 그룹이 중첩되어 있는 경우는 바깥쪽부터 시작하여 안쪽으로 들어갈수록 인덱스가 증가합니다.

