## 데이터 모델링

문제를 현실로부터 뜯어내서 고도의 추상화 과정을 거쳐서 그것을 컴퓨터라는 새로운 현실로 옮겨 담는 과정

---

## 데이터 모델링의 과정

[![2023-09-08-041752.png](https://i.postimg.cc/NFfNzQjT/2023-09-08-041752.png)](https://postimg.cc/JDvcyVJ4)
---

### 개념적 데이터 모델링(Conceptual Data Modeling)이란?

데이터를 개념적으로 일반화시켜 구조, 타입, 속성, 관계 제약 조건 등을 이끌어 내는 과정을 개념적 데이터 모델링이라고 한다. 즉, 어떤 데이터를 저장할 것인가를 정하는 단계라고 생각하면 된다. 첫 번째 단계에서 진행한 요구 사항이 잘못 해석되는 오류를 방지하는 기능을 한다.

---

## 개념적 데이터 모델링의 효용

현실에서 개념을 추출하는 일종의 필터를 제공해준다.
개념에 대해 다른 사람들과 대화하게 해주는 일종의 언어로써 작용하게 된다.

현실은 상당히 복잡하게 이루어져 있기 때문에 하나하나 데이터로 나타내기 쉽지 않다. 그런데 현실을 간단하게 바라볼 수 있게 해주는 도구가 있다면 편할 것 같은데, 그 중 하나가 바로 **ERD** 이다.

[![2023-09-08-041816.png](https://i.postimg.cc/L6s6FWC3/2023-09-08-041816.png)](https://postimg.cc/SjwpWgpn)

---

### ERD란 무엇인가?

- ERD란 Entity Relationship Diagram의 약어로, 데이터베이스 구조를 한눈에 알아보기 위해서 쓰인다.
- DB를 개발하기 전에 보다 많은 아이디어를 도출하고, 데이터베이스 설계의 이해를 높이기 위해 데이터 모델링을 실시한다.
- 쿼리문을 작성할 때 테이블들이 구조화된 다이어그램을 보면서 도움을 받을 수 있다.
- 데이터의 다양한 특징을 확인할 수 있어 요구사항을 그에 맞게 개발할 수 있다.


---


## ERD의 핵심 3요소

---

### 1. **개체(Entity)**
[![2023-09-08-041837.png](https://i.postimg.cc/FzYr3dJn/2023-09-08-041837.png)](https://postimg.cc/m1GWGrjQ)
- Entity는 **정의 가능한 사물 또는 개념**을 의미한다.
- 사람도 될 수 있으며 프로필이나 도서 정보와 같은 무형의 정보도 데이터화가 가능하다.
- 사각형으로 표현
  
---

### 2. 속성(Attribute)
[![2023-09-08-041846.png](https://i.postimg.cc/fbFDZWPc/2023-09-08-041846.png)](https://postimg.cc/Jyb958M0)
- Entity는 개체가 갖고 있는 속성(Attribute)을 포함한다.
- 예를 들어 학생 Entity라면, 학번, 이름, 주소, 전공 ..등 속성들이 있다.
- 타원으로 표현
- 키 애트리뷰트 ( Key Attribute )
- 복합 애트리뷰트 ( Composite Attribute )
- 다중값 애트리뷰트 ( Multi-Valued Attribute )
- 유도된 애트리뷰트 ( Derived Attribute )
  
---

### 3. 관계(Relationship)

[![2023-09-08-041906.png](https://i.postimg.cc/j55w3j7y/2023-09-08-041906.png)](https://postimg.cc/GBWmHdzp)
- Relationship은 Entity간의 상호작용을 표현함
- 1:1 , 1: N , N:M 관계 등이 가능하다.
- 마름모로 표현


## Cardinality(관계의 기수성)

### 1:1 관계(****One-to-One Cardinality)****
---
[![2023-09-08-041921.png](https://i.postimg.cc/BZNsQCRZ/2023-09-08-041921.png)](https://postimg.cc/yWJ2L0V2)

### 1:N 관계(One-to-Many Cardinality)
---
[![2023-09-08-041934.png](https://i.postimg.cc/653K7vNr/2023-09-08-041934.png)](https://postimg.cc/grfQQrjj)

### N:M 관계(Many-to-Many Cardinality)

---

[![2023-09-08-041943.png](https://i.postimg.cc/YCLwRB0j/2023-09-08-041943.png)](https://postimg.cc/k2CZMZxd)

실제 데이터베이스 테이블에서는 N:M 관계를 표현이 어려우므로, 연결 테이블이라는 특별한 테이블을 만들어 최종적으로는 1:N 형태로 컨버팅을 해준다.

[![2023-09-08-041954.png](https://i.postimg.cc/QxW6n8gL/2023-09-08-041954.png)](https://postimg.cc/dLwmhKSn)

---

## Obtionality(관계의 선택성)
[![2023-09-08-042002.png](https://i.postimg.cc/9Q5L661D/2023-09-08-042002.png)](https://postimg.cc/GHKPYSWR)
반드시 필요로 하는지 여부에 따라 표현
저자는 댓글을 반드시 쓰지는 않지만, 댓글은 무조건 저자가 있다!

---

### Cardinality 와 Obtionality 중첩
[![2023-09-08-042015.png](https://i.postimg.cc/FKGGJ7vS/2023-09-08-042015.png)](https://postimg.cc/yJg0M6k6)



## 논리적 데이터 모델링

개념적 데이터 모델링을 한 내용을 표로 전환!

[![2023-09-08-042025.png](https://i.postimg.cc/d0dkzfHV/2023-09-08-042025.png)](https://postimg.cc/7CHZzKrF)

[![2023-09-08-042032.png](https://i.postimg.cc/TwJyPDX8/2023-09-08-042032.png)](https://postimg.cc/WFtpWt3S)
실제 관계형 데이터베이스에서는 위와 같이 바뀐다!

---

[![image.png](https://i.postimg.cc/x8q5nGWf/image.png)](https://postimg.cc/1VhwKFm2)


---
Q .**E-R 모델의 표현 방법**으로 옳지 않은 것은? 

[정답률: 26%]정보처리기사(2020년 이후) 필기 (2020년 1회·2회 통합 기출문제)

① 개체타입 : 사각형

---

② 관계타입 : 마름모

---

③ 속성 : 오각형

---

④ 연결 : 선


---

추가

피터첸 표기법

[[정보처리기사] E-R (개체-관계) 모델, 다이어그램 표기법 및 기호 (tistory.com)](https://liveyourit.tistory.com/208)
