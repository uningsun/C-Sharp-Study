OOP(Object-Oriented Programming) 이란 무엇인가?
==============================================
  객체 지향 프로그래밍(OOP)은 컴퓨터 프로그램의 패러다임 중 하나, 객체 지향 프로그래밍은 컴퓨터 프로그램을 명령어의 목록으로 보는 시각(절차 지향 프로그램,procedural programming)에서 벗어나 여러 개의 독립된 단위, 즉 "객체(Object)"들의 모임으로 파악하고자 하는 것이다. 각각의 개체는 메시지를 주고 받고, 데이터를 처리할 수 있다.
>객체는 변수와 메소드를 그룹핑한 것 뿐이다.

  로직을 상태(state) 와 행위(behave)로 이루어진 객체로 만드는 것이다. 이 객체들을 조립하여 하나의 프로그램으로 만드는 것이 객체지향 프로그래밍이다. 
---------------------------------------

# 1. 기본 구성 요소
* 클래스(Class) : 같은 종류(또는 문제 해결을 위한)의 집단에 속하는 속성(attribute)과 행위(behavior)를 정의한 것으로 객체지향 프로그램의 기본적인 사용자 정의 데이터형(user definded data type,c언어에서는 구조체)이라고 할 수 있다. 클래스는 다른 클래스 또는 외부 요소와 독립적으로 디자인해야 한다. 

* 객체(Object) : 클래스의 인스턴스(실제로 메모리상에 할당된 것)이다. 객체는 자신 고유의 속성(attribute)을 가지며 클래스에서 정의한 행위(behavior)를 수행할 수 있다. 객체의 행위는 클래스에 정의된 행위에 대한 정의를 공유함으로써 메모리를 경제적으로 사용한다.

* 메서드(Method), 메시지(Message) : 클래스로부터 생성된 객체를 사용하는 방법으로 객체에 명령을 내리는 메시지라 할 수있다. 메서드는 한 객체의 서브루틴(subroutine)형태로 객체의 속성을 조작하는데 사용된다. 또 객체 간의 통신은 메시지를 통해 이루어진다.

# 2. 특징

  객체 지향 프로그래밍의 특징은 기본적으로 자료 추상화, 상속, 다형 개념, 동적 바인딩 등이 있으며 추가적으로 다중 상속 등의 특징이 존재한다. 객체 지향 프로그래밍은 자료 추상화를 기초로 하여 상속, 다형 개념, 동적 바인딩이 시스템의 복잡성을 제어하기 위해 서로 맞물려 기능한다.

* 자료 추상화 : 자료 추상화는 불필요한 정보는 숨기고 중요한 정보만을 표현함으로써 프로개름을 간단히 만드는 것이다. 자료 추상화를 통해 정의된 자료형을 **추상 자료형**이라고 한다. 

* 상속 : 상속은 새로운 클래스가 기존의 클래스의 자료와 연산을 이용할 수 있게 하는 기능이다. 상속을 받는 새로운 클래스를 **부클래스, 파생 클래스, 하위 클래스, 자식 클래스**라고 하며 새로운 클래스가 상속하는 기존의 클래스를 **기반 클래스,상위 클래스,부모 클래스**라고 한다.

* 다중 상속 : 다중 상속은 클래스가 **2개 이상의 클래스**로부터 상속받을 수 있게 하는 기능이다. 클래스들의 기능이 동시에 필요할 때 용이하나 클래스의 상속 관계에 혼란이 생길 수 있고(다이아몬스 상속 등)프로그래밍 언어에 따라 사용 가능 유무가 다르므로 주의해서 사용해야 한다. JAVA는 지원하지 않는다.

* 다형성 개념 : 어떤 한 요소에 여러 개념을 넣어 놓는 것으로 일반적으로 **오버라이딩**(같은 이름의 메소드가 여러 클래스에서 다른 기능을 하는 것)이나 **오버로딩**(같은 이름의 메소드가 인자의 개수나 자료형에 따라서 다른 기능을 하는 것)을 의미한다. 다형 개념을 통해서 프로그램 안의 객체 간의 관계를 조직적으로 나타낼 수 있다.

* 동적 바인딩 : 동적 바인딩은 **실행 시간 중에 일어나거나 실행 과정에서 변경될 수 있는 바인딩**으로 컴파일 시간에 완료되어 변화하지 않는 정적 바인딩과 대비되는 개념이다. 동적 바인딩은 프로그램의 한 개체나 기호를 실행 과정에 여러 속성이나 연산에 바인딩함으로써 다형 개념을 실현한다.

# 3. 문법과 설계
  객체 지향 프로그램은 크게 두가지로 구분된다.

#### 문법

  하나는 객체지향을 편하게 할 수 있도록 언어가 제공하는 기능을 익히는 것이다. 이 문법을 이해하고, 숙지해야 객체를 만들 수 있다. 객체를 만드는 법에 대한 학습이라고 할 수 있다.

#### 설계

  두번째는 좋은 객체를 만드는 법이다. 이것을 다른 말로는 설계를 잘하는 법이라고 할 수 있다. 좋은 설계는 현실을 잘 반영해야 한다. 현실은 복잡하지만 복잡한 모든것을 반영할 필요는 없다.

![subway](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/516/1854.gif)

  왼쪽 상단의 지도는 현실을 보여주며 오른쪽 하단의 지도는 지하철 탑승자의 관심사만 반영한다. 역 간의 거리, 실제 위치, 구불구불한 길 등의 요소들은 모두 배제하고 있다. 복잡함 속에서 필요한 관점만 추출하는 것을 **추상화**라고 한다.

  프로그램을 만든다는 것은 소프트웨어의 추상화라고 할 수 있다. 객체 지향 프로그래밍은 좀 더 현실을 반영하기 위한 것이다. 객체 지향의 문법을 이용해서 객체를 만든다고 되는것이 아니라 고도의 추상화 능력이 필요하다. 객체지향이 추구하는 지향점을 생각해보자.

# 객체 지향 프로그램의 지향점

> ### 부품화
프로그래밍은 정신적인 활동이므로 실체가 없고 무한하고 유연하다. 이러한 프로그래밍의 특성(소프트웨어도 상속받는)은 오해나 모순 같은 문제점을 발생한다. 이러한 문제접을 극복하기 위한 노력중에 하나가 부품화이다.

객체 지향은 부품화의 정점으로 메소드는 부품화의 예이다. 메소드의 사용 취지는 연관되어 있는 로직들을 겹합해서 메소드라는 완제품을 만드는 것이다. 그리고 이 메소드를 부품으로 하여 하나의 완제품인 독립된 프로그램을 만드는 것이다. 메소드를 사용하면 코드의 양도 줄일 수 있고, 메소드별 기능이 분류 되어 있어 문제의 진단과 필요한 코드가 찾기 쉽다.
  
메소드와 그 매소드가 사용하는 변수들을 분류하고 그룹핑하는 일이 필요해지면서 객체(Object)라는 개념이 생겼다. 파일과 디렉토리가 있을 때 메소드나 변수가 파일이라면 이 파일을 그룹핑하는 디렉토리가 객체라고 할 수 있다. 객체를 통해서 더 큰 단위의 부품을 만들 수 있게 되었다.

> ### 은닉화,캡슐화
부품화는 단순히 같은 기능을 하는 메소드와 변수를 그룹핑한다고 되는것이 아니다. 제대로된 부품이라면 어떻게 만들어졌는지 모르는 사람도 사용법만 알면 쓸 수 있어야 한다. 이를 은닉화(information Hiding) 또는 캡슐화(Encapsulation)라고 한다. 모니터가 어떻게 동작하는지 몰라도 컴퓨터와 모니터를 연결하는 방법만 알면 화면을 표시 할 수 있는 것과 같은 이치다. 자연스럽게 사용자에게는 그 부품을 사용하는 방법이 중요한 것이 된다.

> ### 인터페이스(interface)
인터페이스는 부품들 간의 약속이다. A사의 모니터와 B사의 모니터를 하나의 컴퓨터에 연결할 슀다. 모니터와 컴퓨터는 서로 교환관계에 있는 것이다. 이것은 모니터와 컴퓨터를 연결하는 케이블의 규격이 표준화 되어있기에 가능한 일이다. 모니터는 컴퓨터가 어떻게 만들어 졌는지, 컴퓨터는 모니터가 어떤 식으로 만들어졌는지 신경쓰지 않고 각각의 부품은 미리 정해진 약속에 따라 신호를 입/출력하고 연결점의 모양을 표준에 맞게 만들면 된다. 이를 인터페이스라고 한다. 
인터페이스는 이질적인 것들을 막아주는 역할도 한다. HDMI를 랜선에 연결할려고 해도 모양이 맞지않아 연결되지 않는것이 그 예이다.

지금까지 하드웨어에 비유하여 객체를 비유하였지만, 객체는 하드웨어가 아닌다. 객체는 하드웨어가 할 수 없는 것을 할 수 있는데 그 중 하나가 복제와 상속이다.


---------------------------------------

출처 : 객체지향 프로그래밍 - 생활코딩 


https://opentutorials.org/course/743/6553


출처 2 : 객체 지향 프로그래밍 - 위키백과 


https://ko.wikipedia.org/wiki/%EA%B0%9D%EC%B2%B4_%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D


출처 3 : 절차적 프로그래밍 - 위키백과


https://ko.wikipedia.org/wiki/%EC%A0%88%EC%B0%A8%EC%A0%81_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D
