# Data Binding 사용법
1. 레이아웃 속성에 기본값 지정
`<TextView android:text="@{user.firstname, default=my_default}" />`
기본값 지정 가능

2. <data> 태그에서 클래스 변수 선언
```
<variable name="user" type="com.example.User">
```
클래스 타입 지정 가능

3. 데이터 결합에 사용하는 클래스 정의
```
public class User {
 public final String firstName;
 public final String lastName;

 public User(String firstName, String lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
 }

 public String getFirstName() {
  return this.firstName;
 }

 public String getLastName() {
  return this.lastName;
 }
}
```
데이터 결합에 사용할 클래스에는 한번 읽은 이후에 변경되지 않는 데이터가 일반적.
위와 같이 정의되어 있어도 레이아웃에서 접근시 @{user.firstName}.

4. 데이터 결합 생성
```
ActivityMainBinding binding = DataBindingUtil.setContentView(this, R.layout.activity_main);
User user = new User("Test", "User");
binding.setUser(user);

ActivityMainBinding binding = ActivityMainBinding.inflate(getlayoutInflater());

ListItemBinding binding = ListItemBinding.inflate(layoutInflater, viewGroup, false);

ListItemBinding binding = DataBindingUtil.inflate(layoutInflater, R.layout.list_item, viewGroup, false);

View viewRoot = LayoutInflater.from(this).inflate(layoutId, parent, attachToParent);
ViewDataBinding binding = DataBindingUtil.bind(viewRoot);
```

5. Null 병합 연산자
```
android:text="@{user.firstName ?? user.lastName}"
```

6. 컬렉션 선언
```
<data>
 <import type="java.util.Map" />
 <variable name="map" type="Map&lt;String, String>"/>
</data>

android:text="@{map[key]}"
```

7. 문자열 리터럴
```
android:text="@{map['firstName']}"
```
", ' 사용을 반대로도 가능.

8. 메서드 참조
```
public void onClickFriend(View view)

android:onClick="@{handlers::onClickFriend}"
```
매개변수가 View 이면 위와 같이 호출 가능.

```
public void onSaveClick(Task task)

<variable name="task" type="com.android.example.Task" />

android:onClick="@{() -> presenter.onSaveClick(task)}"
```
일반적인 메서드 호출.

9. 클래스 가져오기
```
<data>
 <import type="android.view.View" />
</data>
```

10. 식별 가능한 데이터 개체 작업
변수가 수정되면 UI 가 자동으로 업데이트 되도록 관찰한다.
Android Studio 3.0 이하에서는 Observable 사용. (ex. ObservableBoolean)

11. 결합 어댑터 자동 메서드 선택
```
app:drawerListener="@{fragment.drawerListener}"
```
setDrawerListener(DrawerListener) 를 호출한 것과 동일.

12. 결합 어댑터 여러 속성 사용
```
<ImageView app:imageUrl="@{venue.imageUrl}" app:error="@{@drawable/venueError}" />

@BindingAdapter({"imageUrl", "error"})
public static void loadImage(ImageView view, String, url, Drawable error) {
 Picasso.get().load(url).error(error).into(view);
}
```
loadImage() 에서 view 는 기본으로 전달되는 매개변수이고, @BindingAdapter 로 지정하는 변수가 순서대로 이어져 값이 전달된다. requireAll=false 를 추가하면 값을 설정하지 않았을때 기본값이 설정된다.(Int = 0)

참고
- https://developer.android.com/topic/libraries/data-binding?hl=ko
