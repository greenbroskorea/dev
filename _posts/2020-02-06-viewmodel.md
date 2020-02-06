# ViewModel
수명 주기를 고려하여 UI 관련 데이터를 저장하고 관리하도록 설계되었다.
뷰모델 객체는 구성이 변경되는 동안 자동으로 보관된다.

## 1. 구현
계속 가지고 있어야 하는 데이터라면 액티비티나 프래그먼트가 아닌 뷰모델에 보관한다.
예를 들어 사용자 정보를 다음과 같이 보관시킨다.

```
public class MyViewModel extends ViewModel {
    private MutableLiveData<List<User>> users;
    public LiveData<List<User>> getUsers() {
        if (users == null) {
            users = new MutableLiveData<List<User>>();
            loadUsers();
        }
        return users;
    }

    private void loadUsers() {
        // Do an asynchronous operation to fetch users.
    }
}
```
    
사용자 정보의 접근은 다음과 같이 한다.

```
public class MyActivity extends AppCompatActivity {
    public void onCreate(Bundle savedInstanceState) {
        // Create a ViewModel the first time the system calls an activity's onCreate() method.
        // Re-created activities receive the same MyViewModel instance created by the first activity.

        MyViewModel model = ViewModelProviders.of(this).get(MyViewModel.class);
        model.getUsers().observe(this, users -> {
            // update UI
        });
    }
}
```


## 2. 수명주기
수명주기는 ViewModelProvider 에 전달되는 Lifecycle 로 지정된다.
범위가 지정된 Lifecycle 이 영구적으로 경과될 때까지(?), 액티비티가 종료되거나 프래그먼트가 분리될 때까지 메모리에 남아있는다.

아래 그림은 액티비티의 주기동안 뷰모델의 유지범위를 보여준다.
finish() 가 호출된 이후에 완전히 Finished 상태가 될때까지 뷰모델은 존재한다.

![뷰모델 수명주기](https://developer.android.com/images/topic/libraries/architecture/viewmodel-lifecycle.png?hl=ko)


## 3. 프래그먼트간 데이터 공유
뷰모델을 이용하면 여러 프래그먼트 간에 데이터를 쉽게 공유할 수 있다.

아래 코드를 보면 하나의 뷰모델을 두 프래그먼트가 공유하는데 한 프래그먼트는 데이터를 주입하고 다른 프래그먼트는 옵저버로 등록하여 알림을 받는다.

```
public class SharedViewModel extends ViewModel {
    private final MutableLiveData<Item> selected = new MutableLiveData<Item>();

    public void select(Item item) {
        selected.setValue(item);
    }

    public LiveData<Item> getSelected() {
        return selected;
    }
}

public class MasterFragment extends Fragment {
    private SharedViewModel model;
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        model = ViewModelProviders.of(getActivity()).get(SharedViewModel.class);
        itemSelector.setOnClickListener(item -> {
            model.select(item);
        });
    }
}

public class DetailFragment extends Fragment {
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        SharedViewModel model = ViewModelProviders.of(getActivity()).get(SharedViewModel.class);
        model.getSelected().observe(this, { item ->
           // Update the UI.
        });
    }
}
```

    
## 4. 데이터베이스 변경을 UI 업데이트로 자동연결
뷰모델은 Room 및 LiveData 을 사용하여 CursorLoader 를 대체할 수 있다.
데이터베이스가 변경되면 룸이 라이브데이터로 변경알림을 보내고, 라이브데이터는 변경된 데이터로 UI 를 업데이트한다.

![데이터베이스에서 뷰모델로의 데이터 흐름](https://developer.android.com/images/topic/libraries/architecture/viewmodel-replace-loader.png?hl=ko)
