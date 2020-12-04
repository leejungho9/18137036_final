# 프로젝트 명
오픈API를 이용해 영화 박스오피스를 시각화한 어플리케이션

## 프로젝트 구현 
영화의 정보를 받아올 수 있는 JSON형식의 오픈API URL과 Key를 받아 웹서버에 요청한다.
요청하기버튼을 클릭 시, 입력한 날짜에 맞춰 박스오피스순위와 정보를 불러온다. 
RecyclerView과 cardView를 다운로드 하여 list형식으로 나열하고 margin 값을 주어 테두리가 띄어지며 그림자지게 만든다.
그후 중복으로 LinearLayout 을 vertical 형식으로 나타내 오른쪽으로 두 개의 버튼을 차례로 나열했다. 




### TextView구현 
프로젝트 안에 작성한 TextView는 총5가지다. TextView1는 영화 순위, TextView2는 영화제목, TextView3는 개봉일 , TextView4는 일별 관람객 수 TextView5는 누적 관람객 수를 보여주도록 만들었는데, 이는 RecyclerView 에서 상속을 받아 ViewHolder생성해 ViewHolder 각각의 데이터를 받아 TextView로 표시를 해주는 방식으로 진행했다.
구현을 하기 위해서는 MovieAdapter.java 페이지에서 작성하며 findViewById(R.id.textview); 코드를 입력해 xml과 연결시켜줘야한다.





### Button 구현
이 프로젝트에서의 버튼 두 개의 역할은 웹페이지 이동에 목적을 두고있다.
button1은 kobis mobile 페이지로 , button2는 kobis mobile 최신상영작 페이지로 이동하는데
button 구현하는 방법은 OnClick 했을 때 불러올 함수를 지정하는 것이다. button1의 OnClick의 함수는 B1 으로 지정하고 button2의 OnClick의 함수는 B2로 지정했다.
그 후 MainActivity로 가서 button1의 OnClick의 함수인 B1을 호출하고 Intent 함수를 myIntent로 불러 아래와 같은 코드를 작성한다. button2도 같은 방법으로 작성 가능하다.( 단,  button2의 함수는 B2)

public void B1(View V)
{
   Intent myIntent = new Intent(Intent.ACTION_VIEW, Uri.parse("이동할 페이지의 url 입력"));
   startActivity(myIntent);
}
