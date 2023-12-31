## 자료구조
자료구조란?
- 자료들이 논리적으로 정의된 규칙에 의해 나열된 것
- 자료에 대한 처리를 효율적으로 수행할 수 있도록 자료를 구분지어 표현한 것
- 데이터를 효율적으로 관리하고 수정, 삭제, 탐색, 저장할 수 있는 데이터의 구조
<br />


## 알고리즘
알고리즘이란?
- 어떤 문제를 해결하기 위해 필요한 계산 절차나 처리 과정의 순서
- 레고를 조립할 때 설명서를 보지 않을 수도 있지만 설명서를 보면 가장 빨리 조립
- 알고리즘은 입력과 출력 사이의 연산을 가장 빨리 할 수 있게 해주는 지침서이자 설명서
- 가령, 배열 데이터 안의 요소를 숫자가 작은 순으로 정렬해야 한다고 하면 어떤 방법을 사용할지 고민하게 되는데, 이때 적절한 설명서인 적절한 알고리즘을 활용하면 빠르게 처리 가능
<br />


## 시간복잡도
- 특정 알고리즘이 '어떤 문제를 해결하는 데 걸리는 시간'
- 시간복잡도는 효율적인 코드로 개선하는 데 쓰이는 척도로 기능
- 각 알고리즘은 문제를 해결하는데 평균적으로 일정 시간이 걸린다고 할지라도 시간복잡도의 개념에서는 최악의 경우를 계산하는 방식인 빅오(Big-O)표기법을 주로 활용 
- 가령, 4, 2, 3, 9, 7 요소를 가진 배열이 있을 때 3이 어딨는지 앞에서부터 하나씩 검사하면 4, 2, 3 순으로 총 3의 시간이 걸림. 만약, 7이 어딨는지 앞에서부터 하나씩 검사하면 4, 2, 3, 9, 7 순으로 총 5의 시간이 걸림. 5가지 원소를 가진 배열에서 특정 원소가 어디에 위치하는지 앞에서부터 하나씩 검사하며 찾는다고 할 때, 운이 좋으면 한 번에 찾게 되고 운이 나쁘면 5번만에 찾게 됨. 하지만, 1초에 약 1억번 정도를 연산하는 컴퓨터 입장에서는 3번의 연산이든 5번의 연산이든 큰 차이가 없기에 사례에서의 시간복잡도는 상수 시간(O(1))으로 취급.
- 즉, 시간복잡도는 '충분히 큰 수'로 취급되기에 최고차항을 제외한 나머지 항은 무시
- 만약, 입력 크기 n의 모든 입력에 대한 알고리즘에 필요한 시간이 10n^2 + n이라고 하면, 해당 코드의 시간 복잡도는 O(n^2). 앞서 설명한 것처럼 컴퓨터의 연산 속도는 1초당 1억회로 무척 빠르기에 가장 영향을 많이 끼치는 항을 제외하고 나머지 항은 고려하지 않으며 최고차항의 계수 역시 무시.
<br />

#### O(1) (Constant, 상수 시간)
- 입력 데이터의 크기에 상관없이 언제나 일정한 시간이 걸리는 알고리즘
- 데이터가 크든 적든 성능에 영향을 미치지 않음
- 가장 빠른 시간

#### O(log n) (Logarithmic, 로그 시간)
- 입력 데이터의 크기가 커질수록 시간이 로그(log) 만큼 짧아지는 알고리즘
- 가령, 데이터의 크기가 10배가 되면 처리 시간은 2배로 증가

#### O(n) (Linear, 선형 시간)
- 입력 데이터의 크기에 비례해 처리 시간이 증가하는 알고리즘
- 가령, 데이터의 크기가 10배가 되면 처리 시간도 10배로 증가
- 시간 복잡도가 linear하게 증가, for 문이 대표적(range = n)

#### O(n log n) (Linear-Logarithmic, 선형 로그 시간)
- 입력 데이터의 크기가 커질수록 시간이 n * 로그(log)배만큼 커지는 알고리즘
- 가령, 데이터의 크기가 10배가 되면 처리 시간은 20배로 증가

#### O(n^2) (Quadratic, 제곱시간)
- 입력 데이터의 크기가 커질수록 시간이 제곱이 되는 알고리즘
- 가령, 데이터의 크기가 10배가 되면 처리 시간은 100배로 증가


## 공간복잡도
- 시간복잡도와 함께 프로그램의 성능을 나타내는 지표 중 하나
- 작성한 프로그램이 얼마나 많은 메모리를 차지하는지 나타냄
- 컴퓨터 성능의 발달로 인해 메모리 공간이 충분해져 공간복잡도의 중요성은 시간복잡도에 비해 상대적으로 낮아짐
<br />
<img src="https://i1.ruliweb.com/img/22/09/05/1830c558f541ed55e.png"><br />


## 자료구조의 이점
- 코드의 처리시간 단축
- 데이터의 크기를 줄여 메모리 용량 절약
- 데이터를 수정하거나 관리하기 용이
- 쉽고 간단한 코드(가독성이 좋은 코드)
<br />


## 자료구조의 종류
- 자료구조는 크게 선형 자료구조와 비선형 자료구조로 구분
- 선형 자료구조는 데이터가 일렬로 나열되어 있는 것
- 비선형 자료구조는 데이터가 일렬로 나열되어 있지 않고 특정한 형태를 띄고 있는 것
<br />
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbL9JS7%2FbtsqMhurbWD%2FViGSwTliXKBUk5hXTyc6U0%2Fimg.png"><br />


## 선형 자료구조
- 요소가 일렬로 나열되어 있는 자료구조
- 한 원소 뒤에 하나의 원소만이 존재하는 자료구조
- 자료들이 직선 형태로 나열되어 있고, 원소 간의 순서가 고려
- 리스트(선형 리스트 / 연결 리스트), 스택, 큐, 덱이 존재
<br />


## 1. 선형 리스트(Linear List)
- 선형 리스트 자료구조는 프로그래밍에서 배열(Array)에 해당
- 배열은 속성이 동일한 데이터를 순서대로 관리할 필요가 있을 때 활용
- 크기 고정, 중복 허용, 순서 존재(인접한 메모리 위치의 데이터를 집약)
- 인덱스를 사용하기에 검색이 빠르다는 장점이 존재하나, 배열 요소를 변경하는 것이 어렵다는 단점 존재
- 시간복잡도는 탐색에 O(1), 삽입과 삭제에 O(n)
<br />
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdoOO6P%2Fbtrribv3xmb%2FMRzOB32ANw9nNvWJwHGAHK%2Fimg.png"><br />


## 2. 연결 리스트(Linked-List)
- 데이터를 저장하는 공간과 데이터가 저장된 공간을 가리키는 주소 값을 동시에 갖는 자료구조
- 각 노드가 데이터와 포인트를 가지고 한 줄로 연결되어 있는 방식으로 데이터를 저장하는 자료구조
- 데이터를 감싼 노드를 포인터로 연결해서 공간적인 효율성을 극대화시킨 자료구조
- 포인터로 앞과 뒤의 노드를 연결(prev 포인터와 next 포인터 존재, 연결 리스트의 종류에서 후술)
- 시간복잡도는 삽입과 삭제에 O(1), 탐색에 O(n)
<br />

#### 연결리스트 구조
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FvjuCK%2FbtsqM9wj8WJ%2FaoinaXLd5ALMqF79i9n7Ok%2Fimg.png"><br />

#### 연결리스트의 앞에 데이터 추가
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FblKfOC%2FbtsqJB8wCU4%2FI9IFmse9X7APeEbzu1fdoK%2Fimg.png"><br />

#### 연결리스트의 뒤에 데이터 추가
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbemrrP%2FbtsqKzWFKab%2FJ7SZtKchbK32kBy7hlguQK%2Fimg.png"><br />

#### 연결리스트 중간에 데이터 삽입
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FncPix%2FbtsqKg4hGwL%2FUU37ujkYNkmKRMrtuOFzfK%2Fimg.png"><br />

#### 연결리스트 데이터 삭제
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcFqkkW%2FbtsqFsYNF0F%2FB1Q9SybTJaEE8Pv8yqGrt0%2Fimg.png"><br />

### 연결리스트의 종류
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FciHRNw%2FbtsqFsLhsUi%2FfjefhbkdhwPUd4SV3njiek%2Fimg.png"><br />

#### 단순연결리스트 : next 포인터
#### 이중연결리스트 : next 포인터 + prev 포인터 (단, head 노드의 prev 포인터 X, tail 노드의 next 포인터 X)
#### 원형이중연결리스트 : next 포인터 & prev 포인터 (단, tail 노드의 next 포인터가 head 노드를 가리킴)
<br />


### 선형 리스트(Array)와 연결 리스트(Linked-list)의 차이
연결 리스트는 배열과 달리 데이터를 저장할 때 데이터를 저장하는 공간과 함께 그 다음에 나올 데이터가 저장된 공간을 가리키는 주소 값을 동시에 갖는다. 즉, 데이터 값과 다음 공간의 주소 값, 이렇게 두 공간을 하나의 데이터로 관리한다. 배열의 경우 데이터의 크기가 가변적이지 않아 크기가 모자랄 경우 메모리를 더 할당하고 배열 데이터를 복사해야 해서 비효율적이다. 즉, 배열은 데이터의 삽입과 삭제에 불리하다. 하지만, 배열은 인덱스만 알면 바로 접근이 가능하기에 검색에 유리하다. 반면, 연결 리스트의 경우 다음 데이터의 주소 값을 변경하기만 하면 되므로 데이터의 삽입과 삭제에 유리하다. 하지만, 배열만큼 접근 속도가 빠르지는 않기 때문에 (배열에서의 검색의 시간 복잡도는 O(1)인데 반해, 연결리스트의 검색의 시간 복잡도는 O(n)이다.) 검색에서는 배열보다 불리하다. 요약하자면, 데이터의 조회보다 수정이나 삭제가 잦은 경우 연결 리스트가 유리하고, 검색이 위주라면 배열이 유리하다.
<br />
<img src="https://blog.kakaocdn.net/dn/doQavr/btrrjZHVcPs/taH2ltyKhlimKZTxlpxBo1/img.jpg"><br />


## 3. 스택(Stack)
- 마지막에 들어온 데이터가 가장 먼저 나가는 후입선출(LIFO, Last in First Out) 구조를 가진 자료구조
- 한쪽 끝에서만 데이터의 삽입과 삭제가 수행
- stack의 경우 top에서 데이터의 삽입과 삭제가 모두 수행
- 웹 페이지의 뒤로 가기를 하면 가장 마지막에 들어갔던 페이지로 이동하는 것
- push(삽입), pop(삭제 및 출력), peek(top item 반환)
- 시간복잡도는 삽입 및 삭제에 O(1), 탐색에 O(n)
<br />
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkCJfL%2FbtrrocHfMyZ%2FWrkoaTKnHRfh5qPqQBNir0%2Fimg.png"><br />

## 4. 큐(Queue)
- 처음에 들어간 데이터가 가장 먼저 나가는 선입선출(FIFO, First in First Out) 구조를 가진 자료구조
- 한쪽 끝에서는 데이터의 삽입만 수행되고, 다른 한쪽 끝에서는 삭제만 수행
- 가장 앞부분인 front(head)에서 삭제가, 가장 뒷부분인 rear(tail)에서 삽입이 수행
- 은행에서 대기표를 가장 먼저 뽑은 사람이 가장 먼저 은행업무를 보고 나가는 것
- 시간복잡도는 삽입 및 삭제에 O(1), 탐색에 O(n)
<br />
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFVQZu%2FbtrroFbqYc6%2Fxs15mKZwwC39N7VCo5Ds80%2Fimg.png"><br />

## 5. 덱(Deque)
- 어느 쪽으로 입력하고 어느 쪽으로 출력하는지에 따라 스택으로도, 큐로도 사용 가능
- 삽입과 삭제가 리스트의 양쪽 끝에서 모두 수행될 수 있는 자료구조
- 한쪽으로만 입력 가능하도록 설정한 덱은 스크롤(scroll)이라 지칭
- 한쪽으로만 출력 가능하도록 설정한 덱은 셸프(shelf)라 지칭

<br />
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fby21F4%2FbtrrpmvMJXx%2FB6E558PT03jOfscmETKkVk%2Fimg.png"><br />

## 문제
#### 문제 1
스택에 대한 설명으로 틀린 것은? <br />
① 입출력이 한쪽 끝으로만 제한된 리스트이다. <br />
② Head(Front)와 Tail(Rear)의 두 개 포인터를 갖고 있다. <br />
③ LIFO 구조이다. <br />
④ 더 이상 삭제할 테이터가 없는 상태에서 데이터를 삭제하면 언더플로(Underflow)가 발생한다. <br />
<br />

#### 문제 2
자료구조에 대한 설명으로 틀린 것은? <br />
① 큐는 비선형구조에 해당한다. <br />
② 큐는 First in - First out 처리를 수행한다. <br />
③ 스택은 Last in - First out 처리를 수행한다. <br />
④ 스택은 서브루틴 호출, 인터럽트 처리, 수식 계산 및 수식 표기법에 응용된다. <br />
<br />

<br />

## 이미지 출처
<br />
<a href="https://cheris8.github.io/python/DS-Overview/" target="_blank">이미지 출처1</a>
<a href="https://kkangdda.tistory.com/30" target="_blank">이미지 출처2</a>

## 참고
<br />
<a href="https://wpunch2000.tistory.com/28" target="_blank">선형 자료구조</a>
<br />
<a href="https://go-coding.tistory.com/m/5">
<br />
<a href="https://go-coding.tistory.com/m/6">
<br /><br />


#### 문제 정답 2, 1

