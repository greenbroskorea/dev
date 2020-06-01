## 06.01
### Chip 컴포넌트
- gradle 추가 : implementation 'com.android.support:design:28.0.0'
- style AppThmeme : parent="Theme.AppCompat.Light.NoActionBar" 사용해야함
- [Chip component](https://medium.com/wasd/material-design-chip-%EC%82%AC%EC%9A%A9%EB%B2%95-in-android-154f29f88241)
- [이슈] click 리스너 사용시 seletion index 값을 알 수 없음
  - setTag로 데이터 지정해도 값을 못 읽어옴.
  
### Binding
- 서버데이터에서 휴대폰번호를 화면에 보여줄땐 dash값 형태로 포맷하고 서버 업데이트할 땐 dash값 제거하고 싶을땐?
  - Live Data에서 init형식으로 포맷데이터 넣고 request할 LiveData 값을 따로 만든다.
  - [Transformations로 LiveData 사용하기](https://wooooooak.github.io/android/2019/07/13/liveData%EB%B3%80%ED%98%95%ED%95%98%EA%B8%B0/)
  
## 05.26
- [데이터 바인딩 String - Find keyword> Many ways to concat strings](https://stackoverflow.com/questions/40039942/i-want-to-concat-two-strings-for-a-textview-in-android-data-binding-api)

- [json to kotlin plugin](https://lonepine.tistory.com/entry/Android-Studio-%EC%97%90%EC%84%9C-JSON-Kotlin-Class-%EC%89%BD%EA%B2%8C-%EB%A7%8C%EB%93%A4%EA%B8%B0)

- [코틀린 반복문 탈출하기](https://kotlinlang.org/docs/reference/returns.html)

- [constraint layout child view 비율 맞추기](http://dktfrmaster.blogspot.com/2018/05/constraintlayout-11.html)

### 자주쓰는 IntliJ 단축키
- 라인 복제하기
  - MacOS: Cmd + d
  - Win/Linux: Ctrl + d
- 라인 삭제하기
  - MacOS: Cmd + 백스페이스
  - Win/Linux: Ctrl + y
- 이름 일괄 변경하기 (Rename)
  - MacOS: Shift + F6
  - Win/Linux: Shift + F6
- 라인별 코드 일괄 수정
   - Win/Linux: Alt + 마우스 드래그
- 전체 파일 목록 검색
   - Shift, Shift
- [단축키 문서](https://gmlwjd9405.github.io/2019/05/21/intellij-shortkey.html)
