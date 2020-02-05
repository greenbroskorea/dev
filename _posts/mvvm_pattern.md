MVVM 패턴(Software Architectural pattern)

1. 기원
사용자 인터페이스의 사건 기반 프로그래밍을 단순하게 만들 목적으로 마이크로소프트의 설계자 켄 쿠퍼와 테드 페스터스에 의해 발명되었다.
마이크로스프트의 존 고스먼이 2005년 자신의 블로그에 발표하였다.
MVVM 을 구현하는 부하가 단순한 UI 동작에 대해 지나칠 정도로 심하다고 존 고스먼 자신이 지적했다.

참고
* MVVM 은 Model, View, ViewModel 의 약어
* 위키백과

2. 사용이유
굳이 패턴을 사용하지 않아도 프로그램이 충분히 돌아가는 코드를 짤 수 있는데 사용하는 이유

- 유지보수(가독성, 테스트, 기능에 대한 CRUD, 버그수정)
- 비즈니스 및 프레젠테이션 로직이 분리되어 있어 디자이너도 공동작업하기 좋다.

참고
* https://poqw.github.io/about_mvvm/

3. 원리
![image1](./_posts/image1.png)

- 사용자의 action 이 view 를 통해 들어온다.
- command 패턴으로 view 가 action 을 view model 에 전달한다.
- view model 이 필요한 데이터를 model 에 요청한다.
- model 이 요청받은 데이터를 가져와 그대로 응답한다.
- view model 이 받은 데이터를 가공하여 저장한다.
- view 가 view model 과 data binding 하여 화면에 나타낸다.

----------------------------------------------------------------------------------

![image2](./image2.png)

- view 는 view model 을 인식하고 view model 은 model 을 인식한다.
- 반대로 model 은 view model 을 인식하지 않고 view model 은 view 를 인식하지 못한다.
- 따라서 view model 은 중간에서 model 과 view 를 독립적으로 발전시킬 수 있다.

참고
* 첫그림자료
* 마이크로소프트(한글)

4. View
사용자가 화면에서 볼 수 있는 구조, 레이아웃 및 모양을 정의하는 작업 담당.

5. ViewModel
view model 은 view 가 데이터 바인딩할 수 있는 속성 및 명령을 구현하고 변경 알림 이벤트를 통해 상태 변경을 뷰에 알립니다.
view model 에서 제공하는 속성 및 명령은 ui 에서 제공되는 기능을  정의하지만 뷰는 해당 기능을 표시하는 방법을 결정합니다.
view model 은 필요한 모델 클래스와 뷰의 상호작용을 조정해야 합니다.

6. Model
model 은 응용 프로그램의 데이터를 캡슐화하는 비시각적 클래스입니다.

* 마이크로소프트(한글)

7. Android MVVM
Android Jetpack 에 포함된  Architecture Components 인 LiveData, ViewModel 을 이용.
LiveData 사용시 Lifecycle 도 같이 사용한다.
LiveData 대신 RxJava 를 사용할 수 있다.
DataBinding 라이브러리도 같이 사용한다.
