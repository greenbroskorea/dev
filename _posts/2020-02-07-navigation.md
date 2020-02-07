# [탐색 (Navigation)](https://developer.android.com/guide/navigation)

## 1. 구성요소
- 탐색 그래프(navigation graph) : 모든 탐색 관련 정보가 하나의 중심 위치에 모여있는 xml.
- NavHost : 탐색 그래프에서 대상을 표시하는 빈 컨테이너.
NavHost 를 상속한  NavHostFragment 가 기본 프래그먼트가 된다.
- NavController : NavHost 에서 앱 탐색을 관리하는 객체.
사용자가 앱 내에서 이동할 때 NavHost 의 컨텐츠를 전환한다. (NavHostFragment 에 들어가는 프래그먼트를 변경하는 역할)

## 2. 이점
- 프래그먼트 트랜잭션 처리.
- 기본적으로 '위로' 와 '뒤로' 작업을 올바르게 처리.
- 애니메이션과 전환에 표준화된 리소스 제공.
- 딥링크 구현 및 처리.
https://developer.android.com/guide/navigation/navigation-deep-link
- 최소한의 추가 작업으로 탐색 UI 패턴(탐색 창 navigation search, 하단 탐색 bottom navigation) 포함.
- Safe Args : 대상 사이에서 데이터를 탐색하고 전달할 때 유형 안정성을 제공하는 그래프 플러그인.
- ViewModel 지원 : 탐색 그래프 대상 사이에 UI 관련 데이터 공유.
- Navigation Editor 를 사용해 탐색 그래프를 확인하고 편집할 수 있다.

## 3. 탐색 그래프, 중첩 그래프(nested graphs)
탐색 편집기를 이용해서 프래그먼트의 흐름을 만들어준다.
구분해서 묶어줄 필요가 있는 흐름은 중첩그래프를 이용해서 그룹화해준다.
예를 들어 로딩화면 -> 로그인화면 -> 메인화면에서 로딩, 로그인은 중첩 그래프로 만들어주면 유용하다.
만약 인증 문제등이 발생하면 조건부 탐색을 이용하여 다시 로그인화면으로 이동시켜줄 수 있다.

## 4. 전역 작업(Global Actions)
전역 작업을 사용하여 여러 대상에서 사용할 수 있는 공통 작업을 만들 수 있다.
예를 들어 여러 프래그먼트의 버튼이 동일한 기본 앱 화면으로 이동할 수 있다.

## 5. 대상으로 이동(navigate to destination)
NavController 를 사용하면 몇 가지 방식으로 대상으로 이동할 수 있다.

NavController 를 호출하는 방법은 세가지가 있다.
- NavHostFragment.findNavController(Fragment)
- Navigation.findNavController(Activity, @IdRes int viewId)
- Navigation.findNavController(View)
