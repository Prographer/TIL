Fragment 안에 TabLayout같은 것을 할 경우 FragmentAdapter생성자에 getActivity().getSupportFragmentManager()를 넘겨주는데
이럴 경우 다시 해당 Fragment를 Load 할 경우 Adapter의 getItem이 안 먹는 문제가 있다.

이럴 경우 getActivity().getSupportFragmentManager() 대신 getChildFragmentManager()를 써야 한다.
