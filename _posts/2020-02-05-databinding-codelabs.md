# data binding codelabs

- findViewById() 의 여러번 호출로 인한 느려짐을 해결하고, 잘못된 findViewById() 호출을 막아준다.
- onCreate() 에서 값의 초기화가 가능하다.
- android:onClick 으로 메소드 호출하는 것은 안전하지 않지만 data binding 으로 호출된 메소드는 런타임에 충돌한다.
- 액티비티와 프래그먼트의 많은 코드를 밖으로 빼면 테스트와 유지보수에 좋다.

- xml 레이아웃에 data binding 을 추가할때 <data> 부분에는 레이아웃 표현법(layout expressions)으로 작성해야 한다.
- 하지만 복잡한 코드를 레이아웃에 작성하는 것은 읽기 어렵고 유지보수가 힘들다.

레이아웃 표현법의 장점
- 앱 성능 향상
- 메모리 누수와 널 포인터 에러 방지.
- UI 프레임웍 호출을 제거하여 액티비티 코드 간소화.
