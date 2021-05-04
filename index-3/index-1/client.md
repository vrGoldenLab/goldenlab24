# 그래프 실행

\[TOC\]

이 라이브러리는 그래프를 시작하고 연산을 실행하기 위한 클래스를 포함하고 있습니다.

[basic usage](../../index-1/#basic-usage)가이드에는 [`tf.Session`](client.md#Session)에서 그래프가 어떻게 시작되는지에 대한 예시들이 있습니다.

## 세션 관리

### `class tf.Session` <a id="Session"></a>

TensorFlow 연산들을 실행하기 위한 클래스입니다.

`Session` 객체는 `Operation` 객체가 실행되고 `Tensor` 객체가 계산되는 환경을 캡슐화합니다. 예를 들면

```python
# 그래프를 만듭니다.
a = tf.constant(5.0)
b = tf.constant(6.0)
c = a * b

# 세션에서 그래프를 시작합니다.
sess = tf.Session()

# 텐서 `c`를 계산합니다.
print(sess.run(c))
```

세션은 [변수](state_ops.md#Variable), [큐](io_ops.md#QueueBase)그리고 [리더](io_ops.md#ReaderBase)같은 자체 리소스를 가질 것입니다. 이 리소스들이 더 이상 필요하지 않을 때 이를 해제시키는건 중요합니다. 이를 위해선, 세션에서 [`close()`](client.md#Session.close)메서드를 실행하거나 컨텍스트 매니저로써 세션을 사용해야합니다. 다음의 두 예시는 동일합니다.

```python
# `close()`메서드를 사용합니다.
sess = tf.Session()
sess.run(...)
sess.close()

# 컨텍스트 매니저를 사용합니다.
with tf.Session() as sess:
  sess.run(...)
```

\[`ConfigProto`\] \([https://www.tensorflow.org/code/tensorflow/core/protobuf/config.proto](https://www.tensorflow.org/code/tensorflow/core/protobuf/config.proto)\) 프로토콜 버퍼는 세션을 위한 여러가지 설정 옵션을 제공합니다. 예를 들면, 디바이스 위치에 대해 유연한 제약 조건을 사용하고 위치 결정 결과를 로깅하기위해 다음과 같이 세션을 생성합니다:

```python
# 유연한 디바이스 위치와 위치 결정 로깅을 사용하는 세션에서 그래프를 시작합니다.
sess = tf.Session(config=tf.ConfigProto(allow_soft_placement=True,
                                        log_device_placement=True))
```

#### `tf.Session.__init__(target='', graph=None, config=None)` <a id="Session.__init__"></a>

새로운 TensorFlow 세션을 생성합니다.

세션을 생성할 때 `graph` 인자가 지정되지 않으면, 세션에선 기본 그래프가 시작됩니다. 만약 같은 프로세스에서 `tf.Graph()`로 생성되는 그래프를 하나 이상 사용한다면, 각 그래프에 대해서 서로 다른 세션을 사용해야 할 것입니다. 그러나 각 그래프는 여러 세션에서 사용될 수 있습니다. 이 경우에는 때때로 세션 생성자에 그래프가 시작된다는걸 명시적으로 전달하는게 깔끔합니다.

**인자:**

* **`target`**: \(선택\) 접속을 위한 실행 엔진. 기본값으로 프로세스 내부 엔진을 사용합니다. 지금은, 빈 문자열 이외의 값은 지원되지 않습니다.
* **`graph`**: \(선택\) 시작되는 `Graph` \(위에서 설명됨\).
* **`config`**: \(선택\) 세션을 위한 설정 옵션을 가진 [`ConfigProto`](https://www.tensorflow.org/code/tensorflow/core/protobuf/config.proto) 프로토콜 버퍼.

#### `tf.Session.run(fetches, feed_dict=None, options=None, run_metadata=None)` <a id="Session.run"></a>

`fetches`에서 연산과 텐서를 실행합니다.

이 메서드는 모든 `Operation`들과 `fetches`에 있는 모든 `Tensor`들을 실행하기위해 꼭 필요한 그래프 단편을 실행하면서 TensorFlow 계산을 한 스텝씩 실행하고, 입력값들에 대한 `feed_dict`의 값들을 교체합니다.

`fetches`인자는 단일 그래프 요소, 그래프 요소들의 리스트 또는 위의 값들의 딕셔너리가 될 수 있습니다. `fetches`의 타입은 이 메서드의 반환값들 결정합니다. 그래프 요소는 다음 타입중 하나가 될 수 있습니다.

* `fetches`의 요소가 [`Operation`](framework.md#Operation)일 때, 해당 패치값은 `None`이 될 것입니다.
* `fetches`의 요소가 [`Tensor`](framework.md#Tensor)일 때, 해당 패치값은 텐서값을 포함하는 numpy ndarray가 될 것입니다.
* `fetches`의 요소가 [`SparseTensor`](sparse_ops.md#SparseTensor)일 때, 해당 패치값은 희소 텐서의 값을 포함하는 [`SparseTensorValue`](sparse_ops.md#SparseTensorValue)가 될 것입니다.
* `fetches`의 요소가 `get_tensor_handle` 연산에의해 생성되었을 경우, 해당 패치값은 텐서의 처리를 포함하는 numpy ndarray가 될 것 입니다. 

선택적인 `feed_dict` 인자는 그래프의 텐서의 값들을 덮어씌울 수 있도록 해줍니다. `feed_dict`의 각 키들은 다음 타입중 하나가 될 수 있습니다.

* 키가 [`Tensor`](framework.md#Tensor)라면, 값은 텐서와 같은 `dtype`으로 변환될 수 있는 Python 스칼라, 문자열, 리스트 또는 numpy ndarray가 될 것입니다. 추가적으로, 키가 [placeholder](io_ops.md#placeholder)라면, 값의 구조\(shape\)가 플레이스홀더\(placeholder\)와 호환되는지 확인될 것입니다.
* 키가 [`SparseTensor`](sparse_ops.md#SparseTensor)라면, 값은 [`SparseTensorValue`](sparse_ops.md#SparseTensorValue)이어야합니다.

`feed_dict`의 각 값들은 해당하는 키의 dtype의 numpy 배열로 변환이 가능해야합니다.

선택적인 `options` 인자는 \[`RunOptions`\] 프로토콜 버퍼를 받습니다. 옵션은 이 특정한 단계의 행동을 컨트롤할 수 있도록합니다. \(예로, 추적을 가능하게함\)

선택적인 `run_metadata` 인자는 \[`RunMetadata`\] 프로토콜 버퍼를 인자로 받습니다. 적절한 때에, 이 단계의 텐서가 아닌 출력값은 수집될 것입니다. 예를 들면, 사용자가 `options`에서 추적을 활성화할 때, 프로파일 정보는 이 인자로 수집될 것이며 역으로 전달될 것입니다.

**인자:**

* **`fetches`**: 단일 그래프 요소, 그래프 요소의 리스트 또는 이들의 값을 갖는 딕셔너리. \(위에서 설명함.\)
* **`feed_dict`**: 값들에 매핑되는 그래프 요소들의 딕셔너리.
* **`options`**: \[`RunOptions`\] 프로토콜 버퍼.
* **`run_metadata`**: \[`RunMetadata`\] 프로토콜 버퍼.

**반환값:**

`fetches`가 단일 그래프 요소일 때에는 단일값, `fetches`가 리스트일 경우엔 값 리스트, 또는 딕셔너리일 경우엔 `fetches`와 같은 키값들을 가진 딕셔너리. \(위에서 설명함\)

**예외:**

* **`RuntimeError`**: `Session`이 유효하지 않은 상태일 경우 발생. \(예로, 닫혀진 경우\)
* **`TypeError`**: `fetches` 또는 `feed_dict`키들이 적절하지 않은 타입일 경우 발생.
* **`ValueError`**: `fetches` 또는 `feed_dict`키들이 잘못되거나 존재하지 않는 `Tensor`를 참조할 경우 발생.

#### `tf.Session.close()` <a id="Session.close"></a>

세션을 닫습니다.

이 메서드를 실행하면 세션과 관련된 모든 리소스를 해제합니다.

**예외:**

tf.errors.OpError: TensorFlow 세션을 닫는 도중에 에러가 발생할 경우 이 예외 또는 이 예외의 서브클래스중 하나가 발생합니다.

#### `tf.Session.graph` <a id="Session.graph"></a>

세션에서 시작된 그래프.

#### `tf.Session.as_default()` <a id="Session.as_default"></a>

이 객체를 기본 세션으로 만드는 컨텍스트 매니저를 반환합니다.

[`Operation.run()`](framework.md#Operation.run) 또는 [`Tensor.run()`](framework.md#Tensor.run)가 이 세션에서 실행되도록하는 호출을 지정하기위해 `with` 키워드와 함께 사용합니다.

```python
c = tf.constant(..)
sess = tf.Session()

with sess.as_default():
  assert tf.get_default_session() is sess
  print(c.eval())
```

현재 기본 세션을 얻기위해 [`tf.get_default_session()`](client.md#get_default_session)을 사용합니다.

_주의_ `as_default` 컨텍스트 매니저는 컨텍스트를 빠져나왔을 때 세션을 _닫지 않으며_, 명시적으로 세션을 닫아줘야합니다.

```python
c = tf.constant(...)
sess = tf.Session()
with sess.as_default():
  print(c.eval())
# ...
with sess.as_default():
  print(c.eval())

sess.close()
```

대안으로는, 잡을 수 없는 예외가 발생하는 경우를 포함해서, 컨텍스트를 빠져나갈 때 자동으로 닫히는 세션을 생성하기 위해서는 `with tf.Session()`을 사용할 수 있습니다.

_주의_ 기본 그래프는 현재 스레드의 프로퍼티입니다. 새로운 스레드를 생성하고, 스레드 안에서 기본 스레드를 사용하고 싶을 경우엔 반드시 그 스레드의 함수에 `with sess.as_default()`를 명시적으로 추가해 주어야합니다.

**반환값:**

이 세션을 기본 세션으로 사용하는 컨텍스트 매니저.

### `class tf.InteractiveSession` <a id="InteractiveSession"></a>

쉘과 같은 인터랙티브 컨텍스트에서 사용하기 위한 TensorFlow `Session`

일반 `Session`과의 유일한 차이점은 `InteractiveSession`은 생성시 자기 자신을 기본 세션으로 설치한다는 것입니다. [`Tensor.eval()`](framework.md#Tensor.eval)메서드와 [`Operation.run()`](framework.md#Operation.run)메서드는 연산을 실행하기위해 그 세션을 사용할 것입니다.

이는 인터랙티브 쉘과 [IPythonnotebooks](http://ipython.org)에서 편리하며, 연산을 실행하기 위한 `Session` 객체를 명시적으로 전달하지 않아도됩니다.

예시:

```python
sess = tf.InteractiveSession()
a = tf.constant(5.0)
b = tf.constant(6.0)
c = a * b
# 'sess'의 전달없이도 'c.eval()'를 실행할 수 있습니다.
print(c.eval())
sess.close()
```

일반 세션은 `with`문 안에서 생성될 경우 자기 자신을 기본 세션으로 설치합니다. 인터랙티브 프로그램이 아닌 경우의 일반적인 사용법은 다음 패턴을 따르는 것입니다.

```python
a = tf.constant(5.0)
b = tf.constant(6.0)
c = a * b
with tf.Session():
  # 'c.eval()'을 여기에서도 사용할 수 있습니다.
  print(c.eval())
```

#### `tf.InteractiveSession.__init__(target='', graph=None, config=None)` <a id="InteractiveSession.__init__"></a>

새로운 인터랙티브 TensorFlow 세션을 생성합니다.

세션을 생성할 때 `graph` 인자가 지정되지 않으면, 세션에선 디폴트 그래프가 시작됩니다. 만약 같은 프로세스에서 `tf.Graph()`로 생성되는 그래프를 하나 이상 사용한다면, 각 그래프에 대해서 서로 다른 세션을 사용해야 할 것입니다. 그러나 각 그래프는 여러 세션에서 사용될 수 있습니다. 이 경우에는 때때로 세션 생성자에 그래프가 시작된다는걸 명시적으로 전달하는게 깔끔합니다.

**인자:**

* **`target`**: \(선택\) 접속을 위한 실행 엔진. 기본값으로 프로세스 내부 엔진을 사용합니다. 지금은, 빈 문자열 이외의 값은 지원되지 않습니다.
* **`graph`**: \(선택\) 시작되는 `Graph`. \(위에서 설명됨.\)
* **`config`**: \(선택\) 세션을 위한 설정 옵션을 가진 [`ConfigProto`](https://www.tensorflow.org/code/tensorflow/core/protobuf/config.proto) 프로토콜 버퍼.

#### `tf.InteractiveSession.close()` <a id="InteractiveSession.close"></a>

`InteractiveSession`을 닫습니다.

### `tf.get_default_session()` <a id="get_default_session"></a>

현재 스레드에 대한 기본 세션을 반환합니다.

반환된 `Session`은 입력된 `Session` 또는 `Session.as_default()` 컨텍스트에서 가장 안 쪽의 세션이 될 것입니다.

참고 : 기본 그래프는 현재 스레드의 프로퍼티입니다. 새로운 스레드를 생성하고, 스레드 안에서 기본 스레드를 사용하고 싶을 경우엔 반드시 그 스레드의 함수에 `with sess.as_default():`를 명시적으로 추가해 주어야합니다.

**반환값:**

기본 `Session`은 현재 스레드에서 사용됩니다.

## 에러 클래스

### `class tf.OpError` <a id="OpError"></a>

TensorFlow 실행이 실패할 때 발생하는 일반적인 에러.

세션은 언제든지 `tf.errors` 모듈에 있는 더 많은 `OpError`의 특정한 서브클래스 예외를 발생시킬 수 있습니다.

#### `tf.OpError.op` <a id="OpError.op"></a>

알려진 실패한 연산.

_주의_ 실패한 연산이 런타임때 합쳐진 경우엔, 예를 들면, `Send` 또는 `Recv` 연산, 해당하는 [`Operation`](framework.md#Operation) 객체가 없을 것입니다. 이 경우, 이는 `None`을 반환할 것이며, 연산에 대한 정보를 찾으려면[`OpError.node_def`](client.md#OpError.node_def)를 대신 사용해야합니다.

**반환값:**

실패한 `Operation` 또는 None.

#### `tf.OpError.node_def` <a id="OpError.node_def"></a>

실패한 연산을 나타내는 `NodeDef` 프로토콜 버퍼.

#### 그 외 메서드

#### `tf.OpError.__init__(node_def, op, message, error_code)` <a id="OpError.__init__"></a>

특정한 실패한 연산을 가리키는 새로운 `OpError`를 생성합니다.

**인자:**

* **`node_def`**: 알려진 연산의 경우 실패한 연산을 나타내는 `graph_pb2.NodeDef` 프로토콜 버퍼, 이 외에는 None.
* **`op`**: 알려진 연산의 경우 실패한 `ops.Operation`, 이 외에는 None.
* **`message`**: 실패를 설명하는 메시지 문자열.
* **`error_code`**: 에러를 나타내는 `error_codes_pb2.Code`. 

#### `tf.OpError.error_code` <a id="OpError.error_code"></a>

에러를 나타내는 정수 에러 코드.

#### `tf.OpError.message` <a id="OpError.message"></a>

에러를 설명하는 에러 메시지.

### `class tf.errors.CancelledError` <a id="CancelledError"></a>

연산이나 단계가 취소되었을 때 발생합니다.

예를 들면, 장시간 실행하는 연산 \(예로, [`queue.enqueue()`](io_ops.md#QueueBase.enqueue)\)는 또 다른 연산 \(예로, [`queue.close(cancel_pending_enqueues=True)`](io_ops.md#QueueBase.close)\) 또는 [closing the session](client.md#Session.close)을 실행함으로써 취소될 수 있습니다. 장기 실행 연산을 실행하는 단계는 `CancelledError`를 발생시키며 실패할 것입니다.

#### `tf.errors.CancelledError.__init__(node_def, op, message)` <a id="CancelledError.__init__"></a>

`CancelledError`를 생성합니다.

### `class tf.errors.UnknownError` <a id="UnknownError"></a>

알려지지 않은 에러.

이 에러가 반환될 수 있는 한 예는 상태값을 현재 주소 공간에서는 알려지지 않은 에러 공간에 속한 다른 주소 공간으로부터 받는 경우입니다. 또한 충분한 에러 정보를 반환하지 않는 API에 의해 발생하는 에러도 이 에러로 변환될 수 있습니다.

#### `tf.errors.UnknownError.__init__(node_def, op, message, error_code=2)` <a id="UnknownError.__init__"></a>

`UnknownError`를 생성합니다.

### `class tf.errors.InvalidArgumentError` <a id="InvalidArgumentError"></a>

연산이 잘못된 인자를 받는 경우 발생합니다.

이 에러는, 예를 들면, 만약 연산이 잘못된 값이나 구조\(shape\)를 가진 입력 텐서를 받을 경우에 발생할 수 있습니다. [`tf.matmul()`](math_ops.md#matmul) 연산은 행렬이 아닌 입력을 받을 경우에 이 에러를 발생시킬 것이며, [`tf.reshape()`](array_ops.md#reshape) 연산은 새로운 구조\(shape\)가 입력 텐서의 요소들의 갯수와 매칭이 안될 경우 이 에러를 발생시킬 것입니다.

#### `tf.errors.InvalidArgumentError.__init__(node_def, op, message)` <a id="InvalidArgumentError.__init__"></a>

`InvalidArgumentError`를 생성합니다.

### `class tf.errors.DeadlineExceededError` <a id="DeadlineExceededError"></a>

연산이 완료되기 전에 기한이 만료될 경우 발생합니다.

이 예외는 현재 사용되지 않습니다.

#### `tf.errors.DeadlineExceededError.__init__(node_def, op, message)` <a id="DeadlineExceededError.__init__"></a>

`DeadlineExceededError`를 생성합니다.

### `class tf.errors.NotFoundError` <a id="NotFoundError"></a>

요청된 엔티티 \(예로, 파일이나 디렉토리\)를 찾을 수 없는 경우 발생합니다.

예를 들면, [`tf.WholeFileReader.read()`](io_ops.md#WholeFileReader) 연산을 실행하는데 존재하지 않는 파일의 이름을 받게되면 `NotFoundError`을 발생시킬 수 있습니다.

#### `tf.errors.NotFoundError.__init__(node_def, op, message)` <a id="NotFoundError.__init__"></a>

`NotFoundError`를 생성합니다.

### `class tf.errors.AlreadyExistsError` <a id="AlreadyExistsError"></a>

이미 존재하는 엔티티를 생성하려고 할 경우 발생합니다.

예를 들면, 파일을 저장하는 연산 \(예로, [`tf.train.Saver.save()`](train.md#Saver.save)\)을 실행할 때 존재하는 파일의 파일명을 명시적으로 전달할 경우 잠재적으로 이 에러를 발생시킬 수 있습니다.

#### `tf.errors.AlreadyExistsError.__init__(node_def, op, message)` <a id="AlreadyExistsError.__init__"></a>

`AlreadyExistsError`를 생성합니다.

### `class tf.errors.PermissionDeniedError` <a id="PermissionDeniedError"></a>

호출자가 연산 실행에 대한 권한이 없을 경우 발생합니다.

예를 들면, [`tf.WholeFileReader.read()`](io_ops.md#WholeFileReader) 연산을 실행할 때 사용자가 읽기 권한을 갖고 있지 않는 파일명을 받을 경우 `PermissionDeniedError`를 발생시킬 수 있습니다.

#### `tf.errors.PermissionDeniedError.__init__(node_def, op, message)` <a id="PermissionDeniedError.__init__"></a>

`PermissionDeniedError`를 생성합니다.

### `class tf.errors.UnauthenticatedError` <a id="UnauthenticatedError"></a>

요청이 유효한 인증 자격 증명을 가지지 않은 경우.

이 예외는 현재 사용되지 않습니다.

#### `tf.errors.UnauthenticatedError.__init__(node_def, op, message)` <a id="UnauthenticatedError.__init__"></a>

`UnauthenticatedError`를 생성합니다.

### `class tf.errors.ResourceExhaustedError` <a id="ResourceExhaustedError"></a>

리소스가 소진된 경우.

예를 들면, 사용자별 할당량\(quota\)이 소진되거나 전 파일 시스템에 공간이 부족할 경우 이 에러가 발생할 수 있습니다.

#### `tf.errors.ResourceExhaustedError.__init__(node_def, op, message)` <a id="ResourceExhaustedError.__init__"></a>

`ResourceExhaustedError`를 생성합니다.

### `class tf.errors.FailedPreconditionError` <a id="FailedPreconditionError"></a>

시스템이 연산을 실행시킬 수 있는 상태가 아니라 연산이 거부됨.

이 예외는 [`tf.Variable`](state_ops.md#Variable)를 읽는 연산을 초기화 전에 실행할 경우에 발생하는 가장 빈번한 예외입니다.

#### `tf.errors.FailedPreconditionError.__init__(node_def, op, message)` <a id="FailedPreconditionError.__init__"></a>

`FailedPreconditionError`를 생성합니다.

### `class tf.errors.AbortedError` <a id="AbortedError"></a>

보통 동시 작업때문에 연산이 중단됨.

예를 들면, [`queue.close()`](io_ops.md#QueueBase.close)이 이전에 실행된 상태에서 [`queue.enqueue()`](io_ops.md#QueueBase.enqueue) 연산을 실행하면 `AbortedError`가 발생할 수 있습니다.

#### `tf.errors.AbortedError.__init__(node_def, op, message)` <a id="AbortedError.__init__"></a>

`AbortError`를 생성합니다.

### `class tf.errors.OutOfRangeError` <a id="OutOfRangeError"></a>

연산이 유효한 입력 범위를 지나쳐 순회할 경우 발생합니다.

이 예외는 [`queue.dequeue()`](io_ops.md#QueueBase.dequeue) 연산이 빈 큐에서 블로킹 되고 [`queue.close()`](io_ops.md#QueueBase.close) 연산이 실행되는 경우와 같은 "파일의 끝\(end-of-file\)"이라는 조건에서 발생합니다.

#### `tf.errors.OutOfRangeError.__init__(node_def, op, message)` <a id="OutOfRangeError.__init__"></a>

`OutOfRangeError`를 생성합니다.

### `class tf.errors.UnimplementedError` <a id="UnimplementedError"></a>

연산이 구현되지 않은 경우 발생합니다.

몇가지 연산은 유효하지만 현재 지원되지 않는 인자들을 전달할 경우 이 에러를 발생시킬 수 있습니다. [`tf.nn.max_pool()`](nn.md#max_pool) 연산을 실행할 때 배치 차원에 풀링이 요청된 경우 이는 아직 지원되지 않기 때문에 이 에러를 발생시킬 것입니다.

#### `tf.errors.UnimplementedError.__init__(node_def, op, message)` <a id="UnimplementedError.__init__"></a>

`UnimplementedError`를 생성합니다.

### `class tf.errors.InternalError` <a id="InternalError"></a>

시스템 내부 에러가 생길 경우 발생.

망가진 런타임에 의해 몇가지 불변이 예상될 경우 발생하는 예외입니다. 이 예외를 잡는것은 추천하지 않습니다.

#### `tf.errors.InternalError.__init__(node_def, op, message)` <a id="InternalError.__init__"></a>

`InternalError`를 생성합니다.

### `class tf.errors.UnavailableError` <a id="UnavailableError"></a>

런타임이 현재 이용불가능할 때 발생합니다.

이 예외는 현재 사용되지 않습니다.

#### `tf.errors.UnavailableError.__init__(node_def, op, message)` <a id="UnavailableError.__init__"></a>

`UnavailableError`를 생성합니다.

### `class tf.errors.DataLossError` <a id="DataLossError"></a>

복구불가능한 데이터를 잃거나 손상이 생겼을 때 발생합니다.

예를 들면, 이는[`tf.WholeFileReader.read()`](io_ops.md#WholeFileReader)연산을 실행하는데, 읽는 도중에 파일이 잘릴 경우 발생할 수 있습니다.

#### `tf.errors.DataLossError.__init__(node_def, op, message)` <a id="DataLossError.__init__"></a>

`DataLossError`를 생성합니다.

