# 프로젝트 명
Daily Box Office TOP10 

# 프로젝트 설명
오픈API를 이용해 영화 박스오피스를 시각화한 어플리케이션

## 전체적인 프로젝트 구현 


영화의 일일 박스오피스 순위의 정보를 가지고있는 JSON형식의 오픈API URL과 Key를 받아 웹서버에 요청한다.

<b>JSON형식의 데이터 이미지</b>
<img width="1000" height="50" src="./Png/JSON1.png"></img>

웹서버에 URL을 입력하고 요청하기 버튼을 클릭하면 입력한 날짜에 맞춰 박스오피스순위와 정보를 리싸이클러뷰에 표시된다.

이때 웹서버에 요청하고 응답을 받을 때 단순화하기 위해 volley라이브러리를 사용하는데 Volley를 사용하기 위해서는 Request 객체를 만들어 이 객체를 RequestQueue에 넣으면된다.

그 후 MovieList , MovieListResult ,Movie 클래스를 만든다. 이때 Movie 클래스 안에는 JSON문자열 형식에 영화정보를  입력한다.

<b>실제MovieList클래스에 적은 문자열</b>

<img width="300" height="150" src="./Png/movielist.png"></img>

객체를 반환할 클래스로 만든 MovieList 안에 boxofficeResult라는 변수를 추가한다. 이때 주의할 점은 JSON문자열에서 속성의 이름과 같아야 한다.
MovieListResult는 boxofficeResult를 담아둘 클래스를 정의한 것

<b>실제MovieListResult클래스에 적은 문자열</b>

<img width="300" height="150" src="./Png/movielisr.png"></img>

 위에서 만든  boxofficeResult를 담아두기 위해 만든 MovieListResult안에는 배열안에 객체들이 들어가는 경우 해당 객체들을 위한 클래스로 ArrayList를 만든다.

<b>실제Movie클래스에 적은 문자열</b>

<img width="250" height="455" src="./Png/1234.png"></img>

Movie 클래스에서는 JSON문자열 형식의 영화정보를 입력한다.

마지막으로 Movie의 객체를 관리하기 위하여 MovieAdaptet 클래스를 만들고 그 안에 ViewHoler 클래스를 static으로 정의한다. 이때  ViewHoler에 movie 객체가 담기게 된다. 여기서 textviw 또한 생성 한다. 

시각화 되어 보여줄 layout인 movie_item 레이아웃을 생성하고 그안에 cardview를 형식으로 만든다. 이제  MovieAdaptet 클래스가 recyclerview.adapter 클래스를 상속하도록 하게 만들면 리싸이클러뷰가 어댑터와 상호작용하면서 리스트모양으로 보여주게된다.


이제 사용자가 버튼을 누르면 듣답을 받았을 때 호출되는 메서드안에서 JSON문자열을 MovieList객체로 변환하며 그 안에 들어있는 Movie 객체들을 하나씩 어댑터에 추가하면서 왼쪽에는 팝콘이미지 그 옆으로는 순위, 영화제목, 개봉일 같은 영화정보와 일별 관람객 수, 누적 관람객 수, 홈페이지바로가기 버튼, 최신 상영작 페이지를 볼 수 있는 버튼이 나타난다.


## 응용한 부분


### RecyclerView , caraView  구현

activity_main.xml RecyclerView를 화면에 끌어와 다운로드를 진행한다 + caraView 도 같은 방법

### 중복 LinearLayout구현

중복 레이아웃이아웃은 하나의 레이아웃 안에 레이아웃을 여러개 만드는 걸 말한다.
프로젝트 안에서도 사용된 레이아웃은 총 6개로 중복 레이아웃을 통해서 수평 수직 배열의 형태로 지정할 수 있다. 

### TextView구현 

프로젝트 안에 작성한 TextView는 총5가지다. TextView1는 영화순위, TextView2는 영화제목, TextView3는 개봉일 , TextView4는 일별 관람객 수 TextView5는 누적 관람객 수를 보여주도록 만들었는데, 이는 RecyclerView 에서 상속을 받아 ViewHolder생성한 후 각각의 데이터를 받아 TextView로 표시를 해주는 방식으로 진행했다. 구현 하기 위해서는 MovieAdapter.java 페이지에서 작성하며 findViewById(R.id.textview); 코드를 입력해 xml과 연결시켜줘야한다. 

<b>TextView 꾸미기</b>

>1)android:textStyle="bold" 

>2)android:textColor="#E10B0B"

영화순위와 영화제목은 1)과 같이 textStyle 중에 bold 로 선택해 글씨를 굵게 표현하였고 일별 관람객 수와 누적 관람객 수에는 2)와  textColor를 지정해 글씨를 붉은색으로 지정했다.


### Button 구현

>public void B1(View V)

>{ Intent myIntent = new Intent(Intent.ACTION_VIEW, Uri.parse("이동할 페이지의 url 입력"));
   startActivity(myIntent);}

이 프로젝트에서의 버튼 두 개의 역할은 웹페이지 이동에 목적을 두고있다.
button1은 kobis mobile 페이지로, button2는 kobis mobile 최신상영작 페이지로 이동하는데 button 구현하는 방법은 OnClick 했을 때 불러올 함수를 지정하는 것이다. button1의 OnClick의 함수는 B1 으로 지정하고 button2의 OnClick의 함수는 B2로 지정했다. 그 후 MainActivity로 가서 button1의 OnClick의 함수인 B1을 호출하고 Intent 함수를 myIntent로 불러 위와 같은 코드를 작성한다. button2도 같은 방법으로 작성 가능하다.( 단,  button2의 함수는 B2)



### imeageView 구현

>app:srcCompat="@drawable/이미지이름" 

영화와 관련된 이미지가 어떤것이 있을까 고민하다가 영화하면 빠질 수없는 팝콘이 생각나, 무료 이미지제공 사이트에서 다운받아 res - drawavble에 팝콘이미지를 넣어준다. 그 후 이미지를 구현할 레이아웃인 movie_item 에서 ImageView를 추가하고 아래와 같은 코드를 작성한다.

- ### 주의 할 점

1. 앱이 인터넷 권한을 사용하므로 아래의 코드로 AndroidManifest.xml 에서 권한을 추가한다.

>uses-permission android:name="android.permission.INTERNET"

2. 그 후 <application> 안에 아래와 같은 속성을 추가한다.
   
>android:usesCleartextTraffic="true"

3.Gson은 JSON 문자열을 자바 객체로 변환해주고 Volley를 사용해서 웹서버로부터 JSON응답을 받아야 한다. 둘 다 외부라이브러리이기 때문에 사용하려면 build.gradle(Module:app) 라이브러리에 아래와 같은 코드를 추가해야한다.

>implementation 'com.android.volley:volley:1.1.0'

>implementation 'com.google.code.gson:gson:2.8.5'

4. activity_main.xml 에서 text 속성 값에 사이트 URL을 미리 넣어 둘 때, URL이 XML 레이아웃 안에 들어갈 때는 & 기호를 인식하지 못하므로 &#38; 기호로 바꾸어 넣어줘야 한다.

>예시 ) c3ca0e&;targetDt=20200101  -> c3ca0e&#38;targetDt=20200101




## 디자인

<b>1.웹 요청 화면 </b>

(왼쪽) 기존 화면</b>  <b>(오른쪽) 변경 화면</b>

<img width="250" height="455" src="./Png/777.png"></img>
<img width="250" height="455" src="./Png/design2.png"></img>

이 프로젝트 명인 Daily Box Office TOP10 맨 위 상단에 textview로 나타내고 기존에 자리를 많이 차지했던 요청하기 버튼을 imageButton으로 돋보기 모양으로 변경하여 정보를 나타낼 수 있는 공간을 확보했다. 

2.정보 시각화 화면

<img width="500" height="280" src="./Png/design1.png"></img>

## 결과 화면

<img width="250" height="455" src="./Png/b.png"></img>
<img width="250" height="455" src="./Png/c.png"></img>



