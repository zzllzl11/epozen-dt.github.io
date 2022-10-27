---
title: 코드 리팩토링(Code Refactoring)
last_modified_at: 2022-9-30
author: 김수민
---

이번 포스팅에서는 코드 리팩토링에 대해 알아보겠습니다.

---

## 코드 리팩토링(Code Refactoring)

코드 리팩토링(code refactoring)은 외부 동작을 바꾸지 않으면서 내부 구조를 개선하는 방법을 의미합니다.

프로그램의 유지보수 과정에서의 용이성을 높이기 위해 코드를 이해하기 쉽고, 수정하기 쉽도록 만드는 것을 목표로 진행합니다.

---

#### 리팩토링의 필요성

1. 코드를 정돈해 가독성을 높일 수 있습니다.
2. 각 작업에 대한 중복을 제거할 수 있어 코드가 명확해집니다.
3. 코드를 이해하면서 내부 구조를 수정해 자동으로 버그를 찾을 수 있습니다. 
4. 소프트웨어 디자인을 개선해 프로그램 기능 추가 시 빠른 속도로 개발을 진행할 수 있습니다.



#### 수행 시기

1. **삼진규칙**

   ​	세 번째 중복되는 코드를 작성한다면, 그 때는 리팩토링을 수행해야 한다.(Don Robers)

2. **기능 추가 시**

   ​	보통 자신의 코드가 아닌 경우 기능 추가시 어려움을 겪을 수 있습니다. 이때 리팩토링을 수행하게 되면 코드를 이해하기 쉬워지고, 혹은 리팩토링 수행 시 디자인이 이해하기 쉬운 형태로 변경되어 기능 추가에 도움이 됩니다.

3. **버그를 수정 시**

   ​	버그 리포트를 받으면 버그가 있었는지 모를 정도로 코드가 명확하지 않았다는 뜻입니다. 따라서 해당 경우, 리팩토링을 통해 코드를 명확히 해야 할 필요가 있습니다.

4. **코드 검토(Code Review) 시**

   리팩토링은 다른사람의 코드를 검토하는데 도움이 됩니다. 코드가 어떻게 보일지에 대한 고민도 할 수 있습니다.

---

#### 리팩토링이 필요한 부분

이제 본격적으로 어떤 부분에 대해 리팩토링을 해야하는지에 대해 알아보겠습니다.

* **중복된 코드 존재 시(Duplicated Code)**

가장 단순한 형태의 수정사항 입니다. 이때는 중복되는 코드를 하나의 메소드로 빼내는 방식으로 해결이 가능합니다. 

또한 같은 super class를 갖는 두 class에서 같은 코드가 나타난 경우에도 리팩토링 대상이 됩니다. 이때는 반복되는 내용을 정의하고 상속받는 형태로 수정할 수 있습니다.



* **메소드가 지나치게 긴 경우(Long Method)**

메소드는 가능한 길이가 짧을수록 많이 활용되고, 또 마지막까지 수정이 필요하지 않을 가능성이 높습니다.

메소드가 긴 경우에는 여러 기능들을 포함할 가능성이 높으므로 단일의 기능을 갖도록 메소드를 분리하는 것이 좋습니다. 

특히 메소드는 하나의 input에 하나의 output이 나오는게 이상적이며 메소드의 이름은 그 기능을 명확하게 정의하도록 명명해야 내용을 보지 않더라도 그 기능을 파악할 수 있습니다.



* **클래스가 지나치게 큰 경우(Large Class)**

하나의 클래스에 지나치게 많은 인스턴스 변수가 존재한다면 중복된 코드가 존재할 확률이 높습니다.



* 클래스가 충분한 역할을 하지 않는 경우(Lazy Class)

하나의 클래스에 할당된 역할이 코드를 이해하는데 드는 비용에 비해 크지 않는 경우 정리하는 것이 유지보수 비용 절감에 큰 도움이 됩니다.



* 필요하지 않은 것을 처리하기 위한 코드가 존재하는 경우(추측성 일반화)

  

* 임시 필드 존재 시(Temporary Field)

하나의 객체에서 instance 변수가 특정 환경에서만 set되는 것과 같이 임시 필드가 존재하는 경우, 작성자 외의 개발자가 코드를 확인할 때 이해에 어려움을 겪을 수 있습니다.



* 메세지 체인이 존재하는 경우(Message Chains)

한 Client가 어떤 객체를 얻기 위해 다른 객체에 물어보고, 다른 객체는 또 다른 객체에게 물어보는 연속적인 상황이 발생하는 경우 구조적 문제가 있다고 판단 할 수 있습니다.



* 미들맨이 있는 경우(Middle Man)

Class의 Interface를 보았을때, 대부분 다른 Class로 위임하는 경우를 미들맨이라고 부르고, 이와 같은 상황에서는 반드시 제거의 대상이 되어야 합니다.



* 결합도가 높은 경우(Inappropriate Intimacy)

Class가 서로 지나치게 긴밀한 경우 결합도가 높다고 판단 할 수 있습니다. 이 경우 서로에 대한 정보 파악을 진행해 시간 소모가 클 수 있습니다.



* 다른 인터페이스를 가진 대체 클래스가 있는 경우(Alternative Classes with Different)

개발자가 같은 기능을 가진 클래스의 존재를 모를 경우 발생할 수 있습니다. 이는 중복된 코드와 같으므로 제거가 필요합니다.



* 불완전한 라이브러리 클래스일 경우(Incomplete Library Class)

라이브러리의 작성자가 필요 기능을 가지고 있지 않거나 하는 경우에 해결을 위한 방법으로 리팩토링을 필요로 하게 됩니다. 대부분 이경우는 라이브러리가 시간이 지나면서 업데이트를 더이상 하지 않게 되는 경우에 발생합니다.



이외에도 다양한 경우들이 존재하므로 항상 코드를 재 점검 하는 습관을 필요로 합니다.

코드를 작성하는 경우 아래 3가지를 유념해서 작성한다면 좋은 코드가 될 수 있습니다.

1. 가독성을 높이기
2. 결합도를 없애기
3. 하나의 함수/메소드는 하나의 역할만 수행하도록 하기



---

### References

https://xzio.tistory.com/392

https://starblood.tistory.com/entry/%EB%A6%AC%ED%8C%A9%ED%86%A0%EB%A7%81-%EC%84%A4%EB%AA%85-Introduction-to-Refactoring