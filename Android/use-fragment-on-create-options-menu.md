#Fragment에서 OnCreateOptionsMenu 사용

Fragment에서 OnCreateOtpionsMenu를 사용 하기 위해서는 onCreateView에 setHasOptionsMenu(true);를 해줘야 한다.

<pre>
 @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
        View view = inflater.inflate(R.layout.fm_mypage_favorite, container, false);
        setHasOptionsMenu(true);
        return view;
    }
</pre>
