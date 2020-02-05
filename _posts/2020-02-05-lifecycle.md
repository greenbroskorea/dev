# Lifecycle

## 발달원인
액티비티 활동 주기에 맞춰야 되는 기능의 경우에 보통 onStart(), onStop() 에 맞춘다.
기능들이 늘어나 관리하게 되면 유지가 힘들어진다.

## 종류
액티비티 수명주기는 LifecycleOwner
앱 전체 수명주기는 ProcessLifecycleOwner

## 사용법
수명주기 상태의 변경에 반응하는 로직이 액티비티 대신 리스너에서 선언된다.
class MyActivity extends AppCompatActivity {
        private MyLocationListener myLocationListener;

        public void onCreate(...) {
            myLocationListener = new MyLocationListener(this, getLifecycle(), location -> {
                // update UI
            });
            Util.checkUserStatus(result -> {
                if (result) {
                    myLocationListener.enable();
                }
            });
      }
    }
	
class MyLocationListener implements LifecycleObserver {
        private boolean enabled = false;
        public MyLocationListener(Context context, Lifecycle lifecycle, Callback callback) {
           ...
        }

        @OnLifecycleEvent(Lifecycle.Event.ON_START)
        void start() {
            if (enabled) {
               // connect
            }
        }

        public void enable() {
            enabled = true;
            if (lifecycle.getCurrentState().isAtLeast(STARTED)) {
                // connect if not connected
            }
        }

        @OnLifecycleEvent(Lifecycle.Event.ON_STOP)
        void stop() {
            // disconnect if connected
        }
    }

- Lifecycle : 액티비티의 상태를 저장하고 옵저버들에게 상태변화를 알려준다.
- LifecycleOwner : 액티비티를 의미하고 내부에 Lifecycle 을 갖고 있다.
- LifecycleObserver : 생성하여 Lifecycle 에 등록하면 상태변화가 생길때마다 알림을 받는다.

참고
* https://developer.android.com/topic/libraries/architecture/lifecycle?hl=ko
* https://codechacha.com/ko/android-jetpack-lifecycle/
