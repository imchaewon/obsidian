제이쿼리 cdn

https://releases.jquery.com/

1.12.4버전
<script
  src="https://code.jquery.com/jquery-1.12.4.min.js"
  integrity="sha256-ZosEbRLbNQzLpnKIkEdrPv7lOy9C27hHQ+Xp8a4MxAQ="
  crossorigin="anonymous"></script>

----------------------------------------------------------------------------------------------------

탭메뉴

$(".fbtab").siblings().hide()

$(".fbtab a").click(function(){
	$(this).addClass("on").siblings().removeClass("on")
	var idx = $(this).index()
	$(".fbtab_wrap > div:eq("+idx+")").addClass("on").siblings().removeClass("on")
})


탭메뉴2

$(".sub_tab>li").click(function(){
	var idx=$(this).index()
	if($(this).hasClass("active")){
	}else{
		$(this).addClass("active").siblings("li").removeClass("active")
		$(".sub_con>li:eq("+idx+")").show().siblings("li").hide()
	}
});


index없이 해도될때 if로

<div class="msl-r-b">
	<div class="tab">
		<a href="javascript:;" class="on">1</a>
		<a href="javascript:;">2</a>
	</div>
	<ul>
		<li></li>
		<li></li>
	</ul>
	<ul style="display:none">
		<li></li>
		<li></li>
	</ul>
</div>
<script>
	$(".msl-r-b .tab a").click(function(){
		if($(this).hasClass("on")){
		}else{
			$(".tab").children("a").toggleClass("on")
		}
		$(".tab").siblings("ul").toggle()
	})
</script>


탭메뉴영역이 페이지내에 여러개일때(선택자바꿔서수정하기) ★토글안되면 addClass/removeClass,show/hide로

$(".Fls .stit span").click(function(){
	var idx=$(this).index()
	if($(this).hasClass("on")){
	}else{
		$(this).toggleClass("on").siblings("span").toggleClass("on")
		$(this).closest(".fortb").find(".con").eq(idx).toggle().siblings().toggle()
	}
})
(★find는 하위 모두찾기 children은 바로밑 계층에서만 찾음)
$(".tabTwo-tab li").click(function(){
	var idx=$(this).index()
	if($(this).hasClass("on")){
	}else{
		$(this).toggleClass("on").siblings("li").toggleClass("on")
		$(".tabTwo-con").children("li").eq(idx).toggle().siblings().toggle()
	}
})


메뉴리스트..

$(".menu-list .depth1_in_T").click(function(){
	if($(this).hasClass("on"))
	{
		$(this).removeClass("on");
		$(this).children(".depth2").stop(true,true).slideUp(200,function(){
			resetSwipe();
		});
	}
	else
	{
		$(".menu-list .depth1_in_T").not($(this)).removeClass("on")
		$(this).addClass("on")
		$(".menu-list .depth2").not($(this).next(".depth2")).stop(true,true).slideUp(200);
		$(this).children(".depth2").stop(true,true).slideDown(200,function(){
			resetSwipe();
		});
	}
});

toggle 안쓰고 한번씩 슬라이드,아이콘 변경

$(".head_top .btnMoreMenu").click(function(){
	if($(this).hasClass("on")){
		$(this).removeClass("on").text("expand_more");
		$(".head_top .moreMenu").removeClass("on");
	}else{
		$(this).addClass("on").text("expand_less");
		$(".head_top .moreMenu").addClass("on");
	}
})

----------------------------------------------------------------------------------------------------

index eq 쓰는법2

$("li .langType").click(function(){
	var idx = $("li .langType").index(this)		← 이렇게 var 꼭 click function 안에다 쓰기
	console.log(idx)
	$(this).addClass("on").siblings().removeClass("on")
	$("li>ul").eq(idx).slideDown() ← ul안 어딘가에 ul이 또 있을수 있으므로 > 꺽새 해줌 (안하면 안됨)
});

----------------------------------------------------------------------------------------------------

a 태그 위쪽으로 안올라가게 (e.preventDefault 대용)

<a href="#"></a>
<a href="javascript:;"></a>

----------------------------------------------------------------------------------------------------

a태그 걸린 #막기 (href="javascript:;" 대용)

menu1.click(function(){
	e.preventDefault();
})

----------------------------------------------------------------------------------------------------

제이쿼리 a태그 걸린링크이동막기 (이벤트막음)

var menu1=$('.menu li:nth-child(1) a');

menu1.click(function(){
	event.preventDefault();  ← 이줄
	all.fadeIn();
});


혹은 아래처럼 매개변수로
$(".back a").click(function(e){
	e.preventDefault();
	$("html,body").animate({
		scrollTop:0
	},2000)
});

----------------------------------------------------------------------------------------------------

stopPropagation 은 부모태그로의 이벤트 전파를 stop 중지하라는 의미입니다
예시) http://programmingsummaries.tistory.com/313

----------------------------------------------------------------------------------------------------

체크박스/라디오

① 체크 상태 판별하기
1. $("").is(":checked")
2. $("").prop("checked")
4. $(":checked") ★이건 체크된걸 선택하는 선택자이다. 라디오버튼중 뭘 선택했는지 체크해야할때는 이걸로 해야함
	if($("input[name='WAY']:checked").val()){


② 체크/해제 시키기
attr / prop

prop : disabled,checked와 같은 속성 값이 없는 불타입에 주로 사용.
  이때 마크업에는 check유무가 표시가 안되고 내부적으로 체크상태로 전환됨
attr : 모든속성에 사용가능, attr로 처리할경우 체크상태도 is나 prop가 아닌 attr로 판별해야하고
  css도 input:checked{}가 아니고 input[checked='checked']{} 이렇게 해야됨

$("").prop("checked",true)
$("").attr("checked",true)

----------------------------------------------------------------------------------------------------

제이쿼리 animate , css 여러개 숫자는""없이

<script>
.css("width",80)  --- 한개
.css({"width":80,"background":"red"})  --- 여러개
</script>

----------------------------------------------------------------------------------------------------

제이쿼리 윈도우 사이즈 구하기

<script>
	var windowHeight = $(window).height();
	var aaaa = windowHeight/3
	var bb = $(".tt")

	bb.css('height' , aaaa) --- var(변수) 사용시 ""쓰면안됨
</script>

----------------------------------------------------------------------------------------------------

제이쿼리 너비/높이 빼기 , 나누기

<script>
	$(".img_wrap").height($(".new_prd").height()-$(".new_prd .txt").height());

	$('.new_prd .img').each(function(){
		var img_visualsize = $(this).height()/2;
		$(this).css('margin-top' , - img_visualsize);
	})
</script>

----------------------------------------------------------------------------------------------------

제이쿼리 뒤로가기

$(".back").click(function(){
	history.go(-1);
});


마찬가지로 뒤로가기

<a href="#" onclick="location.reload();">새로고침</a> 
<a href="javascript:history.back(-1)">뒤로가기</a> 
<a href="javascript:history.go(1)">앞으로가기</a> 

이미지로 만들때
<a href="#" onclick="location.reload();"><img src="이미지 주소">새로고침</a> 
<a href="javascript:history.back(-1)"><img src="이미지 주소">뒤로가기</a> 
<a href="javascript:history.go(1)"><img src="이미지 주소">앞으로가기</a>   

----------------------------------------------------------------------------------------------------

css 백그라운드
오른쪽에서 15px
background:url('/m/images/bottom_ico14.png') no-repeat right 15px center #fff; background-size:15px;

----------------------------------------------------------------------------------------------------

넓이가 100%로 정해져있지 않을경우 좌우 + / - margin 가능 (100%로 되있을시 한쪽만됨)

----------------------------------------------------------------------------------------------------

리스트 만들기

<ul>
	<li>
		<div class="liWrap">
	
		</div>
	</li>
</ul>

ul - font-size:0;margin:0 -5px(li패딩만큼 ★ul에 width가 정해져있으면 부모기준 -,+ 마진이 안됨 쓰지말거나 빼거나auto하기 , 써야되는 상황이면 랩추가)
	또한 display:table을 넣을경우 foont-size:0을 한것과 동일한 효과가 나옴
li - display:inline-block;width:50%(한줄에 리스트 개수대로 퍼센트설정 2개면50% 3개면33.3%);padding:0 5px;box-sizing:border-box(내부 패딩);
.liWrap - 선/배경 등 적용용 랩

----------------------------------------------------------------------------------------------------

이미지 높이가 달라 리스트 틀어지는거 수정
ul{font-size:0;★중요}   margin:- 쓰면안댐
li{width:50%;padding:7.5px;box-sizing:border-box;position:relative;display:inline-block; vertical-align:top or bottom;}

----------------------------------------------------------------------------------------------------

word-break 속성

keep-all : 문자가 아닌 단어기준으로 줄바꿈하되, 영역을 벗어난것들은 벗어나는데로 놔둠
break-word : 문자가 아닌 단어기준으로 줄바꿈하되, 영역을 벗어난것들은 어쩔수없이 줄바꿈
normal : CJK(한,중,일) 문자는 문자줄바꿈, 그 외는 단어줄바꿈
initial : 기본값

------------------------------

css글자 말줄임

h1{display:inline-block;width:98%;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}


여러줄일때

.ellipsis{overflow:hidden;text-overflow:ellipsis;display:-webkit-box;-webkit-line-clamp:3; /* 라인수 */-webkit-box-orient:vertical;word-wrap:break-word;line-height:1.2em;height:3.6em; /* line-height 가 1.2em 이고 3라인을 자르기 때문에 height는 1.2em * 3 = 3.6em */}

★ 1줄에서 여러줄짜리로바꿀라면 white-space:nowrap; 빼야댐

height 안넣어도되고 세로리스트인경우는 height쓰기 , 아래쪽패딩 넣으면 글자가 보이니 위패딩이나 마진으로 하기

----------------------------------------------------------------------------------------------------

폰트(글꼴)가 무언가 다른 페이지랑 안맞다? or 적용이 잘 안된다? → 폰트를 import시켰나 확인!!! @import url('');

----------------------------------------------------------------------------------------------------

폰트어썸 최신버전(다양한대신무거움 CDN으로 쓰기) - http://fontawesome.io/
폰트어썸 구버전(최신버전보단종류적지만가볍) - https://fontawesome.com/v4.7.0/

----------------------------------------------------------------------------------------------------

아이콘폰트

.ftic-local:before { content: "\e600"; } /* 로컬 */
.ftic-home:before { content: "\e601"; } /* 홈 */
.ftic-mypage:before { content: "\e602"; } /* 마이페이지 */
.ftic-like:before { content: "\e606"; } /* 좋아요&찜한상품 */
.ftic-like2:before { content: "\e626"; } /* 좋아요2&찜한상품2 */
.ftic-zan:before { content: "\e62e"; } /* 엄지, 좋아요 */
.ftic-cart:before { content: "\e604"; } /* 장바구니 */
.ftic-cart2:before { content: "\e63c"; } /*장바구니2*/
.ftic-fax:before { content: "\e61e"; } /* 팩스 */
.ftic-set:before { content: "\e60f"; } /* 설정 */
.ftic-del:before { content: "\e612"; } /* 삭제 */
.ftic-pc:before { content: "\e60e"; } /* PC */
.ftic-cmt:before { content: "\e617"; } /* 댓글 */
.ftic-tel:before { content: "\e61d"; } /* 전화 */
.ftic-warning:before { content: "\e61f"; } /* 경고 */
.ftic-coupon:before { content: "\e609"; } /* 쿠폰1 */
.ftic-coupon2:before { content: "\e60a"; } /* 쿠폰2 */
.ftic-write:before { content: "\e614"; }  /* 편집,쓰기 */
.ftic-search:before { content: "\e613"; } /* 검색 */
.ftic-search2:before { content: "\e637"; } /* 검색 Bold */
.ftic-close:before { content: "\e60d"; } /* 닫기 */
.ftic-coupon-list:before { content: "\e618"; } /* 쿠폰사용내역 */
.ftic-id:before { content: "\e60b"; } /* 아이디 */
.ftic-distribution:before { content: "\e608"; } /* 배송 */
.ftic-fail:before { content: "\e620"; } /* 실패 */
.ftic-intro:before { content: "\e611"; } /* 회사소개 */
.ftic-cscenter:before { content: "\e619"; } /* 고객센터 */
.ftic-member-list:before { content: "\e61a"; } /* 회원리스트 */
.ftic-lately:before { content: "\e607"; } /* 최근 본 상품 */
.ftic-watch:before { content: "\e635"; } /* 시계 */
.ftic-fund:before { content: "\e61b"; } /* 적립금 */
.ftic-faqqna:before { content: "\e60c"; } /* FAQ,QNA */
.ftic-gotop:before { content: "\e610"; } /* 위로가기 */
.ftic-qmark:before { content: "\e622"; } /* 물음표 */
.ftic-inquire:before { content: "\e61c"; } /* 1:1문의하기 */
.ftic-allmenu:before { content: "\e603"; } /* 전체메뉴,카테고리 */
.ftic-pw:before { content: "\e616"; } /* 비밀번호 */
.ftic-join:before { content: "\e615"; } /* 회원가입 */
.ftic-telfax:before { content: "\e621"; } /* 전화&팩스 */
.ftic-other:before { content: "\e605"; } /* 기타 */
.ftic-prompt:before { content: "\e623"; } /* 주의 */
.ftic-success:before { content: "\e624"; } /* 성공 */
.ftic-fenxiang:before { content: "\e62b"; } /* 공유하기1 */
.ftic-fenxiang2:before { content: "\e627"; } /* 공유하기2 */
.ftic-back:before { content: "\e62d"; } /* 이전 */
.ftic-next:before { content: "\e625"; } /* 다음 */
.ftic-next2:before { content: "\e62a"; } /* 다음2 */
.ftic-top:before { content: "\e62c"; } /* 위 */
.ftic-bottom:before { content: "\e629"; } /* 아래 */
.ftic-card:before { content: "\e628"; } /* 카드 */
.ftic-staron:before { content: "\e630"; } /* 별on */
.ftic-staroff:before { content: "\e62f"; } /* 별off */
.ftic-star05:before { content: "\e636"; } /* 반별 */
.ftic-phone:before { content: "\e631"; } /* 핸드폰 */
.ftic-login:before { content: "\e633"; } /* 등록 */
.ftic-logout:before { content: "\e632"; } /* 탈퇴 */
.ftic-calendar:before { content: "\ee634"; } /* 달력 */
.ftic-list:before { content: "\e63a"; } /* list */
.ftic-list1:before { content: "\e63b"; } /* list1 */
.ftic-list2:before { content: "\e63f"; } /* list2 */
.ftic-list3:before { content: "\e63e"; } /* list3 */
.ftic-gallery:before { content: "\e638"; } /* 겔러리 */
.ftic-Favorites:before { content: "\e639"; } /*즐겨찾기 깃발모양*/

없으면 https://material.io/icons/ 여기꺼 (구글폰트)

----------------------------------------------------------------------------------------------------

이모지(아이콘폰트 비슷한것)
https://www.emojiengine.com/ko/
https://snskeyboard.com/emoji/

- 아이콘폰트에비해 사용법은 간단
- 벡터인 아이콘폰트에 비해 선명하지 못함. 확대를 해보면 이미지의 선명도에 차이가 발생
- 색상의 선택이 제한적
- 대칭형 아이콘이 아니여서 애니메이션이 부자연스러움
https://sonylove.tistory.com/1450 참고

----------------------------------------------------------------------------------------------------

탬플릿 다른영역 스타일 쓰는거면 스타일에 배경해놓고 그대로 사용가능
ex)

영역1에 background:url({{BANNER_SRC:1}}) 하고
영역2에서 영역1스타일꺼 쓰면(클래스동일) 등록안해도 영역1에있는 배너 불러와짐

---------------------------------------------------------------------------------------------------

탬플릿 상품번호 정렬되는 규칙

숫자가 높을수록 늦게(마지막에) 페이지에 추가된 영역(스타일x 영역o)
앞쪽(왼쪽)에 있을수록 페이지 위쪽(앞쪽) 영역에 있음
뒤쪽(오른쪽)에 있을수록 페이지 아래쪽(뒤쪽) 영역에 있음

---------------------------------------------------------------------------------------------------

img{width:auto;height:auto;max-width:100%;}
한번씩하기

---------------------------------------------------------------------------------------------------

주요 서브페이지

이벤트, 검색, 리스트, 상세, 장바구니, 결제페이지, 로그인, 회원가입, (고객센터)

----------------------------------------------------------------------------------------------------

클래스에 tmb_login 넣으면 로그인상태일때
클래스에 tmb_logout 넣으면 로그아웃상태일때

----------------------------------------------------------------------------------------------------

콘솔창에 입력하면 텍스트맘대로수정할수
document.body.contentEditable=true

----------------------------------------------------------------------------------------------------

css , 스크립트 속성선택자


① 속성이 일치하는 것 적용

input[속성="값"]{}

이렇게 선택가능하다
input[readonly="true"]{}

다른 속성도 전부 가능
div.layerFix.escrow[idxlyr="1"]{}

클래스 등이랑 위치 바꿔도 됨
div[idxlyr="1"].layerFix.escrow{}


② class 속성이 box로 시작하는 것 적용

<div class="box1"><span></span></div>
<div class="box2"><span></span></div>  

$("[class^=box] span").click(function () {
	
});


③ class 속성이 a로 끝나는 것 적용

div[class$=a]


④ class 속성이 a를 포함하면 적용

div[class*=a]

ex) [class*="test"] { color: red}


⑤ class 속성이 a가 아닌 것 적용

div[class!=a]


⑤ class 속성이 있기만 하면 적용

div[class]


⑥ a속성과 b속성을 동시에 갖고있는 것 적용

div[a][b]


★ 클래스 등 속성의 값이 여러개여도 각각 적용된다
ex) class="asdf qwer" 이면 asdf 와 qwer 둘다 체크해서 하나라도 조건에 속하면 적용됨

참고
https://blog.naver.com/bog123451/221204122107 

---------------------------------------------------------------------------------------------------

★ css/jquery 선택자

input중에 text만 선택
input[type=text]

input중에 name이 'asd'인것만 선택
input[name='asd']

input중에 radio중에 체크 된것만 선택
input[type=radio]:checked

input중에 text중에 readonly 된것만 선택
input[type=text]:read-only

input중에 text중에 disabled 된것만 선택
input[type=text]:disabled

input중에 text중에 체크되있으며 선택할수없게해논것
input[type=text]:checked:disabled{display:none}	or
input[type=text]:disabled:checked{display:none}

★ readonly / disabled 차이
readonly : 읽기전용, 전원On + 입력 기능 비활성화 → 서버 전송 가능
disabledy : 비활성화, 전원Off + 모든 기능 비활성화 → 서버 전송 불가능

input 속성 중 accesskey="s" → Alt + s 누르면 포커스이동됨 (단축키)
input 속성 중 autofocus → 새로고침시 포커스이동됨

input 속성 중 autocomplete="off" → 자동완성 기능 off (input태그에 id를 같은걸 쓴적이 있을경우 추천목록이 뜨는데 이걸 안나오게 하기위함)
만약 이거 해도 안되면
input-text 앞뒤로 아래 임의의 input-text 추가
<input type="text" aria-hidden="true" tabindex="-1" style="width:0;height:0;position:absolute;top:-9999px">

----------------------------------------------------------------------------------------------------

★ css 선택자

h1:first-child{} : 첫번째 자식
h1:first-of-type{} : 첫번째 같은 타입의 자식(두번째위치에 있어도 타입의 첫번째라면 적용됨)

li+li{} 
두번째부터 끝까지 (형제 li태그)
ex)
리스트에서 선 첫번째꺼 빼고넣을때 li a+a{border-left:solid 1px #e6e6e6;}
이렇게 쓰면 두번째거부터 되서 child안쓰고도 유용히 사용가능함 (클래스도됨 .classWrap .class+.class)

div~p{}
div뒤에있는 모든 p에 적용. div와 p는 형제여야함
 
li+li+li{} 
세번째부터 끝까지
 
:nth-child(-n+5){}
처음부터 5번째까지

:nth-last-child(5)
뒤에서 5번째 

:nth-last-child(-n+5){}
뒤에서 5번째까지
 
:nth-child(n+16):nth-child(-n+19){}
16번째부터 19번째까지
 
:nth-child(odd){} 홀수
:nth-child(even){} 짝수

:nth-child(?n){} --- ?부터시작해서 ?의배수
:nth-child(?n-?){} --- ?n에서 -?씩 이동
:nth-child(?n+?){} --- ?n인데 ?번째를 시초로 진행

ex)
:nth-child(5n){} --- 5부터 5,10,15..
:nth-child(5n+1){} --- 1부터 1,6,11..
:nth-child(5n+2){} --- 2부터 2,7,12..
:nth-child(5n-2){} --- 3부터 3,8,13..
:nth-child(7n-6) or (7n+1) --- 1부터 1,8,15 (달력같은데 씀)

다른 태그랑 섞여있을경우 nth-of-type() 로 (nth-child는 index와 태그형태까지 일치해야 적용된다)
ex) .tit:nth-of-type(2)

------------------------------

not 선택자

<div class="av_one_fifth org_obj first">뭐1</div>
<div class="av_one_fifth org_obj">뭐2</div>
<div class="av_one_fifth org_obj">뭐3</div>
<div class="av_one_fifth org_obj">뭐4</div>
<div class="av_one_fifth org_obj">뭐5</div>

div .av_one_fifth.org_obj:not(.first){margin-left:3%;}

-----

제이쿼리 not 함수

ex) box클래스가 붙은것들중 balance클래스가 안붙은것만 선택
.find(".box").not(".balance").hide()

------------------------------

* 선택자

.insta_cont2 .storyArea-cont-info *
해석)insta_cont2 안에 .storyArea-cont-info 다음의 모든 형제 태그

----------------------------------------------------------------------------------------------------

input 클릭시 placeholder 바로사라지도록 (사파리X)

input:not([type='checkbox,radio']):focus::-webkit-input-placeholder {
 color: transparent;
}

----------------------------------------------------------------------------------------------------

placeholder만 글자 색깔 바꾸기 안되면 !important
input::-webkit-input-placeholder{color:red !important;}
input::-moz-placeholder{color:red !important;}

textarea#tipTxt::-webkit-input-placeholder{color: #f4543d;}
textarea#tipTxt::-moz-input-placeholder{color: #f4543d;}

----------------------------------------------------------------------------------------------------

★이벤트 제어

<명령>
$(선택자).click() → 클릭시키기
$(선택자).focus() → 포커스 이동시키기
$(선택자).blur() → 포커스 해제시키기


<이벤트감지>

- 마우스이벤트
click → 노드(elements)를 마우스 포인터로 눌렀다가 떼었을 때에 발생
dblclick → 노드를 더블 클릭 했을 때에 발생
hover → mouseenter와 mouseleave 이벤트를 한번에 bind한다.
mousedown → 노드 영역에서 마우스를 눌렀다가 떼었을 때에 발생
mouseenter → 노드에 마우스가 진입했을 때에 발생(자식노드에서는 이벤트를 감지 못함)
mouseleave → 마우스가 노드에서 벗어났을 때에 발생
mousemove → 노드 영역에서 마우스를 움직였을 때에 발생
mouseout → 노드에서 마우스 포인터가 떠났을 때에 발생
mouseover → 노드 영역에서 마우스를 올려놓았을 때 발생 (내부노드까지 이벤트를 감지)
mouseup → 마우스 포인터를 노드에 올려놓고 마우스 버튼을 눌렀다 떼었을 때에 발생
toggle → click 이벤트에 핸들러를 바인딩하고 클릭할 때마다 실행될 함수들을 차례대로 실행

- 키보드이벤트
keydown → 해당 영역에서 키보드를 눌렀을 때에 발생
keypress → 해당 영역에서 키보드를 계속 누르고 있을 때에 발생
keyup → 해당 영역에서 키보드를 눌렀다가 떼었을 때 발생

- 폼이벤트
blur → 노드에서 포커스가 떠날 때에 발생
change → 노드의 값이 변경될 때에 발생
focus → 노드가 포커스를 획득했을 때에 발생
select → 유저가 텍스트를 선택했을 때에 발생
submit → 폼의 내용을 전송할 때에 발생

- 문서로딩 이벤트
ready → 해당 페이지가 로딩되었을 때에(처음 읽힐 때에) 발생
load → 모든 요소 로딩완료시 발생. window객체와 바인딩해야함 → $(window).load(function or $(window).on("load",function
on("beforeunload" → 해당 페이지를 빠져나갈 때에 발생. window객체와 바인딩해야함
	tmi:옛날에는 alert/confirm도 넣을수 있었는데 악성 장난사이트때문에 막힘. 추가로 메시지도 크래커때문에 변경할수없게 막힘
	페이지를 나가시겠습니까? 띄우기 $(window).on("beforeunload", function(){ return "나가시겠습니까?" });
	새로고침시에도 적용되며,
	내용은 익스에서는 변경 가능하고, 크롬에서는 고정이다 (익스에서도 고정되게하려면 return "")
	폼전송 이후에는 창이 안열리게 하려면 ↓↓↓
	$("#admin_post_write_form").on("submit", function() {
		$(window).off("beforeunload");
	});
	만약 이외의 다른 기능을 넣고싶으면 레이어모달창 내에서 정보를 보여주고 닫는 버튼을 만들어서 구현하기

- 웹브라우저 이벤트
resize → 웹브라우저 윈도우 사이즈의 변화가 있을 때
scroll → 스크롤이 움직일 때에 발생


<쓰는법1 - html태그 속성으로 함수호출>
<div onclick="f1();"
<div focus="f1();"
<input keyup="f1();"
.
.
.

<쓰는법2 - 스크립트영역에서 함수호출(소괄호 쓰면 안됨 = 매개변수 없는함수만됨)>
function f1(){
	console.log(111);
}
$(선택자).click(f1);
$(선택자).focus(f1);
$(선택자).blur(f1);
.
.
.

<쓰는법3 - 직접쓰기>
$(선택자).click(function(){
	console.log(111);
});
$(선택자).focus(function(){
	console.log(111);
});
$(선택자).blur(function(){
	console.log(111);
});
.
.
.
<쓰는법4 - on메소드를 이용해 함수호출(소괄호 쓰면 안됨 = 매개변수 없는함수만됨)>
function f1(){
	console.log(111);
}
$(선택자).on("click",f1);
$(선택자).on("focus",f1);
$(선택자).on("blur",f1);
.
.
.

<쓰는법5 - on메소드를 이용해 직접쓰기>
$(선택자).on("click",function(){
	console.log(111);
});
$(선택자).on("focus",function(){
	console.log(111);
});
$(선택자).on("blur",function(){
	console.log(111);
});
.
.
.

----------------------------------------------------------------------------------------------------

input란에 숫자만 입력가능하게하기

<첫번째 방법 - 바로 사라지게>
<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
 $(function(){
  $('#phone').keyup(function() {   
   $(this).val($(this).val().replace(/[^0-9]/g,""));
  }); //#phone.keyup 
 });
</script>

<두번째 방법 - 확인을 눌렀을때 경고창뜨게>
<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
 $(function(){
  $('#phone').keyup(function() {
   if (	event.which && (event.which > 36 && event.which < 58 || 
    event.which > 95 && event.which <106 ||
    event.which == 8 || event.which == 9)){
     //alert("숫자다");
   }else{ 
    alert("숫자만 입력해주세요");
    $('#phone').val("");
    $('#phone').focus();
   }
  }); //#phone.keyup 
 });
</script>

----------------------------------------------------------------------------------------------------

자바스크립트 id/class 선택자

getElementById("#id1")
getElementsByClassName(".class1 .class1_2")

----------------------------------------------------------------------------------------------------

html5로 유효성 검사

<input type="number" min="0" max="100" step="10"> → 숫자
<input type="email"> → 이메일
<input type="url"> → url
<input type="range" min="0" max="100"> → 범위

<input type="range" min="0" max="100" onchange="document.getElementById('rtxt').value = this.value;">
<input type="text" id="rtxt"> 이런식으로 사용가능

<input type="color"> → 컬러

<input type="color" id="ctxt" onchange="document.getElementById('ctxt').value;document.body.bgColor=this.value;">
이런식으로 사용 가능

<input type="date"> → 날짜/시간
<input type="month"> → 날짜/시간
<input type="week"> → 날짜/시간
<input type="time"> → 날짜/시간
<input type="datetime"> 지원하는 브라우저 전무
<input type="datetime-local"> → 날짜/시간
 <progress value="0.85"></progress> → 진행률
 <progress max="100" value="85"></progress>
<meter min="-100" max="100" value="50"></meter> → 진행률(progress에서 min을 포함한 몇가지 기능이 추가됨)

----------------------------------------------------------------------------------------------------

익스9이하에서 placeholder 적용

http://jamesallardice.github.io/Placeholders.js/
에서 placeholder.min.js 다운 연결

---------------------------------------------------------------------------------------------------

필수 입력 input 속성 - required (단, 디자인 수정 어려움)
<input type="text" placeholder="아이디" required>

---------------------------------------------------------------------------------------------------

textarea 크기조절 안되게 만들기

<textarea style="resize:none"></textarea>

---------------------------------------------------------------------------------------------------

textarea 속에서 탭키 작동되게 (원래 다음 영역으로 넘어감)

$(".useTab").keydown(function(e) {
	if(e.keyCode === 9) { // tab was pressed
		// get caret position/selection
		var start = this.selectionStart;
		var end = this.selectionEnd;

		var $this = $(this);
		var value = $this.val();

		// set textarea value to: text before caret + tab + text after caret
		$this.val(value.substring(0, start)
					+ "\t"
					+ value.substring(end));

		// put caret at right position again (add one for the tab)
		this.selectionStart = this.selectionEnd = start + 1;

		// prevent the focus lose
		e.preventDefault();
	}
})

----------------------------------------------------------------------------------------------------

select 값이나 순번으로 선택

$("#mobile1").ready(function(){
	$("#mobile1").val("011").prop("selected",true);
	or
	$("#mobile1 option[value='011']").prop("selected",true);
});

----------------------------------------------------------------------------------------------------

select 속성중 다중 선택 속성

<select size="5" multiple>
	<option value="1">강아지</option>
	<option value="2">고양이</option>
	<option value="3">병아리</option>
</select>

----------------------------------------------------------------------------------------------------

select 그룹화

<select name="size">
	<optgroup label="female">
		<option value="225">225mm</option>
		<option value="230">230mm</option>
	</optgroup>
	<optgroup label="male">
		<option value="255">255mm</option>
		<option value="260">260mm</option>
	</optgroup>
</select>

----------------------------------------------------------------------------------------------------

파비콘

http://www.favicon.cc/
Import Image 눌러서 이미지를 아이콘파일로 변환

http://convertico.com/
드래그앤드랍해서다운

적용법
<link rel=" shortcut icon" href="파일.ico">
<link rel="icon" href="파일.ico">

----------------------------------------------------------------------------------------------------

외부의 CDN 서버에서 가장 최신의 jQuery 배포판을 불러 올 수 있음

<script src="http://code.jquery.com/jquery-latest.min.js"></script>

----------------------------------------------------------------------------------------------------

공백 없애기

font-size:0

----------------------------------------------------------------------------------------------------

구글에 검색해주는 사이트
http://lmgtfy.com/?q=검색어 입력

----------------------------------------------------------------------------------------------------

박스 좌우 간격 padding 으로만 하면 화면 축소시 터짐
width 정하면 안터짐

----------------------------------------------------------------------------------------------------

테이블 내에서 세로정렬
vertical-align:top , middle , bottom / line-height / margin 조절

----------------------------------------------------------------------------------------------------

0.5 0.8 에서 0생략가능

예) opacity:.5 rgba(0,0,0,.8)

----------------------------------------------------------------------------------------------------

없던선이 갑자기 생김에 의해 깨질때 → 미리 투명선을넣어놓기

.line{border:1px solid transparent;} or .line{border:1px solid rgba(0,0,0,0)}
.line.on{border-color:red;}

----------------------------------------------------------------------------------------------------

css 트랜스폼

{transform:scale(숫자);} 
태그의 크기를 변형시킴. 작성된 숫자의 값이 배수로 적용됨. 단위 붙이기.

{transform:translate(X축값,Y축값);}
{transform:translateX(값);}
{transform:translateY(값);}
태그의 위치를 변형시킴. 
X축의 값이 플러스면 오른쪽으로, 마이너스면 왼쪽으로 이동.
Y축의 값이 플러스면 아래쪽으로, 마이너스면 위쪽으로 이동.

{transform:rotate(숫자deg);}
태그를 회전시킴.
플러스값은 오른쪽으로 회전, 마이너스값은 왼쪽으로 이동.

{transform:skew(Xdeg,Y축값);}
{transform:skewX(값);}
{transform:skewY(값);}
태그를 비틀어 모양을 왜곡시킴.

transform:rotateX(180deg); x축기준 뒤집기
transform:scale(-1,1); y축 기준 뒤집기
transform:rotateY(180deg); y축 기준 뒤집기
transform:scale(-1); x축/y축 모두 뒤집기

transform-origin:50% 50%;
기준점위치 기본 50% 50%



css 애니메이션(keyframes) > 트렌스폼과 응용

축약형)
.box{animation:hello→키프레임이름 1s→진행시간(속도) 1s→처음대기시간 ease-in-out→이징효과 infinite→무한반복 alternate→갔다오기(0%→100%찍고 다시100%→0%로);}

@keyframes circle{
	0% {opacity: 1;background:red;transform:translate(-144px,0) rotate(360deg) scale(1.2) skew(250deg,100deg);}
	50% {opacity: .5;background:blue;transform:translate(0);}
	100% {opacity: 0;background:#e3e;transform:translate(0,200px) rotate(0deg) skew(0deg,290deg);transform-origin:40% 90%;}
}

클래스가 추가되면 애니메이션이 실행되도록 응용 가능


파이어폭스에서 안깨지게 → outline:solid 1px transparent;

애니메이션 완료상태로 유지 → animation-fill-mode: forwards;


css 트랜지션(트랜스폼,애니메이션과 별개)

hover/active/클래스바뀔 시 등등 바뀌는 속도 조절
예)
.box{transition:all .5s ease-in .5s;}
첫번째 인자 : 적용할 속성(background/opacity/margin등. 생략하면 all)
두번째 인자 : 변환속도
세번째 인자 : 변환종류(ease-in-out/cubic-bezier등. 크롬개발자도구에서 종류별 확인/테스트 가능 , 생략시 linear)
네번째 인자 : 변환시작되기까지시간(딜레이)

---------------------------------------------------------------------------------------------------

transition 애니메이션 형태 사용자설정

transition:all 0.2s cubic-bezier(0.175, 0.885, 0.32, 1.275) → 통으로
transition-timing-function:cubic-bezier(0.7, 1, 0.7, 1); → 속성분리

----------------------------------------------------------------------------------------------------

브라우저별 css 옵션 적용
-moz- 파폭
-webkit- 사파리
-ms- 익스
-o- 오페라

예)
-webkit-animation:hello 4s infinite;

@-webkit-keyframes example {
0% { left:0px; top:0px; }
25% { left:420px; top:0px; }
50% { left:420px; top:220px; }
75% { left:0px; top:220px; }
}

----------------------------------------------------------------------------------------------------

스크립트 배경/폰트색 랜덤
var selector = document.getElementById('rdm');
selector.style.background = "#"+(parseInt(Math.random()*0xffffff)).toString(16);

새로고침할때마다


var divBackgroundColor = $(".rdm")
setInterval(function(){
	var randomColor = Math.random()*0xffffff
		randomColor = parseInt(randomColor)
		randomColor = randomColor.toString(16)
	divBackgroundColor.css({
		backgroundColor : "#"+randomColor
	})
},3000)

지정 시간마다

----------------------------------------------------------------------------------------------------

.class .calss + a {}
.class 안에 .class 안에 첫번재 a만

.class .calss a + a {}
.class 안에 .calss 안에 첫번째a 다음(두번째) a부터

----------------------------------------------------------------------------------------------------

테이블방식 견적서같은거 스크롤안될때 전체 div감싸고 아래속성

body{background:#fff;}
.tbscl {width:100%; overflow-y:auto; max-height:600px;}

----------------------------------------------------------------------------------------------------

모바일 반응형으로 다른박스 넓이/높이 따라가게 만들기

$(document).ready(function(){
	//배너높이맞추기
	$(window).resize(function(){ //브라우저 사이즈가 변경될시 실행
		$(".st_pro_list_box .st_bnr").height(($(".st_height").height()*2)+11)
		var pp = $(".st_pro_wrap .st_pro_percent")
		var pph = pp.height()
		pp.css("line-height",pph+2+"px")
	});
})

클릭했을때 리사이징 응용 가능

$(document).ready(function(){
	$(".board_list td .img .smallimg").click(function(){
		$(this).parent().toggleClass("active ");
		$(window).resize();
	});
	$(".board_list td .img .bigimg_box").click(function(){
		$(this).parent().toggleClass("active ");
		$(window).resize();
	});
});
 $(window).resize(function(){
	 $('.board_list td .img .bigimg').css("margin-left",-$('.board_list td .img .bigimg').width()/2);
	 $('.board_list td .img .bigimg').css("margin-top",-$('.board_list td .img .bigimg').height()/2);
 });

----------------------------------------------------------------------------------------------------

화면 높이에따라 뭐 변하게하기 ★if 마지막괄호 주의 })←X }←O
아래처럼 두번써야 처음로드된상태에서도 적용이됨 document.ready 나 window.load 묶어도됨

if ($(window).height()<=950) {
	$(".container").css("top","466px")
}else{
	$(".container").css("top","50%")
}

$(window).resize(function(){
	if ($(window).height()<=950) {
		$(".container").css("top","466px")
	}else{
		$(".container").css("top","50%")
	}
})


화면 높이에서 빼기

$(window).load(function(){
	$(".all_menu_cont").height($(window).height()-$(".all_menu_head").height()-$(".all_menu_links").height());
})

----------------------------------------------------------------------------------------------------

스크립트실행안되면 캐시삭제해보고 안되면

$(function(){
	$("html").niceScroll();
});
혹은
$(() => {
	$("html").niceScroll();
});

이렇게 묶거나

document.ready 나 window.load 로 묶어야댐 (페이지 다 불러오고실행)

----------------------------------------------------------------------------------------------------

처음에 안보여야되는게 css/스크립트 로드될동안(css/스크립트 딜레이로인한) 살짝 보였다 불러오고난뒤에서야 사라질경우

링크연결말고(<link href=""> , <script src="">) 그냥 내부나 인라인 스타일로 써야함
ex) on클래스나 display:none 등 할때

----------------------------------------------------------------------------------------------------

슬릭(slick) 슬라이드 참고(예제) (jquery.com Plugins 가면 다른것도 많음)

https://github.com/kenwheeler/slick/

----------------------------------------------------------------------------------------------------

슬릭 복사용

$(".slide").slick({
	//fade:true,
	dots:true,
	arrows:true,
	swipe:true,
	autoplay:true,
	autoplaySpeed:4000,
	pauseOnHover:false,
	//slidesToShow:1,
	//slidesToScroll:1,
	slide:"li"
})


스와이퍼 슬라이드 복사용(버전3)
<html>
<div class="swiper-container">
	<div class="swiper-wrapper">
		<div class="swiper-slide p1">
		</div>
		<div class="swiper-slide p2">
		</div>
		<div class="swiper-slide p3">
		</div>
	</div>
	<div class="swiper-button-next"></div>
	<div class="swiper-button-prev"></div>
	<div class="swiper-pagination"></div>
</div>
<js>
var pdSl = new Swiper(".pdSl .swiper-container",{
	//effect:"fade"
	pagination:".pdSl .swiper-pagination",
	nextButton:".pdSl .swiper-button-next",
	prevButton:".pdSl .swiper-button-prev",
	//slidesPerView:4,
	//slidesPerGroup:4,
	paginationClickable:true,
	//autoHeight:true,
	//spaceBetween:30,
	//centeredSlides:true,
	//autoplay:2500,
	loop:true,
	autoplayDisableOnInteraction:false
});


bx 복사용 (fade 말고 swipe로 하면 슬라이드 1개만있을때 이상해짐)

$(".bxslider").bxSlider({
	//mode:"fade",
	auto:true,
	pagerSelector:".visualPaging",
	controls:true,
	onSlideBefore:function($slideElement, oldIndex, newIndex){
		$(".simg li").removeClass("on");
		$(".simg li").find("img").removeClass("siteborder2");
		$(".simg li").eq(newIndex).addClass("on");
		$(".simg li").eq(newIndex).find("img").addClass("siteborder2");
	}
});
$(".bxsliderWrap .prev").click(function(){
	$(".bxsliderWrap .bx-controls .bx-prev").click();
	console.log($(".bxsliderWrap .bx-controls .bx-prev"))
});
$(".bxsliderWrap .next").click(function(){
	$(".bxsliderWrap .bx-controls .bx-next").click();
	console.log($(".bxsliderWrap .bx-controls .bx-next"))
});


----------------------------------------------------------------------------------------------------

스와이퍼swiper 슬라이드 슬라이드 세로 가운데 정렬
swiper-slide{display:flex;align-self:center;}

슬라이드 바뀔시 자동 높이 변환
autoHeight:true,

----------------------------------------------------------------------------------------------------

슬라이드에서 가운데오는등 것만 속성 넣기

.new_pro .swiper-slide-active{} 나
.new_pro .swiper-slide-active+div{}
transition:all .5s 섞어서 활용가능

----------------------------------------------------------------------------------------------------

스와이퍼슬라이드 객체 생성 후 옵션 추가

let menu = new Swiper($container.find(".special_box .menu .swiper-container"), {
	spaceBetween: 10,
	watchOverflow: true,
	slidesPerView: "auto",
	navigation: {
		nextEl: ".swiper-button-next",
		prevEl: ".swiper-button-prev",
	}
});
menu.params.centeredSlides = true;
menu.update();

----------------------------------------------------------------------------------------------------

백그라운드 한줄쓰기(축약형)

{background:#fff url("../ico_select.gif") no-repeat scroll right 5px center / 25px auto;}
								↑
								size
이렇게도 됨 (/auto 100% 가로오토 세로백)
li:before{content:"";position:absolute;left:-5px;width:12px;height:16px;background:url(/m/images/ico_my_arrow2.png)no-repeat center/auto 100%;}

----------------------------------------------------------------------------------------------------

백지에서 만들때

<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
헤드에 넣으면 한글안깨짐

<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
헤드에 이거 넣으면 모바일에서 글자 안깨짐
user-scalable=no 이거 빼거나 yes로 넣으면 확대/축소 가능 

initial-scale=1.0 , maximum-scale=2.0 , minimum-scale=1.0
이것들도 잘 조절하면 기본사이즈,max확대축소 조절할수있음

----------------------------------------------------------------------------------------------------

포토샵 클리핑마스크 같은거할때 z-index로 하기 애매한것들
overflow:hidden;padding-top:20px;margin-top:-20px; 이런식으로 padding으로영역늘리고 margin으로땡기면 다른영역 침범안하고 쉽게가능

absolute는 아닌데 위로 올릴때 ex) 속에서 영역 벗어나기용 제자리띄우기
position:relative;z-index:99; 한다음 마찬가지로 margin-top,padding-top

----------------------------------------------------------------------------------------------------

css 수치 빼거나 나누기 곱하기 (익스8 X)
{width:calc(55% - 1px); 연산자 양쪽 한칸띄어야댐}

----------------------------------------------------------------------------------------------------

fadeIn() / fadeOut()

fast: 200
slow: 600
기본값: 400

----------------------------------------------------------------------------------------------------

js 함수 만들기

function menuonoff(name){
	$("#submenu"+name).stop(true,true).slideToggle("fast");
	$(".allMenu span").toggleClass("on");
}
 
<span onclick="menuonoff(1)"><span class="iconfont ftic-allmenu"></span>전체보기</span> 
<a href="javascript:menuonoff(1)"> href 안에 바로가능
 
(name) , (1) , +name 들의 의미:같은 스크립트인데 조금씩 다른 기능일때 씀



함수 호출하기

function wmallAlign(t1,t2){	
	$(".bestSl li").each(function(){
		var chdbox = $(this).find(".pdImg")
		if(t1==1){
		}else if{ //2가지 경우만일때는 그냥else
		}
	})
}

wmallAlign(1); ← wmallAlign에 값 넣어서 불러오는거
wmallAlign(2); ← 다른값 넣어서 불러오기

<script></script> 안에 그냥 썼는데 안갖고와지면
$(function(){
	wmallAlign(2)
})
이렇게 감싸기


예)

function edit(uid, manual) {
	if (manual) {
		layerBox.open("offline_manual.asp?uid="+uid+"&params=<%=encParams(params_detail)%>");
	}
	else {
		layerBox.open("offline_detail.asp?uid="+uid+"&params=<%=encParams(params_detail)%>");
	}
}
이렇게 해서
<a href="javascript:addManual()" class="btns btn01">추가하기</a>
<a href="javascript:downExcel()" class="btns btn02">엑셀출력</a>
이렇게 쓸수있다


<script>
function followTo(box,height){
	$(window).scroll(function(){
		if($(window).scrollTop() > height)
		{
			box.addClass('on')
		}
		else
		{
			box.removeClass('on')
		}
	});
}
followTo($('#positiontoptop , .title_menu_box'),170);
</script>
이렇게도 쓸수있다

----------------------------------------------------------------------------------------------------

제이쿼리로 링크걸기

$(".formanual .manual").eq(0).click(function(){
	location.href="#1"
	//또는
	location.href="http://www.naver.com"
})

----------------------------------------------------------------------------------------------------

일반링크
function menu01() { location.href("index.html"); }
 
새창 열기
function menu02() { window.open("index.html","_blank"); }
 
팝업을 원하는 좌표로 열기
function menu03() { window.open("index.html","google","left=0,top=0,width=600,height=500"); }
 
팝업을 정가운데 새창으로 열기
function menu04() { var w=750; var h=600; var top=(screen.availHeight-h)/2; var left=(screen.availWidth-w)/2; window.open("index.html", "theWindow", "toolbar=0, resizable=no, status=1, scrollbars=no, copyhistory=0, width=" + w + ", height=" + h + ", top=" + top + ", left=" + left); }

----------------------------------------------------------------------------------------------------

드랍 메뉴 등 오버했을때 나오게하는걸 css로 하려면 오버할 태그 안에 오버했을때 나올게 있어야함

예)
.dropdown:hover .dropdown-content{display:block;}

<div class="dropdown">
  <span>Mouse over me</span>
  <div class="dropdown-content">
    <p>Hello World!</p>
  </div>
</div>

----------------------------------------------------------------------------------------------------

input text 클릭했을때 배경등 속성적용

.focus {
  width: 99%;
  padding: 14px 20px;
  box-sizing: border-box;
  border: 3px solid #ccc;
}

.focus:focus {
  background-color:#555555; 
  color: white;
  outline: none;
}

<input type="text" name="" class="focus">


----------------------------------------------------------------------------------------------------

플롯 클리어 시킬때
.clear:after{content:'';display:block;clear:both;}

----------------------------------------------------------------------------------------------------

박스에 화살표삐져나온거 css로

아래
.class:after{content:"";top:100%;left:50%;border:15px solid transparent;content:"";height:0;width:0;position:absolute;pointer-events:none;border-top-color:#262223;border-top-width:10px;margin-left:-15px;}

위
.class:before{content:"";top:-12px;left:50%;border:4px solid transparent;height:0;width:0;position:absolute;pointer-events:none;border-bottom-color:{{COLORTYPE1}};border-bottom-width:8px;margin-left:-4px;}

----------------------------------------------------------------------------------------------------

자바스크립트 if + each 함수

$(".prSection2 .prBox .prSlide2 .liWrap li").each(function(){
	var hgt = $(this).children('.img').height()
	if(hgt>100){
		$(this).children('a').show()
	}else{
		$(this).children('a').hide()
	}
})

설명 : 각각의 li 바로밑 .img들의 높이가 100이상일때 li 바로밑 a를 보이고 아님 숨김

+++

$(".list_product_30 .liWrap li").each(function(){
	var vvv = $(this).find('.tit').text()
	if(vvv == "" || vvv == "\xa0"){
		$(this).hide()		
	}else{
		$(this).show()
	}
})

설명 li밑 .tit안에 텍스트가 없거나 &nbsp; 면 li숨김

★ 상황에 따라 $(window).load로 감싸기

----------------------------------------------------------------------------------------------------

eval() : 문자로 표현된 JavaScript 코드를 실행하는 함수(동적으로 변수를 만들 수 있는 함수)

사용법
eval( string )

ex1)
var key = "nara";
eval("var haha" + key + "= 100");
console.log(hahanara) → 100

ex2)
for (var i=1;i<=6;i++){
	eval("var ofstop" + i + " = $('.sct" + i + "').offset().top");
}
$(".btn_page li").click(function(){
	var idx = $(this).index() + 1;
	$("html,body").animate({"scrollTop":eval("ofstop" + idx)},"easeOutQuad");
);

----------------------------------------------------------------------------------------------------

each 쓸때

★find(".box") 쓰면 안에있는 모든 box 선택됨

find안쓰고 일케해도댐
var chdbox = $(this).children(".goods-container").children(".productCont").children("table").children("tbody").children("tr").children("td").children(".list_img")
var chdimg = $(this).children(".goods-container").children(".productCont").children("table").children("tbody").children("tr").children("td").children(".list_img").children("a").children("img")


$(".pc_hot_issue_list_cls li").each 이렇게 같은선상(형제)에 있어도 되고 뒤죽박죽되있으면 걍 클래스로 써도 됨
$(".pc_hot_issue_list_cls .cutImg").each 단, 안의 find(".box") 의 box클래스가 두개있으면 box도 li로 옮기든가해야됨 (아래아래예시)

----------------------------------------------------------------------------------------------------

★ 이미지를 액자크기에맞게 수직/수평으로 확대/축소 및 가운데정렬 (img태그에 다음 css 적용해서 대체 가능 object-fit:cover;width:300px;height:300px;)
(background-size:cover;background-position:50%랑 동일한 효과)
최초에 이미지가 영역밖을 벗어나는 모습이 보여지는게 싫다면 css로 이미지에 opacity:0 적용해놓기

<imgBoxAlign.js>

var cutImgBox = () => {
	let i = $(".cutImgBox img");

	i.width("100%");
	$(".cutImgBox").each(function(){
		let t = $(this);
		let i = t.find("img");

		t.css("overflow","hidden");
		if(i.length>0){
			let iw = i.width();
			let bh = t.innerHeight();
			let inw = i.get(0).naturalWidth;
			let inh = i.get(0).naturalHeight;
			let iwwh = (inw*(bh/inh)-iw)/2;
			let iwhw = (inh*(iw/inw)-bh)/2;

			if(inw>inh && iwhw<0 || inw<=inh && iwwh>=0){
				i.height("100%");
				i.width("auto");
				i.css({"margin-left":-iwwh,"max-width":"none"});
			}else if(inw<=inh && iwhw>=0 || inw>inh && iwwh<0){
				i.width("100%");
				i.height("auto");
				i.css({"margin-top":-iwhw,"max-height":"none"});
			}
		}
	});
	i.css("opacity",1);
}
해설) (속에 이미지가 들어있는) 모든 .cutImgBox를 box로 만들고 안에 img를 찾아서 있으면 적용한다

<조건>
1. 박스는 이미지랑 최대한 가까운 부모위치에 있어야한다
2. 박스에 넓이/높이지정이 되어있어야한다
3. 박스와 이미지 사이에 블럭태그 부모가 있으면 안됨.. 인라인인 a는가능(inline-block도 안됨)
	css로 inline으로바꾸면되긴하지만, 이미지와 박스사이에는 그냥 a빼고 아무것도 넣지 말것
5. 만약 로드가 되기전에 
ex)
<div class="cutImgBox"> --액자 역할
	<a href="###">
		<img src="###"> --액자크기에 맞춰서 넣을 이미지
	</a>
</div>

----------------------------------------------------------------------------------------------------

위에 있는 스크립트 대신 img태그에 아래 속성 지정하면 background의 contain / cover 속성을 간편히 쓸 수 있음

object-fit: cover; or contain
width: 100%;
height: 100%;

----------------------------------------------------------------------------------------------------

페이지안의 내용일부를 참조하는 스크립트(이미지의 크기 등) 적용시
스크립트실행시점을 참조할 개체가 로드된 이후에 실행되도록

window.load로 하거나,
$("#eventToday_list").load(function(){ImgBoxAlign()})

이런식으로 그 내용이 먼저 로드된 이후 스크립트가 적용될수 있도록 작성할것

----------------------------------------------------------------------------------------------------

html 상식

나중에쓴게 레이어가 상위로감 (z-index 높게 적용됨)
	
----------------------------------------------------------------------------------------------------

자바스크립트 hasClass + if

$('.joinMemberType label').click(function(){
	if($(".joinMemberType label:eq(1)").hasClass("on")){
		$(".joinAddOn").show()
	}
})

----------------------------------------------------------------------------------------------------

자바스크립트 태그선택할때

$(".joinMemberType label:first").click
$(".joinMemberType label:last").click
$(".joinMemberType label:eq(3)").click

----------------------------------------------------------------------------------------------------

제이쿼리로 wrap 추가/없애기

$("#top_visualwrap").parent().unwrap()
$(".section").next().wrap("<div></div>")

이렇게 응용가능 (클래스추가도가능)
$(".section").next().wrap("<div class='sss'></div>")

----------------------------------------------------------------------------------------------------

이미지 테두리만 따로만들때 참고

<style>
	.productInfo .img_box .simg .item {display:inline-block; position:relative; width:80px; height:80px; margin:0 5px; overflow:hidden; cursor:pointer;}
	.productInfo .img_box .simg .item img {width:80px; height:80px;}
	.productInfo .img_box .simg .item .ck_border{display:none; position:absolute; top:0; left:0; width:100%; height:100%; border:3px solid <%=cfgColor1%>; box-sizing:border-box;}
</style>

<div class="item">
	<div><img src="/data/yangjimall/goods/yangjimall/other/201706/메트로폴리스_펠티_코인월렛_10_000_2.jpg" alt=""></div>
	<div class="ck_border"></div>
</div>

----------------------------------------------------------------------------------------------------

파일을 못 찾겠을경우


☆기본적으로 찾는 방법

<div class="selected_option_wrap" id="optList">
</div>

이렇게되있는거 파이어폭스에서 f12 → 왼쪽위 html옆에 스크립트 → 클래스나 아이디로 검색하면 어디폴더에있는지 왼쪽위에 경로랑 아래에는 코드가 나옴
아니면 크롬개발자도구에서 ctrl + shift + f 눌러서 그냥찾거나
밑에있는 클래스/아이디/텍스트 아무거나 찾아도 파일위치나옴 (서버코드는못찾으니 로컬다운받기)
☆이를 활용해 작업해논거 백업해두면 나중에 스크립트같은거 어느상황에서 썼는지 대충 탐색가능


☆처음에 안보였다 뭘 클릭하거나 선택했을때 보이는건데 못찾겠을때
그 클릭하거나 선택해야 열리는 태그(호출하는)로 찾기 = (연결된링크로 찾기)

----------------------------------------------------------------------------------------------------

function외 모든 텍스트 찾기

하드(로컬)에서 찾을수있음 대신 파일이 저장되어있어야됨 ftp에서 상위폴더 저장해놓고 찾기


크롬(ctrl+shift+f)

개발자도구에서 ctrl + shift + f 로 함수/클래스/아이디 검색 (서식 비슷한페이지 예시찾을때유용하고 admin에서 폼예제는 /admin/mallinmall/dealer_list.asp 상세정보 버튼 클릭하면 나오는 페이지 ←여기 거의다있음)
위에 Elements Console Sources Network 등 있는 탭에서 Sources에 들어간다음 빈곳에 우클릭누르면 하드속에서 찾고싶은 폴더를 추가할수있음


에플 검색→여러파일찾기 (alt + s + i)

찾을말 → 파일종류 : *.* → 폴더지정 → "하위 폴더 포함" 체크 → 찾기

---------------------------------------------------------------------------------------------------

파일안 내용을 못찾겠을 경우

하나씩 지워보기..

---------------------------------------------------------------------------------------------------

colgroup쓰는법

<colgroup>
	<col width="120" style="background-color:#F5F5F5;" />
	<col width="*" style="background-color:#FFFFFF;" />
</colgroup>

----------------------------------------------------------------------------------------------------

개발되있는 table td에 껴넣을때(주문 등)

width가 100%인데도 td넓이가 안늘어나면 colgroup 되있는거니 colspan으로 풀어야댐

----------------------------------------------------------------------------------------------------

카테고리 전체보기 아이콘 넣을때 세로가운데정렬
li.first span{display:inline-block;vertical-align:top;}

----------------------------------------------------------------------------------------------------

.unwrap() 부모 태그 지우기
.wrapInner() 자신 태그 지우기

----------------------------------------------------------------------------------------------------

가로 일정 너비 리스트 만들때 table-layout을 같이 넣으면 목록의 너비가 동일해짐
ul에 display:table;table-layout:fixed
li에 display:table-cell

또한 리스트 내용물의 넓이가 더 커져서 넘쳤다면 테이블(ul)에 word-break:break-all 넣기

----------------------------------------------------------------------------------------------------

테이블화 세로가운데정렬

박스에 display:table
바로 밑 자식에 display:table-cell;vertical-align:middle;

<div class="imgBox">
	<a href="/product/sublist.asp?branduid=3965&nowType=BRAND">
		<img src="/data/ilikelux/brand/Chloe.jpg">
	</a>
</div>

테이블셀 이미지에다하면 안되고
위처럼되있으면 img말고 a에다가 table-cell해야됨

형제있으면 다중적용가능

----------------------------------------------------------------------------------------------------

이미지 아이콘이 위에있고 글자가 밑에있을때 넓이/높이 조절

이미지에 max- 넣고 겉에 line-height

.ico{line-height:50px;}
.ico img{max-width:120px;max-height:90px;}
<span class="ico"><img src="http://fingerich.com/data/sailormoon/banner/brdlogo2.png" border="0"></span>

----------------------------------------------------------------------------------------------------

이미지 앨범리스트 만들때

.BrandPageList .BrandLogolist dl dd ul li .img{width:110px;height:110px;box-sizing:border-box;padding:5px;border:1px solid #dddddd;margin:0 auto;display:table;}
.BrandPageList .BrandLogolist dl dd ul li .img a{display:table-cell;vertical-align:middle;}
.BrandPageList .BrandLogolist dl dd ul li .img img{max-width:100px;max-height:100px;} (max-width/max-height는 img에다 넣어야 댐)


width:auto;max-width:100%;max-height:300px; 이렇게하고 부모에 text-align:center 하면
100%보다 큰건 100%가되고 max높이에걸려서 작아진건 가운데로 됨 

----------------------------------------------------------------------------------------------------

이미지 앨범리스트를 모바일 반응형으로 정렬하려면 css나 스크립트로 해야 되는데 아래는 css로 하는법이다

li padding을 width의 반만큼 넣기 ex) 3줄이면 width:33.333%의 반 padding:16.666%
아님 속안의 이미지박스를 padding-top:100% 이렇게

.brandWrap .List ul {overflow:hidden; font-size:0; box-sizing:border-box; padding:0 5px;}
.brandWrap .brand_List ul li{display:inline-block; font-size:12px; box-sizing:border-box;float:left;position:relative;padding:12.5%;margin-bottom:42px;(vertical-align:top or bottom)}.brandWrap .brand_List ul li .listcon{width:100%;height:100%;position:absolute;left:0;top:0;padding:0 2%;box-sizing:border-box;}
.brandWrap .brand_List ul li .img {width:100%;height:100%;box-sizing:border-box; border:1px solid #dddddd;display:table;}
.brandWrap .brand_List ul li .img a{display:table-cell;vertical-align:middle;}
.brandWrap .brand_List ul li .img img {width:100%;}
.brandWrap .brand_List ul li .text {white-space: nowrap; text-overflow: ellipsis; overflow:hidden; text-align:center;}

<ul>
	<li>
		<div class="listcon">
			<div class="img"><a href="/m/goods/brandlist.asp?branduid=3986"><img src="http://ilikelux.com/data/ilikelux/brand/09.jpg" border="0"></a></div>
			<div class="text"><a href="/m/goods/brandlist.asp?branduid=3986&quot;">프로엔자 슐러</a></div>
			<div class="text"><a href="/m/goods/brandlist.asp?branduid=3986&quot;">Proenza Schouler</a></div>
		</div>
	</li>

	~~~

	<li>
		<div class="listcon">
			<div class="img"><a href="/m/goods/brandlist.asp?branduid=3972"><img src="http://ilikelux.com/data/ilikelux/brand/Hogan.JPG" border="0"></a></div>
			<div class="text"><a href="/m/goods/brandlist.asp?branduid=3972&quot;">호간</a></div>
			<div class="text"><a href="/m/goods/brandlist.asp?branduid=3972&quot;">Hogan </a></div>
		</div>
	</li>
</ul>

핵심
	li{position:relative;float:left;padding:25%;}
	li div{position:absolute;top:0;left:0;width:100%;height:100%;}

----------------------------------------------------------------------------------------------------

제이쿼리 stop() 종류 (미세한 차이가 있음)
 
<button>stop()</button>
<button>stop(true)</button>
<button>stop(false,true)</button>
<button>stop(true,true)</button>
 
 
슬라이드에 쓰임

$(".all_cate li.first").click(function(){
$(".gnbBox").stop(true,true).slideToggle(300)
	$(".allMenu").toggleClass("on");
})
$(".gnbBox").mouseleave(function(){
	$(this).stop(true,true).slideToggle(300)
	$(".allMenu").toggleClass("on");
})


접힐때만 stop(true,true) 적용한 경우

gnb.on("mouseover", function(){
	sub.slideDown(300);
	head.addClass("on");
})
head.on("mouseleave", function(){
	sub.stop(true,true).slideUp(300);
	head.removeClass("on");
})

https://blog.naver.com/chance_shin/220070971410

----------------------------------------------------------------------------------------------------

모바일에서 넓이 100%에 좌우여백 넣고 싶음 width:100% 빼고 margin:0 15px 이렇게 해야 댐

전체를 감싸야하는 totar_width 같은 랩이 중간에 끝나있으면 중간에어디 두번 잘못닫았나 확인 <div></div>줄바뀌고</div> ←이렇게

----------------------------------------------------------------------------------------------------

검색창 디자인

<div class="searchBox" style="width:250px;">
	<span class="iconfont ftic-search"></span>
	<a href="javascript:">검색</a>
	<input type="text" name="" id="" placeholder="Search...">
</div>

.searchBox{display:inline-block;border:1px solid #a9a9a9;height:30px;vertical-align:middle;box-sizing:border-box;}
.searchBox span.iconfont{vertical-align:top;line-height:28px;display:inline-block;padding:0 5px;font-weight:bold;color:#a9a9a9;}
.searchBox input[type=text]{width:calc(100% - 79px);width:-webkit-calc(100% - 76px);width:-moz-calc(100% - 76px);background:none;border:0;line-height:26px;vertical-align:top;color:#222;float:right;}
.searchBox a{width:50px;line-height:28px;background:#666;color:#fff;display:inline-block;float:right;text-align:center;float:right;}

----------------------------------------------------------------------------------------------------

관리자에서 내용 ftp꺼 갖고오는거 슬라이드 시킬때

$(window).load(function(){
	이 안에다 슬라이드 스크립트 넣어야 댐
	(내용먼저 불러오고 나서 실행)
})

----------------------------------------------------------------------------------------------------

bx슬라이드 옵션

자동넘김 시간
speed 아니고 pause임 ex) pause:2000
speed 는 전환되는과정의 fade속도

루프 삭제
infiniteLoop:false,
hideControlOnEnd:true



옵션들 자세히

http://dlevelb.tistory.com/929

----------------------------------------------------------------------------------------------------

슬라이드 안될때(아예 안되거나 숫자페이지네이션기능이 안되거나 되긴되는데 높이가 매우늘어날때)

위에 이거 넣기 (3버전)

<script type="text/javascript" src="/jscript/swiper.min.js"></script> ← pc,m js동일하고 한페이지안에서 슬라이드 여러개있을때 버전 동일하게 맞춰야됨
<link rel="stylesheet" type="text/css" href="<%=pathMobile%>/css/swiper.min.css" /> ← js너보고 안되면 이것도 넣는데 이건 pc랑 m구분해서 너여야댐

★ pc/m 맞게 경로변경

----------------------------------------------------------------------------------------------------

<div class="swiper-slide">
	<div></div>
	<div></div>
</div>
<div class="swiper-slide">
	<div></div>
	<div></div>
</div>

이렇게 슬라이드마다 나누지않고 그냥 쭉

<div class="swiper-slide"></div>
<div class="swiper-slide"></div>
<div class="swiper-slide"></div>
<div class="swiper-slide"></div>

이렇게쓰는법

↓↓

slidesPerView : "auto"로 하면 swiper-slide에 걸린 width로 적용 , 숫자로 하면 그만큼 나눠서 적용(4는 25%) 소수도가능
slidesPerGroup : 스와이프 한번에 넘길 개수 (view랑 맞추기)

----------------------------------------------------------------------------------------------------

네이게이션(gnb)슬라이드에서 끝까지 스와이프가 안되면 부모넓이/높이 값이 들어있는지 확인후 빼거나 100%로 해보기

네이게이션(gnb)슬라이드에서 제한이 안되고 끝보다 초과해서 스와이프될경우 html에 swiper-container 이거 들어있는지 확인하기 (스크립트에는 안너도되는데 html에는 넣어놔야됨)

----------------------------------------------------------------------------------------------------

슬라이드 좌우화살표 노멀css

.pdSl .swiper-button-prev,
.pdSl .swiper-button-next{width:42px;height:42px;background-size:100% 100%;background-position:center;background-repeat:no-repeat;top:50%;margin-top:-21px;position:absolute;z-index:1;cursor:pointer;}
.pdSl .swiper-button-prev{background-image:url({{BANNER_SRC:2}});left:10px;}
.pdSl .swiper-button-next{background-image:url({{BANNER_SRC:3}});right:10px;}

아님 스프라이트이미지로 해도됨

.swiper-button-prev,
.swiper-button-next{width:24px;height:42px;background:url(/images/sl_arrow_sp.png)no-repeat 0/200%;top:50%;margin-top:-21px;position:absolute;z-index:1;cursor:pointer;}
.swiper-button-prev{left:10px;}
.swiper-button-next{background-position:100%;right:10px;}


슬라이드 페이지네이션 노멀css

.pdSl .swiper-pagination{width:auto or 50px;height:20px;position:absolute;left:auto;right:2%;top:-29px;text-align:right;z-index:10;}
.pdSl .swiper-pagination-bullet{display:inline-block;border-radius:50%;width:15px;height:15px;margin:0 !important;background:none;box-sizing:border-box;opacity:1;cursor:pointer;text-align:center;line-height:15px;font-size:11px;}
.pdSl .swiper-pagination-bullet-active{background:#000;color:#fff;margin:0 2.5px !important}

----------------------------------------------------------------------------------------------------

스와이퍼 슬라이드 예제

var rnkslide = new Swiper('.swiper-container.rankSl',{

})
이거랑(ver.3)

var HBNB_wrapSwiper = $('.bestSl').swiper({

});
이거(ver.2) 버전이 다르니 유의하기


var rnkslide = new Swiper('.swiper-container.rankSl',{
	prevButton: '.rankSl .swiper-button-prev',
	nextButton: '.rankSl .swiper-button-next',
	onInit: function(swiper){
		console.log(111)
	},
	onSlideChangeEnd: function(swiper){
		console.log(222);
	}
})
화살표도 이것도 이거랑(ver.3)

var HBNB_wrapSwiper = $('.bestSl').swiper({
	autoplay: 3000,
	},
	onSlideChangeStart: function(swiper){
		$(".tabSl .tabSlTab a").removeClass("on");
		$(".tabSl .tabSlTab a").eq(swiper.activeLoopIndex).addClass("on");
	},
	onFirstInit: function(swiper){
		$(".rankSl .swiper-button-prev").click(function(){
			swiper.swipePrev(); //ver.3 은 slidePrev
		});
		$(".rankSl .swiper-button-next").click(function(){
			swiper.swipeNext(); //ver.3 은 slideNext
		});
	}
})
일케 밖에다 쓰는거 있음(ver.2)

onSlideChangeStart 는 슬라이드가 바뀔때 실행 ver.3은 onSetTransition 로도 쓸수있는듯(http://3.swiper.com.cn/api/callbacks/2014/1217/101.html Callbacks부분참고)

$(".tabSl .tabSlTab a").eq(swiper.activeLoopIndex).addClass("on") 의 .activeLoopIndex이런거는 메소드라고함 (이메소드는 슬라이드루프될때포함 인덱스인데 ver.2꺼) ver.3은 realIndex
위 메소드 사용으로
페이지네이션 글자로치환하는거가능

다른 메소드들로
eq(0).click(function(){
	section_F3.slideTo(0,500)
})
eq(1).click(function(){
	section_F3.slideTo(1,500)
})
이렇게 슬라이드 왔다갔다 하는등 여러가지 활용가능함

인덱스 쓰면 아래처럼 가능
$(this).click(function(){
	portSl.slideTo($(this).index()+1,500)
})

안쓰고하는방법도있다
function wrap_page01click(){$(".swiper_wrap > .swiper-pagination span").eq(1).click();} 이렇게 대신 페이지네이션이 소스내에있어야함


콜백함수중 onFirstInit(ver.2)/onInit(ver.3) 이건 먼지모르겠음(이 안에다 쓰면 메소드 쓸때 슬라이드 변수선언한걸로 안쓰고 swiper. 으로 사용해야함)

스와이퍼선언한거 바깥으로 완전 뺀다음 안에 swiper.swipePrev의 swiper를 HBNB_wrapSwiper(슬라이드변수)로 바꿔도 됨

아래는 위의 예시
<script>
var pdSl = new Swiper(".pdSl .swiper-container",{
	pagination:".pdSl .swiper-pagination",
	nextButton:".pdSl .swiper-button-next",
	prevButton:".pdSl .swiper-button-prev",
	slidesPerView:4,
	slidesPerGroup:4,
	paginationClickable:true,
	//spaceBetween:30,
	//centeredSlides:true,
	//autoplay:2500,
	loop:true,
	autoplayDisableOnInteraction:false
});
$('.pdSl .swiper-button-next').on('click', function(e){
	pdSl.swipePrev();
});
$('.pdSl .swiper-button-prev').on('click', function(e){
	pdSl.swipeNext();
});
</script>


<아래는 콜백,메소드를이용한 클릭,슬라이드 했을 시 슬라이드이동,표시되는 스크립트이다>
var portSl = new Swiper('.section_portfolio .swiper-container',{
	nextButton:'.section_portfolio .swiper-button-next',
	prevButton:'.section_portfolio .swiper-button-prev',
	speed:500,
	loop:true,
	autoplay:2500,
	slidesPerView:1,
	onSlideChangeStart:function(swiper){
		var idx = swiper.realIndex
		$(".f5Top .brdlogo li").removeClass("on")
		$(".f5Top .brdlogo li:eq("+idx+")").addClass("on")
	}
});
$(".f5Top .brdlogo li").each(function(){
	$(this).click(function(){
		portSl.slideTo($(this).index()+1,500)
	})
})


<페이지네이션>

버전2
.swiper-pagination					페이지네이션 버튼들을 감싸는 랩
.swiper-pagination-switch				페이지네이션 버튼들 모두
.swiper-active-switch					페이지네이션 버튼중 엑티브

버전3
.swiper-pagination 이나 swiper-pagination-bullets	페이지네이션 버튼들을 감싸는 랩
.swiper-pagination-bullet				페이지네이션 버튼들 모두
.swiper-pagination-bullet-active			페이지네이션 버튼중 엑티브


★ 슬라이드할때 스크립트에 페이지네이션/화살표 있는데 html에 없으면 그것만 안되는게아니라 슬라이드 전체오류남
다른 스크립트 쓸때도 마찬가지 그래서 주석할땐되도록 html에서말고 css나 스크립트에서하기

----------------------------------------------------------------------------------------------------

스와이퍼슬라이드 속성

이펙트
effect:"fade"

여백없애기
spaceBetween:false

클릭/스와이프해도 계속 자동넘김
autoplayDisableOnInteraction:false

높이 이상하면
autoHeight: true

전환과정 속도조절
speed:500

자동넘김 속도조절
autoplay:3000

맨 끝으로 가면 해당 방향 화살표버튼 안보이게
watchOverflow: true

----------------------------------------------------------------------------------------------------

스와이퍼(swiper) 슬라이드 참고

http://2.swiper.com.cn/demo/index.html ←피씨(익스8호환용인거같은데 이거쓸바엔 슬릭쓰길추천)
http://3.swiper.com.cn/api/index.html ← 모바일 , 익스8안되는 피씨
http://idangero.us/swiper/demos/#.WXhdqISLSHv ←??

각각 오른쪽 위에 검색 , 왼쪽에 메뉴있음

----------------------------------------------------------------------------------------------------

슬라이드 페이지네이션

번호나오는 스크립트 123‥쭉 나오는 버전 (★끼워넣을때 꼭 ,(쉼표) 붙이기)

var sl1 = new Swiper('.swiper-container', {
	pagination: '.swiper-pagination',
	paginationClickable: true,
	paginationBulletRender: function (sl1, index, className) {
		return '<span class="' + className + '">' + (index + 1) + '</span>';
	}
});

번호나오는건데 1of2 이렇게나오는 버전

var sl1 = new Swiper('.swiper-container', {
	pagination : '.swiper-pagination',
	paginationType : 'custom',
	paginationCustomRender: function (sl1, current, total) {
		return current + ' of ' + total;
	}
});

번호나오는건데 1/2 이렇게나오는 버전

var mySwiperprod_slide_wrap = new Swiper('.prod_slide_wrap .swiper-container',{
	pagination: '.prod_slide_wrap .pagination',
	loop:true,
	grabCursor: true,
	paginationClickable: true,
	autoplay:2500,
	paginationType : 'fraction',
	autoplayDisableOnInteraction:false
});

----------------------------------------------------------------------------------------------------

페이지네이션 다른걸로 바꾸기

var tabSl = $(".tabSl .swiper-container").swiper({
	loop: true,
	autoplay: 2500,
	pagination : ".swpPaging",
	paginationClickable :true,
	onSlideChangeStart: function(swiper){
		$(".tabSl .tabSlTab a").removeClass("on");
		$(".tabSl .tabSlTab a").eq(swiper.realIndex).addClass("on");
	},
	onInit: function(swiper){
		$(".tabSl .tabSlTab a").eq(0).addClass("on");
		//bind paging click
		$(".tabSl .tabSlTab a").each(function(index){
			$(this).click(function(){
				$(".tabSl .swpPaging span").eq(index).click();
			});
		});
	}
})

----------------------------------------------------------------------------------------------------

슬라이드 화살표or페이지네이션 하나만나오고 슬라이드 안될때

화살표or페이지네이션이 컨테이너 밖에 나와있는지 확인
나와있으면 나와있는것까지 감싸는 랩 만든다음 거기다 클래스를 넣어서 연결시켜야댐

----------------------------------------------------------------------------------------------------

var section_F4 = new Swiper('.section_F4 .swiper-container',{
nextButton: '.section_F4 .swiper-button-next',
prevButton: '.section_F4 .swiper-button-prev',
speed:500,
autoplay:3000,
slidesPerView : 'auto',
onSlideChangeStart: function(){
	$(".add_tabs .active").removeClass('active')
	$(".add_tabs a").eq(section_F4.activeIndex).addClass('active')
	$(".layerLink.floorNum .active").removeClass('active')
	$(".layerLink.floorNum a").eq(section_F4.activeIndex).addClass('active')
}
})
$(".add_tabs a , .add_tabs2 a").on('touchstart mousedown',function(e){
	e.preventDefault()
	$(".add_tabs .active").removeClass('active')
	$(this).addClass('active')
	section_F4.slideTo( $(this).index() )
})
$(".add_tabs a , .add_tabs2 a").click(function(e){
	e.preventDefault()
})
$('.section_F4 .swiper-container').mouseover(function(){
	section_F4.stopAutoplay();
})
$('.section_F4 .swiper-container').mouseout(function(){
	section_F4.startAutoplay();
})


$(".layerLink a").click(function(){
	$(".layerAll").addClass("on")
	var idx=$(this).index()
	var idxx=$(".layerCon > li:eq("+idx+")")
	$(".layerCon > li").removeClass("on");
	$(".layerCon").addClass("on")
	idxx.addClass("on");
	section_F4.stopAutoplay();

	var lh=idxx.height()/2
	console.log(lh)
	idxx.css("margin-top",-lh)

	$(".gnb_menu,.swiper-pagination.high,.swiper-button-next.high,.swiper-button-prev.high").css("z-index",0)
})
$(".layerBg").click(function(){
	$(".layerAll").removeClass("on")
	$(".layerCon").removeClass("on")
	section_F4.startAutoplay();

	$(".gnb_menu,.swiper-pagination.high,.swiper-button-next.high,.swiper-button-prev.high").css("z-index",1000)
})

이렇게 다른데서 슬라이드 제어할수있음
단 슬라이드 생성부분이 전역이여야함
var section_F4 = new Swiper('.section_F4 .swiper-container',{  ←이게 어디 안에 들어있으면 안됨

----------------------------------------------------------------------------------------------------

제이쿼리 delay쓸때
hide/show가 아닌 fadeIn/fadeOut , slideUp/slideDown , animate({}) 등과 조합해서 쓰기

잘 안되면 자바스크립트 settimeout으로 쓰기
setTimeout(함수,초);
setTimeout(function(){
	$("header").css("z-index",100);
},500);

----------------------------------------------------------------------------------------------------

wow 플러그인 (https://wowjs.uk/)

★적용 방법
1. 클래스로만 적용 <li class="wow flip">
2. 클래스와 css속성으로 적용 <li class="wow"> → li{animation-name:fadeInRight;}

★html속성(필요하면 추가)
data-wow-duration="1s" : 변환속도
data-wow-delay="1s" : 딜레이
data-wow-offset : 애니메이션 시작 거리
data-wow-iteration : 애니메이션 반복 횟수

★css animation 속성으로도 적용 가능
animation-delay : 로드되고 나서 언제 시작할지(딜레이)
animation-direction : 애니메이션이 종료되고 다시 처음부터 시작할지 역방향으로 진행할지 지정
	(normal,reverse,alternate,alternate-reverse,initial,inherit)
animation-duration : 애니메이션이 진행시간 (3초 = 3s 으로 표시)
animation-iteration-count : 몇 번 반복 (infinite : 계속반복)
animation-name : 애니메이션이름
animation-play-state : 애니메이션 시작 또는 정지 상태(running,paused)
animation-timing-function : 애니메이션 속도(가속/감속 시간간격등 설정)
	(linear,ease,ease-in,ease-out,ease-in-out,step-start,step-end,steps(int,start|end),cubic-bezier(n,n,n,n),initial,inherit)
animation-fill-mode : 시작되기 전이나 끝나고 난 후 어떤 값이 적용될지 지정합니다
	애니메이션이 끝난후 처음상태로? 끝난 상태로?
	(none,forwards,backwards,both,initial,inherit)


슬라이드에 사용시 첫슬라이드는 wow로 애니메이션 가능

<script type="text/javascript" src="/jscript/wow.min.js"></script>
<script type="text/javascript" src="/jscript/swiper.animate.min.js"></script>
<script type="text/javascript" src="/jscript/swiper-3.4.2.min.js"></script>

<div class="swiper-container">
	<div class="swiper-wrapper">
		<div class="swiper-slide p1">
			<div class="tit ani2 wow bounceInUp" swiper-animate-effect="bounceInUp" swiper-animate-duration="1.5s" swiper-animate-delay="0s">다양한 중국내 <span class="bold">현지마케팅 기능</span></div>
			<ul class="ani2 wow bounceInUp" swiper-animate-effect="bounceInUp" swiper-animate-duration="1.5s" swiper-animate-delay="0s">
				<li>
					<a href="javascript:;" class="btnforsl1"><img src="/images/sl3-11.png" alt=""></a>
				</li>
				<li>
					<a href="javascript:;" class="btnforsl2"><img src="/images/sl3-12.png" alt=""></a>
				</li>
				<li>
					<a href="javascript:;" class="btnforsl3"><img src="/images/sl3-13.png" alt=""></a>
				</li>
				<li>
					<a href="javascript:;" class="btnforsl4"><img src="/images/sl3-14.png" alt=""></a>
				</li>
				<li>
					<a href="javascript:;" class="btnforsl5"><img src="/images/sl3-15.png" alt=""></a>
				</li>
			</ul>
		</div>
		<div class="swiper-slide p2">
			<div class="tit">
				<div>다양한 중국내 <span class="bold">현지마케팅 기능</span></div>
				왕홍 <span class="bold">추천인 제도</span> & 실시간 <span class="bold">라이브 방송</span> 마케팅
			</div>
			<div class="image ani2" swiper-animate-effect="bounceInUp" swiper-animate-duration="1.5s" swiper-animate-delay="0s"><img src="/images/sl3-2.png" alt=""></div>
		</div>
		<div class="swiper-slide p3">
			<div class="tit">
				<div>다양한 중국내 <span class="bold">현지마케팅 기능</span></div>
				스마트폰 통해 바로 SNS공유
			</div>
			<div class="image ani2" swiper-animate-effect="bounceInUp" swiper-animate-duration="1.5s" swiper-animate-delay="0s"><img src="/images/sl3-3.png" alt=""></div>
		</div>
		<div class="swiper-slide p4">
			<div class="tit">
				<div>다양한 중국내 <span class="bold">현지마케팅 기능</span></div>
				상품/기획전 QR코드 생성 및 홍보 마케팅
			</div>
			<div class="image"><img src="/images/sl3-4.png" alt=""></div>
		</div>
		<div class="swiper-slide p5">
			<div class="tit">
				<div>다양한 중국내 <span class="bold">현지마케팅 기능</span></div>
				O2O  현지 마케팅
			</div>
			<div class="image"><img src="/images/sl3-5.png" alt=""></div>
		</div>
	</div>
	<div class="swiper-button-next"></div>
	<div class="swiper-button-prev"></div>
</div>


<script type="text/javascript">
	var section_F3 = new Swiper('#F3 .swiper-container',{
		nextButton: '#F3 .swiper-button-next',
		prevButton: '#F3 .swiper-button-prev',
		speed:500,
		loop:true,
		autoplay:0,
		slidesPerView : 'auto',
		onInit: function(swiper){
			swiperAnimateCache2(swiper);
			swiperAnimate2(swiper);
		},
		onSlideChangeEnd: function(swiper){
			swiperAnimate2(swiper);
		}
	});

	$(".btnforsl1").click(function(){
		section_F3.slideTo(1,500)
		swiperAnimate2(swiper);
	})
	$(".btnforsl2").click(function(){
		section_F3.slideTo(1,500)
		swiperAnimate2(swiper);
	})
	$(".btnforsl3").click(function(){
		section_F3.slideTo(2,500)
		swiperAnimate2(swiper);
	})
	$(".btnforsl4").click(function(){
		section_F3.slideTo(3,500)
		swiperAnimate2(swiper);
	})
	$(".btnforsl5").click(function(){
		section_F3.slideTo(4,500)
		swiperAnimate2(swiper);
	})
</script>

----------------------------------------------------------------------------------------------------

체크박스 체크/해제시 이벤트(숨김/보이기)

$(".reserv-switch").change(function(){
	if($(".reserv-switch").is(":checked")){
		$(".reserv-con").show()
	}else{
		$(".reserv-con").hide()
	}
})

----------------------------------------------------------------------------------------------------

백지에서 새로 만들때(알림톡,견적서 등)

<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
헤드에 넣으면 글자안깨짐

<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
헤드에 이거 넣으면 모바일에서 글자 안깨짐

----------------------------------------------------------------------------------------------------

colgroup 사용법

<colgroup>
	<col width="120" style="background-color:#F5F5F5;" />
	<col width="*" style="background-color:#FFFFFF;" />
</colgroup>

----------------------------------------------------------------------------------------------------

폰트 적용(웹폰트 크롬에서 안될때)

폰트 다운받은뒤 css폴더에 확장자 바꿔서(https://onlinefontconverter.com 여기서 변경)
.svg / .ttf / .woff / .eot
4개 저장하고 common.css에다 아래 이름바꿔서 넣은다음 css에서 쓸때 base에
아래처럼 font-family:'' 여기안에 적은것과 동일한 이름으로 사용 (이름 바꿔도 상관없음 대소문자구분X)

@font-face {
 font-family:'BMJUA';
 src:url('/css/font/BMJUA_ttf.eot');
 src:local(※),
  url('/css/font/BMJUA_ttf.eot#iefix') format('embedded-opentype'), /* IE6-IE8 */
  url('/css/font/BMJUA.woff') format('woff'),
  url('/css/font/BMJUA.ttf') format('truetype'),
  url('/css/font/BMJUA.svg#webfonturzspG4F') format('svg');
}

otf↔ttf
https://www.files-conversion.com/font-converter.php

----------------------------------------------------------------------------------------------------

무료폰트
https://noonnu.cc/

----------------------------------------------------------------------------------------------------

bgcolor="fff"
bgcolor는 이렇게하면 안된다고 함 (확실하진 않음)

bgcolor="ffffff"
6자리로 하라고 함

----------------------------------------------------------------------------------------------------

float 되잇거나 이거나 테이블이 안에 있으면
vertical-align:middle 이 안됨 할려면 table,table-cell로

----------------------------------------------------------------------------------------------------

모바일에서 레이어팝업을 띄우고 본문에서는 스크롤 안되게 할려면


적용
$('body').bind('touchmove', function(e){e.preventDefault()});

해제
$('body').unbind('touchmove');


안되면 ↓↓↓


적용
$("body").css({overflow:'hidden'}).bind('touchmove', function(e){e.preventDefault()});

해제
$("body").css({overflow:'auto'}).unbind('touchmove');


이마저도 안된다면 감싸고있는랩에 position:fixed 하기 ↓↓↓


적용
$(".wrap").css(position,fixed)

해제
$(".wrap").css(position,relative)

----------------------------------------------------------------------------------------------------

아이폰(사파리) input-text 그림자 생기는거 제거
-webkit-appearance:none;appearance:none;

----------------------------------------------------------------------------------------------------

input-checkbox , input-radio 기본 체크박스 , 라디오 버튼 없앨때 -webkit-appearance:none;appearance:none;

----------------------------------------------------------------------------------------------------

appearance:none 되있는거 살릴때

http://webdir.tistory.com/430 참고 (구글에 "appearance속성" 검색)

select 버튼 ↓
select{appearance:menulist-button;-webkit-appearance:menulist-button;}

menulist-button 의 button빼고 menulist만 써도 됨

----------------------------------------------------------------------------------------------------

할인없을때 세일퍼센트를 텍스트로 바꾸기

css로 on추가되면 텍스트로

.prod_slide_wrap .goods .txt .numValue .per span{font-size:22px;color:#000;}
.prod_slide_wrap .goods .txt .numValue .per span em{color: #f84839; display: inline-block; font-size: 35px; font-weight: normal; line-height: 40px; margin-right: 5px;}
.prod_slide_wrap .goods .txt .numValue .per.on span{display:none;}
.prod_slide_wrap .goods .txt .numValue .per.on:before{content:"내여펫가";font-size:20px;color:#f84839;padding-left:5px;line-height:30px;}

----------------------------------------------------------------------------------------------------

레이어팝업 세로가운데정렬

.pop_box {display:table; z-index:998; position: fixed; top: 0; left: 0; width: 100%; height:100%;}
.pop_mask { z-index: 999; position: fixed; top: 0; bottom: 0; width: 100%; background: #000; opacity: .3;}
.pop_inner_wrap {display:table-cell; vertical-align:middle; text-align:center;}
.pop_box_inner { position: relative; z-index: 1000; width: 500px; border:1px solid #9e9e9e; margin:0 auto; vertical-align: middle;}

----------------------------------------------------------------------------------------------------

완전 block이면 margin:auto 되고 inline-block이면 랩에 text-align:center

----------------------------------------------------------------------------------------------------

버튼 등 안에서 이미지랑 텍스트 세로가운데정렬시킬때
이미지랑 텍스트 둘다 valtical-align:middle 해야 제대로 가운데정렬됨 (★label 은 vertical-align:initial 이나 baseline 으로 해야 가운데로 정렬됨)

박스안에 이미지,텍스트 등 여러가지 내용있을때
감싸는 박스에 line-height:하지말고 박스엔 높이만 넣은다음
내부에서 vertical-align:middle 모두 적용하고 ★필요에 따라 display:inline-block 추가후(이미지를 감싸는 태그) 그다음 line-height로 조절하기

----------------------------------------------------------------------------------------------------

세로슬라이드

<link rel="stylesheet" type="text/css" href="<%=pathMobile%>/css/swiper.min.css" />
<script type="text/javascript" src="/jscript/swiper.min.js"></script>

<style>
.conWrap .swiper-container {
  width: 100%;
  height: 100%;
}
.conWrap .swiper-slide {
  height: auto;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}
</style>

<ul class="pictures">
<!-- Swiper -->
      <div class="swiper-container">
        <div class="swiper-wrapper">
          <div class="swiper-slide">
			<li><div class="con"><img src="/m/images/sample.jpg" alt=""></div></li>
			<li><div class="con"><img src="/m/images/sample.jpg" alt=""></div></li>
			<li><div class="con"><img src="/m/images/sample.jpg" alt=""></div></li>
			<li><div class="con"><img src="/m/images/sample.jpg" alt=""></div></li>
			<li><div class="con"><img src="/m/images/sample.jpg" alt=""></div></li>
			<li><div class="con"><img src="/m/images/sample.jpg" alt=""></div></li>
			<li><div class="con"><img src="/m/images/sample.jpg" alt=""></div></li>
			<li><div class="con"><img src="/m/images/sample.jpg" alt=""></div></li>
			<li><div class="con"><img src="/m/images/sample.jpg" alt=""></div></li>
			<li><div class="con"><img src="/m/images/sample.jpg" alt=""></div></li>
			<li><div class="con"><img src="/m/images/sample.jpg" alt=""></div></li>
			<li><div class="con"><img src="/m/images/sample.jpg" alt=""></div></li>
			<li><div class="con"><img src="/m/images/sample.jpg" alt=""></div></li>
		 </div>
        </div>
        <!-- Add Scroll Bar -->
        <div class="swiper-scrollbar"></div>
      </div>
      <!-- Swiper End -->
	</ul>

<script>
  var swiper = new Swiper(".conWrap .swiper-container", {
    scrollbar:".conWrap .swiper-scrollbar",
    direction:"vertical",
    slidesPerView:"auto",
    mousewheelControl: true,
    freeMode: true
  });

 //첨로딩시 높이지정
  resetSwipe();
  //가로세로 resize
  $(window).resize(function(){
    resetSwipe();
  });

//swipe 리셋
  function resetSwipe(){
    $(".pictures").height($(window).height()-$(".fixedTop").height()-$(".fixedGnb").height()-$(".picbnrWrap").height());
    swiper.update();
  }
</script>


----------------------------------------------------------------------------------------------------

백그라운드 속성

background-size:cover; 너비나 높이를 확대/축소해서 짤리게 맞춤 (여백x)
background-size:contain; 너비나 높이를 확대/축소해서 안짤리게 맞춤 (여백o)

정렬은 cover/contain 과는 별개로
background-position 으로 한다 , 중앙은 center로해도되지만 50%도 됨

----------------------------------------------------------------------------------------------------

백그라운드 축약형에 background-size 넣으려면 /(슬래시)

body { background: #f00 url("bg-img.png") repeat-x fixed left top/100% 100%;}

----------------------------------------------------------------------------------------------------

백그라운드 한쪽 기준잡아서 늘릴때

background:url()repeat-y center 0/100%;

----------------------------------------------------------------------------------------------------

탭메뉴 on된거 뒤에배경넣을때 background-position:100% 100% 하면 반응형댐
이미지에 그림자있을경우 첫번째/마지막 li:first-child.on{background-position , text-indent}로 위치 조정

----------------------------------------------------------------------------------------------------

탭메뉴 기본스크립트

$(".bestobWrap .tab li:eq(0)").addClass("on")
$(".pdListWrap ul:eq(0)").show()
$(".bestobWrap .tab li").click(function(){
	$(this).addClass("on").siblings("dd").removeClass("on") //siblings대신next써도댐
	var idx = $(this).index()
	$(".pdListWrap > ul:eq("+idx+")").show().siblings().hide()
})

----------------------------------------------------------------------------------------------------

단위에서 vw = %랑비슷한데 %는 부모기준 vw/vh는 화면크기기준 vh(높이)도 가능 ★모바일버전할때 이미지최대지정 하려면 width/height 둘다 max vw/vh로

설명:width에는 vw를 hright에는 vh를 사용합니다. 이 부분은 반응형웹과 같은 곳에서 쓰일수록 더욱 편리함이 높아집니다. 이 단위는 요소의 뷰포트값의 100분의 1을 하는 값을 뜻합니다. 즉 값에 해당하는 숫자는 1부터 100이 됩니다. (1vh -100vh)
가령 브라우저의 전체 넓이가 1000px이 된다면 1vh는 10px가 되는 것을 뜻합니다.위 단위를 사용하는 사례로는,퍼센테이지 값이 아닌, 좀더 명확한 단위를 씀으로써 편리하면서도 가변적으로 변할 수 있는 전체화면을 만들었습니다.다만 이 단위를 쓰는 경우, IE의 하위 브라우저는 지우너이 가능하지 않다는 점을 알아두어야합니다.


ex)
<div class="member_input" style="position:relative; padding-left:38vw; font-size:0; line-height:0; margin-top:12px;">
	<a href="javascript:openNewAddr()" class="btn_style2" style="width:33vw;position:absolute;left:15px;top:0;margin-top:0px">우편번호찾기</a><span class="box" style="width:2%;"></span><input type="hidden" id="post" name="post">
	<input name="addr" id="addr" class="text" type="text" placeholder="주소 입력<%=iif(checkBitwise(JOINSET_REQUIRE, permAddr), " *","")%>" style="width:100%;margin-top:0" />
</div>

----------------------------------------------------------------------------------------------------

밴더프리픽스(크로스브라우징)

- 브라우저별로 각각 따로 속성을 지정할 수 있음
- 구형 브라우저에서 쓸수 있게 해줌

-webkit-	구글, 사파리 브라우저
-moz-	파이어폭스 브라우저
o-	페라 브라우저
-ms-	익스플로러 (대부분 생략함)

--안붙은(기본) 속성을 마지막에 작성

참조
https://dolly77.tistory.com/9
http://blog.naver.com/hsoojy_/220887253788

변환사이트
http://cssprefixer.appspot.com/

----------------------------------------------------------------------------------------------------

empty() : 태그안의 내용을 없앰

remove() : 태그 자체를 없앰

ex) 페이지전체 br태그 제거
$(document).ready(function(){
	$(this).find("br").remove();
})

----------------------------------------------------------------------------------------------------

css에서 !important 되있는거 더 쎄게 먹일려면
클래스를 붙여서 !important 하면됨
안으로 들어갈수록 세게 먹음 (불러오는 클래스나 태그를 많이)

ex)
.top_fix_head{background:#fefefe !important;}
.sitebg1{background:<%=cfgColor1%> !important;}

<div class="top_fix_head sitebg1">

위 상황에서 더 쎄게 넣을려면
.top_fix_head.sitebg1{background:none !important;} 이나
div.sitebg1 등 좀 섞어서 넣기

★ css적용 중요도순
외부 < 내부 < 인라인 < 스크립트 < !important 외부 < !important 내부..


/참고
캐스케이딩 (cascading)
엘리먼트는 다양한 CSS 선언의 영향을 받는다. 이 때 충돌을 피하기 위해서 우선순위를 정하는데 이를 캐스케이딩이라고 함.
캐스케이딩에는 다음과 같이 세가지 규칙이 있음.
중요도 - css가 어디에 선언 되었는지에 따라서 우선순위가 달라짐
명시도 - 대상을 명확하게 특정할수록 명시도가 높아지면서 우선순위가 높아짐
소스순서 - css 선언을 나중에 할수록 우선순위가 높아짐

----------------------------------------------------------------------------------------------------

스크롤에따라 변화

$(window).scroll(function(){
  var s = $(document).scrollTop()
  console.log(s)
  if(s>=20 && s<=140){
    $(".head_top").addClass("on")
    $(".head_top").removeClass("on2")
    $(".appearanceWrap").show()
  }else if(s>=140){
    $(".head_top").addClass("on")
    $(".head_top").addClass("on2")
    $(".appearanceWrap").hide()
  }else{
  	$(".head_top").removeClass("on")
  	$(".head_top").removeClass("on2")
    $(".appearanceWrap").show()
  }
})

----------------------------------------------------------------------------------------------------

스크롤 이동


페이지 스크롤 이동
$(".paging a").click(function(){
	$("html, body").scrollTop($(".listBannerwrap").height())
})

$(".btn1").click(function(){
	$("html, body").animate({"scrollTop":0})
})


다른 방법
window.scrollTo(xpos, ypos);

부드러운 이동
window.scrollTo({left:0, top:250, behavior:'smooth'});

요소내 스크롤 이동
function option_box_Layer_close(){
	$('div.option_box_Layer').scrollTop(0);
}

----------------------------------------------------------------------------------------------------

background-attachment:scroll / fixed

쓸일은거의없다 (원페이지스크롤할때등 가끔 사용 가능)

----------------------------------------------------------------------------------------------------

가끔가다 css적용안되면 그 페이지에
<link rel="stylesheet" href="/admin/css/common.css"> 걸기

----------------------------------------------------------------------------------------------------

엔티티코드(entity code)

http://cafe.naver.com/webmarkup/1628 참고
&#문자코드; 도 가능 ex) &#65 → A

----------------------------------------------------------------------------------------------------

스크립트에서 엔터 넣을때

\n (역슬레시n)

----------------------------------------------------------------------------------------------------

Hex 변환

https://r12a.github.io/apps/conversion/

----------------------------------------------------------------------------------------------------

리스트이미지 차곡차곡 벽돌 계단정렬(+창크기변화따라 자동애니메이션 정렬)
masonry.js

$(document).ready(function(){
	$(".cont_list li dl dt img").imagesLoaded().then(function(){
		$('.cont_list').masonry({
			itemSelector : 'li',
			isFitWidth : true,
			animate: true,
		})
	}).masonry();
});
$(window).resize(function(){
	$(".cont_list li dl dt img").css("max-width","100%");
});

----------------------------------------------------------------------------------------------------

관리자에서 갖고가지는경우(ex.팝업) 관리자에서 스크립트를 iframe바깥으로 or 상위한테 적용시킬때

함수 앞에 parent. 붙이기
ex) <span class="btnClosePop" style="cursor:pointer; position:absolute; top:0; right:0;"><img src="/data/hanguoshopping/MarketingBanner/close.png" class="btn_pop_main_close" onclick="parent.closewin();" border="0"></span>

----------------------------------------------------------------------------------------------------

리스트 상품들 hover 했을때 선 생기는거 할때 여백같은 선자국(border:1px solid #fff or transparent) 이거 없애고 padding으로 하는법

background 로 상위에다 백그라운드 안보이게 해놓고 (box-sizing:border-box도)
hover했을때 padding:1px로

단점 : 애니메이션(transition) 효과 넣으면 이미지가 안쪽으로 밀리면서 약간 흔들흔들거릴 수 있음

----------------------------------------------------------------------------------------------------

슬라이드 등 api(플러그인) 헤더에 연결 css/js

pc : /_include/header.asp
m : /m/_include/mobile_header.asp

----------------------------------------------------------------------------------------------------

끝으로 가면 해당방향 화살표 사라지는 슬라이드

http://elizabetharden.mallshopping.co.kr/m/page.asp?uid=1182
참조 bx슬라이더

----------------------------------------------------------------------------------------------------

vertical-align:middle은 같은부모속 자신과붙어있는형제가 inline이나 inline-block일때만 가능 (line-height 없이)
float이 근처에 있으면 안됨

<a href="#"><img src="http://wmall.wavayo.com/data/wmall/banner/ico_tl2.png" border="0"><span>즐겨찾기</span></a>
이렇게 되있을경우 이미지랑 span에 직접 따로따로 vertical-align:middle 넣어야댐 바깥쪽 a에다 넣으면 안됨 (꼭 형제인 span에도 같이 넣어야됨!)

아니면 이미지에다만 vertical-align top or middle 한다음 자체line-height 조절

아니면 이미지에 top한다음 부모의 line-height로 조절

----------------------------------------------------------------------------------------------------

radio라디오 선택에따라 보이는 항목 다르게(숨김/노출 되게)

<style>
.deliveryTypeS{display:none;}
</style>

<tr>
	<th scope="row">배송선택</th>
	<td class="deliveryType">
		<label for="deliveryTypeI"><input type="radio" name="deliveryType" id="deliveryTypeI" class="radioClick" checked style="margin-top:-2px">개별배송</label>
		<label for="deliveryTypeS" style="margin-left:20px"><input type="radio" name="deliveryType" id="deliveryTypeS" class="radioClick" style="margin-top:-2px">복수배송</label>
	</td>
</tr>

<tr class="deliveryTypeI">
	개별일때
</tr>
<tr class="deliveryTypeS">
	복수일때
</tr>

<!-- 배송유형 스크립트 -->
<script>
	$('.deliveryType .radioClick').on('click',function(){
		$('.radioClick').parent().removeClass('on');
		$(this).parent().addClass('on');
		var operator = $(this).attr('data');
		if (operator == 'T'){
			$('#deliveryType').val('T');
		}else{
			$('#deliveryType').val('F');
		}
	});
	$('.deliveryType .radioClick').each(function(){
		if ($(this).is(':checked')){
			$(this).parent().addClass('on');
			if ($(this).attr('data') == 'T'){
				$('#deliveryType').val('T');
			}else{
				$('#deliveryType').val('F');
			}
		}
	});
	$('.deliveryType label').click(function(){
		if($(".deliveryType label:eq(1)").hasClass("on")){
			$(".deliveryTypeI").hide()
			$(".deliveryTypeS").show()
		}else{
			$(".deliveryTypeS").hide()
			$(".deliveryTypeI").show()
		}
	})
</script>
<!-- 배송유형 스크립트끝 -->

----------------------------------------------------------------------------------------------------

아래처럼도 사용가능

$("#ac-gn-menustate").change(function(){
	if($(this).is(":checked")){
		console.log(1)
	}else{
		console.log(0)
	}
})

----------------------------------------------------------------------------------------------------

페이지 복사해서 새로만들때

<!--#include virtual="/m/_include/mobile_header.asp"-->
<!--#include virtual="/_lib/function.Goods.asp"-->
<!--#include virtual="/m/_lib/mobile.function.Page.asp"-->
<!--#include virtual="/m/_include/mobile_bodyS.asp"-->

이거 넣으면

페이지 하단 끝에

<!--#include virtual="/m/_include/mobile_footer.asp"-->
<!--#include virtual="/m/_include/mobile_bodyE.asp"-->

이거도 넣어야됨

----------------------------------------------------------------------------------------------------

이미지 리스트 만들때

이미지를 늘려 짜를지 다 나오게하고 여백남길지 정하기

----------------------------------------------------------------------------------------------------

아이프레임으로 관리자꺼 이미지(값) 저장하면 ftp로 불러오는거 에서 불러오는 위치에(아이프레임 바깥) 닫기버튼 있을때 닫기버튼을 이미지따라가게 하기 (스크립트로 값 불러오기)

불러오는 파일에 = 닫기버튼 있는곳
var fnImgNavi = function(hgt){
	$(".btnClosePop").css("margin-top",-hgt/2);
}


불려가는 파일에 = 이미지 있는곳
$(window).load(function(){
	var hgt=$(".popMainImg").height();
	parent.fnImgNavi(hgt);
})
$(window).resize(function(){
	var hgt=$(".popMainImg").height();
	parent.fnImgNavi(hgt);
})

----------------------------------------------------------------------------------------------------

위에거 혹시나안되면 불려가는곳에 아래 추가 (이미지 리사이즈 계속시키는거인듯)

function adjustParentIFrame() {
	if (parent.resizeFrame) { parent.resizeFrame(window); }
	else { setTimeout("adjustParentIFrame()", 250); }
}
adjustParentIFrame();

----------------------------------------------------------------------------------------------------

표 내 모든 선 1px 만들기


방법1) 표에서 배경으로 1px 선넣기

cellspacing="1" 하면 1px 간격띄워지는데 테이블에 선 색깔 할거 bgcolor로 배경색 넣은다음
tr이나 td에 bgcolor #ffffff 해서 안에서 이중으로 칠해야한다


방법2) table의 선과 th/td 의 선을 합치기

table,th/td 모두 1px 넣고 table스타일에 border-collapse:collapse 로 합친다
(다른태그도 display:table 하면 똑같이 할 수 있고 반대로 테이블도 td나 어디에 float같은거 들어있으면 디스플레이바껴서 collapse안된다)

방법3) first-of-type/nth-of-type/last-of-type + border-top:0 등 조합하기

---------------------------------------------------------------------------------------------------

border-collapse 속성

separate : 기본
collapse : 서로 이웃하는 테이블이나 셀의 테두리션을 분리시켜 표현 (한마디로 선 겹치는거 제거)

---------------------------------------------------------------------------------------------------

기본값인 auto는 내용에 따라 셀의 넓이가 달라지는데, fixed로 지정해놓으면 셀 너비가 고정된다
안에내용이 많아도 테이블 넓이를 작게할수있음

table-layout:fixed

---------------------------------------------------------------------------------------------------
 
내용이 한줄일때는 띄어쓰기가 나올때까지 줄바꿈이 안되는데 띄어쓰기가 없어도 강제로 줄 바꿈을 시키려면 아래처럼하면됨

word-break:break-all

---------------------------------------------------------------------------------------------------

익스 position:fixed 쓸거면

div안에 iframe있음 div에다말고 ifrane에다 너야댐

----------------------------------------------------------------------------------------------------

내부스타일 안먹으면 (인라인말고)

<style></style> 위아래로 if같은거 들어가있는지 확인

<%
	If SITEID = "zonskin" Then
%>
<style type="text/css">
	.fixedBarBox {display:block !important;}
	.headClass-wrap {display:none;}
</style>
<%
	End If
%>

밖에다가 새로 <style></style> 만들어서 써야댐

----------------------------------------------------------------------------------------------------

서브페이지들 헤더같은거 한번에 바꿀때는 페이지마다 말고 관리자 서브상·하단에서 한번에가능(!important 활용)
없으면 하나 새로등록

----------------------------------------------------------------------------------------------------

에디트플러스 팁


[단축키]

ctrl+[ : 커서위치 쌍을 이루는 태그로 이동★
ctrl + shift + [ : 커서위치 쌍을 이루는 시작태그와 끝맺음태그의 '내부'만 선택★ a태그안에 텍스트수정할때 유용 , 내용이없을경우에도 됨
ctrl + shift + d : 커서위치 포함한 요소선택★
ctrl+j : 행 아래로복사★
alt+c / clt 좌클릭 : 블럭선택
f12 : 이전작업파일

ZC → zencoding이나emmet후 <탭키로 확장>  탭으로 ctrl+e가능 

Ctrl+N 새 보통 문서 (보통 문서를 새로 생성)
Ctrl+S 저장 (현재 문서를 저장)
Ctrl+Shift+S FTP 업로드 (파일을 서버로 업로드)
Ctrl+D 날짜  (현재 날짜를 삽입)
Ctrl+Shift+D 날짜 길게 (현재 날짜를 긴 형식으로 삽입)
Ctrl+Shift+Delete 줄 끝까지 지우기 (현재 줄의 끝까지 지움)
Ctrl+Delete 단어 끝까지 지우기 (현재 단어의 끝까지 지움)
Alt+Shift+Delete 줄 지우기 (현재 줄을 지움)
Alt+Delete 단어 지우기 (현재 단어를 지움)
Ctrl+J 줄 복제 (현재 줄을 복제)
Ctrl+K 대소문자 뒤바꿈 (선택한 텍스트에서 대소문자를 뒤바꿈)
Ctrl+L 소문자로 (선택한 텍스트를 소문자로 변환)
Ctrl+U 대문자로 (선택한 텍스트를 대문자로 변환)
Alt+Shift+E 칸 단위 선택 (시작/종료 칸 단위 선택영역 지정을 시작하거나 종료)
Ctrl+R 줄 선택 (현재 줄을 선택)
Ctrl+B 브라우저로 보기 (현재 열린 문서를 웹 브라우저에 읽어 들임)
Alt+Shift+I 탭과 공백 기호 (탭과 공백 기호를 보이거나 숨김)
Alt+F3 찾기  (지정한 문자열을 찾음)
F3 다음 찾기  (다음 일치하는 말을 찾음)
Shift+F3 이전 찾기  (이전에 일치하는 말을 찾음)
Ctrl+H 바꾸기  (지정한 문자열을 다른 문자열로 바꿈)
Ctrl+] 괄호 찾기  (짝을 이루는 괄호를 검색)
Ctrl+F3 다음 단어 찾기★  (현재 단어나 선택한 텍스트와 다음에 일치하는 말을 찾음)
(Ctrl+)Shift+F3 이전 단어 찾기★  (현재 단어나 선택한 텍스트와 이전에 일치하는 말을 찾음)
F8 URL로 가기  (강조된 URL로 찾아감)
F12 최근 작업 창 (바로 전에 작업한 문서 창으로 이동)
F11 창 목록 (모든 문서 창들의 목록을 보여줌)
Ctrl+Tab 다음 창 (다음 문서 창으로 이동)
Ctrl+Shift+Tab 이전 창 (이전 문서 창으로 이동)
Ctrl+Shift+A 젠코딩 랩씌우기


[기타]

기본왼쪽 디렉토리 폴더,파일선택 하는곳에 커서대고 우클릭+f 하면 현재파일 위치로 감 (여러사이트 대조해서작업할때 유용)

자동백업파일 찾을때 파일명 뒤에 한칸 뛰고 폴더명 적으면 해당폴더에있는 파일들만 검색됨 ex) reg_goods_form.asp wava

새로저장할때 왼쪽에 폴더경로위치에 놓고 저장누르면 계속 그위치에 저장할수있다,파일목록에놓고 새로고침하면 저장되는거 바로바로확인도가능(백업파일 하드에만들때유용함)

----------------------------------------------------------------------------------------------------

★서브라임 & 엑셀로 일괄처리/자동화 팁

1. dto에서 필드 모두 긁어서 서브라임에 붙이기
2. dto.setSeq(rs.getString("seq")); 넣을거 만들기or복사
3. 다중 커서 잡아놓고 붙이기 → 위치이동 + ctrl + k + u로 대소문자 일괄 수정

엑셀은 sql문 한꺼번에 처리해서 나중에 보기쉽게 하기위해 파일로 저장해놓을때 좋음
테이블명 붙여넣어서 원본셀 만들어놓고 다른셀에서 '&' 이용해서 일괄처리
엑셀 셀들을 여러줄 복사후 sql디벨로퍼에 바로 붙이기는 안됨, 메모장을 한번 거쳐서 가져가야됨

( ) 괄호안의 글자 모두 선택할때 : 괄호안에 커서 놓고 ctrl+shift+m (sql문에서 쓰기좋음, 다중커서(alt+f3)이랑 연계하기)
( ) 괄호안에서 처음과 끝 이동할때 : 괄호안에 커서 놓고 ctrl+shift+m


서브라임에서 여러행의 한 위치에 다른내용 여러행을 붙여넣을때 팁 (붙여넣을 공간들이 멀리 떨어져있어도 상관없음)
복사한 요소의 개수와 붙여넣을 커서의 개수가 같아야함
다르다면 붙여넣을 커서 하나당 복사한 요소 전체가 한세트씩 들어가버림

ex) 복사한 요소의 개수와 붙여넣을 커서의 개수가 같을때
a				z
s		→		x
d				c
asd를 zxc에 붙이기 - 이건 가능(a,b,c가 한줄씩 각각 들어가짐)

ex) 복사한 요소의 개수와 붙여넣을 커서의 개수가 다를때
a				z
s		→		x
d				c
				d
asd를 zxcd에 붙이기 or zxcd를 asd에 붙이기 - 이건 안됨(asd 3줄이 z,x,c,d줄 각각에 들어가짐 or zxcd 4줄이 a,s,d줄 각각에 들어가짐)


줄이 붙어있지 않고 사이가 떨어져있는 줄들을 일괄로 붙이고 싶은데 alt+f3으로 잡을게 없을때 
ex)
d

s

a

이때는 처음부터 끝까지(빈줄들까지) 모두 드래그한다음 tab(들여쓰기) 한번 해주면 빈 줄은 들여쓰기가 안된다
이점을 이용해 들여쓰기만 다중선택하면됨

----------------------------------------------------------------------------------------------------

서브라임 팁 (emmet 설치해야 다 사용가능)


초기설정

1. https://packagecontrol.io/installation#st3 복사후 ctrl+` 눌러서 붙인후 엔터


2. 플러그인들 설치할목록

처음에 ctrl + shift + p 누르고 install package입력후 엔터.
우측 하단에 설치로딩이 끝나면 다시 ctrl shift + p 누르고 install package입력후 엔터
이후 아래 목록 설치
  ⓐ colorsublime - 이거 설치하면 다음 사이트에 있는 테마 모두 사용가능(https://colorsublime.github.io/)
	적용법 : ctrl + shift + p → colorsublime: Install Theme 선택후 엔터 후 기다리면 테마 고를수 있는 창이 뜸 → 맘에드는 테마 고르기(kane/blackrain)
  ⓑ Emmet - 축약식
  ⓒ Alignment (영역선택후 ctrl+alt+a로 자동정렬된다고함)


3. 유저세팅바꾸기

{
	"color_scheme":"Packages/Color Scheme - Default/Sunburst.tmTheme",
	"draw_white_space":"all",
	"font_size":12,
	"tab_size": 4,
	"translate_tabs_to_spaces":false,
	"word_wrap":true,
	"ignored_packages":
	[
		"Vintage"
	]
}

4. 여러 케이스 변환 플러그인 설치
https://github.com/jdavisclark/CaseConversion 에서 ZIP 다운후
서브라임 Preferences → Browse Packages... 누르면 나오는 Packages폴더 안에 폴더째로 붙여넣기 → 서브라임 재시작

이후 단축키로 Case를 일괄 변경할 수 있음 (맥 : ctrl+option+ 조합, 맥+윈도우키보드 : ctrl+win+ 조합으로 쓰기)
단축키 쓸때 한영키 주의(영어로 돼있어야함)
여러줄 동시변환은 다중커서 이용해야함 (전체드래그 하고 단축키 쓰면 한줄이됨)

To snake_case: "ctrl+alt+c", "ctrl+alt+s"
To SCREAMING_SNAKE_CASE: "ctrl+alt+c", "ctrl+alt+shift+s"
To camelCase: "ctrl+alt+c", "ctrl+alt+c"
To PascalCase: "ctrl+alt+c", "ctrl+alt+p"
To dot.case: "ctrl+alt+c", "ctrl+alt+d"
To dash-case: "ctrl+alt+c", "ctrl+alt+h"
To separate words: "ctrl+alt+c", "ctrl+alt+w"
To separate with forward slashes: "ctrl+alt+c", "ctrl+alt+/"
To separate with backslashes: "ctrl+alt+c", "ctrl+alt+b"
To toggle between snake_case, camelCase and PascalCase: "ctrl+shift+-"

----------------------------------------------------------------------------------------------------

[단축키]

(입력쪽)

ctrl + e / tab			자동완성·젠코딩
ctrl + 방향키 좌우이동		_포함 점프이동★ (shift누르고할시 키보드 드래그 가능)
alt + 방향키 좌우이동		점프 이동★ (shift누르고할시 키보드 드래그 가능)
ctrl + L				한줄선택
shift + del			한줄제거
ctrl + shift + d			한줄복제(복사X)
ctrl + shift + 방향키 상하이동	줄 옮기기
ctrl + alt + 방향키 상하이동		같은줄 다중선택
스크롤 클릭중 드래그		블록 선택
shift + 우클릭중 드래그		블록 선택
ctrl + alt + j			커서위치 쌍을 이루는 태그로 이동★ (에디트플러스의 "ctrl + [")
ctrl + shift + '			포인터가 쌍을 이루는 시작태그와 끝맺음 태그 선택★ (태그변경용)
ctrl + shift + ;			포인터가 쌍을 이루는 시작태그와 끝맺음 태그 삭제
ctrl + ,				커서위치 쌍을 이루는 시작태그와 끝맺음 태그 포함 내부선택★ 다중/연속 유용
ctrl + shift + a			다중 커서 확장, 커서위치 쌍을 이루는 시작태그와 끝맺음 태그 내부만 선택★★★ a태그안에 텍스트수정할때 유용 , 내용이없을경우안됨
ctrl + shift + , / ctrl + shift + .	커서위치 선택★ 클래스변경/선택용
ctrl + shift + [			축약 ★다중선택 유용
ctrl + shift + ]			축약풀기 ★다중선택 유용
드래그 + tab / ctrl + ]		들여쓰기 앞으로
드래그 + shift + tab / ctrl + [	들여쓰기 뒤로
ctrl + alt + a			드래그하고 쓰면 앞으로 들여쓰기 되어 다른줄이랑 맞춰짐(플러그인)
ctrl + shift + p →
ind rein: Indentation:Reindent Lines	자동 정렬
ctrl + shift + p →
Indentation:Convert to Spaces	탭을 스페이스로 변환
ctrl + shift + p →
Indentation:Convert to Tabs		스페이스를 탭으로 변환
우측 하단 Tab Size 조절		탭 크기 설정
ctrl + /				커서위치 주석 or 드래그 한거 주석
ctrl + shift + /			커서위치 태그포함 하위태그 주석
ctrl + u				커서위치 포함 되돌리기(세밀단위 실행취소)
ctrl + shift + l			드래그로 잡은 여러줄을 줄 각각의 커서로 분열★
ctrl + m				"("괄호 등 Bracket 범위 처음/끝으로 이동
ctrl + shift + m			"("괄호 등 Bracket 범위 안의 내용 선택	★
ctrl + shift + space			같은 스코프(Scope)의 내용 선택★★
ctrl + shift + j			들여쓰기 레벨이 같은 내용 선택

ctrl + d				동일문자열 추가선택★★
ctrl + f3				동일문자열 이동★		안되면 ctrl + f 누르고 쓰기
shift + f3				동일문자열 거꾸로 이동★		안되면 ctrl + f 누르고 쓰기
alt + f3				동일문자열 전체선택★
ctrl + k + u			선택영역 대문자로★★★ setter/getter dto에서 긁어서 일괄 삽입용
ctrl + k + l			선택영역 소문자로

ctrl + tab (+ shift) / 우클릭 + 휠 / ctrl + PgUpDown + 좌우키 / alt + 숫자키 / 마우스 앞뒤키 	탭이동


(증가/감소 액션)★ 다중적용 가능

ctrl + ↑				1씩 증가
ctrl + ↓				1씩 감소
alt + ↑				0.1씩 증가
alt + ↓				0.1씩 감소
shift+alt + ↑			10씩 증가
shift+alt + ↓			10씩 감소


---

잘안쓰는거

ctrl + alt + enter			html젠코딩 확장
ctrl + shift + g			html젠코딩 감싸서 확장
ctrl + shift + y			수학식을 평가
ctrl + u				이미지 너비와 높이 속성을 삽입
ctrl + shift + r			css 변경 값을 반영
ctrl + '				Encode/Decode Image to data:URL


(설정쪽)

ctrl + shift + p								Command Palette(이하 커멘드)
Package Contro커멘드 → install(Package Control: Install Package)			플러그인 설치
커멘드 → list (Package Control: List Package)					설치한 플러그인목록
커멘드 → remove (Package Control: Remove Package)				플러그인 삭제
커멘드 → settings(Package Control: Remove Package)				사용자설정
커멘드 → settings → "draw_white_space":"all"					들여쓰기,공백표식(플러그인)


기타 단축키모음 http://w3devlabs.net/wp/?tag=%EC%84%9C%EB%B8%8C%EB%9D%BC%EC%9E%84%ED%85%8D%EC%8A%A4%ED%8A%B8

----------------------------------------------------------------------------------------------------

[젠코딩]


(html)

li{$}*5

<li>1</li>
<li>2</li>
<li>3</li>
<li>4</li>
<li>5</li>


ul>li.item$$$*5

<ul>
    <li class="item001"></li>
    <li class="item002"></li>
    <li class="item003"></li>
    <li class="item004"></li>
    <li class="item005"></li>
</ul>

.ex 탭 → <div class="ex"></div>

ul>li*5>{{{BANNER:$}}} 탭
<ul>
	<li>{{BANNER:1}}</li>
	<li>{{BANNER:2}}</li>
	<li>{{BANNER:3}}</li>
	<li>{{BANNER:4}}</li>
	<li>{{BANNER:5}}</li>
</ul>

dl+ 탭
<dl>
	<dt></dt>
	<dd></dd>
</dl>

ul>li*7>a[javascript:;] 탭
<ul>
	<li><a href="javascript:;"></a></li> *7
</ul>

div>lorem20 탭 (lorem단어수/단어수생략가능)
<div>Lorem ipsum dolor sit amet consectetur adipisicing elit. Maiores delectus qui atque aut unde ut minima eaque aliquid, asperiores autem?</div>

((h1>lorem5)+p>lorem200)*10 탭
<h1>제목</h1>
<p>내용</p>	..... × 30회


자세한내용

http://makingweb.tistory.com/8
https://docs.emmet.io/cheat-sheet/


(css)

<형태>

db : displat:block
dib : display:inline-block
dn : displat:none
poa : position:absolute
por : position:relative
	
ex) wdt100 탭 → width:100px;
ex) wdt100p 탭 → width:100%;
ex) ha 탭 → height:auto;
ex) t10 탭 → top:10px;
ex) op1 탭 → opacity:1;
ex) z99 탭 → z-index:99;
ex) m- 탭 → margin:auto;
ec) brs50p 탭 → border-radius:50%;


<여백>

mg : margin:
ex) mg0-10 탭 → margin:0 10px;

mt : margin-top:
mr : margin-right:
mb : margin-bottom:
ml : margin-left:

pd : padding:
pt : padding-top:
pr : padding-right:
pb : padding-bottom:
pl : padding-left:

ex) pb110 탭 → padding-bottom:110px;
ex) m-10--15 탭 → margin:-10px -15px;

<선>

bd+ : boeder:1px solid #000;

bt : border-bottom:
br : border-right:
bb : border-bottom:
bl : border-left:

bru : border-radius:
bbb : box-sizing:border-box;

ex) bd1px-solid#000 탭 → border:1px solid #000;

<텍스트>

fo : font-size:
c : color:
ex) c#000 탭 → color:#000;
fb : font-weight:bold
lep/lsg/lgs : letter-spacing:
ex) ls-.1px 탭 → letter-spacing:-.1px;
tl : text-align:left
tc : text-align:center
tar : text-align:right
lh : line-height
ex) lh20px 탭 → line-height:20px;
fz : font-size:
ti : text-indent:


자세한내용

https://docs.emmet.io/cheat-sheet/

----------------------------------------------------------------------------------------------------

서브라임 기타팁
 
우클릭한채로 스크롤하면 탭전환가능 alt누르고 숫자도 됨 (ctrl+PgUp / ctrl+PgDn , ctrl+tab / ctrl+shift+tab)

태그클릭했을때 하위에 오류가있으면(두번닫음 등) 밑줄안쳐짐 (밑줄이 안쳐지면 잘못 된게있나 확인해보기)

css단축해서쓸때 bdn까지치고 보기뜰때 탭치지말고 방향키위아래로 border:none이나 다른걸로 조정가능하다 한번 선택해놈 저장되기때매 주의,활용

alt+f3으로 전체선택할때 축약해논거 안에 속해있을시 축약된채로 변경은 되는데 선택커서위치 이동은 안됨

-----

서브라임으로 문서 인코딩포맷 변경

ctrl + shift + p → Package Install → Package Control: Install Package → ConvertToUTF8 입력

그 다음
File → Set File Encoding to → Korean (EUC-KR) 선택

그러면 파일 인코딩이 EUC-KR → UTF-8로 바뀜

----------------------------------------------------------------------------------------------------

css애니메이션으로 체크박스 on/off스위치아이콘으로 변경

<label class="switch">
	<input type="checkbox" name="isOnline" id="isOnline" value="T"<%=isChecked(IsOnline,"T")%>  onclick="changeOnlineUse(this)" />
	<div class="slider round"></div>
</label>


label.switch{position:relative;display:inline-block;width:56px;height:24px;margin:2px 0 5px;padding:0;}
label.switch input{display:none;}
label.switch input + :after{content:"Off";font-size:14px;color:#fff;font-weight:bold;width:56px;text-align:right;display:inline-block;padding:0 11px;box-sizing:border-box;}
label.switch input + div.slider{position:absolute;cursor:pointer;top:0;left:0;right:0;bottom:0;background-color:#ccc;-webkit-transition:.4s;transition:.4s;line-height:24px;}
label.switch input + div.slider:before{position:absolute;content:"";height:16px;width:16px;left:4px;bottom:4px;background-color:white;-webkit-transition:.4s;transition:.4s;}
label.switch input:checked + .slider{background-color:#2196F3;}
label.switch input:checked + :after{content:"On";font-size:14px;color:#fff;font-weight:bold;line-height:24px;text-align:left;}
label.switch input:focus + .slider{box-shadow:0 0 1px #2196F3;}
label.switch input:checked + .slider:before{-webkit-transform:translateX(31px);-ms-transform:translateX(31px);transform:translateX(31px);}

----------------------------------------------------------------------------------------------------

function 으로 a클릭하면 b클릭되게 만들었거나 만들어져있고 b클릭되면 c실행되게 되있있는경우 ↓해석

<a href="javascript:cateClick()">img</a> 이나 <a onclick="cateClick()">img</a>클릭했을때 <a class="btn-all-menu">img</a> (= b)가 클릭
(그리고 b가 클릭이 되면

$(".btn-all-menu, .close-all-menu").click(function(){
	resetSwipe();
	$(".all_menu_box").toggleClass("open");
});

이게 실행되야댐 = c) 이럴경우 a에서 c로 바로 못가니까 b에 클래스를 아래처럼 마크업에만 넣어놓으면 온전히 실행이 가능하다.

<div class="btn-all-menu" style="display:none"></div>

----------------------------------------------------------------------------------------------------

반복적인 텍스트나 기호, 아이콘 할땐

before/after 로 할수있는지 확인

---------------------------------------------------------------------------------------------------

제이쿼리 한번만 실행
$(".cate-Depth1 li:eq(1)").one().click()

---------------------------------------------------------------------------------------------------

유튜브 동영상퍼올때 반응형으로 넓이100퍼에 높이 영상비율로 자동조절 해주는 사이트 

http://embedresponsively.com 들어가서 영상 주소창 링크 입력하면 소스나옴  
ex) https://www.youtube.com/watch?v=VQtonf1fv_s 입력 

게시판같은곳이라 스타일 자동지워지면 인라인으로 변경

---------------------------------------------------------------------------------------------------

select 태그 기본 선택 option에 selected="true" 넣기

---------------------------------------------------------------------------------------------------

asp에서 elesif 쓸때 붙여써야댐

<%if boardID="article" then%>
	<h1>홍보기사</h1>
<%elseif boardID="news_product_event" then%>
	<h1>상품평이벤트</h1>
<%elseif boardID="eventnews" then%>
	<h1>이벤트/뉴스</h1>
<%else%>
	<h1>게시판</h1>
<%end if%>

파라미터 불러오는 getRequest 객체 필요

---------------------------------------------------------------------------------------------------

제이쿼리 문서객체탐색

eq(), first(), laster(), add(), find()

제이쿼리 first,last 는css랑 다름

---------------------------------------------------------------------------------------------------

소스 안 해치고 페이지 테스트

mainPagePath 불러오는곳 밑에 그리고 Server.Execute(mainPagePath) 위에다가

둘 사이에
<%
	println mainPagePath
	Response.end
%>

이거 넣으면

페이지 실제 경로(?)가 나옴

println쓰는법
println "표시할 내용"
println 변수
Response.end는 프로그램 종료 구문

if등 있으면 <% %> 떼고 안에다 넣어도 됨

---------------------------------------------------------------------------------------------------

메일폼(메일보내는거) 인라인스타일에 position:absolute 넣으면 스타일 사라짐

---------------------------------------------------------------------------------------------------

한 함수 안에서 this 하면 다 처음걸로 인식되는듯

$(".prod_slide_wrap .swiper-slide").each(function(){
	var chd = $(this).children(".goods").children(".img").children("a").children("img")
	console.log(chd)
	var wdt = chd.width()
	var hgt = chd.height()
	console.log(wdt)
	console.log(hgt)
	wdt = $(this).height() ← 여기서 this 는 $(".prod_slide_wrap .swiper-slide")	
	$(this).children().height(1000)
	$(this).height(wdt)  ← 여기도 this 는 $(".prod_slide_wrap .swiper-slide")	
})

---------------------------------------------------------------------------------------------------

여러파일에 동시적용된거 한번에삭제할땐 공통css로

---------------------------------------------------------------------------------------------------

개발자도구 인라인스타일에 적혀있는거 값이안바뀌거나 밑에 똑같이 적었을때 바로 사라지면
스크립트로 넣은것임

---------------------------------------------------------------------------------------------------

자체압축(축약)된 ~min.~ 파일 풀어주는곳

https://tools.arantius.com/tabifier
Options 에서 파일형식 선택후 실행

---------------------------------------------------------------------------------------------------

부트스트랩등 api/플러그인 겹치는거방지

css/js 넣을때 맨 위에다 넣기,, (common위에)
넣은후 box-sizing:border-box등 점검要

---------------------------------------------------------------------------------------------------

스윗알럿 플러그인
https://sweetalert.js.org/

---------------------------------------------------------------------------------------------------

제이쿼리 모음
https://hyeonseok.com/soojung/contents/upload/jQueryBasicAPIs.pdf 

---------------------------------------------------------------------------------------------------

gnb등 에서 중간에 높이가 작은 선 끼워넣을땐 :before/:after 사용 후 vertical-align:middle
세로형 리스트에서 중간에 넓이가 작은 선 끼워넣을땐 :before/:after 사용 후 display:block;margin:auto넓이조절

---------------------------------------------------------------------------------------------------

index function으로 쓰기(1~20순위*많을때 사용)

<div class="swiper-container rankSl">
	<div class="swiper-wrapper">
		<ul class="swiper-slide rank">
			<li><a href="javascript:;"><span></span>가을롱원피스</a></li>
			<li><a href="javascript:;"><span></span>모이몰론</a></li>
		</ul>
		<ul class="swiper-slide rank">
			<li><a href="javascript:;"><span></span>가을롱원피스2</a></li>
			<li><a href="javascript:;"><span></span>모이몰론2</a></li>
		</ul>
	</div>
</div>
<script>
	$(".rankSl li").each(function(rnk){
		$(this).find("span").text(rnk+1)
	})
</script>

++

http://mylife365.tistory.com/221

---------------------------------------------------------------------------------------------------

회원가입 등페이지 튕기는거

If agreechk<>"T" Then
	response.redirect pathMobile &"/member/regist_agree.asp"
	'Call jsmsgLink("잘못된 접근입니다.", siteURL &"/member/regist_agree.asp", "")
End If

없으면 튕긴페이지 url검색

---------------------------------------------------------------------------------------------------

<input type="tel"> 로 하면 모바일에서 숫자 자판만나옴

---------------------------------------------------------------------------------------------------

원인모르겟는 상하공백은 vertical-align:top 해보기

---------------------------------------------------------------------------------------------------

메일폼페이지는 네이버등에서 내부스타일·스크립트지원을 안하기때매 스크립트는못쓰고 스타일은 인라인으로 써야댐


페이지에서 내부스타일안되면 아래html기본서식 풀로 넣기

<!DOCTYPE html>
<html>
<head>
<style>
p{color:red;}
</style>
</head>
<body>
<p>qweqwe</p>
</body>
</html>


페이지관리에있는 그냥 page
이용약관 등 상점운영정책 page
게시판통합관리 page
기획전 page
팝업 창

모바일 기본 페이지는 내부스타일이 아예 안되는듯 (내용이pc와 동일한경우 새로추가안하고 pc url그대로 쓰는거 좋음)

관리자에서 생성/수정하는 페이지들은 <script></script> 미지원 (a href="javascript:;" 도 사라지니 그냥#으로쓰기)

---------------------------------------------------------------------------------------------------

복잡한 표 , 이미지 세로정렬할때는 테이블방식도 좋음

---------------------------------------------------------------------------------------------------

<슬라이드>

페이지네이션 치환해서 글자로 만드는거랑
숫자 페이지네이션 페이지내에서 같이쓸 때
 
<script type="text/javascript" src="/jscript/swiper.min.js"></script>
이걸 글자치환페이지네이션슬라이드 밑에 숫자페이지네이션슬라이드 위에 넣어야됨
맨 위에 넣음 글자치환페이지네이션슬라이드에 글자치환페이지네이션이 안나옴
(이거 쓰면 아래부터 다적용되서 그 밑에 글자치환페이지네이션슬라이드 못쓰는것같음) 
 
<link rel="stylesheet" type="text/css" href="/css/swiper.min.css" /> 
이거는 모바일에서 쓰는모양이고 pc에서는 높이고정시키면됨
※pc에서 쓸경우 높이는 자동으로되지만 넓이가 이상해짐 (단 위에 스크립트처럼 pc에서 버전3 내용을 쓸때에는 그부분에만 어떻게 잘 넣어줘야 함 <script type~> 는 절차지향인반면 css는 저거 넣으면 페이지전체에 swiper.css적용되는거라서 어느위치에넣든 상관없이 다적용됨)


페이지네이션 안될경우

paginationClickable:true, 있나 보고 없거나 false로 되있음 바꾸기 (기본값 false로 되있을수있음)
 
---------------------------------------------------------------------------------------------------
 
스크립트 시작할때 하위브라우저와 호환성등 생각하려면 <script type="text/javascript" language="javascript"> 이렇게 써야하지만 
 
html 5 부터는 디폴트로 script 는 js로 쓰기때문에 <script> 로만 사용하셔도 무방합니다. 아니라면 <script type="text/javascript"> 이렇게 써주시는게 맞겠죠. style 태그의 경우에도 type="text/css" 이렇게 명시해줘야 합니다만 html 5 부터는 디폴트로 <style> 을 적으면 css를 의미하죠.
 
현재 표준은 <script type="text/javascript"> 라고 만든 개발자가 이야기 했어요
 
--------------------------------------------------------------------------------------------------- 
 
<script></script>는 html구조에 종속되서
 
<div class="a1">
<div class="b1">
</div>
<div class="b1">
</div>
</div>
이렇게 있을때 일부영역에만 스크립트를 넣고싶으면
 
<div class="a1">
<div class="b1">
</div>
<div class="b1">
</div>
<script>
</script>
</div>
이렇게 넣으면 a1내에서만 스크립트가 적용됨
 
이를활용해 일부영역 내에서 각각의 클래스에 적용되는 스크립트를 만들 수 있다
 
---------------------------------------------------------------------------------------------------
 
메인과 서브 스타일을 분리할때
 
예) 관리자에서 서브상단등 모든페이지에 적용되는 스타일에다가는 body에 넣지말고
메인에만 적용할건 메인에서만쓰는 영역에다 넣거나 메인스타일용 영역을 새로만들기
 
---------------------------------------------------------------------------------------------------
 
서브 페이지들과 메인 보통width 가 크게 차이나거나 이상한지 확인
 
예) 메인은 1300인데 서브는 1200일경우 이상하므로 헤더푸터만 해놓고 서브들어가서 한번물보기
 
--------------------------------------------------------------------------------------------------- 
 
슬라이드배너 등 관리자에서 등록하는걸경우 다한담에 개발자도구에서<a></a> 한번너보기
 
---------------------------------------------------------------------------------------------------

인라인적 스타일은 내부까지 적용(상속)됨

예) font-size , text-indent , line-height 등
때문에 ul li 안에 다른스타일로 ul li 을 하고싶으면 안쪽에서 빼야함

---------------------------------------------------------------------------------------------------

1단의 제목 내용 색이 다른 ul li ul li 와 같은 가로형 표 레이아웃(1단 : 세로로긴 가로2행 세로 n열 / 2단 : 표)
table로 안하고 세로가운데 정렬하기

테이블 처럼 2단 크기에맞춰 늘어나게하며
세로가운데정렬 까지 하려면
1단 ul background
1단 li vertical-align:middle
2단이 있는 1단 li에 세로padding
2단 ul width로 축소 후 퍼센트 li 위해 font-size:0 을 재적용

---------------------------------------------------------------------------------------------------

content:"" 안에서 줄바꿈 <br>이나 /n 이 아니라 \A 사용
:before{content:"업계 최저\a수수료!!";white-space:pre;}

---------------------------------------------------------------------------------------------------

content:"" before/after 로 선넣을때 inline-block했는데 여백생기면 block로하기
상하간격조정은 padding-top:5px;margin-bottom:-5px; 활용

---------------------------------------------------------------------------------------------------

가로 리스트 많을때/퍼센트애매할때 리스트들 각각 table-cell 하고

부모 display:table 하고 100% 한다음 상황에 따라 table-layout:fixed 넣음 내용개수 바껴도 ok

---------------------------------------------------------------------------------------------------

문서 내 요소위치

.offset()
.offset().top // 위쪽(수직)
.offset().left // 왼쪽(수평)


position도 offset과 거의동일

요소가 아닌 현재 스크롤의 위치를 알고싶으면 $(document).scrollTop()


2단메뉴가 길면 부모에 걸린 relative 풀고 자식에 bottom 0 적용(http://hipslips.com)
<script>
	$(".menu3>li").mouseenter(function(){
		console.log($(this).find(".menu4").offset().top)
		console.log($(this).find(".menu4").height())
		console.log($(this).find(".menu4").offset().top+$(this).find(".menu4").height())
		console.log($(".menu3").height())
		if($(".menu3").height()<$(this).find(".menu4").offset().top-$(".utilWrap").height()-$(".logoSearchWrap").height()-$(".gnbWrap").height()+$(this).find(".menu4").height()){
			console.log("tttttttttttttttttttttttt")
			$(this).css("position","static")
			$(this).find(".menu4").css({"top":"auto","bottom":0})
		}
	})
</script>

------------------------------

상대 위치

.position()
.position().top // 위쪽(수직)
.position().left // 왼쪽(수평)

---------------------------------------------------------------------------------------------------

리스트 벽돌쌓기정렬 플러그인 → masonry

<script type="text/javascript">
var $cont_list = $('.cont_list').masonry({
  itemSelector: 'li',
});


cont_list 에 ul 넣기

↓↓↓↓↓↓ 안되면 추가

$cont_list.imagesLoaded( function() {
	$cont_list.masonry('layout');
})
</script>

---------------------------------------------------------------------------------------------------

each closest 활용

<script>
	$(".order_totalBox .product_box_01").each(function(){
		var ivclyr = $(this).closest(".product_box_01").find(".invoiceChgLayerWrap")
		$(this).find(".product_box_BTN").click(function(){
			ivclyr.toggle()
		})
		$(".product_box_BTN2.refund").click(function(){
			$(this).closest(".invoiceChgLayerWrap").toggle()
		})
		$(".invoiceChgLayerBg").click(function(){
			$(this).parent().toggle()
		})
	})
</script>

---------------------------------------------------------------------------------------------------

이미지맵 폼

<img class="wyditor_img" src="/data/hanguoshopping/editor/201710/m%5Feventmall%5Fcj.jpg" style="width:100%" usemap="#link">
<map name="link">
	<area shape="rect" coords="445,1053,758,1138" href="/eventmall.asp?uid=279" target="blank">
	<area shape="rect" coords="140,1497,1052,1798" href="/goods/content.asp?guid=31544" target="blank">
</map>

파폭 개발자도구에서 영역 확인 & 조정

pc와 모바일 같이쓰긴 힘드나 굳이 같이쓰려면
1) 이미지를 position relative인 div 등으로 감싸주신 후 각각의 area를 a태그로 변경시킨 후 position absolute 및 top, left값으로 영역을  %로 잡아주시는 방법
2) css transform의 scale을 이용해 축소하는 방법,
3) 그리고 js를 이용해 이미지의 비율만큼 area의 coord 값을 재계산하여 부여하는 방법 
등이 있다 링크참조
http://goldxxx.blog.me/220761803008 

---------------------------------------------------------------------------------------------------

pc/m , 본사/파트너 등 어디에 페이지/스타일 만들면 연동되어있어 다른데서 같이만들어지거나 수정되거나 지워질 수 있음

---------------------------------------------------------------------------------------------------

파트너에서만 본사와 별개로 상품등록/스타일변경 안되서 본사에서 스타일,영역 등록한다음 본사랑 다른파트너들을 숨김해야됨
배너이미지도 본사에서 관리

---------------------------------------------------------------------------------------------------

js string langth 글자수/byte로 자르기
http://blog.naver.com/ijoos/221003407739

---------------------------------------------------------------------------------------------------

toggle / toggleClass
클래스나 id가 두개이상 겹칠경우 나왔다가 사라짐 개발자도구로보면 깜빡이는것처럼 보임

그럴땐 show , hide / add , remove 로 나누기

---------------------------------------------------------------------------------------------------

max-width:unset 할때 unset은 익스에서 안되니

오토로하거나 다른걸로 쓸수 있는건 다른걸로 쓰기 ex)max-width:none

---------------------------------------------------------------------------------------------------

검색이 안되면 이미지

---------------------------------------------------------------------------------------------------

운영관리 → 게시판통합관리 안에 있는 페이지

board/list.asp
board/content.asp
board/write.asp

---------------------------------------------------------------------------------------------------

datepick (달력)

<1개(단일)>
<input type="hidden" id="sHidden" />
<input type="text" id="deliverDate" name="deliverDate" value="<%=deliverDate%>" class="box" style="width:120px"  maxlength="10" readonly>
<img src='<%=adminImgURL2%>/button/btn_open.gif' alt='달력' id="sDateImg" style="cursor:pointer">


<link rel="stylesheet" href="//code.jquery.com/ui/1.12.1/themes/base/jquery-ui.css">
<link rel="stylesheet" type="text/css" href="../css/datepicker.css" />
<script src="https://code.jquery.com/jquery-1.12.4.js"></script>
<script src="https://code.jquery.com/ui/1.12.1/jquery-ui.js"></script>
<script>
	// 달력 클릭 시에만, 달력 표시되게.
	$(function () {
		$("#dDateImg").on('click', function () {
			$("#dHidden").datepicker({
				constrainInput: false,
				dayNamesMin: ['일', '월', '화', '수', '목', '금', '토'],
				monthNames: ['. 01', '. 02', '. 03', '. 04', '. 05', '. 06', '. 07', '. 08', '. 09', '. 10', '. 11', '. 12'],
				changeMonth: false, //월변경가능
				changeYear: false, //년변경가능
				showMonthAfterYear: true, //년 뒤에 월 표시
				dateFormat: "yy-mm-dd",
				showOtherMonths: "true"
			});
			$("#dHidden").datepicker("show");
		});

		$("#cDateImg").on('click', function () {
			$("#cHidden").datepicker({
				constrainInput: false,
				dayNamesMin: ['일', '월', '화', '수', '목', '금', '토'],
				monthNames: ['. 01', '. 02', '. 03', '. 04', '. 05', '. 06', '. 07', '. 08', '. 09', '. 10', '. 11', '. 12'],
				changeMonth: false, //월변경가능
				changeYear: false, //년변경가능
				showMonthAfterYear: true, //년 뒤에 월 표시
				dateFormat: "yy-mm-dd",
				showOtherMonths: "true"
			});
			$("#cHidden").datepicker("show");
		});

		$("#dHidden").on('change', function () {
			$('#depositConfirmDate').val($("#dHidden").val());
		}); //값 변경되면 찍은 날짜 텍스트로 보이게
		$("#cHidden").on('change', function () {
			$('#completionConfirmDate').val($("#cHidden").val());
		}); //값 변경되면 찍은 날짜 텍스트로 보이게
	});
</script>


<2개(~부터~까지)>
<table cellpadding="0" cellspacing="0" border="0" class="border_none">
<tr>
	<td style="border:none; width:90px; padding:0;">
		<span class="input_wrap">
			<input type="hidden" id="sHidden" />
			<input type="text" id="sdts" name="sdts" value="<%=sdts%>" class="box border_input"  maxlength="10">
			<img src='<%=adminImgURL2%>/button/btn_open.gif' alt='달력' id="sDateImg" style="cursor:pointer">
		</span>
	</td>
	<td style="border:none; text-align:center; padding:0;" width="30" align="center">~</td>
	<td style="border:none; width:90px; padding:0;">
		<span class="input_wrap">
			<input type="hidden" id="eHidden" />
			<input type="text" id="sdte" name="sdte" value="<%=sdte%>" class="box border_input"  maxlength="10">
			<img src='<%=adminImgURL2%>/button/btn_open.gif' alt='달력' id="eDateImg" style="cursor:pointer">
		</span>
	</td>
	<td style="border:none; padding:10px;">직접 입력시에는 “2007-01-01” 형식으로 입력해주세요.</td>
</tr>
<tr>
	<td style="border:none; padding:10px 0;" colspan="5">
		<span onClick="inputDate('sdts', 'sdte', 'W', 0)" class="date_span">전체</span>
		<span onClick="inputDate('sdts', 'sdte', 'T', 0)" class="date_span">오늘</span>
		<span onClick="inputDate('sdts', 'sdte', 'T', 1)" class="date_span">어제</span>
		<span onClick="inputDate('sdts', 'sdte', 'D', 3)" class="date_span">3일간</span>
		<span onClick="inputDate('sdts', 'sdte', 'D', 7)" class="date_span">7일간</span>
		<span onClick="inputDate('sdts', 'sdte', 'D', 10)" class="date_span">10일간</span>
		<span onClick="inputDate('sdts', 'sdte', 'D', 20)" class="date_span">20일간</span>
		<span onClick="inputDate('sdts', 'sdte', 'D', 30)" class="date_span">30일간</span>
	</td>
</tr>
</table>


<link rel="stylesheet" href="//code.jquery.com/ui/1.12.1/themes/base/jquery-ui.css">
<link rel="stylesheet" type="text/css" href="../css/datepicker.css" />
<script type="text/javascript" src="/jscript/date.js"></script> <!-- 구간지정버튼 -->
<script src="https://code.jquery.com/jquery-1.12.4.js"></script>
<script src="https://code.jquery.com/ui/1.12.1/jquery-ui.js"></script>
<script>
	// 달력 클릭 시에만, 달력 표시되게.
	$(function(){
		//var rangeDate = 30; //오늘날짜 이전 선택못하게
		$("#sDateImg").on('click',function(){
			$("#sHidden").datepicker({
				constrainInput: false,
				dayNamesMin: ['일', '월', '화', '수', '목', '금', '토'],
				monthNames: ['. 01', '. 02', '. 03', '. 04', '. 05', '. 06', '. 07', '. 08', '. 09', '. 10', '. 11', '. 12'],
				changeMonth: false, //월변경가능
				changeYear: false, //년변경가능
				showMonthAfterYear: true, //년 뒤에 월 표시
				dateFormat: "yy-mm-dd",
				showOtherMonths: "true",
				/*minDate : 0,
				onSelect: function(selectDate){
					var stxt = selectDate.split("-");
						stxt[1] = stxt[1] - 1;
					var sdate = new Date(stxt[0], stxt[1], stxt[2]);
					var edate = new Date(stxt[0], stxt[1], stxt[2]);
						edate.setDate(sdate.getDate() + rangeDate);

					$('#deliverDate').val($("#sHidden").val()); //찍은 날짜 텍스트로 보이게 여기 쓰면 onchange에 안써도됨

					$('#sHidden').datepicker('option',{
						minDate: selectDate,
						beforeShow : function(){
							$("#sHidden").datepicker( "option", "maxDate", edate );
						}
					});
				}*/ //오늘날짜 이전 선택못하게
			});
			$("#sHidden").datepicker("show");
		});
		$("#eDateImg").on('click',function(){
			$("#eHidden").datepicker({
				constrainInput: false,
				dayNamesMin: ['일', '월', '화', '수', '목', '금', '토'],
				monthNames: ['. 01', '. 02', '. 03', '. 04', '. 05', '. 06', '. 07', '. 08', '. 09', '. 10', '. 11', '. 12'],
				changeMonth: false, //월변경가능
				changeYear: false, //년변경가능
				showMonthAfterYear: true, //년 뒤에 월 표시
				dateFormat: "yy-mm-dd",
				showOtherMonths: "true",
			});
			$("#eHidden").datepicker("show");
		});

		$("#sHidden").on('change',function(){
			$('#sdts').val($("#sHidden").val());
		}); //값 변경되면 찍은 날짜 텍스트로 보이게
		$("#eHidden").on('change',function(){
			$('#sdte').val($("#eHidden").val());
		}); //값 변경되면 찍은 날짜 텍스트로 보이게

		$(".date_span").click(function(){
			$('.date_span').removeClass('on');
			$(this).addClass('on');
		}); //구간지정버튼
	});
</script>


id , name , value 등 바꾸기 스크립트쪽도
2개일땐 sdts sdte input width:90px로 바꾸기
파일 맨 밑에다 쓰기

하다가 달력뜨는 위치를 바꾸고싶으면 input-text 에 absolute left top으로 위치 조절하고 visibility:hidden 으로 숨기기

---------------------------------------------------------------------------------------------------

daum 주소찾기

<script src="http://dmaps.daum.net/map_js_init/postcode.v2.js"></script>
<script>
checkCmsType();
checkDelivery();	// 배송관련 추가
addEvent(window, "load", checkDeliveryLimit);


	// 다음지도 api
	function openNewAddr(mode){				//ord, rcv.
		var f = document.Frm;
		set_zipcode(mode);
	}
	function set_zipcode(mode){			//ord, rcv
		/////R(도로명), J(지번)
		////K(한글주소), E(영문주소)
		var width = 500; //팝업의 너비
		var height = 600; //팝업의 높이
		new daum.Postcode({
			oncomplete: function(data) {
				var e_address1=data.roadAddressEnglish;	///////영문도로명주소
				var e_address2=data.jibunAddressEnglish;	/////// 영문지번주소
				var address1=data.roadAddress;	////////한글도로명주소
				var address2=data.jibunAddress;	////////// 한글지번주소
				var code=data.zonecode;  //////////우편번호

				var SelectedType=data.userSelectedType;
				var LanguageType=data.userLanguageType;


					if (SelectedType=='J')	{/////////////지번
							$("#"+mode+"addr").val(address2);
							//$("#"+mode+"Addr_en").val(e_address2);
							$("#"+mode+"addrDetail").val('');
							//$("#"+mode+"AddrDetail_en").val('');
							$("#"+mode+"addrDetail").focus();
					}
					if (SelectedType=='R')	{/////////////도로명
						$("#"+mode+"addr").val(address1);
						//$("#"+mode+"Addr_en").val(e_address1);
						$("#"+mode+"addrDetail").val('');
						//$("#"+mode+"AddrDetail_en").val('');
					}

				$("#"+mode+"post").val(code);
			}
		}).open({
			left: (window.screen.width / 2) - (width / 2),
		    top: (window.screen.height / 2) - (height / 2)
		});
	}
	function checkDelivery() {
	var f = document.Frm;
	var isFree;

	if (getRadioVal(f.deliveryMethod) == "<%=CM_DELIVERY_PREPAY%>") {
		isFree = false;
	}
	else if (getRadioVal(f.deliveryMethod) == "<%=CM_DELIVERY_COLLECT%>") {
		isFree = false;
	}
	else {
		isFree = true;
		setRadioVal(f.deliveryMethod, "<%=CM_DELIVERY_FREE%>");
	}

	if (isFree) {
		document.getElementById("tbDeliveryPay").style.display = "none";
		document.getElementById("tbDeliveryFree").style.display = "";
	}
	else {
		document.getElementById("tbDeliveryFree").style.display = "none";
		document.getElementById("tbDeliveryPay").style.display = "";
	}
}
</script>

<div>
	<input type="text" name="post" id="post" class="box" style="width:70px;" value="<%=encQuote(post)%>" maxlength="7">
	<span class="btnxs btn02 valignMid" onClick="openNewAddr('')">우편번호검색</span>
	<font color="#999999">(예: 423-030)</font>
</div>
<div style="margin-top:5px;"><input type="text" name="addr" id="addr" class="box" style="width:450px;" value="<%=encQuote(addr)%>" maxlength="50"></div>
<div style="margin-top:5px;"><input type="text" name="addrDetail" class="box" style="width:450px;" value="<%=encQuote(addrDetail)%>" maxlength="50">&nbsp;<font color="#999999">(나머지 주소)</font></div>

---------------------------------------------------------------------------------------------------

관리자 왼쪽메뉴 현재페이지 표식

<script  type="text/javascript">
setleftmenu_on("4-31");
</script>

---------------------------------------------------------------------------------------------------

<script>안에 불러오는 스크립트</script> 맞게썻는데 안되면

맨 밑에다 쓰기

---------------------------------------------------------------------------------------------------

익스는 크롬이랑 달라 박스에 꽉 차게 퍼센트 말고 수동으로 조절 하면
1~2px 차이로 크롬은 박스안에들어가고 익스는 박스밖으로 삐져 나갈 수 있음

---------------------------------------------------------------------------------------------------

스크롤을 없애(숨기)려면

감싸는박스, 없으면 하나 만들어서 밖에거에 overflow:hidden 넣고
안에꺼에 overflow-y:scroll 해서 무조건 스크롤을 만든다음
넓이를 17픽셀 늘리든가 margin-right:-17px 해서 숨김댐


더 좋은 방법

스크롤컨테이너::-webkit-scrollbar{
	display: none;
	width: 0;  /* Remove scrollbar space */
	height: 0;
	background: transparent;  /* Optional: just make scrollbar invisible */
	-webkit-appearance: none;
}

---------------------------------------------------------------------------------------------------

동적으로 추가된 요소에 클릭 이벤트를 적용시킬때

$("#btn").on("click", function(){

})

이것은 단순히 btn이란 아이디를 가진 태그에게 click 이벤트를 주는 것과 같다면

 

$("#table").on("click", "#btn", function(){

})

이것은 table이라는 아이디를 가진 태그 범위안에 존재하는 btn이란 태그를 클릭했을 때 click 이벤트를 주는 것이다.


첫번째 방식은 live 성격이 포함되어 있지 않고, 두번째방식은 live 성격이 포함 되어 있다.

동적으로 html 태그를 생성하고 그 안에서 이벤트를 부여하고 싶으면 두번째 방식으로 접근해야한다.

↓↓↓

예를 들어서

$('li .pdBtnMore').click(function(){

})

이렇게 안하고

$(document).on('click', '.aa', function(){

})

이렇게 document 에 먹여주면 새로 생성되는것도 클릭 이벤트가 먹힌다
ex) 스크롤 내렸을때 내용 추가되는것 등

참고 : http://mylife365.tistory.com/167

------------------------------

html 요소가 추가된 시점에 클릭 이벤트리스너를 등록해도 됨

function addHtml(){
	.
	.
	html요소를 추가하는 코드
	.
	.
	$('#specialBox .menu .swiper-slide').on('click', function(){
		console.log($(this))
	});
}

------------------------------

html을 추가하는 스크립트에서 요소에 onclick 속성으로 함수를 넣어도 되지만, 이경우 this가 window객체로 반환됨

---------------------------------------------------------------------------------------------------

display:inline-blcok 속성은 디스플레이가 작아 인라인속성인 글자가 짤릴때 통째로 다음줄로 넘어가게(내려가게,떨어지게) 함

---------------------------------------------------------------------------------------------------

'다른아이디로 로그인' 이런거 복사 할때,, 기능작동되게하려면(콘솔에러)

<script type="text/javascript" src="/OAuth/oauth.js"></script>

<input type="hidden" id="token" name="token" value="<%=createCSRPToken()%>">
<input type="hidden" id="redirect" name="redirect" value="<%=redirect%>">
<input type="hidden" id="mainURL" name="mainURL" value="<%=mainURL%>">
<input type="hidden" id="pwd" name="pwd">

이것도 같이 가져가야됨

뭘 가져가야할지 모르겠다면 개발자도구 sources탭에서 id등 검색해논다음 폴더하나하나 파일 하나하나 클릭해서 찾아보기

---------------------------------------------------------------------------------------------------

안보였다 보이는경우 ex)탭메뉴,레이어팝업등 에서 높이 등 구하는 스크립트 사용시 (hasClass도 마찬가지)

계산될영역이 '나타나는 타이밍(display:block등) 이나 체크되는 타이밍 이후' 에다가 넣어야 읽힘 그전에넣으면씹힘


ex) 레이어팝업 높이 중앙정렬

$(".layerLink li").click(function(){
	$(".layerAll").addClass("on")
	var idx=$(this).index()
	var idxx=$(".layerCon li:eq("+idx+")")
	$(".layerCon li").removeClass("on");
	$(".layerCon").addClass("on")
	idxx.addClass("on");

	var lh=idxx.height()/2		//이부분
	console.log(lh)			//이부분
	idxx.css("margin-top",-lh)	//이부분

	$(".gnb_menu,.swiper-pagination.high,.swiper-button-next.high,.swiper-button-prev.high").css("z-index",0)
})
$(".layerBg").click(function(){
	$(".layerAll").removeClass("on")
	$(".layerCon").removeClass("on")
	$(".gnb_menu,.swiper-pagination.high,.swiper-button-next.high,.swiper-button-prev.high").css("z-index",1000)
})

이렇게 같이 넣기

---------------------------------------------------------------------------------------------------

화면에 따라 종횡비가 맞춰지는 layer.js [html/css/jquery]

-css-

pc)
/* 레이어 */
.layerFix{display:none;font-size:0;}
.layerFix.on{display:block !important;}
.layerFix .layerBg{position:fixed;width:100%;height:100%;background:rgba(0,0,0,.7);left:0;top:0;width:100%;height:100%;z-index:9998;}
.layerFix .layerCon{position:fixed;z-index:9999;background:#fff;font-size:initial;overflow:auto;padding:15px;box-sizing:border-box}
.layerFix .btn.closeLayerFix{display:inline-block;width:53px;height:53px;font-size:0;background:url("./xxx2.png")no-repeat center / 40% 40%;position:absolute;right:0;top:0;cursor:pointer;text-align:right;}
.layerFix .btn.closeLayerFix i{font-size:40px;line-height:53px;width:53px;text-align:center;}

.layerFix .secTop{position:absolute;height:53px;left:0;top:0;width:100%;z-index:99;}
.layerFix .secTop .tit{font-size:20px;text-align:center;line-height:53px;font-weight:bold;box-shadow:0 0 8px #666;}
.layerFix .secMid{font-size:14px;overflow-y:auto;}
.layerFix .secBot{position:fixed;left:0;bottom:0;width:100%;height:53px;}
.layerFix .secBot .btnCp{display:inline-block;width:100%;font-size:18px;color:#fff;text-align:center;line-height:53px;}

.layerTab{display:none;}
.layerTab.on{display:block;}
.layerTab .layerBg{position:fixed;width:100%;height:100%;background:rgba(0,0,0,.7);left:0;top:0;width:100%;height:100%;z-index:9998;}
.layerTab li{display:none;position:fixed;z-index:9999;top:50%;left:50%;background:#fff;overflow-y:auto;}
.layerTab li.on{display:block;}
.layerTab .btnCloseLayerFix{display:inline-block;width:53px;height:53px;font-size:0;background:url("./xxx2.png")no-repeat center / 40% 40%;position:absolute;right:0;top:0;cursor:pointer;}
.layerTab .btnCloseLayerFix i{font-size:40px;line-height:53px;width:53px;text-align:center;}

m)
/* 레이어 */
@keyframes slideupt{
	0% {top:1000px}
	100% {top:0;}
}
@keyframes slideupb{
	0% {bottom:-1000px}
	100% {bottom:0;}
}
.layerFix{display:none;font-size:0;}
.layerFix.on{display:block !important;}
.layerFix.on .layerCon{animation:slideupt .5s linear;}
.layerFix .layerBg{position:fixed;width:100%;max-width:568px;height:100%;background:rgba(0,0,0,.7);left:0;top:0;width:100%;height:100%;z-index:9998;}
.layerFix .layerConWrap{position:fixed;z-index:99999;max-width:568px;top:50%;padding:0;left:50%;background:#fff;box-sizing:border-box;font-size:initial;overflow-y:auto;}
.layerFix .btnClLyr{display:inline-block;width:53px;height:53px;font-size:0;background:url(/m/images/xxx2.png)no-repeat center / 40% 40%;position:absolute;right:0;top:0;cursor:pointer;}

.layerFix .secTop{position:absolute;height:53px;position:absolute;left:0;top:0;width:100%;z-index:99;}
.layerFix .secTop .tit{font-size:20px;text-align:center;line-height:53px;font-weight:bold;box-shadow:0 0 8px #666;}
.layerFix .secMid{font-size:14px;overflow-y:auto;}
.layerFix .secBot{position:absolute;left:0;bottom:0;width:100%;height:53px;z-index:999;animation:slideupb .5s ease-in-out;}
.layerFix .secBot .btnClLyr{background:none;}
.layerFix .secBot .btnCp{display:inline-block;width:100%;font-size:18px;color:#fff;text-align:center;line-height:53px;}

.layerTab{display:none;}
.layerTab.on{display:block;}
.layerTab .layerBg{position:fixed;width:100%;max-width:568px;height:100%;background:rgba(0,0,0,.7);left:0;top:0;width:100%;height:100%;z-index:9998;}
.layerTab li{display:none;max-width:568px;position:fixed;z-index:9999;top:50%;left:50%;background:#fff;overflow-y:auto;}
.layerTab li.on{display:block;}
.layerTab .btnClLyr{display:inline-block;width:53px;height:53px;font-size:0;background:url(/m/images/xxx2.png)no-repeat center / 40% 40%;position:absolute;right:0;top:0;cursor:pointer;}
.layerTab .btnClLyr i{font-size:40px;line-height:53px;width:53px;text-align:center;}

@media (min-width:568px){
	.limWdt{width:568px !important;left:calc(50% - 284px) !important;}
	.layerFix .layerBg,
	.layerTab .layerBg,
	.layerFix .layerConWrap,
	.layerTab>ul>li{left:calc(50% - 284px) !important;margin-left:0 !important;}

	.shareLayer{padding:0 2% 2.5rem;}
	.float_btn_wrap{right:50% !important;margin-right:-270px;}
}


/*상하단메뉴추가*/
.layerFix .secTop{position:absolute;height:53px;position:absolute;left:0;top:0;width:100%;z-index:99;}
.layerFix .secTop .layerClBtn{display:inline-block;width:53px;height:53px;text-indent:-9999px;font-size:0;background:url(/m/images/xxx2.png)no-repeat center / 40% 40%;position:absolute;left:0;top:0;}
.layerFix .secTop .tit{font-size:20px;text-align:center;line-height:53px;font-weight:bold;box-shadow:0 0 8px #666;}
.layerFix .secMid{font-size:14px;overflow-y:auto;}
.layerFix .secBot{position:fixed;left:0;bottom:0;width:100%;height:53px;}
.layerFix .secBot .btnCp{display:inline-block;width:100%;font-size:18px;color:#fff;text-align:center;line-height:53px;}

/*특정내용추가*/
.layerFix.L-filter .layerCon{width:100% !important;left:0 !important;top:0 !important;margin-top:0 !important;}
.layerFix.L-filter .secMid ul{margin:0;}
.layerFix.L-filter .secMid ul li .tit{background:#e7e7e7;line-height:35px;padding:0 15px;}
.layerFix.L-filter .secMid ul li .con{background:#fff;padding:10px 15px;font-size:0;}
.layerFix.L-filter .secMid ul li .con .ui-checkbox,.layerFix.L-filter .secMid ul li .con .ui-radio,.layerFix.L-filter .secMid ul li .con label{display:inline-block;}
.layerFix.L-filter .secMid ul li .con .ui-checkbox-on{border-color:red;}
.layerFix.L-filter .secMid ul li .con .ui-radio-on{border-color:blue;}
.layerFix.L-filter .secMid ul li .con label{padding:3px 5px;margin:2px;font-size:12px;border:1px solid #ddd;border-radius:3px;}
.layerFix.L-filter .secMid ul li .con label:after{display:none;}
.layerFix.L-filter .secMid ul li .con input[type=checkbox],.layerFix.L-filter .secMid ul li .con input[type=radio]{display:none;}*/

<div class="layerFix L-filter" style="display:none">
	<div class="layerBg L-filter"></div>
	<div class="layerCon L-filter">
		<div class="secTop">
			<a href="javascript:;" class="layerClBtn L-filter">X</a>
			<div class="tit">쇼핑몰 필터</div>
			<a href="javascript:;">초기화</a>
		</div>
		<div class="secMid">
			<ul>
				<li>
					<div class="tit">카테고리</div>
					<div class="con">
						<a href="javascript:;">의류</a>
						<a href="javascript:;">가방</a>
					</div>
				</li>
				<li>
					<div class="tit">연령대</div>
					<div class="con">
						<a href="javascript:;">10대</a>
						<a href="javascript:;">20대 초반</a>
					</div>
				</li>
				<li>
					<div class="tit">스타일</div>
					<div class="con">
						<a href="javascript:;">페미닌</a>
						<a href="javascript:;">모던시크</a>
					</div>
				</li>
			</ul>
		</div>
		<div class="secBot sitebg2">
			<a href="javascript:;">선택 완료</a>
		</div>
	</div>
</div>


.layerTab{display:none;}
.layerTab.on{display:block !important;}
.layerTab .layerBg{position:absolute;background:rgba(0,0,0,.7);left:0;top:0;width:100%;height:100%;z-index:9998;}
.layerTab .layerCon{position:absolute;z-index:9999 !important;top:50% !important;}
.layerTab .layerCon li{display:none !important;position:absolute;top:0 !important;padding:0 10px !important;background:#fff;}
.layerTab .layerCon li.on{display:block !important;}
.layerTab .layerCon li img{width:100%;height:auto;}

<div>
	<ul class="layerLink L-guide">
		<li class="ani" swiper-animate-effect="bounceInUp" swiper-animate-duration="1s" swiper-animate-delay="0s">
			<a href="#"><span class="F info">Info</span> 식당가 목록 및 정보</a>
		</li>
		<li class="ani" swiper-animate-effect="bounceInUp" swiper-animate-duration="1s" swiper-animate-delay="0.1s">
			<a href="#"><span class="F">10F</span> 남성 패션 이벤트홀 </a>
		</li>
		<li class="ani" swiper-animate-effect="bounceInUp" swiper-animate-duration="1s" swiper-animate-delay="0.2s">
			<a href="#"><span class="F">9F</span> 전문식당가 / 최가을헤어드레서 / yido카페</a>
		</li>
	</ul>
</div>

<div class="layerTab L-guide" style="display:none">
	<div class="layerBg L-guide"></div>
	<ul class="layerCon L-guide">
		<li>
			<img src="/images/GUIDE11-2.png" class="" alt="">
		</li>
		<li>
			<img src="/images/GUIDE10-2.png" class="" alt="">
		</li>
		<li>
			<img src="/images/GUIDE9-2.png" class="" alt="">
		</li>
	</ul>
</div>


- js -

function layerFix(version, index){
	var wiw = $(window).width(); // 윈도우 넓이
	var wih = $(window).height(); // 윈도우 높이
	var lyr = $(".layerFix"); // 레이어 전체(장막까지)
	var con; // 레이어 내용(흰색)
	var bg = lyr.find(".layerBg");  // 레이어 장막
	var btnOpen = $(".openLayerFix"); // 레이어 열기 버튼
	var btnClose = $(".closeLayerFix"); // 레이어 닫기 버튼

	var cow; // 내용 넓이
	var coh; // 내용 높이
	//var cnt = 0; // 레이어 크기/위치 자동 정렬 변수

	if(version == "open"){
		if (index > 0){
			open(index);
		}else{
			open();
		}
		return;
	}

	btnOpen.on("click",function(){
		var idx = $(this).attr("layerIdx");
		if (idx > 0){
			open(idx);
		}else{
			open();
		}
	});

	btnClose.on("click",function(){
		var idx = $(this).attr("layerIdx");
		closeLayer(idx);
	});
	
	function open(idx){
		lyr.each(function(){
			if ($(this).attr("layeridx") == idx){
				lyr = $(this); // 선택된 레이어 저장
			}
		});

		lyr.addClass("on"); // 레이어 열기
		con = lyr.find(".layerCon");

		cow = con.outerWidth(true) // display:block 이후 내용 넓이 계산
		coh = con.outerHeight(true) // display:block 이후 내용 높이 계산

		if(version == "section"){ //ver.상하단고정, 가운데영역 스크롤, 쓰인페이지 - /addon/m_admin/goods/goods_reg , /m/goods/main , /product/sublist
			lyr.css("opacity",1);
			var st = con.find(".secTop");
			var sm = con.find(".secMid");
			var sb = con.find(".secBot");
			sm.outerHeight(con.outerHeight() - (st.outerHeight() + sb.outerHeight()));
			sm.css("margin-top",st.outerHeight());
		}else{
			var sw;
			if(con.outerWidth() > wiw && con.outerHeight() > wih){ // 내용 넓이/높이가 화면보다 클경우
				con.css({
					"left": 25,
					"width": wiw - 50,
					"top": 25,
					"height": wih - 50,
				});
			}else if(con.outerWidth() > wiw){ // 내용넓이가 화면보다 클경우
				con.css({
					"left": 25,
					"width": wiw - 50,
				});
				sw = 1;
			}else if(con.outerHeight() > wih){ // 내용높이가 화면보다 클경우
				con.css({
					"top": 25,
					"height": wih - 50,
				});
				sw = 2;
			}else{ // 내용 넓이/높이가 화면보다 작을경우
				con.css({
					"top": "50%",
					"left": "50%",
					"margin-left": -(cow / 2),
					"margin-top": -(coh / 2)
				});
			}
			cow = con.outerWidth(true); // 내용 넓이 재계산
			coh = con.outerHeight(true); // 내용 높이 재계산
			switch(sw){ // 내용 위치 재조절
				case 1:
					con.css({
						"top": "50%",
						"margin-top": -(coh / 2)
					});
					break;
				case 2:
					con.css({
						"left": "50%",
						"margin-left": -(cow / 2)
					});
					break;
			}
		}

		lyr = $(".layerFix"); // 레이어변수 재배열화

		$(".gnb_menu, .swiper-pagination.high, .swiper-button-next.high, .swiper-button-prev.high").css("z-index",0);
		$("body").css({overflow:'hidden'}).bind('touchmove', function(e){e.preventDefault()});
		//$("#mobile_wrap").addClass("on"); 모바일 본문스크롤제거용
	}
	
}

function layerTab(img){ //연속적인 탭레이어, 쓰인페이지 - wmallhomepage
	var llink = $(".layerLink");
	var lyr = $(".layerTab");
	llink.children("li").click(function(){
		lyr.addClass("on");
		var idx = $(this).index();
		var idxx = $(".layerTab li:eq("+idx+")");
		lyr.find("li").removeClass("on");
		idxx.addClass("on");
		if(img == 1){ //이미지원본넓이따라
			var idxximg = idxx.find(".image img");
			idxx.width(idxximg.width());
		}
		var lh = idxx.outerHeight();
		var lw = idxx.outerWidth();
		idxx.css({"margin-top":-lh / 2, "margin-left":-lw / 2});
		var wdw = $(window).width();
		var wdh = $(window).height();
		if(lcon.outerWidth() > wdw || lcon.outerHeight() > wdh){
			if(lcon.outerWidth() > wdw){ //내용넓이가 화면보다 클경우
				lcon.css({"height":wdw-50, "margin-top":-((wdw-50) / 2)});
			}
			if(lcon.outerHeight() > wdh){ //내용높이가 화면보다 클경우
				lcon.css({"height":wdh-50, "margin-top":-((wdh-50) / 2)});
			}
		}else{
			lcon.css({"margin-top":-lh / 2, "margin-left":-lw / 2});
		}
		$(".gnb_menu, .swiper-pagination.high, .swiper-button-next.high, .swiper-button-prev.high").css("z-index",0);
	})
}

function closeLayer(idx){
	var lyr = $(".layerFix, .layerTab");
	var con;

	if(idx > 0){ // 레이어 여러개 쓸경우
		lyr = $(".layerFix[layerIdx=" + idx + "], .layerTab[layerIdx=" + idx + "]");
	}
	
	lyr.removeClass("on"); // 레이어 닫기

	con = lyr.find(".layerCon")
	con.removeAttr("style",""); // 정렬 초기화

	$(".gnb_menu, .swiper-pagination.high, .swiper-button-next.high, .swiper-button-prev.high").css("z-index",1000);
	$("body").css({overflow:'auto'}).unbind('touchmove');
	//$("#mobile_wrap").removeClass("on"); 모바일 본문스크롤생성용
}




↓↓↓ 쓰는법 ↓↓↓

<열때>
1. 버튼이용
	window.load에 layerFix(); 호출 후 여는버튼에 "openLayerFix" 클래스 삽입
	( 제이쿼리 3버전부터 $(window).on("load",function(){ 이처럼 on메소드 이용해야함 )
2. 함수호출
	a. 페이지 뜨자마자 열리게 하려면 window.load에 layerFix("open"); 호출
	b. 특정 상황(이벤트 발생시)에 열리게 하려면 마찬가지로 해당 이벤트에서 layerFix("open") 호출
		이때는 layerFix()를 window.load에 미리 호출해놓을 필요 없음
3. 레이어가 여러개일경우
	a. 버튼이용
		layeridx=2 이처럼 ①열기버튼과 ②레이어전체div에 layeridx(사용자속성)을 추가해 서로 연결하기.
	b. 함수호출
		layerFix('open',2) 이처럼 뒤에 번호를 붙이기
	

<닫을때>
1. 버튼 이용
	클릭하면 닫힐요소(버튼)에 "closeLayerFix" 클래스 삽입 (함수호출로 연 레이어는 함수로 닫거나, 클래스로 닫으려면 layerfix()를 한번 호출해야됨)
	레이어 배경 클릭시 닫기 할때 배경div에 클래스 넣기
	(닫기버튼엔 속성을 넣을필요 없지만 동시에띄워놓은 여러레이어가 하나씩 닫히길 원할경우 닫기버튼에도 속성을 넣어도 됨)
2. 함수호출
	a. 특정 상황(이벤트 발생시)에 닫히게 하려면 마찬가지로 해당 이벤트에서 closeLayer() / closeLayer(번호) 호출


//layerFix("section") : 레이어에 상단/내용/하단 구역이 생김 (나중에다시만들기)


<html부>
<a href="javascript:layerFix('open',2);" class="" layerIdx=2>레이어2 오픈버튼1</a> <!-- 여는 버튼. 여러개 쓸려면 layerIdx 속성 추가 -->
<a href="javascript:" class="openLayerFix" layerIdx=2>레이어2 오픈버튼2</a><br> <!-- 여는 버튼. 여러개 쓸려면 layerIdx 속성 추가 -->

<div class="layerFix" layerIdx=2> <!-- 레이어 전체. 여러개 쓸려면 layerIdx 속성 추가 -->
	<div class="layerBg closeLayerFix"></div> <!-- 레이어 배경(장막). 클릭시 닫히게 하려면 closeLayerFix클래스 추가 -->
	<div class="layerCon"> <!-- 레이어 내용 (흰색) -->
		<a href="javascript:" class="btn closeLayerFix"></a> <!-- 닫기 버튼 -->

		내용

	</div>
</div>
 

---------------------------------------------------------------------------------------------------

탭 레이어

function layerTab(sw,ns){
	var llink=$(".layerLink")
	var lyr=$(".layerTab")
	var lbg=lyr.find(".layerBg")
	var lcon=lyr.find(".layerCon")
	llink.children("li").click(function(){
		lyr.addClass("on")
		var idx=$(this).index()
		var idxx=$(".layerTab .layerCon li:eq("+idx+")")
		lyr.find("li").removeClass("on");
		lyr.find(".layerCon").addClass("on")
		idxx.addClass("on");

		var lh=idxx.height()/2
		idxx.css("margin-top",-lh)

		$(".gnb_menu,.swiper-pagination.high,.swiper-button-next.high,.swiper-button-prev.high").css("z-index",0)
	})
	lbg.click(function(){
		lyr.removeClass("on")
		lyr.find(".layerCon").removeClass("on")
		$(".gnb_menu,.swiper-pagination.high,.swiper-button-next.high,.swiper-button-prev.high").css("z-index",1000)
	})

	if(sw==2){
		sm.height($(window).height()-(st.height()+sb.height()))
		sm.css("margin-top",st.height())
	}else{
		var idx=$(this).index()
		var idxx=$(".layerTab .layerCon li:eq("+idx+")")
		var lh=idxx.height()/2
		lcon.css("margin-top",-lh/2)
	}

}

function layerTab2(){
	$(".layerLink.floorNum").click(function(){
		swiper_wrap.disableMousewheelControl();
		$(".swiper-slide.wrap_list.section2").addClass("swiper-no-swiping")
		//console.log($(".swiper-slide.wrap_list.section2"))
		$(".floorNum.layerAll").addClass("on")
		var idx=$(this).closest("li").index()
		//console.log(idx)
		var idxx=$(".floorNum.layerCon > li:eq("+idx+")")
		$(".floorNum.layerCon > li").removeClass("on");
		$(".floorNum.layerCon").addClass("on")
		idxx.addClass("on");

		var lh=idxx.height()/2
		//console.log(lh)
		idxx.css("margin-top",-lh)

		$(".gnb_menu,.swiper-pagination.high,.swiper-button-next.high,.swiper-button-prev.high").css("z-index",0)
		
		return false;
	})
	$(".floorNum.layerBg,.floorNum.layerClBtn").click(function(){
		swiper_wrap.enableMousewheelControl()
		$(".swiper-slide.wrap_list.section2").removeClass("swiper-no-swiping")
		$(".floorNum.layerAll").removeClass("on")
		$(".floorNum.layerCon").removeClass("on")

		$(".gnb_menu,.swiper-pagination.high,.swiper-button-next.high,.swiper-button-prev.high").css("z-index",1000)
	})
}

---------------------------------------------------------------------------------------------------

슬라이드전용 레이어 스크립트

$(".movieSl .slide").click(function(){
	var len = $(".layerTab li").length
	var idxMinus = $(this).index()-len
	$(".layerTab").addClass("on")
	$(".layerTab li").removeClass("on")
	$(".layerTab li:eq("+idxMinus+")").addClass("on")
})
$(".layerBg").click(function(){
	$(".layerTab").removeClass("on")
})


★그런데 이걸 쓰면 스와이프끝나고 클릭이벤트가 발생되어버려서 swiper에서는 callbacks(이벤트)제어로 가능하지만 slick에서는 이방식을 못쓰고 onclick + 아이프레임으로 해야함

function openMovPopup(url){
	$("#popMov").show();
	$("#popMov iframe").attr('src',url+'?wmode=transparent&rel=0&autoplay=1');
}
function closeMovPopup(){
	$("#popMov").hide();
	$("#popMov iframe").attr('src','');
}

이렇게 사용

---------------------------------------------------------------------------------------------------

table li구조로 바꾸기 병합할때 사용

function fnSet_liGr(){
	var chkCSS
		, setNo
		, obj1 = $(".section_F4 .table ul li");

	$.each(obj1, function(en, ev) {
		chkCSS = $(this).attr("class")
		setNo = chkCSS ? chkCSS.replaceAll2("r", "") : "1";
		$(".section_F4 .table ul li.r"+ setNo).css({"height":"calc(24px * "+ setNo +")","line-height":"calc(24px * "+ setNo +")"});
	});
}

---------------------------------------------------------------------------------------------------

return false 활용 하기

<li class="ani" swiper-animate-effect="bounceInUp" swiper-animate-duration="1s" swiper-animate-delay="0s">
	<a href="#"><span class="F info">F&B</span> 식당가 목록 및 정보</a><a href="javascript:;" class="floorNum">전화번호 안내</a>
</li>

이렇게 되있고 li에 스크립트 걸려 있는상황
floorNum 눌렀을때 li에걸린 스크립트가 실행되지 않게 하려면 아래처럼

$(".floorNum").click(function(){
	// 전화번호 레이어 생성
	alert('전화번호 레이어 생성')
	return false;
})

---------------------------------------------------------------------------------------------------

아래처럼 children/parents/parent/find/closest 으로 클릭 등 한 부모나 자식의 순번도 찾을 수 있음

var idx=$(this).closest("li").index()

---------------------------------------------------------------------------------------------------

document.ready 는 문자로드후 실행
window.load 는 이미지까지 로드된 다음 실행
새로고침 했을시도 좀 다름

---------------------------------------------------------------------------------------------------

원페이지 스크롤 스와이퍼로 할때

html,body{width:100%;height:100%;} 이거 꼭 넣어야 함 안그럼 이미지 세로로 겁나늘어남 (이건 스크립트문제 X)

var swiper_wrap = new Swiper('.swiper_wrap', {
        pagination: '.swiper_wrap .swiper-pagination',
		nextButton: '.swiper_wrap .swiper-button-next.wrap',
		prevButton: '.swiper_wrap .swiper-button-prev.wrap',
        direction: 'vertical',
        slidesPerView: 1,
        paginationClickable: true,
        spaceBetween: 0,
        mousewheelControl: true,
		onInit: function(wrapswiper){
			swiperAnimateCache(wrapswiper);
			swiperAnimate(wrapswiper);
		},
		onSlideChangeEnd: function(wrapswiper){
			swiperAnimate(wrapswiper);
			gnb_menuonoff(wrapswiper);
			if($(".wrap_list.first").hasClass("swiper-slide-active")){
				$(".top_fix_head,.bfmWrap").show()
			}else{
				$(".top_fix_head,.bfmWrap").hide()
			}
		}
    });


어떤상황에서 위아래 스와이퍼,스크롤 안되게하려면 이렇게 사용

swiper_wrap.enableMousewheelControl()
$(".swiper-slide.wrap_list.section2").removeClass("swiper-no-swiping")

---------------------------------------------------------------------------------------------------

미디어쿼리

@media screen and (max-width:1600px){

}

이나

@media(max-width:px){

}

@media only screen and (max-width:735px){

}

@media (min-width: 576px) and (max-width: 767px) { ... }

screen 이나 all 이나 and 등 사용시 띄어쓰기 必

---------------------------------------------------------------------------------------------------

미디어쿼리랑 키프레임이랑 동시에 썻는데 안될땐 키프레임을 위쪽에 쓰기

---------------------------------------------------------------------------------------------------

크롬 바로캡처후 바로저장

ctrl + shift + c 클릭드래그

---------------------------------------------------------------------------------------------------

css나 script 잘 안먹으면 같은파일에서 조금씩 위쪽으로 옮겨보기

---------------------------------------------------------------------------------------------------

colspan은 합칠게 없어도 colgroup 순번에 적용됨 잘안되면 colspan있나확인

---------------------------------------------------------------------------------------------------

서브페이지 전체 이상하게 깨지는데 원인을 모르겠을때는
관리자 서브상하단에서 하나씩 숨겨보기

---------------------------------------------------------------------------------------------------

와봐요모바일 함수만들때 경로적어놓기

---------------------------------------------------------------------------------------------------

css호환 사이트
https://caniuse.com/

---------------------------------------------------------------------------------------------------

font-size 0 하고 사이 여백있는3칸만들때
32%씩 3개하면 96% 사이여백 2%+2% 100%

---------------------------------------------------------------------------------------------------

<!-- --> 이걸로

속안에있는 asp 주석 안됨 따로 ' 하나씩 찍기
<%'=joinText%> 한줄일때도 이렇게

---------------------------------------------------------------------------------------------------

background 여러개 이미지만바꾸고 다른속성은 똑같이하려면

background-size:cover or 100% 100%;background-position:center;background-repeat:no-repeat; 공통적용은 이렇게 풀어쓴다음 (굳이이렇게안해도됨)
background-image:url() 이것만 따로따로쓰면됨

축약식으로써도됨

---------------------------------------------------------------------------------------------------

반응형 정사각이미지 높이 계산법

33.333vw 에서 가로 여백모두(선포함)를 더한다음 3으로나눈 결과를 뺀다 (적용될 것에다는 border-box하면 포함안해도됨)
모든여백의합이45px일때 width:calc(33.333vw - 15px);height:calc(33.333vw - 15px)

3등분이 아니여도 똑같이 하면됨

max-width 가 정해져있는경우 미디어쿼리로 최대넓이에 맞춰 자체계산 고정값넣기
@media (min-width:568px){
	.pdListR3style1 ul li .liWrap>.image{width:174px;height:174px;}
}

---------------------------------------------------------------------------------------------------

메인할때 페이지내에서 스타일 똑같은거 스타일하나로 여러개 쓰기 (제목같은거)

.titStyle1{font-size:1.3em;text-align:center;font-weight:bold;padding-top:15px;}
.titStyle1 .stitStyle1{color:#ffcc00;}
.titStyle1 .stitStyle2{font-size:12px;}

이렇게 맨위에써놓기

---------------------------------------------------------------------------------------------------

css 그라디언트(그라데이션)

background:linear-gradient(-90deg,rgba(255,255,255,1),rgba(255,255,255,0)) 나
background:linear-gradient(0deg,rgba(0,0,0,.6),rgba(0,0,0,0))
background:radial-gradient(#000 50%,#ccc 50%) ← 이렇게 하면 '반반'

만들어주는 사이트
http://www.colorzilla.com/gradient-editor/

---------------------------------------------------------------------------------------------------

em은 부모 폰트크기기준이고 rem은 html(최상위,루트)폰트크기기준

---------------------------------------------------------------------------------------------------

좀늦게실행시켜야되는데 window.load안될때

아무클래스로나 $(".").ready(function(){}) 해서안에다써보기

---------------------------------------------------------------------------------------------------

스크롤 따라다니는 메뉴
fixed를 넣으면 안되고 absolute로만 해야함, stop써야함(안쓰면 뒤늦게 버벅이면서 따라옴)
if (s >= 200) {
	const position = $(window).scrollTop();
	element.stop().animate({"top":position+"px"},500);
}else{
	element.stop().css("top","174px");
}

$(function() {
	var offset = $("#right_bn_wrap").offset();
	var topPadding = 15;
	$(window).scroll(function() {

		if ($(window).scrollTop() > offset.top) {
			$("#right_bn_wrap").stop().animate({
				marginTop: $(window).scrollTop() - offset.top + topPadding
			}, 500);
		} else {
			$("#right_bn_wrap").stop().animate({
				marginTop: 0
			});
		};
	 });
});

---------------------------------------------------------------------------------------------------
 
z-index 는 아무리높아도 부모가 낮게 적용되있으면 부모위로는 못올라간다 , 마찬가지로 부모보다 내려가지도 못함

활용해서 부모를 높이고 배경을 낮추면

---------------------------------------------------------------------------------------------------
 
상하애니메이션이동 스크립트 (document까지 써야 모바일에서 됨) 
 
function go_top(){
	$('html,body',document).stop().animate({
		scrollTop:0
	}, 500);
}
function go_btm(){
	$("html,body",document).stop().animate({
		scrollTop:(document.body.scrollHeight)
	});
};

---------------------------------------------------------------------------------------------------

박스밑에 자식으로 table 쓸때는 width:100%;table-layout:fixed; 쓰기 (익스에서 부모 벗어남)

---------------------------------------------------------------------------------------------------

★익스에서 table 한테 100% 넣기

---------------------------------------------------------------------------------------------------

파이어폭스에서 100%가 자동으로 안되니 참고확인

---------------------------------------------------------------------------------------------------

리스트 순위 css로

.w_mall_wrap .gnb_box2 .gnb_box2_tabcont .gnb_box2_ul>li .cont{position:relative;}
.w_mall_wrap .gnb_box2 .gnb_box2_tabcont .gnb_box2_ul>li .cont:before{display:inline-block;position:absolute;left:0;top:-1%;width:22%;height:22%;font-size:1.3rem;color:#fff000;padding-top:9%;background-repeat:no-repeat;background-position:center top;background-size:100%;text-indent:-1%;text-align:center;}
.w_mall_wrap .gnb_box2 .gnb_box2_tabcont .gnb_box2_ul>li:nth-of-type(1) .cont:before{content:"1";background-image:url({{BANNER_SRC:25}})}
.w_mall_wrap .gnb_box2 .gnb_box2_tabcont .gnb_box2_ul>li:nth-of-type(5) .cont:before{content:"2";background-image:url({{BANNER_SRC:26}})}

---------------------------------------------------------------------------------------------------

이메일 페이지는 스크립트안되고 css도 외.내부 안되서 다 인라인으로 써야지 됨


테스트하려면

방법1)

기본메일폼백업후 테스트할거 기본으로 옮긴다음
회원관리 → 회원메일발송가서 이메일치고 보낸다

방법2)

네이버 내게쓰기로 html 눌러서 확인

---------------------------------------------------------------------------------------------------

인라인으로 쉽게 바꾸는방법

http://inlinestyler.torchboxapps.com/styler/

설명
http://trend21c.tistory.com/682
https://hyeonseok.com/soojung/css/2009/06/08/532.html

---------------------------------------------------------------------------------------------------

hover 인라인으로쓰는법

<a href="##" onmouseover="this.style.color='#66ccff';" onmouseout="this.style.color='#ff0000';">12345</a>

---------------------------------------------------------------------------------------------------

스크립트 hover효과 (hover 와 mouseenter 차이)

마우스 mouseover / mouseout 이거는 해당 엘리먼츠 안에서 움직여도 발생된다 
그런데  mouseenter / mouseleave 는 처음 엘리먼츠 안에 들어왔거나 나갈때만 발생된다

---------------------------------------------------------------------------------------------------

스크롤안되는거 수정할때

감싸는거 하나 만들어서 overflow-y:auto;height:90vh 높이는조절
margin:0 -15px;padding:0 15px은 필요에 따라서 추가

---------------------------------------------------------------------------------------------------

로고(이미지)밑 글자 리스트구조일때 글자들 크기 10px밑으로 쭐일라면 letter-spacing이랑
글자에만 가로로 margin:0 -10 하면 아이폰5에서도 웬만함 잘보인다

---------------------------------------------------------------------------------------------------

margin에 좌우 -(마이너스) 값 넣을때는

넓이가 고정되있지않아야한다

---------------------------------------------------------------------------------------------------

다른거랑 붙어있는거에 그림자 할때는 마진이랑 같이
box-shadow:0 3px 10px rgba(0,0,0,.05);margin-bottom:20px

---------------------------------------------------------------------------------------------------

솔루션 관련

---------------------------------------------------------------------------------------------------

pc/m 상품리스트모음 url

/product/list.asp 메인에서 타임세일/베스트/뉴 등 눌렀을때 나오는 페이지(/product/list.asp?type=best)
/product/sublist.asp 메인에서 카테고리 눌렀을때 나오는 페이지
/product/search.asp 검색했을때 나오는 페이지
eventmall.asp 관리자 디자인 → 기획전
eventmall_category.asp 관리자 디자인 → 기획전(분류)
/m/goods/main.asp m메인에서 타임세일/베스트/뉴 등 눌렀을때 나오는 페이지
/m/goods/brandlist.asp (pc버전은 /brand.asp)
/product/best100.asp
/m/goods/best100.asp?menuType=new


실제경로

pc
/product/ajaxList.asp
/product/ajaxSubList.asp
/product/ajaxGoodsList.asp
/product/search.asp → /product/ajaxSubList.asp
/ajaxEventmall.asp
/eventmall_category.asp
/product/ajaxBest.asp

m
/m/goods/main.asp
/m/common/exec_getMainGoodsList.asp → 여기도 넣기(로드되는 리스트)
/m/product/list.asp
/m/product/ajaxList.asp
/m/goods/brandlist.asp
/m/goods/search.asp
/m/goods/eventmall.asp
/m/goods/eventmall_category.asp
/m/goods/ajaxBest.asp

--------------------------------------------------------------------------------------------------- 

치환코드

<%=siteID%>
이미지 등 경로에 /<%=siteID%>/img.jpg이런식으로 사용

<%=site_width%>
<%=adminsite_width%>
<%=cfgSiteName%>
<%=pathSite%>

★ .sitebg1 ← 이건 모바일에서만 pc 는 css에서 아래처럼 {color:<%= %>;} 이거나
{color:{{COLORTYPE1}};} 이걸로 ← 이건 관리자에서
width:{{SITE_WIDTH}}px ← 이것도 관리자에서

.sitebg1 {background:<%=cfgColor1%> !important;}
.sitebg2 {background:<%=cfgColor2%> !important;}
.sitebg3 {background:<%=cfgColor3%> !important;}

.sitecolor1 {color:<%=cfgColor1%> !important;}
.sitecolor2 {color:<%=cfgColor2%> !important;}
.sitecolor3 {color:<%=cfgColor3%> !important;}

.siteborder1 {border-color:<%=cfgColor1%> !important;}
.siteborder2 {border-color:<%=cfgColor2%> !important;}
.siteborder3 {border-color:<%=cfgColor3%> !important;}

.priceStyle1 {color:<%=cfgPriceStyle%> !important;}



탬플릿 치환코드

** 상품 관련 **
{{GOODS_IMG:1}} 상품이미지
{{GOODS_BACKGROUND_IMG:1}} pc상품 이미지 배경으로 넣을때 ※이거쓸때는 {{GOODS_IMG:1}} 이거 아무데나상관없으니 넣고 display:none 해야함 (모바일은 이거 안써도 {{GOODS_IMG:1}} 에 두개 들어감)
{{GOODS_TITLE:1}} 상품제목
{{GOODS_SUBTITLE:1}} 간략한설명
{{GOODS_LINK:1}} 상세페이지 <a href="{{GOODS_LINK:1}}" class="itemt_link" target="_blank"><i class="material-icons">open_in_new</i></a> 이렇게 사용
{{GOODS_BRAND_NAME:1}} 상품브랜드
{{GOODS_CATE:1}} 상품 카테고리
{{GOODS_SALEPERCENT:1}} 세일퍼센트
{{GOODS_MARKETPRICE:1}} 취소선(할인전/시중) 가격
{{GOODS_PRICE:1}} 그냥가격
{{BRAND_IMG:1}} 브랜드 이미지
{{BRAND_TITLE_IMG}} 브랜드 타이틀 이미지 ??
{{BANNER:1}} 배너이미지
{{BANNER_SRC:1}} 배너이미지 경로 ★ img 속성넣고싶으면 <img src="{{BANNER_SRC:1}}" alt=""> 이렇게해도되지만 {{BANNER:1}}의 기능(사용자가 관리자에서 링크수정)은 못함

{{GOODS_CMONEY:1}} 포인트(적립금)
{{COLORTYPE1}} 싸이트컬러     ★ 탬플릿(admin) 에서는 <%=cfgColor1%> 말고 이걸로 써야댐

{{GOODS_STAR:1}} 별점아이콘,별점숫자,인원수
{{GOODS_STAR_AVG:1}} 별
{{GOODS_STAR_SCORE:1}} 별점수

{{GOODS_OPINION_CNT:1}} 상품평수
{{GOODS_FAVORITE:1}} 좋아요수
{{GOODS_LIKE:1}} 좋아요하기
{{GOODS_CART:1}} 장바구니
{{INSTA_IMG:1}} 인스타연동이미지

{{GOODS_ICON_A:1}}
{{GOODS_ICON_B:1}}
{{GOODS_ICON_C:1}}
{{GOODS_ICON_D:1}}
{{GOODS_ICON_E:1}}
{{GOODS_ICON_F:1}}

{{GOODS_CART:1}} 옵션이 있으면 레이어뜨고, 없으면 장바구니에 담음
{{GOODS_DIRECT_SCRIPT:1}} 옵션이 있으면 레이어뜨고, 없으면 바로구매로 이동
<a href="javascript:go_direct({{GOODS_UID:1}});" class="btn buy"><span class="material-icons">credit_card</span></a> 바로구매
판매리워드 {{GOODS_REWARD:1}}
소개리워드 {{GOODS_IREWARD:1}}
{{GOODS_UID:1}} 상품번호
아이콘 , 클릭위치 조절할때 {{GOODS_CART:1}} , {{GOODS_LIKE:1}} 대신
<a class='HoverIconBtn cart' href='javascript:;' onclick="go_cart('{{GOODS_UID:1}}');"><span class='iconfont ftic-cart2'></span></a>
<a class='HoverIconBtn like' href='javascript:;' onclick="favorite('{{GOODS_UID:1}}');"><span class='iconfont ftic-like' id="w_{{GOODS_UID:1}}"></span></a>
이렇게 사용가능

{{GOODS_TIMESALE_PERCENT:4}} 타임세일 퍼센트
{{GOODS_TIMESALE_IMG:4}} 타임세일 이미지
{{GOODS_TIMESALE_BRAND_IMG:4}} 타임세일 브랜드 이미지
{{GOODS_TIMESALE_TITLE:4}} 타임세일 타이틀
{{GOODS_TIMESALE_SUBTITLE:4}} 타임세일 서브타이틀
{{GOODS_TIMESALE_PRICE:4}} 타임세일 가격
{{GOODS_TIMESALE_MARKETPRICE:4}} 타임세일 시중가

{{BOARD_TITLE:notice:1:20}} 게시판 제목
{{BOARD_IMG:notice:1:100*100}} 게시판 이미지
{{BOARD_CONTENT:notice:1:200}} 게시판 내용

(notice를 event/community/upgrade 등 id 바꾸면 다른 게시판 거 가능) 위에는 공지꺼 (뒤에붙은숫자는 max글자수 스크립트로짜른거)

★메인에서 치환코드 수정시 확인할 파일
/main/main_template.asp {{GOODS_IMG
/_lib/function.User.asp {{BANNER
/m/_lib/mobile_template.asp
/_lib/function.MainTpl.asp
/m/_lib/goods/function.GoodsRegist.asp


** 상품정렬 **
{{GOODS_SORT:NEW:1234}} BEST(판매,정렬순),FAVORITE(조회수순),NEW(신규 등록순)
1234는 url에 카테고리번호임 상품찍을때있는번호x
상품찍힌 영역 맨위에 한번만쓰면댐

**아이콘폰트**
<span class="iconfont ftic-local"></span> ←사용법 ★클래스 두개써야댐

**타임세일 퍼센트 게이지**
{{GOODS_TIMESALE_NOW_SEC:1}}	타임세일 현재기준 남은시간(초)
{{GOODS_TIMESALE_TOTAL_SEC:1}}	타임세일 토탈 시간(초)

** 회사정보(주로푸터) **
{{SITE_NAME}}	사이트명
{{SITE_URL}}	사이트도메인
{{CEO_NAME}}	대표자명
{{SECURITY_NAME}}	개인정보 보호 관리자 명
{{SECURITY_EMAIL}}	개인정보 보호 관리자 Email
{{COM_NAME}}	회사명
{{COM_ADDR}}	회사 주소
{{COM_TEL}}	회사전화
{{COM_FAX}}	회사팩스
{{BIZ_NO}}	사업자번호
{{TONGSIN_NO}}	통신판매업신고번호
{{COM_DAY}}	회사영업일(요일)
{{COM_TIME}}	회사영업일(시간)
{{COM_HOLIDAY_DAY}}	회사공휴일(요일)
{{COM_HOLIDAY_TIME}}	회사공휴일(시간)

---------------------------------------------------------------------------------------------------

치환코드 쓸 때 개발자도구에서 어케바뀌나 그리고 열리나 확인해보기 (<head></head>쪽)

<link rel="stylesheet" type="text/css" href="<%=pathSite%>/m/css/sweetalert.css" /> 이런거
----------------------------------------------------------------------------------------------------

치환코드 이미지에 속성추가
$(".usem img").attr("usemap","#Map01")


id나 name도 추가가능(class추가는 addClass())
$(".usem img").attr("id","usem")

id에 이미지맵 추가
document.getElementById("usem").setAttribute("usemap","#Map01")

----------------------------------------------------------------------------------------------------

치환코드랑 섞인 경로 따옴표

<img src='"& imgURL & pathPopup &"/"& imgClosePopup &"close.png' border='0' class='btn_pop_main_close' onclick='closewin();' />

--------------------------------------------------------------------------------------------------- 

관리자 메뉴 이동할때 바꿔야할목록


해당 페이지에서
 
Call checkAdminPageAuth("3-16-r", Null) --- 그 페이지를 읽을 수 있는 권한이 있는가 체크하는거 부운영자가 접근할 경우 그 권한이 있나 체크하고 없으면 팅겨냄

<!--#include file="../goods/left.asp"-->   ---   left파일경로

setleftmenu_on("3-16");   ---   왼쪽메뉴 현재위치불켜지는거

pageNavi = "<a href='"& adminURL &"/setup'>상품관리</a> > 상품관리 > 상품정보고시설정"   ---   현재위치


해당 left파일에서

<div id="lm2-15"><a href="<%=adminURL%>/setup/config_goodsInfoNoti.asp" onfocus="this.blur()">상품정보고시설정</a></div>
이동하고 id 원래있던거랑 맞추기 / 중복확인


새로만들땐 딴메뉴 복사한다음
setleftmenu_on("
찾아서 숫자만 바꾸기(해당left도같이)

---------------------------------------------------------------------------------------------------

치환코드 올메뉴{{ALL_MENU}} 경로

pc /common/ajax/exec_fullCategory.asp
m /m/_lib/mobile_template.asp

----------------------------------------------------------------------------------------------------

메인팝업관련 파일경로 상위순

/main/popup_main.js.asp
ifrm_popupLayer.asp 레이어팝업말고 그냥팝업은→popup.asp
관리자

모바일은 /partner/mobile/design/ifrm_popupLayer.asp 도 있음

---------------------------------------------------------------------------------------------------

pc자주쓰는 url들


(회원)

로그인 : /member/login.asp
로그아웃 : /member/logout.asp
회원가입(약관동의) : /member/regist_agree.asp
회원가입(입력폼) : /member/join.asp
회원가입(완료페이지) : /m/member/regist_final.asp


(마이페이지)

메인 : /my/main.asp
장바구니 : /product/cart.asp
주문조회 : /my/order_total.asp?mode=normal
배송조회 : /my/order_total.asp?mode=deliver
취소/반품 : /my/order_total.asp?mode=cancel
교환/AS : /my/order_total.asp?mode=change
내 포인트 : /my/my_point.asp
내 쿠폰 : /my/my_coupon.asp
내 좋아요누른목록 : /my/my_wishlist.asp
내 샘플신청목록 : /my/sample.asp
내 1:1문의 : /my/my_qa.asp
내 상품평 : /my/my_evaluation.asp
내 Q&A : /my/qna.asp
내 상품 Q&A : /m/my/product_q_a.as
내 최근본상품 : /my/todayhistory.asp
나를추천한회원목록 : /my/rec_member.asp
추천홍보관리 : /my/my_share.asp
개인정보 수정 : /my/info_edit.asp
내 배송지관리 : /my/my_delivery.asp
회원탈퇴 : /my/secession.asp
출첵 : /member/check_date.asp


(고객센터)

고객센터 메인 : /cscenter/
1:1문의(고객센터) : /cscenter/consultReg.asp
FAQ : /cscenter/faq.asp
공지사항 : /cscenter/notice_list.asp
이용안내 : /other/InformationUse.asp
이용약관 : /other/licensing.asp
제휴문의 : /other/partner.asp
등급혜택 : /cscenter/membership.asp


(상품리스트)

서브 리스트 : /product/sublist.asp
검색 : /product/search.asp
타임세일 : /product/list.asp?type=timeSale
베스트 : /product/list.asp?type=best
뉴 : /product/list.asp?type=new
세트상품 : /product/setcontent.asp


(이벤트 등 기타)

메인 : /main/main_real.asp (인트로 패스용) (모바일 : /m/main/main.asp)
리뷰 : /board/best_list.asp
이벤트/쿠폰 : /event/event_list.asp
pc버전 : /?v=full



모바일 자주쓰는 url

로그인 : /member/login.asp
로그아웃 : /m/mobile_logout.asp
메인 : /m/main/main.asp
타임세일 : /m/product/list.asp?type=timeSale
베스트 : /m/product/list.asp?type=best
신규상품 : /m/product/list.asp?type=new
기획전 : /m/promotion.asp
이벤트&쿠폰 : /m/event/event.asp?mode=A
출석체크 : /m/member/check_date.asp
공지사항 : /m/customercenter/cscenter_notice.asp
FAQ : /m/customercenter/cscenter_FAQ.asp
my : /m/my/main.asp
my 장바구니 : /m/product/cart.asp
my qna/문의내역 : /m/my/my_qna.asp
my 상품 qna : /m/my/product_q_a.asp
my 상품평/후기/리뷰 : /m/my/evaluate_list.asp
my 좋아요 : /m/my/favorite.asp
my 적립금 : /m/my/my_point.asp
my 주문내역 : /m/my/order_total.asp?mode=normal
my 취소/반품/환불 : /m/my/order_total.asp?mode=cancel
my 교환/as : /m/my/order_total.asp?mode=change
my 게시물 : /m/my/my_board_list.asp
1:1문의 : /m/customercenter/cscenter_one.asp?mode=A
고객센터 : /m/customercenter/cscenter_main.asp
회원탈퇴 : /m/my/member_leave.asp?mode=C

---------------------------------------------------------------------------------------------------

pc/m 구분방식

default는 모바일, pc로접속시 모바일연결을 막는방식

--------------------------------------------------------------------------------------------------- 

파비콘 이미지경로 /data/사이트아이디/favicon.ico

이미지 불러오는 경로는 /m/_include/mobile_header.asp

<%=iif(flag2Bool(cfgIsFavicon), "<link rel=""SHORTCUT ICON"" href="""& imgURL & pathSite &"/favicon.ico?"& getUnixTimeStamp() &""" />", "")%>

---------------------------------------------------------------------------------------------------

같은 솔루션내 (소스가 더티해지지만) 부분 추가/수정

<%if siteID="ilikelux" then%>
	.sub_ul li img {width:150px;}
<%end if%>


<%if SiteID = "coindoll" and board="application" Then %>
<% End If %>

<%If siteid= "coindoll" Or siteid="osaka" then%>
<% End If %>

<% if siteID <> "e-giverny" then %>
<% End If %>

<% If SiteID = "familymall" And joinWho = "dealer" Then %>
	<a href="/mallinmall/login.asp" class="btn_yellow02 loginSeller">판매자로그인</a>
<%Else%>
	<a href="/" class="btn_yellow02">메인으로</a>
<% End If %>

(or을 우선시할땐 괄호로 묶기)
<%If (cfgPartnerID=siteID Or cfgPartnerID="kr") And checkPerm(JOINSET_USE, permRec) Then%>

(ex2)
<%if SiteID = "familymall" and (cfgPartnerID=siteID or cfgPartnerID="DBMall") then%>

리스트타입 : listType
파트너 아이디 : cfgPartnerID
본사 : cfgPartnerID=siteID

---------------------------------------------------------------------------------------------------

site id 찾을땐

print siteid

---------------------------------------------------------------------------------------------------

글자수로 끊기

title = cutString(title, 18)

---------------------------------------------------------------------------------------------------

솔루션폴더 확인

/api/test/debugSession.asp

---------------------------------------------------------------------------------------------------

솔루션 관련 끝

---------------------------------------------------------------------------------------------------

원스크롤페이지 라이브러리

fullpage.js (jquery.fullPage.js)

보내고싶은 목적지에 data-anchor="이름" 속성 넣고 (data-anchor속성 말고 id속성으로 넣어도 됨)
링크 걸때는 a href="이름" 넣으면 됨

$(".fullpage-area").fullpage({
        //anchors: ["allsearch", "network", "statistics", "infomation", "footer"],
        lockAnchors: true,
        slidesToSections: true,
        fitToSection: true,
        fitToSectionDelay: 0,
        scrollingSpeed:400,
        scrollBar: true,
        // navigation: true,
        easingcss3: "ease-out",
        //�묎렐��
        keyboardScrolling: true,
        animateAnchor: true,
        recordHistory: true,

자세한 사용법은 웹검색

---------------------------------------------------------------------------------------------------

구글 무료 폰트
http://fonts.google.com

1. 원하는 폰트 들어가서 Download family버튼으로 다운받아서 사용 가능
2. 원하는 폰트 들어가서 Select this style버튼으로 폰트를 추가 후 <link> or @import 방식으로 불러서 사용가능
  (이 방법은 사이트가 좀더 무거워짐)

---------------------------------------------------------------------------------------------------

css로 스크롤바 변경 (#커스텀 스크롤바 #스크롤 디자인 #스크롤css)
https://webisfree.com/2019-01-08/css-%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EC%8A%A4%ED%81%AC%EB%A1%A4%EB%B0%94-%EC%8A%A4%ED%83%80%EC%9D%BC-%EC%A7%80%EC%A0%95-%EB%B0%94%EA%BE%B8%EB%8A%94-%EB%B0%A9%EB%B2%95-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0

나이스 스크롤 (스크롤바 플러그인)
sw_scroll = true; // 나이스 스크롤 변수 (특정상황에 스크롤 안되게 하고싶을때 js 수정후 변수이용)
$(function(){
	$("요소").niceScroll();
});

<아래 두개 함수에 조건문 추가하고 쓰면됨>
self.onkeypress = function(e) {
self.debounced("mousewheely",function(){

if(!sw_scroll){ //스크롤(휠) on/off 설정을 위한 조건문
	return;
}


생 css로 하는방법
<회색바탕 검은바>
(요소 혹은 생략)::-webkit-scrollbar{width:10px;}
(요소 혹은 생략)::-webkit-scrollbar-thumb{background-color:#2f3542;}
(요소 혹은 생략)::-webkit-scrollbar-track{background-color:grey;}

<흰바탕 회색바>
(요소 혹은 생략)::-webkit-scrollbar{width:10px;}
(요소 혹은 생략)::-webkit-scrollbar-track{background:#fff;}
(요소 혹은 생략)::-webkit-scrollbar-thumb{background:#aaa}

---------------------------------------------------------------------------------------------------

부모영역을 자식이 벗어나면
inline에 padding 들어있는지 확인 → inline-block 으로 바꾸기

---------------------------------------------------------------------------------------------------

스크립트 last-child , first-child 등 사용 가능

llink.children("li:last-child").click(function(){

---------------------------------------------------------------------------------------------------

탬플릿 내용분리할때

마지막에 <div style="display:none;"> 열고 끝내서

다음 영역에서
시작하자마자 </div> 닫기

같은스타일 여러개슬때도 동일하게 or $(".swiper-slide").unwrap()

wrap이랑 헷깔릴수있으니
탭구분없이 맨앞에다 쓰면좋다

ex)

1영역
--------------------------------------------------
	<div class="swiper-container">
		<div class="swiper-wrapper">
<div class="forJoin" or style="display:none" (암것도 안써도 댐)>
--------------------------------------------------

2영역
--------------------------------------------------
</div>
			<div class="swiper-slide">
			</div>
<div style="display:none;">
--------------------------------------------------

3영역
--------------------------------------------------
</div>
		</div>
	</div>
--------------------------------------------------

이렇게

---------------------------------------------------------------------------------------------------

가끔 링크된 스크립트가 잘 안불러와지면 ctrl+f5말고 ctrl+shift+del 에서 삭제

---------------------------------------------------------------------------------------------------

박스보다 긴데 줄바꿈 안되면 중간중간 띄어쓰기 넣기

ex) 3333333333333333333333333 → 33 33 333333333333 3 33333333333 333 333333333 33333

---------------------------------------------------------------------------------------------------

함수 안에 이벤트를 넣는 스크립트
ex)
function layerTab(img){
	llink.children("li").click(function(){
	})
}
(함수안에 클릭 이벤트가 들어가 있다)

는 가능하지만

$(document).ready / $(window).load 가 함수 밖에나 안쪽에 있어야됨


function layerTab(img){
	llink.children("li").click(function(){
	})
}

선언을해놓고 아래처럼

<script>
	$(window).load(function(){
		layerTab();
	})
</script>

이리쓰거나


function layerTab(img){
	$(window).load(function(){

		llink.children("li").click(function(){
		})
	})
}

선언해놓고 사용할때 아래처럼 그냥 함수만 쓰기 이경우에는 또 윈도우로드로 감싸면 오류

<script>
	layerTab();
</script>


이렇게해도 되긴하지만 되도록 이렇게는 안하는게 좋다고 함 (느려질 수 있음)

---------------------------------------------------------------------------------------------------

min-width랑 max-width랑 범위가 안맞으면 이상해짐
ex) min-width가 80%인데 max-width가 568px일때

이럴땐 min-width 쓰면안되고 그냥width

---------------------------------------------------------------------------------------------------

개발자도구 style탭에서 창 늘려보면 filter라고 속성 검색할수있는창나옴

---------------------------------------------------------------------------------------------------

if로 checkbox , label 처음,클릭/값변경 시 라벨(부모)의 상태가 바뀌게

$(window).load(function(){
	$(".radioWrap label").each(function(){
		if($(this).find("input").prop("checked")){
			$(this).closest(".radioWrap").find("label").removeClass("on")
			$(this).closest("label").addClass("on")
		}
	})
	$(".checkboxWrap label").each(function(){
		if($(this).find("input").prop("checked")){
			$(this).closest("label").addClass("on")
		}else{
			$(this).closest("label").removeClass("on")
		}
	})
})

$(".radioWrap label").click(function(){
	$(this).closest(".radioWrap").find("label").removeClass("on")
	$(this).addClass("on")
})
$(".checkboxWrap label").click(function(){
	if($(this).find("input").prop("checked")){
		$(this).addClass("on")
	}else{
		$(this).removeClass("on")
	}
})

★if부분에서
if($(this).find("input").prop("checked",true)){}	나
if($(this).find("input").prop("checked"==true)){}

이렇게하면 if가 안되고 그냥 바로 체크되어버림(if밖에 안써도)
라디오도되는거같지만 모두 체크되고 원래상태가어떻든 마지막걸로만 체크가됨(ladio는 하나밖에체크안되서 순차적으로 체크되면서 마지막것만 체크된것처럼보이는것)

그냥 prop("checked") 이렇게만 쓰면 된다 prop/attr 머로하든상관x

---------------------------------------------------------------------------------------------------

이벤트 사용 체크박스 일괄체크,해제

$("input[name=cbListAll]").on("change",function(){
	var c;
	if ($(this).is(":checked")) {
		c = true;
	}else{
		c = false;
	}
	$(this).parents("table").find("input[name=cbList]").prop("checked",c);
});

자스에서 확인할때

document.getElementById("asd").checked

---------------------------------------------------------------------------------------------------

페이지.페이징.페이지네이션 숫자.앞으로.뒤로.맨앞으로.맨뒤로 기본 css

.paging_box {padding:40px 20px 20px; margin-top:30px;}
.paging_box .prev,.paging_box .first {width:35px; margin-right:10px; padding-left:14px; color:#000; font-size:14px; font-weight:bold; text-align:left;vertical-align:middle;}
.paging_box .prev:hover,.paging_box .first:hover {background:none; border-radius:0; color:#000; font-weight:normal;}
.paging_box .next,.paging_box .last {width:35px; margin-left:10px; padding-right:14px; color:#000; font-size:14px; font-weight:bold; text-align:right;vertical-align:middle;}
.paging_box .next:hover,.paging_box .last:hover {background:none; border-radius:0; font-weight:normal;}
.paging_box .pagenation{display:inline-block; width:30px; height:30px; color:#000; font-size:12px; line-height:28px;vertical-align:middle;}
.paging_box .pagenation:hover{font-weight:bold;}

---------------------------------------------------------------------------------------------------

css 적용 우선순위가 동일하지않아도 클래스안쓰고 태그로만하면 더 낮게적용됨

ex) a로 선택한게위에있고 b로 선택한게 아래에있어서 b걸로 덮힐상황이여도
a가 .label이고 b가 그냥 label이면 a것이 적용됨

---------------------------------------------------------------------------------------------------

조그만 아이콘같은거 할땐 jpg말고 png로 하기
용량도 적고 선명함

---------------------------------------------------------------------------------------------------

리스트안의 내용이 1개일때 2개일때 3개일때 4개일때·· 꽉 차게 하려면 table tabel-cell 쓰면 유동적으로 가능함

---------------------------------------------------------------------------------------------------

자식이 퍼센트로 되있고 부모가 inline-block 으로 되있을때 부모가 자식넓이만큼 유동적으로 따라가게 하기위해서는
자식의 넓이가 px로 되있어야됨 %로 되있으면 이상하게됨

---------------------------------------------------------------------------------------------------

제이쿼리 모바일 해제(input,button등)

해당 태그에 data-role="none"

---------------------------------------------------------------------------------------------------

meta태그 확대(줌인/줌아웃)

<meta name="viewport" content="user-scalable=yes, initial-scale=1.0, maximum-scale=2.0, minimum-scale=1.0, width=device-width">

initial-scale:페이지 배율 기본값(0~10)
user-scalable:사용자가 배율 확대, 축소가능여부
minimun-scale:축소 최소배율(0~10)
maxmum-scale:확대 최대 배율(0~10)


meta태그 공유 정보

<meta property="og:type" content="website">
<meta property="og:title" content="1">
<meta property="og:description" content="2">
<meta property="og:image" content="/images/limgSNS.gif">
<meta property="og:url" content="<%=siteURL%>">

---------------------------------------------------------------------------------------------------

리스트 1px선 on시 색변경 css

.f5Top .brdlogo{width:1100px;font-size:0;border:1px solid #ddd;border-width:1px 0 0 1px;}
.f5Top .brdlogo li{display:inline-block;/*opacity:.45;*/cursor:pointer;width:calc(20% - 1px);line-height:68px;border:1px solid #ddd;border-width:0 1px 1px 0;}
.f5Top .brdlogo li.on{border-color:#ffd402;border-width:1px;margin:-1px 0 0 -1px;}
.f5Top .brdlogo li img{max-width:100%;max-height:38px;}


두줄이상리스트 css
↓ ex)5*2 리스트

.eventsCate tr:first-of-type td a{border-top-width:1px;}
.eventsCate tr:first-of-type td a.on{margin:0 0 0 -1px;}
.eventsCate tr td:first-of-type a{border-left-width:1px;}
.eventsCate a{display:block;padding:10px 20px; font-size:12px; border:1px solid #e0e0e0;border-width:0px 1px 1px 0px;overflow:hidden;}
.eventsCate a.on{border-width:1px;border-color:<%=cfgcolor1%>;color:<%=cfgcolor1%>;margin:-1px 0 0 -1px;}

---------------------------------------------------------------------------------------------------

리스트 사이선 on시 사라지는 css

.visualWrap .simg li{float:left;width:16.666%;position:relative;background:rgba(255,255,255,.75);color:#000;padding:10px 0;cursor:pointer;z-index:5;}
.visualWrap .simg li:before{content:"";display:block;position:absolute;height:14px;border-left:1px solid #b0b4b6;left:0;top:50%;margin-top:-7px;}
.visualWrap .simg li.on{z-index:10;background:#f43142;color:#fff;}
.visualWrap .simg li:first-child:before,.visualWrap .simg li.on:before,.visualWrap .simg li.on+li:before{display:none;}

---------------------------------------------------------------------------------------------------

슬라이드 늦게 뜨면

document.read 나 window.load 지우거나

슬라이드 높이지정이 안되있으면 미리지정 해놓기

---------------------------------------------------------------------------------------------------

슬라이드 loop 쓰면 복제되니까 내부 기능이 잘 안되는거같으면 loop빼기

---------------------------------------------------------------------------------------------------

포토샵 액션만들때 새로만들기,저장등 넣고싶을때는 왼쪽 '대화 상자 켜기/끄기'에 체크해야 실행됨

---------------------------------------------------------------------------------------------------

익스/크롬/파폭 따로따로 css적용

익스 핵
http://www.biew.co.kr/5

크롬,사파리
@media screen and (-webkit-min-device-pixel-ratio:0) { 스타일 }

파이어폭스
@-moz-document url-prefix(){ 스타일 }


익스버전별 html
https://blog.naver.com/wwe700/220096238900 참고

---------------------------------------------------------------------------------------------------

js 논리연산자

https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/%EB%85%BC%EB%A6%AC_%EC%97%B0%EC%82%B0%EC%9E%90(Logical_Operators)

---------------------------------------------------------------------------------------------------

setTimeout (딜레이) 쓰는법 (함수,시간)

$(".btn-all-menu").click(function(){
	resetSwipe();
	function open(){
		$(".all_menu_box").addClass("open")
	}
	$(".all_menu_box").show()
	setTimeout(open,100)
});

또는 아래와같은 방식으로 메소드를 생성하지 않고 바로 사용 가능
$(".help").click(function(){
	$(".btn_page_txt").stop().toggle(500)
	setTimeout(function() {
		$(".btn_page_txt").stop().hide(500)
	}, 2000);
})


다른 예제

$(".cont_list li .pdBtnMore").click(function(){
	var _pdtItem = $(this).closest("li");
	var _tPos = _pdtItem.offset().top;
	if (_pdtItem.hasClass('on')){
		_pdtItem.removeClass('on');
		setTimeout(function(){
			_pdtItem.find('.pdBtnBox').removeAttr('style');
		}, 300);
	} else{
		_pdtItem.addClass('on').find('.pdBtnBox').css('z-index', '20');
		//$("html,body").animate({"scrollTop":(_tPos - $(".brandBest .tab").innerHeight() + 5)},500);
	};
});


★ setTimeout(open,2000) 이렇게 사용해도 됨

setTimeout(function(){
	open();
});

setInterval(정한시간마다 실행) 도 동일

---------------------------------------------------------------------------------------------------

슬라이드애니메이션으로 닫히는 타이밍에 내용이 뭔가 깨져보일땐 슬라이드애니메이션 걸 클래스를 좀 더 위쪽으로 올려보기(아님 랩만들어서 걸거나)

---------------------------------------------------------------------------------------------------

edit 플러스 앞으로가기 안될때

에플백업에서 젤최근파일 가져오기

안되면

에플 새로열고 백업 최근저장된 같은파일 30개정도 불러온다음 '다음파일로 계속' 키고 최근에 작업한 단어 검색

---------------------------------------------------------------------------------------------------

포토샵 자동화 예시

이미지 크기 300으로 변경
다른이름으로 저장 (파일 아무거나 뒤에s붙여서 같은폴더에 저장)

이렇게 액션 등록 한다음

파일 > 자동화 > 일괄처리에서 바꿀폴더,저장될폴더 두개 선택후 파일명뒤에 붙일거 있으면 적고
★액션"다른 이름으로 저장"명령 무시 이거 킨다음에 실행

---------------------------------------------------------------------------------------------------

안에 내용이 감싸는거보다 크게하여 스크롤 해야될때

감싸는애를 100%로 하는데 안에 내용만큼 늘어나면 table안에있는지 확인 맞다면 table-layout:fixed 넣고 colgroup 빼기

---------------------------------------------------------------------------------------------------

오버시 아래 선 중앙에서 좌우로 퍼졌다 사라졌다 효과css

.cateSearch .category > li:before{content:"";display:block;width:0;height:2px;position:absolute;left:50%;bottom:0;background:{{COLORTYPE1}};transition:all .2s;}
.cateSearch .category > li:hover:before{left:0;width:100%;}

---------------------------------------------------------------------------------------------------

클릭 이벤트를 제거해주는 css ★슬라이드에 클릭이벤트 있을시 활용 추천 (스와이프중 클릭방지용)

pointer-events:none; , pointer-events:auto;

---------------------------------------------------------------------------------------------------

a에 가상요소(before,after) 쓸때 부모꺼 적용되어 커서 포인터되므로 필요없는상황엔auto로 빼기

---------------------------------------------------------------------------------------------------

gnb 2단 슬라이드 메뉴 할때 2단메뉴의 내용을 1단과 분리해서 만들면 오버영역 조절이 매우어려우니

li안에다 쓰고 오버이벤트는 스크립트로(※ 지베르니카테고리 참고)

<li class="brand acwell">
	<div class="tit"><a href="javascript:;">ACWELL</a></div>
	<div class="sctCateDepth">
		<div class="wrap">
		</div>
	</div>
</li>

---------------------------------------------------------------------------------------------------

세로정렬 간단히 할때 table 대신 display:flex;align-items:center
이때 가로정렬은 text-align:center도 적고(줄바뀐텍스트용)
justify-content:center도 적기(줄안바뀐텍스트용)

flex-direction: column; 배열을 수직으로 나열 (기본은 수평)

flex속성중
justify-content:space-around → 내부의 모든 요소를 균등 가운데 정렬(내부 좌우 여백 조금)
justify-content:space-between → 내부의 모든 요소를 균등 가운데 정렬(내부 좌우 여백 X)
justify-content:space-evenly → 내부의 모든 요소를 균등 가운데 정렬(내부 좌우 여백 많이)
justify-content:center → 내부의 모든 요소를 가운데 정렬

---------------------------------------------------------------------------------------------------

함수를 a href="javascript:;" 이 안에쓰는것과 onclick="" 이안에 쓰는것은 차이가있음 각각 removeAttr("href") 이렇게 삭제가능

---------------------------------------------------------------------------------------------------

리스트속 아이콘 반응형으로 높이조절되게 하고싶을때(정원,정사각형)

부모 li에 넓이는 퍼센트로 넣은다음
내부 아이콘들 감싸는 박스에 position:absolute 한다음 padding-top:22% 이렇게 퍼센트로 패딩 넣으면 댐
그러면 부모인 li의 높이를 따라간다

속의 아이콘감싸는 랩은 넓이,높이 100%로하고
이미지는 감싸는랩에 background로 넣거나 안에 또 하나 만들어서 넣기

---------------------------------------------------------------------------------------------------

setTimeout 쓰는법

 

$(".btn-all-menu").click(function(){

	resetSwipe();

	function open(){

		$(".all_menu_box").addClass("open")

	}

	$(".all_menu_box").show()

	setTimeout(open,0)

});

$(".close-all-menu").click(function(){

	function close(){

		$(".all_menu_box").hide()

	}

	$(".all_menu_box").removeClass("open")

	setTimeout(close,200)

}); 

 

그냥쓰는법

setTimeout(function() { // (A) console.log('A'); }, 0);

---------------------------------------------------------------------------------------------------

제이쿼리줌
http://www.jacklmoore.com/zoom/ 

또다른줌
http://w-mall.co.kr/

---------------------------------------------------------------------------------------------------

jpg 뿌옇게 보이면 png로 하기

---------------------------------------------------------------------------------------------------

글자뒤선

.sctInsta>.titStyle1{padding-top:50px;margin:0 10px;}
.sctInsta>.titStyle1 img{width:20px;margin-top:-15px;padding-left:3px;}
.sctInsta>.titStyle1:after{content:"";display:block;border-top:1px solid #ccc;margin-top:-12px;}
.sctInsta>.titStyle1 span{background:#fff;padding:0 15px;}

<div class="titStyle1">
	<span>INSTAGRAM<img src="http://new.e-giverny.com/data/e-giverny/banner/ico_insta_1.png" border="0"></span>
</div>

이렇게 after로 선넣은다음 -margin으로 올리기

---------------------------------------------------------------------------------------------------

크롬개발자도구

style 탭에 창을 좀만 키워보면 여백들 표시되면서 스타일 어디에서 상속된것들(line-height,font-weight:bold,text-align 등)인지 알수있음
Filter로 바로검색가능

---------------------------------------------------------------------------------------------------

크롬 주소창 자동완성기록 삭제 단축키 shift + del

---------------------------------------------------------------------------------------------------

gnb 현재위치 표식

<script>
	$(function(){
		var subPage = new Array;
		subPage[0] = "/my/main.asp";
		subPage[1] = "/my/my_qa.asp";
		subPage[2] = "/my/my_evaluation.asp";
		subPage[3] = "my/qna.asp";
		var url = location.href;
		var getAr0 = url.indexOf(subPage[0]);
		var getAr1 = url.indexOf(subPage[1]);
		var getAr2 = url.indexOf(subPage[2]);
		var getAr3 = url.indexOf(subPage[3]);
		if(getAr0 != -1){
			$(".left_menu>ul>li:eq(0)>a").addClass("on")
		};
		if(getAr1 != -1){
			$(".left_menu>ul>li:eq(1)>a").addClass("on")
		};
		if(getAr2 != -1){
			$(".left_menu>ul>li:eq(2)>a").addClass("on")
		};
		if(getAr3 != -1){
			$(".left_menu>ul>li:eq(3)>a").addClass("on")
		};
	});
</script>

---------------------------------------------------------------------------------------------------

구 달력

<input type="text" id="anDate" name="anDate" value="<%=anDate%>" class="box" style="width:100px;" maxlength="10" onClick="openCalendar(event, this, 'YYYY-MM-DD');" readOnly><img src="/images/calendar/btn_open.gif" width="15" height="13" hspace="2" onClick="openCalendar(event, 'anDate', 'YYYY-MM-DD');" id="ssssDateImg" style="cursor:pointer">

---------------------------------------------------------------------------------------------------

ftp 파일에서 검색할때 경로가 참조되어있을수있으니
잘 안찾아지면 그냥 개발자도구에서 찾는게 빠름

---------------------------------------------------------------------------------------------------

애프터워크상세

/addon/servicegoods/m/goods/content.asp

---------------------------------------------------------------------------------------------------

<input type="checkbox" id="ac-gn-menustate" class="ac-gn-menustate">

<li class="ac-gn-item ac-gn-menuicon"> <label class="ac-gn-menuicon-label" for="ac-gn-menustate" aria-hidden="true">


이렇게해노면 css로 check를 이용해서 클릭이벤트를 자바스크립트 안쓰고도 구현가능함

@media only screen and (max-width: 735px){
#ac-gn-menustate:checked~#ac-globalnav .ac-gn-list, #ac-gn-menustate:target~#ac-globalnav .ac-gn-list {
    visibility: visible;
    -webkit-transition-delay: 0s;
    transition-delay: 0s;
}

---------------------------------------------------------------------------------------------------

한 요소에 3단 테두리적용

div {
  border: 4px solid red; /* 1 */
  box-shadow: 0 0 0 8px green; /* 3 IE9+ */
  outline: 4px solid blue; /* 2 IE8+ */
}

https://codepen.io/anon/pen/YeYQrj

---------------------------------------------------------------------------------------------------

function btnLike(){

	$(".like_ani:eq(0)").clone().appendTo(".forClone")

	//.addClass("clone n"+iiiiiiiiii)

	.addClass("clone")

	setTimeout(btnLikeAni,100)

	setTimeout(btnLikeReset,1200)

}

function btnLikeAni(){

	$(".like_ani.clone").addClass("ani")

}

function btnLikeReset(){

	$(".like_ani.clone:eq(0)").fadeOut(3000).remove()

}

---------------------------------------------------------------------------------------------------

클래스 1씩 올리기

 
var iiiiiiiiii = 0

function btnLike(){

	iiiiiiiiii++

	$(".like_ani:not(.clone)").clone().appendTo(".forClone")

	.addClass("clone n"+iiiiiiiiii)

	.addClass("clone")

	setTimeout(btnLikeAni,100)

	setTimeout(btnLikeReset,3200)

}

function btnLikeAni(){

	var rMath = Math.random()*0x3;

	var rInt = parseInt(rMath)+1

	$(".like_ani.clone:last").addClass("ani"+rInt)

}

function btnLikeReset(){

	var a = $(".like_ani.clone").attr("class")

	var b = a ? a.replaceAll2("like_ani clone n","") : "1";

	var c = b ? b.replaceAll2("ani","") : "1";

	var d = c ? c.replaceAll2(" ","") : "1";

	$(".like_ani.clone:eq(0)").fadeOut(3000).remove()

	console.log(a)

	console.log(b)

	console.log(c)

	console.log(d)

}

--------------------------------------------------------------------------------------------------- 

랜덤 애니메이션 적용

 

function btnLike(){

	$(".like_ani:not(.clone)").clone().appendTo(".forClone")

	.addClass("clone")

	setTimeout(btnLikeAni,100)

	setTimeout(btnLikeReset,3200)

}

function btnLikeAni(){

	var rMath = Math.random()*0x3;

	var rInt = parseInt(rMath)+1

	$(".like_ani.clone:last").addClass("ani"+rInt)

}

function btnLikeReset(){

	$(".like_ani.clone:eq(0)").fadeOut(3000).remove()

}

---------------------------------------------------------------------------------------------------

<!DOCTYPE html> → html5버전으로 하겠단뜻 (선언)

--------------------------------------------------------------------------------------------------- 

메타태그

<meta charset="utf-8"><!--글자깨짐방지-->

<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" /><!--모바일 화면에서 zoom을 1.0 즉 확대하지도 축소하지도않은 상태로 웹페이지를 시작해라 라는 뜻--> 

<meta name="description" content="생활코딩의 소개자료"><!-- 검색엔진 -->

<meta name="keywords" content="코딩,coding,생활코딩,프로그래밍,html,css,jabascript"><!-- 카테고리 -->

<meta name="author" content="egoing"><!--저자 라는 뜻 , 닉네임 등-->

<meta http-equiv="refresh" content="30"><!-- 30초마다 refresh됨 -->

---------------------------------------------------------------------------------------------------

html 태그 연대기

http://www.martinrinehart.com/frontend-engineering/engineers/html/html-tag-history.html 

---------------------------------------------------------------------------------------------------

html 태그 통계

https://www.advancedwebranking.com/html/ 

---------------------------------------------------------------------------------------------------

용어 동의어

요소 = 엘리먼트(element) = 태그(tag)

속성(properties)

방법(methods)

콜백(callbacks)

--------------------------------------------------------------------------------------------------- 

details 태그와 summary 태그로 내용 접고펴기 (익스,파이어폭스 X)

<details><!--open 추가하면 처음에 열려있음 ex)<details open>-->
<summary>생략한 내용의 간추림</summary>
<p>부연 설명 생략해도 될만한 내용들을 summary태그 아래에 만듭니다.</p>
</details>

--------------------------------------------------------------------------------------------------- 

border-bottom 하고 border-radius 50% 넣으면 그림자생긴거처럼 할수잇다

---------------------------------------------------------------------------------------------------

페이지 로딩시 focus

<body onload="document.formName.id.focus(); //document.폼의name.인풋의name.fouce()">
해도되고

$(window).load(function(){
	document.Frm.title.focus(); //document.폼의name.인풋의name.fouce()
})
해도되고

$(window).load(function(){
	$(".inputTit").focus();
})

---------------------------------------------------------------------------------------------------

레이어 동영상팝업


<div class="slide"><a href="javascript:openMovPopup('https://youtube.com/embed/9SI3m4H_zyM');" class="wrap"><div class="img">{{BANNER:1}}</div></a></div>

function openMovPopup(url){
	$("#popMov").show();
	$("#popMov iframe").attr('src',url+'?wmode=transparent&rel=0&autoplay=1');
}
function closeMovPopup(){
	$("#popMov").hide();
	$("#popMov iframe").attr('src','');
}

---------------------------------------------------------------------------------------------------

css

inherit 상위 엘리먼트 상속 (익스8↓X)
initial 기본값 (익스X)

---------------------------------------------------------------------------------------------------

엔터칠때 이동 이벤트 onKeyDown=""
마우스 클릭시는 onclick=""


기타

keydown() - 키보드가 눌러질 때 발생
keypress() - 키보드를 누르고 있을때 계속 발생
keyup() - 키보드가 떼어질 때 발생


키 관련 함수

function blockKey(e) {
	var e = window.event || e;
	if (window.event) {
		e.returnValue = false;
	}
	else {
		if (e.which != 8) e.preventDefault(); // 8 : Back Space
	}
}

function blockEnter(e) {
	var e = window.event || e;
	if (window.event) {
		if (e.keyCode == 13) e.returnValue = false;
	}
	else {
		if (e.which == 13) e.preventDefault();
	}
}

function blockNotNumber(e) {
	var e = window.event || e;
	if (window.event) {
		if (e.keyCode < 48 || e.keyCode > 57) e.returnValue = false;
	}
	else {
		if (e.which != 8 && (e.which < 48 || e.which > 57)) e.preventDefault(); // 8 : Back Space
	}
}

function onEnter(e, exec) {
	var e = window.event || e;
	var keyCode = (window.event) ? e.keyCode : e.which;
	if (keyCode == 13) eval(exec);
}

키보드 막기
onKeyPress="blockKey(event)" onKeyDown="blockKey(event)"

---------------------------------------------------------------------------------------------------

css :target 사용법

http://micropilot.tistory.com/2515

---------------------------------------------------------------------------------------------------

슬라이드 속 내용이 어디서 불러오는것일경우(상품 등)

window.load 같은걸로 감싸서 불러온 다음에 슬라이드가 실행되게 해야함(안그럼 이상해짐)

---------------------------------------------------------------------------------------------------

슬라이드가 처음에 display:none되있는(안보였다보이는)것 속에있어서 풀리고 나서 작동이 안되면

function recSl(){
	var recent_sl = new Swiper(".recent_bg_wrap",{

	})
}

이렇게 한 후

보이게 하는 함수에다가 넣으면 (opacity 등으로 안해도)됨

$(".btn-all-menu").click(function(){
	$(".all_menu_box").addClass("open")
	recSl()
})

---------------------------------------------------------------------------------------------------

a에다 border-radius 넣으면 크롬에서 약간 짤리는 버그

---------------------------------------------------------------------------------------------------

키코드(key code) 확인 사이트
https://keycode.info/
https://www.cambiaresearch.com/articles/15/javascript-char-codes-key-codes

---------------------------------------------------------------------------------------------------

단축키만들기 기본

document.onkeydown = function(e){
  e = e||event;
  if(e.keyCode == 82) { //r 키 눌렸을 때
	실행될함수();
  }
}

---------------------------------------------------------------------------------------------------

단축키 플러그인 shortcut.js
http://www.openjs.com/scripts/events/keyboard_shortcuts/

shortcut.add("Ctrl+Enter",function() {
	alert("The bookmarks of your browser will show up after this alert...");
},{
	'type':'keydown',
	'propagate':true,
	'target':document,
	'disable_in_input':true // input이나 textarea 포커스시 실행안되게
});

---------------------------------------------------------------------------------------------------

css 화살표 / 엑스표 (1px생각해서 홀수로 하기)

.noticeWrap .more{display:inline-block;width:25px;height:25px;position:relative;}
.noticeWrap .more:before,
.noticeWrap .more:after{content:"";position:absolute;}
.noticeWrap .more:before{left:2px;right:2px;border-top:1px solid #ddd;top:50%;}
.noticeWrap .more:after{top:2px;bottom:2px;border-left:1px solid #ddd;left:50%;margin-left:-1px;}

---------------------------------------------------------------------------------------------------

line-height 초기화

1em 이나 100%

---------------------------------------------------------------------------------------------------

input박스 연노란색배경으로 나오는이유 → 크롬 비밀번호 저장기능 때문

---------------------------------------------------------------------------------------------------

안전하지않음 해결방법

돈 내고 페이지를 <https> 로 바꾸거나 ,

input type password를 text로 한다음
autocomplete=off ★속성 추가
"text-security:disc; -webkit-text-security:disc; -mox-text-security:disc; ★***표시나오게 css추가

★익스9이하는 안됨 , 크롬 비밀번호 저장기능 안됨

참고 : https://blog.naver.com/csaiur/220947330070

---------------------------------------------------------------------------------------------------

크롬 개발자도구 a태그에걸린 링크 복사하려고 클릭했을때 바로열리는거 짜증나면 18.2.6 꺼로 다운그레이드하기

다운후 주소창에서 탭으로 네이버 등 바로검색안되면 직접 네이버에서 검색 한번 하면됨

---------------------------------------------------------------------------------------------------

외부css or 내부css 로 했는데 느려서 새로고침할때 살짝 보이면 인라인으로 바꾸기 ex) style="display:none"

---------------------------------------------------------------------------------------------------

width는 안쓰면 100%니까 100%일때 굳이 쓰지않기 (padding margin 등에 개입)

---------------------------------------------------------------------------------------------------

index

$(document).ready(function(){
	$(".title_content").each(function(index){
		$(this).mouseover(function(){
			$("#titleCont_" + index).css("display", "block");
		});
		$(this).mouseout(function() {
			$("#titleCont_" + index).css("display", "none");
		});
	});
});

---------------------------------------------------------------------------------------------------

아이폰에서 불러오는js 파일 안에 있는 클릭이벤트 스크립트가 실행 안될때

불러온 파일에 빈 이벤트 한번 더 쓰기

---------------------------------------------------------------------------------------------------

WinMerge 문서비교 프로그램

---------------------------------------------------------------------------------------------------

masonry 와 비슷하게 쓸 수 있는 css

column-count:3;(퍼센트) 이나 column-width:13em; or px (반응형처럼)
column-gap:1em;

참고 : http://thrillfighter.tistory.com/570

---------------------------------------------------------------------------------------------------

스크립트로 iframe 속에 css를 적용하는 방법
https://code.i-harness.com/ko/q/352b0
https://sir.kr/qa/137576

---------------------------------------------------------------------------------------------------

if(this.getAttribute('class') == 'idxLyr'){attr  : HTML의 프로퍼티를 취급

prop : Java Script의 프로퍼티를 취급

---------------------------------------------------------------------------------------------------

제이쿼리 속성선택자

https://blog.naver.com/bog123451/221204122107 

---------------------------------------------------------------------------------------------------

자바스크립트 논리연산자

and(&&) or(||) not(!) 

http://justmakeyourself.tistory.com/45 

---------------------------------------------------------------------------------------------------

자바스크립트 해당속성 있는지 체크

if(this.hasAttribute("idxLyr")){ //해당 속성이 있는지 
if(this.getAttribute("idxLyr")){ //해당 속성의 값 ex)if(this.getAttribute("type")=="checkbox"){

참고
http://www.w3big.com/ko/jsref/met-element-hasattribute.html
https://appear.github.io/2017/09/14/JavaScript/javascript_22/  

--------------------------------------------------------------------------------------------------- 

자바스크립트로 쓸거면 자바스크립트로 쓰고 제이쿼리로 쓸거면 제이쿼리로 통일해야함

ex)
제이쿼리에서 if($(this).hasClass("idxLyr")){
이렇게 썼다면

자바스크립트에선 if(this.getAttribute("class") == "idxLyr"){
이렇게 쓴다

$(this).getAttribute() 이렇게 섞으면 안됨

addClass→addClassName참고 https://tk2rush90.blog.me/221122320046

--------------------------------------------------------------------------------------------------- 

자바스크립트 DOM

https://appear.github.io/2017/09/14/JavaScript/javascript_22/ 

---------------------------------------------------------------------------------------------------

스크립트 지역변수 매개변수로 넘기고받기

var open=function(chk,test){
	if(chk==true){
		var lyr=$(".layerFix[idxLyr='1']")
	}
}

lbtn.click(function(){
	if(this.hasAttribute("idxLyr")){
		var chk=true
		var idx=$(this).attr("idxLyr");
		open(chk,idx);
	}else{
		open();
	}
})

참고
https://kin.naver.com/qna/detail.nhn?d1id=1&dirId=1040202&docId=69605585&qb=7Iqk7YGs66a97Yq4IOuLpOuluCDtlajsiJjroZwgdmFy&enc=utf8§ion=kin&rank=38&search_sort=0&spq=0 
https://kin.naver.com/qna/detail.nhn?d1id=1&dirId=1040202&docId=65010242&qb=7Iqk7YGs66a97Yq4IOuLpOuluCDtlajsiJjroZwgdmFy&enc=utf8§ion=kin&rank=31&search_sort=0&spq=0

--------------------------------------------------------------------------------------------------- 

체크박스,라디오 > 이미지 등으로 바꾸는css

label{vertical-align:middle;display:inline-block;line-height:30px;cursor:pointer;}
label + label{padding-left:10px;}
label input[type=checkbox],label input[type=radio]{position:absolute;left:-9999px;}
label input[type=checkbox] + span{content:"";display:inline-block;width:20px;height:20px;background:url(/admin/images/sp_input.png) no-repeat -26px -26px;background-size:46px;vertical-align:middle;padding-right:3px;}
label input[type=checkbox] + span + span{vertical-align:middle;}
label input[type=checkbox]:checked + span{background-position:0 -26px;}
label input[type=checkbox]:disabled + span{opacity:.5;}
label input[type=radio] + span{content:"";display:inline-block;width:20px;height:20px;background:url(/admin/images/sp_input.png) no-repeat -26px 0;background-size:46px;vertical-align:middle;padding-right:3px;}
label input[type=radio]:checked + span{background-position:0 0;}
label input[type=radio]:disabled+ span{opacity:.5;}

--------------------------------------------------------------------------------------------------- 

요소 크기

width() : 딱 요소의 크기 순수한 크기 만큼만
.innerWidth() : width + padding
.outerWidth() : width + padding + border
.outerWidth(true) : width + padding + border + margin

--------------------------------------------------------------------------------------------------- 

input - checkbox 체크시 불들어오게 하는 스크립트

<label class="check_text ck_login cklabel mgt5 ico_label">
	<div class="iconfont ftic-success"></div>
	<input type="checkbox" id="C2"  name="EstimateType" class="ico_check" value="입점형몰인몰" style="display:none;" />
	입점형몰인몰
</label>

$(".ico_check").each(function(index){
	if(this.getAttribute("type")=="checkbox"){
		if($(this).prop("checked")){
			$(".ico_label").eq(index).find(".iconfont").addClass("sitecolor1");
		}else{
			$(".ico_label").eq(index).find(".iconfont").removeClass("sitecolor1");
		}
		$(this).change(function(){
			if($(this).prop("checked")){
				$(".ico_label").eq(index).find(".iconfont").addClass("sitecolor1");
			}else{
				$(".ico_label").eq(index).find(".iconfont").removeClass("sitecolor1");
			}
		});
	}else if(this.getAttribute("type")=="radio"){
		if($(this).prop("checked")){
			$(".ico_label").eq(index).find(".iconfont").addClass("sitecolor1");
		}else{
			$(".ico_label").eq(index).find(".iconfont").removeClass("sitecolor1");
		}
		$(this).change(function(){
			if($(this).prop("checked")){
				$(".ico_label").find(".iconfont").removeClass("sitecolor1");
				$(".ico_label").eq(index).find(".iconfont").addClass("sitecolor1");
			}else{
				$(".ico_label").eq(index).find(".iconfont").removeClass("sitecolor1");
			}
		});
	}
});

--------------------------------------------------------------------------------------------------- 

ajax 로드

$.ajax({
	url:"/page.asp?uid=2051",
	type:"POST",
	success:function(data){
		$(".clauseWrap").html(data)
	},
	error:function(){
		alert("오류가 발생하여\n로드되지 않았습니다.");
	}
})


안에 데이터만

$.ajax({
	url:"/other/licensing.asp",
	type:"POST",
	success:function(data){
		var content = $(data).find("#tbContent")
		$(".clauseWrap").html(content)
	}
})


error는 없으면 안써도됨

--------------------------------------------------------------------------------------------------- 

position:absolute 를 넣으면 자동으로 block요소가 된다 absolutea적용한 a같은 태그에 display:block/display:inline-block 쓰지말것

--------------------------------------------------------------------------------------------------- 

우클릭/드래그 방지

<body oncontextmenu="return false" ondragstart="return false" onselectstart="return false">

oncontextmenu="return false" : 우클릭 방지
ondragstart="return false" : 텍스트/이미지 등 클릭하며드래그 방지
onselectstart="return false" : 텍스트/이미지 드래그로 선택방지

--------------------------------------------------------------------------------------------------- 

드래그된 텍스트 css

::selection{}

i. 텍스트 색상 - color 속성
ii. 백그라운드 - background 속성
iii. 커서의 종류 - cursor 속성
iv. 외곽선 - outline 속성

--------------------------------------------------------------------------------------------------- 

이스케이프 코드(escape code) - html로 인식되는걸 피하기 위한 코드

&lt : <
&gt : >
&amp : &
&quot : "
&copy : ⓒ
&nbsp : 공백

참고 : http://darusamu.tistory.com/entry/HTML%EC%97%90%EC%84%9C-%EC%82%AC%EC%9A%A9%EB%90%98%EB%8A%94-quot-amp-lt-gt

--------------------------------------------------------------------------------------------------- 

안보여야 할것이 순간적으로 보였다가 사라지는거 고칠때
크롬 개발자도구에서 Network 탭 → Online 되있는거 slow 3G로 해놓고 테스트

--------------------------------------------------------------------------------------------------- 

자바스크립트 this의 이해

http://darusamu.tistory.com/entry/javascript-this%EC%9D%98-%EC%9D%B4%ED%95%B4?category=695380

--------------------------------------------------------------------------------------------------- 

		공간 차지		클릭 이벤트 사용가능여부		화면에 표시
opacity:0		     O			O			      X
visibility:hidden	     O			X			      X
display:none	     X			X			      X
position + z-index:-1   O			X		화면에 보일수도 안보일수도 있음
(inline의 부모에 text-indent:-9999px) or (inline-block/block에 직접
text-indent:-9999px)     O			X			      X

★ visibility:hidden으로 숨기면 opacity와 다르게 뒤의 것을 클릭할 수 있다
★ pointer-events:none과 opacity:0을 같이 쓰면 visibility:hidden과 똑같아진다
★ 위를 이용하면 on클래스 애니메이션 구현가능(display:none은 불가)
★ text-indent는 텍스트/before/after에 사용 가능 (before/after에 쓰려면 before/after의 대상에 걸어야함)

슬라이드요소를 한번 display:none시키면 다시 풀어도 슬라이드가 동작하지 않는데, 이를 해결하려면
position:absolute;left:9999px; 이렇게 하면 됨

그럼 display:none방식으로 했을때와 달리 focusable 할텐데

이는 자바스크립트의
document.querySelector('.slide');
slide.tabIndex = -1;

이렇게 하거나

css의 pointer-events: none; 로 제거 가능함

--------------------------------------------------------------------------------------------------- 

모바일 max-width 썼으면 그냥 width도 %로 할건지 auto로 할건지 정해야한다 안그럼 페이지마다 달라짐

--------------------------------------------------------------------------------------------------- 

원인불명 여백 확인방법

※자식 태그에 여백이 있는경우

--------------------------------------------------------------------------------------------------- 

모바일 상태표시줄 색변경 (시간,배터리나오는곳)

<meta name="theme-color" content="#원하는색상">

--------------------------------------------------------------------------------------------------- 

세로 열었다접었다 하기

$(document).on("click",".order_sender .more",function(){
	if($(this).hasClass("on")){
		$(".choice_box.sender").stop(true,true).slideUp(500,"swing")
		$(this).removeClass("on").text("expand_more")
	}else{
		$(".choice_box.sender").stop(true,true).slideDown(500,"swing")
		$(this).addClass("on").text("expand_less")
	}
})

ps) 이징효과 swing이 기본임

---------------------------------------------------------------------------------------------------

easing 효과모음

http://superkts.com/jquery/@easingEffects

linear/swing/easeInQuad/easeOutQuad/easeInOutQuad/easeInCubic/easeOutCubic/easeInOutCubic/easeInQuart/easeOutQuart/easeInOutQuart/easeInQuint/easeOutQuint/easeInOutQuint/easeInSine/easeOutSine/easeInOutSine/easeInExpo/easeOutExpo/easeInOutExpo/easeInCirc/easeOutCirc/easeInOutCirc/easeInElastic/easeOutElastic/easeInOutElastic/easeInBack/easeOutBack/easeInOutBack/easeInBounce/easeOutBounce/easeInOutBounce

---------------------------------------------------------------------------------------------------

2줄이상*2줄이상 리스트 있을때 선택한 항목에 불 들어오게 하는거

.pay_ul {overflow:hidden; background:#fff; /* margin:10px -15px; */margin:10px 0;text-align:center;}
.pay_ul table{width:100%;table-layout:fixed;margin-bottom:0;border:1px solid #ddd;border-radius:5px;}
.pay_ul tr:first-of-type td:first-of-type label{border-radius:5px 0 0 0;}
.pay_ul tr:first-of-type td:last-of-type label{border-radius:0 5px 0 0;}
.pay_ul tr:last-of-type td:first-of-type label{border-radius:0 0 0 5px;}
.pay_ul tr:last-of-type td:last-of-type label{border-radius:0 0 5px 0;}
.pay_ul tr + tr td{border-top:1px solid #ddd;}
.pay_ul td+td{border-left:1px solid #ddd;}
.pay_ul td img{max-width:100%;max-height:30px;}
.pay_ul td{height:70px;text-align:center;}
.pay_ul td label.pay_label {margin:5px;background:#f5f7f8;height:70px;line-height:20px;border:0;margin:0;position:relative;display:table;width:100%;}
.pay_ul td.on label.pay_label{z-index:10;margin:-1px;border:1px solid#FF4242;color:#FF4242;}
.pay_ul td label>span{display:table-cell;vertical-align:middle;}
.pay_ul td label span input[type=radio] + span{display:block; vertical-align:middle;height:18px;line-height:24px;font-size:11px; color:#000;background:none;width:auto;padding:0;}
.oderbottomBox .member_input{float:right; width:66%;height:46px;}
.oderbottomBox .member_input .ui-radio{display:inline-block;vertical-align:middle;margin:0;}

<div class="pay_ul">
	<table>
		<tr>
			<td class="on">
				<label for="p_1" class="pay_label">
					<span>
						<img src="/images/sample2.jpg" alt="">
						<input type="radio" id="p_1" name="payway" value="<%=CM_PAYWAY_CARD%>" class="pay_radio" onClick=" checkPayway()" checked="checked" data-role="none"/>
						<span>신용카드</span>
					</span>
				</label>
			</td>
			<td>
				<label for="p_2" class="pay_label">
					<span>
						 <img src="/images/sample2.jpg" alt="">
						<input type="radio" id="p_2" name="payway" value="<%=CM_PAYWAY_BANK%>" onClick=" checkPayway()" class="pay_radio" data-role="none"/>
						<span>실시간 계좌이체</span>
					</span>
				</label>
			</td>
		</tr>
		<tr>
			<td>
				<label for="p_3" class="pay_label">
					<span>
						<img src="/images/sample2.jpg" alt="">
						<input type="radio" id="p_3" name="payway" value="<%=CM_PAYWAY_VIRTUAL%>" onClick=" checkPayway()" class="pay_radio" data-role="none"/>
						<span>가상계좌</span>
					</span>
				</label>
			</td>
			<td>
				<label for="p_4" class="pay_label">
					<span>
						<img src="/images/sample2.jpg" alt="">
						<input type="radio" name="payway" onClick=" checkPayway()" value="<%=CM_PAYWAY_ONLINE%>" id="p_4"  class="pay_radio" data-role="none"/>
						<span>무통장입금</span>
					</span>
				</label>
			</td>
		</tr>
</table>

<script>
	$(".pay_radio").each(function(index){
		if($(this).prop("checked"))
		{
			$(this).closest("td").addClass("on");
		}else{
			$(this).closest("td").removeClass("on");
		}
	
		$(this).change(function(){
			if($(this).prop("checked")){
				$(".pay_label").closest("td").removeClass("on");
				$(this).closest("td").addClass("on");
			}
		});
	});
</script>

---------------------------------------------------------------------------------------------------

세로정렬하는 또다른 방법 (display:flex는 안에 내용물들을 감싸는 박스가 있어야하지만 이건 안쪽에 wrap 없이 알맹이들만 있어도 된다 , 하지만 webkit계열(크롬엔사파리)에서만됨 , 익스에서도 되는방법은 네이버페이 주문페이지 카드간편결제참고)

display:-webkit-box;-webkit-box-orient:vertical;-webkit-box-pack:center;

---------------------------------------------------------------------------------------------------

다른 모든 depth1_in_T on제거후 클릭한 상위에on추가

$(document).on("click",".menu-list .depth1",function(){
	$(".depth1_in_T").removeClass("on")
	$(this).closest(".depth1_in_T").addClass("on")
})

---------------------------------------------------------------------------------------------------

페이지 로드 후 좋아요 누른것 불들어오게

$(window).load(function(){
	$(".story_detail_wrap .insta_cont2 .storyArea-cont-info2 .storyArea-cont-favorite .material-icons").each(function(){
		if($(this).text()=="favorite"){
			$(this).addClass("on")
		}
	})
})

---------------------------------------------------------------------------------------------------

제이쿼리 형제중 앞쪽만 모두 선택 prevAll (뒤쪽은nextAll)

자바스크립트 텍스트를 숫자(정수)형으로 변환 parseInt

제이쿼리 텍스트를 일부 고치기 replace , 뒤에붙은10은 10진수를뜻함 , +20으로 여백까지 추가

예) 클릭시 앞쪽형제 li들의 높이 구해서 ul에다가 그만큼 스크롤되게
$(".sublist_lmenu .more").click(function(){
	var thisp = $(this).parent()
	if(thisp.hasClass("on")){
		thisp.removeClass("on")
	}else{
		var orgH = $(this).closest("li").height()
		thisp.addClass("on")
		thisp.siblings().removeClass("on")
		if($(this).closest("li").height()!=orgH){
			var height = 0;
			$(this).closest("li").prevAll("li").each(function(){
				height += parseInt($(this).css("height").replace("px",""),10)+20;
			})
			$(".sublist_lmenu ul").scrollTop(height)
		}
	}
})

---------------------------------------------------------------------------------------------------

함수안에 함수쓸때는

function fffff(){
	이렇게 하기 보다는
}

var fffff = function(){
	이렇게 하기
}

---------------------------------------------------------------------------------------------------

안에 li가 있을때만 버튼 보이게 하기

$(window).load(function(){
	$(".sublist_lmenu>ul").height($(".smartSearch .inWrap").height()-59)
	$(".sublist_lmenu .depth2").each(function(e,v){
		let tmp = $(this).children("li").length;
		if(tmp!=0){
			$(this).prev().show()
		}
	})
})

let는 '블록단위지역함수' 라고함

---------------------------------------------------------------------------------------------------

주석을 감싸 주석할때는 이렇게 표식남기기

<!--<div>
	<div>추가주석할내용</div>
	<!-<div>기존주석내용</div>->
</div>-->

---------------------------------------------------------------------------------------------------

font-size:initial 하면 익스에선 안나올 수 있음 . checking

---------------------------------------------------------------------------------------------------

ie(익스)에서 label안에 이미지 클릭시에도 체크되게

img였나 label에
onclick="if(navigator.appVersion.indexOf('MSIE') != -1){naver2.click()}"
써보고 안되면

css로 ↓
label {display:inline-block;}
label img {pointer-events:none;}

이것도 안되면 
label을 <form></form> 으로 감싸보고 그래도 안되면

스크립트 추가
$(document).ready(function(){
   if ($.browser.msie){
        $img = $('label img');
        $img.click(function(e){
	    $('#'+ $(this).parent().attr('for')).change().click();
        });
   }
});

또 안되면

$("label img").on("click",function(){
	$("#" + $(this).parents("label").attr("for")).click();
})

이렇게 변경

---------------------------------------------------------------------------------------------------

특정 클래스나 뭔가가 있을때를 체크하려면 length>0으로 하면댐

$(window).load(function(){
	if($(".smartSearch").length>0){
	}else{
	}
})

---------------------------------------------------------------------------------------------------

$(".quick_menu li:eq(0) a").attr("href","javascript:;")
$(".quick_menu li:eq(0) a").click(function(){
	layerFix(0);
})

를 아래처럼 축약가능

$(".quick_menu li:eq(0) a").attr("href","javascript:;").click(function(){
	layerFix(0);
})

---------------------------------------------------------------------------------------------------

form.action 속성
- 데이터를 수신할 서버측의 프로그램 주소(URL)
- 서버측 프로그래밍 언어로 작성된 프로그램의 주소가 온다

form.method 속성
- 데이터를 전달하는 방식(클라이언트가 서버에게 자원을 요청하는 방식)
1. GET
    - http://localhost:8090/ClientTest/ex18_ok.jsp?name=임채원&age=23
    - http://localhost:8090/ClientTest/ex18_ok.jsp?name=%EC%9E%84%EC%B1%84%EC%9B%90&age=23
    - 데이터를 전송할 URL뒤에 붙여서 보내는 방식
    - URL(256자 제한) → GET방식으로 보내는 데이터가 짤릴 위험이 있다.
    - 크기가 작은 데이터만 전송하는 방식
    - 한글 사용X → 영단어 or 숫자 정도만 전송하는 용도로 사용
    - URL?이름=값&이름=값&이름=값
                ↑물음표부터를 쿼리 스트링(Query String) 이라고 부름
2. POST
    - http://localhost:8090/ClientTest/ex18_ok.jsp
    - 데이터를 상자안에 담아서 보내는 방식
    - 전송하는 데이터가 노출이 안된다. (하지만 완전히 안보이는것은 아니기때문에 암호화 필요)
    - 전송하는 데이터의 크기에 제한이 없다.

---------------------------------------------------------------------------------------------------

css로 사다리꼴 만들기

position:absolute;left:0;top:0;width:30px;border-right:transparent 50px solid;border-left:transparent 20px solid;border-top:#333 36px solid;transform:rotate(74deg);

---------------------------------------------------------------------------------------------------

슬라이드 만들때 overflow-y나 overflow-x에 hidden 꼭 해야함 안그러면 다른 영역의 슬라이드가 깨질수 있다
잘 모르겠다면 overflow-hidden하기

---------------------------------------------------------------------------------------------------

jQuery
- Javascript 기능 집합 → 개발에 필요한 여러가지 기능을 미리 구현해서 제공
- 무거워진다고하지만 100만분의 1초라서 일반 대다수의 업무에는 거의 차이가 없음
- 크로스브라우저 지원 : Chrome, Edge, Firefox, IE, Safari, Android, iOS, and more
- 로컬참조(파일로저장) : jquery.com에서 다운받는곳에서 우클릭 → 새탭에서 링크열기 → 저장
- CDN(네트워크상의 파일을 참조) : jquery.com에서 다운받는곳에서 좌클릭 → 링크복붙
  - 네트워크트래픽 조금↓(서버운용비용감소), cdn서버가 터지면 같이터짐, 인터넷안되면 못함
- 1.x버전 : 거의 모든 브라우저 지원
- 3.x버전 : 1.x에 비해 기능 조금 추가됨, 익스등 브라우저 호환성↓
- 비압축버전에는 압축버전에는 없는 개발환경이 조금더 추가되있는데 거의 같다
- 브라우저에 탭→Network→새로고침해보면 제이쿼리가 평범하게 보이면 잘 연결된것

라이브러리 : 도구들의 모음, 새로 꾸며야 하는 집(틀이 없음)
프레임워크 : 빌트인 타입의 집(틀이 꾸며져있는 상태에서 사용만 하는 집)

---------------------------------------------------------------------------------------------------

jQuery 함수
- jQuery 함수는 css선택자를 사용해서 태그를 검색한다.
1. 태그를 검색해서 반환한다.
2. BOM or DOM 객체를 jQuery객체로 변환한다
3. jQuery() 함수의 결과는 항상 배열이다
4. jQuery() 결과에 제이쿼리 메소드를 적용하면 자동으로 내부 루프가 적용된다

---------------------------------------------------------------------------------------------------

동일한 엘리멘트를 찾았더라도 BOM/DOM과 jquery는 자료형이 다르기때문에 호환이 안됨

1. BOM(DOM)객체는 jquery기능을 사용할 수 없고
2. jquery객체는 BOM(DOM)기능을 사용할 수 없다

---------------------------------------------------------------------------------------------------

jquery 함수 형태

1. 전용 함수 ex) val()
  a. obj.test() //getter, 읽기
  b. obj.test(param) //setter, 쓰기

2. 범용 함수 ex) css()
  a. obj.test(param) //getter, 읽기
  b. obj.test(param,param) //setter, 쓰기

---------------------------------------------------------------------------------------------------

jquery 이벤트

1. 전용 이벤트 함수
  - 객체.이벤트함수명(함수명)
  $("#btn1").click(function(){
  });

2. 범용 이벤트 함수 (이벤트명이 문자열이라 변수처리 가능 → 전용이벤트보다 활용도가 아주조금더 높음)
  - 객체.bind("이벤트명",함수)
  - 객체.live("이벤트명",함수)
  - 객체.on("이벤트명",함수) ★
  $("#btn1").on("click",function(){
  });

---------------------------------------------------------------------------------------------------

animate(객체,시간)

ex)
$("#box").animate({
	width : "+=100", //(or) width : "+=100px",
	height : 200, //(or) height : "200px",
	"margin-left" : "+=50px",
	marginRight : "+=50px",
	opacity : 0
},3000);

ex)
$("#box").animate({
	width : "toggle",
	height : "toggle",
	"font-size" : "toggle"
},3000);

---------------------------------------------------------------------------------------------------

콜백 함수(Callback) - 시스템이나 환경이 호출하는 함수
  - 개발자가 부르는것이 아닌 시스템에 의해서 불려지는것 ex) setInterval

$("#btn2").click(function(){
	$("#box").hide(3000,functionm(){
		//콜백
		$("body").css("background-color","black");
		location.href = "https://google.co.kr";
	})
})


---------------------------------------------------------------------------------------------------

대부분의 jquery함수는 객체 자신을 반환한다

var temp = $("#box").css("color","white");
var temp2 = temp.css("background","gray");
temp2.css("border-width","10px");

↓↓↓

$("#box").css("color","white").
	css("background","gray")
	.css("border-width","10px");

메소드 체인

---------------------------------------------------------------------------------------------------

요소의 크기

$(".box").width() / $(".box").height() : 크기
$(".box").innerWidth() / $(".box").innerHeight() : padding 포함한 크기
$(".box").outerWidth() / $(".box").outerHeight() : padding,border 포함한 크기
$(".box").outerWidth(true) / $(".box").outerHeight(true) : padding,border,margin 포함한 크기

---------------------------------------------------------------------------------------------------

태그 속성 조작

1. BOM
  - obj.prop		//읽기
  - obj.prop = "값"		//쓰기
2. DOM
  - obj.getAttribute("prop")	//읽기
  - obj.setAttribute("prop")	//쓰기
3. jquery
  - obj.attr("prop")		//읽기
  - obj.attr("prop","값")	//쓰기

---------------------------------------------------------------------------------------------------

탬플릿 리터럴(Template Literal) - 객체 동적생성
  - ` : 역홀따옴표(back-quote, back-tick) 로 묶고 그 안에 달러/중괄호를 같이 쓴다

ex1)
var n=0;
$("#list").append(`<img src="../images/catty0${n+1}.png">`);
n++;

ex2)
var n=0;
var c = $(`<img src="../images/catty0{n}.png">`)
	.css("opacity",".5")
	.click(function(){
		$(this).hide();
	});
$("#list").append(c);
n++;

ex3)
var n=0;
var c = $(`<img src="../images/catty0{n}.png">`)
	.css({
		"opacity",".5",
		"box-shadow" : "2px 2px 2px gray"
	})
	.mouseover(function(){
		$(this).css({
			opacity : 1,
			"box-shadow" : "7px 7px 7px gray"
		});
	})
	.mouseout(function(){
		$(this).css({
			opacity : .5,
			"box-shadow" : "2px 2px 2px gray"
		});
	});
$("#list").append(c);
n++;

ex4)
var n=0;
var c = $(`<img src="../images/catty0{n}.png">`)
	.css({
		"opacity",".5",
		"box-shadow" : "2px 2px 2px gray"
	})
	.on({
		mouseover : function(){
			$(this).css({
				opacity : 1,
				"box-shadow" : "7px 7px 7px gray"
			});
		},
		mouseout : function(){
			$(this).css({
				opacity : .5,
				"box-shadow" : "2px 2px 2px gray"
			});
		});
	});
$("#list").append(c);
n++;

---------------------------------------------------------------------------------------------------

제이쿼리 메소드 https://api.jquery.com/

---------------------------------------------------------------------------------------------------

첫째 자식
eq(0) / first()

막내(마지막) 자식
eq(-1) / last()

자손중 찾기
find("선택자")

부모/자식/모든조상 (인자값으로 선택자를 넣어도 됨)
parent()/children()/parents()

형제 (매개변수로 선택자를 넣어도 됨)
prev() / next() / siblings()

filter - 찾은 범위에서 일부 구하기
ex) $("li").filter(":nth-child(2n)").css("background-color","red");

특정 요소의 다음의 모든형제요소 선택
.nextAll()

특정 요소의 이전의 모든형제요소 선택
.prevAll()

---------------------------------------------------------------------------------------------------

$(document).scrollTop() → 읽기
$(document).scrollTop(5000) → 쓰기
$(document).scrollLeft → 읽기
$(document).scrollLeft(5000) → 쓰기

ex) 스크롤 퍼센트 시각적으로 표시
#bar{width:0;height:5px;background:darkslateblue;position:fixed;left:0;top:0;}
$(window).scroll(()=>{
	var x = $(document).scrollTop() * 100 / ($(document).outerHeight() - $(window).outerHeight());
	$("#bar").css("width",x + "%");
})

ex) 스크롤 퍼센트 시각적으로 표시 - 제이쿼리로만
var bar = $("<div id='bar'></div>").css({
	width:0,
	height:"5px",
	"background-color":"cornflowerblue",
	position:"fixed",
	left:0,
	top:0
})
$(window).load(function(){
	$("body").prepend(bar);
});
$(document).scroll(function(){
	var x = $(document).scrollTop() * 100 / ($(document).outerHeight() - $(window).outerHeight());
	bar.css("width",x + "%");
});

---------------------------------------------------------------------------------------------------

사용자정의속성/사용자속성 (data-XXX)

DOM(바닐라자스)
입력 : this.dataset.asd = "1"
출력 : this.dataset.asd

jquery
입력 : $(this).data("asd","1")
출력 : $(this).data("asd")


물론 아래처럼 해도 된다

바닐라자스
입력 : .setAttribute("data-속성명","값")
출력 : .getAttribute("data-속성명")

제이쿼리
입력 : .attr("data-속성명","값")
출력 : .attr("data-속성명")

---------------------------------------------------------------------------------------------------

제이쿼리 ui

(jquery-ui.css , jquery-ui.min.js) 다운받고
https://jqueryui.com/demos/ 예제등 확인

---------------------------------------------------------------------------------------------------

드래그 기능
제이쿼리 ui > interactions > draggable

드래그
$(".cat").draggable();

y축으로만 드래그
$(".cat").draggable({
	axis:"y"
});

최소 이동거리
$(".cat").draggable({
	grid:[128,128]
});

박스안에서만 이동
<div id="box1">
	<img src="../images/catty01.png" alt="" id="cat1">
</div>
$("#cat1").draggable({
	containment:"#box1"
})

스냅(자석)
<img src="../images/catty07.png" alt="" class="cat">
<img src="../images/catty08.png" alt="" class="cat">
<img src="../images/catty09.png" alt="" class="cat">
<img src="../images/catty09.png" alt="" id="cat1">
$("#cat1").draggable({
	snap:".cat"
})

---------------------------------------------------------------------------------------------------

해당 영역에 드래그했을때 이벤트를 실행하는 기능
제이쿼리 ui > interactions > draggable

$("#cat").draggable();

$("#box").droppable({
	drop:function(){
		console.log(this);
	}
});


ex)드래그했을때 갇혔다가 더블클릭하면 나가기

$("#box").droppable({
	drop:function(){
		$(this).css("background","tomato");
		$("#cat").draggable({
			containment:"#box"
		});
	}
});

$("#cat").dblclick(function(){
	$("#box").css("background","gold");
	$("#cat").draggable({
		containment:""
	});
});

---------------------------------------------------------------------------------------------------

영역 드래그해서 크기 조절하기
제이쿼리 ui > interactions > resizable

크기조절
$("#box").resizable();

옵션
<style>
.helper{border: 1px dashed #000;}
</style>
$("#box").resizable({
	maxWidth:500, //최대넓이
	maxHeight:400, //최대높이
	minWidth:100, //최소넓이
	minHeight:100, //최소높이
	grid:[50,50], //격자
	animate:true, //드래그할때 바로 조절 안되고 마우스를 놓으면 스르륵
	helper:"helper", //애니메이트 전용 미리보기, helper클래스로 css설정
	aspectRatio:true, //종횡비 유지
	alsoResize:"#cat" //하나를 조절하면 다른것(들)도 같이 크기조정되게
});

---------------------------------------------------------------------------------------------------

리스트에서 선택한것을 조작
제이쿼리 ui > interactions > selectable

<ul id="list1">
	<li>사과</li>
	<li>바나나</li>
	<li>포도</li>
	<li>오렌지</li>
	<li>자두</li>
</ul>

<script type="text/javascript">
	$("#list1").selectable();

</script>

ul에는 ui-selectable 클래스
li에는 ui-selectee 클래스가 붙고
li선택하면 ui-selected 클래스가 추가됨


세부 사용법 https://api.jqueryui.com/selectable/#event-selected

ex) 선택한사람(이미지)의 투명도가 바뀌고 정보 출력
<style>
#list3 img{cursor: pointer;opacity: 0.2;}
#list3 img:hover{opacity: 0.5;}
#list3 img.ui-selected{opacity: 1;}
</style>

<div id="list1">
	<img src="../images/man_01.png" alt="">
	<img src="../images/man_02.png" alt="">
	<img src="../images/man_03.png" alt="">
	<img src="../images/woman_01.png" alt="">
	<img src="../images/woman_02.png" alt="">
	<img src="../images/woman_03.png" alt="">
</div>
$("#list1").selectable({
	selected:function(event,ui){
		console.log($(ui.selected).index())
		alert(
			"이름 : " + mlist[$(ui.selected).index()].name + "\n" +
			"나이 : " + mlist[$(ui.selected).index()].age + "\n" +
			"직급 : " + mlist[$(ui.selected).index()].pos
		);
	}
});

var mlist = [
	{
		name:"송중기",
		age:30,
		pos:"과장"
	},
	{
		name:"박보검",
		age:28,
		pos:"과장"
	},
	{
		name:"이승기",
		age:33,
		pos:"부장"
	},
	{
		name:"신세경",
		age:28,
		pos:"부장"
	},
	{
		name:"한가인",
		age:29,
		pos:"대리"
	},
	{
		name:"이열음",
		age:27,
		pos:"사원"
	},
];

---------------------------------------------------------------------------------------------------

리스트에서 드래그로 순서 바꾸기
제이쿼리 ui > interactions > sortable

$("#list1").sortable();

ex) 바뀌기 전 index구하기
<div id="list3">
	<img src="../images/man_01.png" alt="" data-no="1">
	<img src="../images/man_02.png" alt="" data-no="2">
	<img src="../images/man_03.png" alt="" data-no="3">
	<img src="../images/woman_01.png" alt="" data-no="4">
	<img src="../images/woman_02.png" alt="" data-no="5">
	<img src="../images/woman_03.png" alt="" data-no="6">
</div>

<input type="button" value="순서 확인" id="btn1">

$("#list3").sortable();
$("#btn1").click(function(){
	$("#list3").children().each(function(index,item){
		console.log($(item).data("no"));
	});
});

---------------------------------------------------------------------------------------------------

아코디언 메뉴
제이쿼리 ui > widgets > accordion

<div id="a1">
	<h3>Lorem, ipsum, dolor.</h3>
	<div>Lorem ipsum dolor sit amet</div>
	<h3>Labore, veritatis, minima.</h3>
	<div>Atque, soluta at suscipit, eveniet</div>
	<h3>Tenetur dicta, eum.</h3>
	<div>Perferendis rerum dolor facere</div>
</div>
<script>
	$("#a1").accordion({
		collapsible:true //어느 하나도 미리 안 펼저져 있게
	});
</script>

---------------------------------------------------------------------------------------------------

버튼 ui
제이쿼리 ui > widgets > button

$(".btn").button();
$("b1").controlgroup(); 자식 엘리먼트들이 서로 붙게됨


체크박스/라디오 ui
제이쿼리 ui > widgets > checkboxradio

$(".cb").checkboxradio();
$(".cb").controlgroup(); 자식 엘리먼트들이 서로 붙게됨


프로그래스 바 (=html5 progress태그)
제이쿼리 ui > widgets > progressbar

$("#p1").progressbar({
	value:30 //현재값
})


셀렉트(select/option) ui
제이쿼리 ui > widgets > selectmenu
$("#sel1").selectmenu(); //select태그에 걸기


숫자조절ui (=html5 input:number태그)
제이쿼리 ui > widgets > spinner

<input type="text" id="age">
$("#age").spinner({
	min:0,
	max:100,
	step:10
});


슬라이드바 (=html5 input:range태그)
제이쿼리 ui > widgets > slider

<div id="slider1"></div> <!--range 영역-->
<div id="slider1value"></div> <!--선택한 값이 나올영역-->

$("#slider1").slider({
	slide:function(event,ui){
		$("#slider1value").text(ui.value);
	},
	min:0, //최솟값
	max:1000, //최댓값
	value:500, //기본값
	stop:100 //단계(미지정시 1)
});

ex) 사용자 rgb설정에 따른 배경색 변경
#color > div{width:500px;margin:15px 0px;height:5px;}
#color > div > span{width:20px;height:13px;}
<div id="color">
	<div></div>
	<div></div>
	<div></div>
</div>
$("#color > div").slider({
	min:0,
	max:255,
	value:255,
	step:1,
	slide:function(event,ui){
		var r = $("#color>div:eq(0)").slider("value");
		var g = $("#color>div:eq(1)").slider("value");
		var b = $("#color>div:eq(2)").slider("value");

		$("body").css("background",`rgb(${r},${g},${b})`)
	},
});

ex) 쇼핑몰 가격범위 다중value로 구현
$("#slider5").slider({
	range:true,
	min:1000,
	max:1000000,
	values:[200000,500000],
	step:100000,
	//slide:움직이는 동안
	//change:움직임이 끝난후
	change:function(event,ui){
		console.log("최저가 : ",ui.values[0]);
		console.log("최고가 : ",ui.values[1]);
	}
});


title툴팁 ui
제이쿼리 ui > widgets > checkboxradio

$("#age").tooltip({ //title이 들어있는 엘리먼트 지정
	track:true,
	show:{
		effect:"slideDown"
	},
	hide:{
		effect:"explode"
	}
});


탭 ui
제이쿼리 ui > widgets > tabs

<div id="tab1">
	<ul>
		<li><a href="#page1">HTML</a></li>
		<li><a href="#page2">CSS</a></li>
		<li><a href="#page3">JavaScript</a></li>
	</ul>
	<div id="page1">
		<h1>HTML</h1>
		<p>amet consectetur adipisicing
			<hr>
			<input type="button" value="CSS 보기" id="btnNext"> 
		</p>
	</div>
	<div id="page2">
		<h1>CSS</h1>
		<p>Lorem ipsum dolor</p>
	</div>
	<div id="page3">
		<h1>JavaScript</h1>
		<p>dolor sit amet</p>
	</div>
</div>

$("#btnNext").click(function() {
	$("#tab1").tabs({
		active: 1
	});
});

---------------------------------------------------------------------------------------------------

날짜선택 ui
제이쿼리 ui > widgets > datepicker

$("#date1").datepicker({
	dateFormat: "yy-mm-dd",
	// minDate : "2021-01-10",
	// maxDate : "2021-01-29",
	// minDate : "-5",
	// maxDate : "+5",
	// minDate : "-1m",
	// maxDate : "+1m",
	minDate : "-1m 5d",
	maxDate : "+1m 5d",
});

div말고 텍스트상자에도 적용 가능 (선택된날짜가 dateFormat옵션에 추가한 형식으로 찍힘)

---------------------------------------------------------------------------------------------------

대화상자 팝업ui
제이쿼리 ui > widgets > dialog

<input type="button" value="확인" id="btn5">
<div id="dialog">안녕하세요. 한가인입니다</div>

$("#btn5").click(function(){
	$("#dialog").dialog({
		title:"제목입니다", //제목
		width:300, //넓이
		height:250, //높이
		draggable:false, //드래그 방지
		resizable:false, //크기조절 방지
		modal:true //부모 클릭 방지 (모달팝업)
		buttons:{ //버튼 객체 생성
			"Save":function(){
				alert("저장 완료");
			},
			"Cancel":function(){
				$("#dialog").dialog("close");
			}
		}
	});
});

tmi
1. modal (ex. 메모장 ctrl+g)
- 자식창이 보일때 부모창이 포커스를 가질 수 없는 상태
- 자식의 업무가 끝나야 부모로 돌아갈 수 있다.
- 부모 → 자식 → 부모 : 시퀀스 업무
2. modeless (ex. 메모장 ctrl+f)
- 자식창이 보여도 부모창이 포커스를 가질 수 있는 상태
- 부모의 업무와 자식의 업무를 병행 가능

---------------------------------------------------------------------------------------------------

차트

1. 하이차트 https://www.highcharts.com/
2. 구글차트 https://developers.google.com/chart

---------------------------------------------------------------------------------------------------

부트스트랩 (jqueryUI랑 한 페이지에서 같이쓰지말것)

- 디자인프레임워크(jqueryUI + 디자인 확장)
- 반응형 웹디자인 제공
- jQuery 기반
- 트위터에서 만듬
- http://getbootstrap.com : 공식 (4.X ~ 5.X beta)
- http://bootstrapk.com : 번역 (3.X)


기타 디자인 프레임워크
1. Foundation
2. Pure
3. Semantic UI
4. Materialize CSS
6. Skeleton

---------------------------------------------------------------------------------------------------

에디트플러스 여러파일 찾기

서버 또는 로컬 폴더 우클릭 → 디렉토리에서 찾기

찾을 말 : 찾을단어
파일 종류 : *
제외(이미지파일 제거용, 세미콜론으로 구분) : *.gif; *.jpg; *.jpeg; *png; *.bmp
폴더 : 우클릭해서 들어왔다면 선택되있음

하위 폴더 포함 체크

---------------------------------------------------------------------------------------------------

css로 그린 여러가지 도형
https://css-tricks.com/the-shapes-of-css/

css 별모양 (transform:scale로 크기조절)
#star-five{margin:50px 0;position:relative;display:block;color:red;width:0px;height:0px;border-right:100px solid transparent;border-bottom:70px solid red;border-left:100px solid transparent;transform:rotate(35deg);}
#star-five:before{border-bottom:80px solid red;border-left:30px solid transparent;border-right:30px solid transparent;position:absolute;height:0;width:0;top:-45px;left:-65px;display:block;content:'';transform:rotate(-35deg);}
#star-five:after{position:absolute;display:block;color:red;top:3px;left:-105px;width:0px;height:0px;border-right:100px solid transparent;border-bottom:70px solid red;border-left:100px solid transparent;transform:rotate(-70deg);content:'';}

css로 디자인한 여러가지 라디오버튼
https://www.sliderrevolution.com/resources/styling-radio-buttons/


체크박스 심플디자인

.funkyradio label{box-sizing:border-box;cursor:pointer;-webkit-user-select:none;-moz-user-select:none;-ms-user-select:none;user-select:none;}
.funkyradio input[type="checkbox"]:empty{position:absolute;left:-9999px;}
.funkyradio input[type="checkbox"]:empty ~ span{display:inline-block;width:20px;height:20px;line-height:18px;border:1px solid #ddd;}
.funkyradio input[type="checkbox"]:empty ~ span:before{content:'\2714';font-size:14px;color:#C2C2C2;}
.funkyradio input[type="checkbox"]:not(:checked) ~ span{background:#eee;border:1px solid #ddd;}
.funkyradio input[type="checkbox"]:checked ~ span{background:#337ab7;}
.funkyradio input[type="checkbox"]:checked ~ span:before{color:#fff;}
.funkyradio input[type="checkbox"]:focus ~ span:before {box-shadow:0 0 0 3px #999;}

---------------------------------------------------------------------------------------------------

라디오,체크박스 도장찍히는 별디자인

.star-five {margin:50px 0;position:relative;display:block;color:<%=cstColor1%>;width:0px;height:0px;border-right:100px solid transparent;border-bottom:70px solid <%=cstColor1%>;border-left:100px solid transparent;transform:rotate(35deg);pointer-events:none;}
.star-five:before {border-bottom:80px solid <%=cstColor1%>;border-left:30px solid transparent;border-right:30px solid transparent;position:absolute;height:0;width:0;top:-45px;left:-65px;display:block;content:'';transform:rotate(-35deg);}
.star-five:after {position:absolute;display:block;color:<%=cstColor1%>;top:3px;left:-105px;width:0px;height:0px;border-right:100px solid transparent;border-bottom:70px solid <%=cstColor1%>;border-left:100px solid transparent;transform:rotate(-70deg);content:'';}

.radio .star-five,
.checkbox .star-five{transform:rotate(35deg) scale(.08);position:absolute;left:-94px;top:-86px;}
.radio label, .checkbox label{padding-left:15px;}
.radio label:nth-of-type(1),
.checkbox label:nth-of-type(1){padding-left:0;margin-left:0;}
.checkbox label:after, 
.radio label:after {content:'';display:table;clear:both;}
.checkbox .cr,
.radio .cr {position:relative;display:inline-block;border:1px solid #a9a9a9;border-radius:.25em;width:20px;height:20px;display:inline-block;margin-right:5px;box-sizing:border-box;}
.radio span{vertical-align:middle;}
.radio .cr {border-radius:50%;}
.checkbox .cr .cr-icon,
.radio .cr .cr-icon {position:absolute;font-size:.8em;border-color:<%=cstColor1%>;line-height:0;top:55%;left:15%;}
.radio .cr .cr-icon {margin-left:0.04em;}
.checkbox label input[type="checkbox"],
.radio label input[type="radio"] {display:none;}
.checkbox label input[type="checkbox"] + .cr > .cr-icon,
.radio label input[type="radio"] + .cr > .cr-icon {transform:scale(3) rotateZ(-20deg);opacity:0;transition:all .3s ease-in;}
.checkbox label input[type="checkbox"]:checked + .cr,
.radio label input[type="radio"]:checked + .cr{border-color:#486BB8;}
.checkbox label input[type="checkbox"]:checked + .cr > .cr-icon,
.radio label input[type="radio"]:checked + .cr > .cr-icon {transform:scale(1) rotateZ(0deg);opacity:1;}
.radio label input[type="radio"]:disabled + .cr {opacity:.5;}

<div class="radio">
	<label><input type="radio" name="gender"><span class="cr"><span class="cr-icon"><span class="star-five"></span></span></span>남자</label>
	<label><input type="radio" name="gender"><span class="cr"><span class="cr-icon"><span class="star-five"></span></span></span>여자</label>
</div>

---------------------------------------------------------------------------------------------------

리턴을 활용하면

function submit(){
	if ($("input[name='subject']").val() == "") {
		alert("제목을 입력하세요.")
	}else{
		if ($("textarea").val() == "") {
			alert("내용을 입력하세요.")
		}
	}
}

이렇게 써야될걸 아래처럼 쓸 수 있다

function submit(){
	if ($("input[name='subject']").val() == "") {
		alert("제목을 입력하세요.")
		return;
	}
	if ($("textarea").val() == "") {
		alert("내용을 입력하세요.")
		return;
	}
}

---------------------------------------------------------------------------------------------------

a태그의 링크를 레이어팝업으로 띄우는 플러그인

ColorBox (http://www.jacklmoore.com/colorbox/)
LightBox (http://leandrovieira.com/projects/jquery/lightbox/)
LightBox2 (http://lokeshdhakar.com/projects/lightbox2/)
FancyBox (http://fancybox.net/)
PrettyPhoto (http://goo.gl/3Qmy)

<li><div class="con"><a href="images/ps/work07.gif"><img src="images/ps/work07.gif"><h3>Click</h3></a></div></li>
$(".group1").colorbox({rel:'group1'})

아래처럼도 사용가능
$(".sct3 li a").each(function(){
	$(this).colorbox();
});

---------------------------------------------------------------------------------------------------

background 스크롤 스크립트(스크롤따른 배경 위치 변경)
https://jos39.tistory.com/246

window.onload = function(){
$('.img-holder').imageScroll({
	image:null, //이미지경로를 data-image속성에 넣는대신 이곳에 넣어도 됨
	imageAttribute:'image',
	container:$('body'),
	speed:0.2, //스크롤당 이동거리
	coverRatio:0.75, //확대/축소배율(화면넓이/높이기준)
	holderClass:'imageHolder', //생성되는 요소의 클래스
	holderMinHeight:200, //확장높이
	extraHeight:0, //높이조절(픽셀)
	mediaWidth:1420, //원본이미지 넓이
	mediaHeight:756, //원본이미지 높이
	parallax:true,
	touch:false
});
}

---------------------------------------------------------------------------------------------------

스크롤따른 배경 변경 (스크롤 오버레이)
https://nykim.work/31

---------------------------------------------------------------------------------------------------

transform:translate3d(-50%, 0, 0);	//수평이동
transform:translate3d(0, -50%, 0);	//수직이동

위 속성 사용으로
기존 margin : - 넓이/높이의 반을 구해서 땡기는것을 대체가능(텍스트등 크기가 가변일때 유용)

애니매이션 사용시에는 조작하기 어려우므로 margin으로 하기

---------------------------------------------------------------------------------------------------

svg태그이용하면 다양한 도형을 만들 수 있다
https://ossam5.tistory.com/112

---------------------------------------------------------------------------------------------------

css 문법 이클립스css파일에서 보면 찾기 좋음

---------------------------------------------------------------------------------------------------

Uncaught SyntaxError: Invalid or unexpected token

인코딩 문제일 가능성 다분

---------------------------------------------------------------------------------------------------

이미지 로딩 미루기 (사이트 최적화)

<html> 이미지태그 src대신 data-src , "lazy" class 추가 (src속성은 페이지 어디에있든 무조건 로드를 시킴)
<img class="zoom_in lazy" data-src="https://imchaewon.github.io/screenshot/spring/아이디찾기-1.png" data-zoom-image="https://imchaewon.github.io/screenshot/spring/아이디찾기-1.png">

<js>
document.addEventListener("DOMContentLoaded", function() {
	var lazyloadImages;		

	if ("IntersectionObserver" in window) {
		lazyloadImages = document.querySelectorAll(".lazy");
		var imageObserver = new IntersectionObserver(function(entries, observer) {
			entries.forEach(function(entry) {
				if (entry.isIntersecting) {
					var image = entry.target;
					image.src = image.dataset.src;
					image.classList.remove("lazy");
					imageObserver.unobserve(image);
					
					/*setTimeout(function(){
						cutImgBox();
					},100)*/
				}
			});
		});

		lazyloadImages.forEach(function(image) {
			imageObserver.observe(image);
		});
	} else {
		var lazyloadThrottleTimeout;
		lazyloadImages = document.querySelectorAll(".lazy");
		
		function lazyload () {
			if(lazyloadThrottleTimeout) {
				clearTimeout(lazyloadThrottleTimeout);
			}		

			lazyloadThrottleTimeout = setTimeout(function() {
				var scrollTop = window.pageYOffset;
				lazyloadImages.forEach(function(img) {
						if(img.offsetTop < (window.innerHeight + scrollTop)) {
							img.src = img.dataset.src;
							img.classList.remove('lazy');
						}
				});
				if(lazyloadImages.length == 0) {
					document.removeEventListener("scroll", lazyload);
					window.removeEventListener("resize", lazyload);
					window.removeEventListener("orientationChange", lazyload);
				}
			}, 20);
		}
		document.addEventListener("scroll", lazyload);
		window.addEventListener("resize", lazyload);
		window.addEventListener("orientationChange", lazyload);
	}
});



<속성>
$("img.lazy").lazyload({
	effect : "fadeIn", // 나타날때 Fadein 효과
	threshold : 200, // 스크롤 200 픽셀 전에 미리 로딩
	event:"click" // 클릭시에 로딩
	placeholder:"img/loading.gif" // 로딩전 보여줄 이미지 설정
	// ... 등등
});

https://appelsiini.net/projects/lazyload/
http://blog.fuplay.net/archives/19

---------------------------------------------------------------------------------------------------

로딩이미지(gif/svg/css)
https://loading.io/
https://loading.io/spinner/

css
https://projects.lukehaas.me/css-loaders/

---------------------------------------------------------------------------------------------------

흘러가는 슬라이드
https://www.jqueryscript.net/animation/Carousel-Style-Content-Ticker-Plugin-with-jQuery-Carousel-Ticker.html

---------------------------------------------------------------------------------------------------

카카오 api 쓸때 다음과 같은 오류 나면
'kakao' is not defined`

[발급받은 APP KEY를 사용하세요] 자리에 발급받은 키값을 넣어야한다
https://developers.kakao.com/console/app들어가서 JavaScript키 넣기 (928a6c45f558ef11e74ba2c15c0c484f)


카카오 api 라이브러리 여러개 쓰기
<script type="text/javascript" src="//dapi.kakao.com/v2/maps/sdk.js?appkey=자기 앱 키&libraries=services,clusterer,drawing"></script>

---------------------------------------------------------------------------------------------------

$ is not defined → 제이쿼리 연결 안해서 발생하는 오류

---------------------------------------------------------------------------------------------------

input text 등에서 특정키(엔터)입력할때 함수 실행

<input type="text" id="addr" placeholder="주소를 입력하세요" onKeypress="javascript:if(event.keyCode==13)searchAddr()">

---------------------------------------------------------------------------------------------------

input요소 자동완성 기능 해제 속성

<input type="" autocomplete="off">

---------------------------------------------------------------------------------------------------

text() / html() 차이

<div class="asd">
	<p class="ccc">zxc</p>
</div>

<읽기>
$(".asd").text() → '\n\n\n\tzxc'
$(".asd").html() → '\n\n\n\t<p class="ccc">zxc</p>'
$(".ccc").text() → 'zxc'
$(".ccc").html() → 'zxc'

<쓰기>
$(".asd").html("<span class='sss'>xxx</span>");
↓↓↓
<div class="asd">
	<span class="sss">xxx</span>
</div>

$(".asd").html("<span class='sss'>xxx</span>");
↓↓↓
<div class="asd"><span class="sss">xxx</span></div> → 문자열로 출력됨(<div class="asd">&lt;span class='sss'&gt;xxx&lt;/span&gt;</div>)

$(".asd").html("rrr")
↓↓↓
<div class="asd">rrr</div>

$(".asd").text("rrr")
↓↓↓
<div class="asd">rrr</div>

---------------------------------------------------------------------------------------------------

익스에서 localhost안될때

http:// 까지 쓰면 됨
http://localhost:8080/

---------------------------------------------------------------------------------------------------

form태그내 모든요소에서 / 일부요소에서 자동완성기능 해제하는 속성 → autocomplete="off"

---------------------------------------------------------------------------------------------------

데이터를 submit대신 ajax로 보내기위해 form태그안의 모든 폼요소를 문자열로 묶어서 보낼때

$("폼").serialize();

---------------------------------------------------------------------------------------------------

폼요소는 제이쿼리 선택자로 여러개를 갖고올수없음 ( = 체크박스/라디오가 둘 이상있을때 뭘 체크했는지 알 수 없음)

뭘 체크했는지 판별하려면 바닐라자바스크립트로
document.폼이름.checkbox/radio이름

그리고 스크립트로 스타일 못줌

---------------------------------------------------------------------------------------------------

라디오 체크막기
onclick="return(false)"

---------------------------------------------------------------------------------------------------

each문 내에서 break 쓸때 return false 로 해야함

lyr.each(function(){
	console.log($(this));
	if ($(this).attr("layeridx") == idx){
		lyr = $(this);
		return false; // break 불가
	}
});

---------------------------------------------------------------------------------------------------

스와이퍼 슬라이드 lazy load (슬라이드를 넘겼을때 이미지가 로드되게)

for (var i=0; i<courseLen; i++) {
	courseHtml += '			<li class="swiper-slide">';
	courseHtml += '				<em>'+(i+1)+'</em>';
	courseHtml += '				<a href="/detail/detail_view.do?cotid='+courseCotIdList[i]+'">';
	courseHtml += '					<img class="img swiper-lazy" data-src="'+mainimgurl+courseImgIdList[i]+'&mode=custom&height=180'+'"style= "50% 50%; cover no-repeat;">';
	courseHtml += '					<div class="tit"><span>'+courseList[i]+'</span></div>';
	courseHtml += '				</a>';
	courseHtml += '			</li>';
}

var swiper = new Swiper('.cos_wrap .swiper-container', {
	pagination: {
		el: '.swiper-pagination',
		type: 'fraction',
	},
	navigation: {
		nextEl: '.swiper-button-next',
		prevEl: '.swiper-button-prev',
	},
	slidesPerView: 4.5, //4.5 개 보임
	slidesPerGroup: 4.5, //4.5 개씩 넘어감
	preloadImages: false,
	lazyLoading: true,
	lazy: {
		loadPrevNext: true,
		loadOnTransitionStart : true,
		//loadPrevNextAmount : 2
	}
});

---------------------------------------------------------------------------------------------------

css grid

flex가 1차원 레이아웃 시스템이라면
grid는 2차원 레이아웃 시스템이다

12를 100%로 비율을 조절 가능


<쓰는법>

부모에 display:grid 를 넣고 시작

- 컨테이너에 적용하는 속성
grid-template-rows : 행(row)의 배치
grid-template-columns : 열(column)의 배치
ex)
grid-template-columns: 200px 200px 500px; // 200px 200px 500px; 크기로 컬럼을 만들겠다
grid-template-columns: 1fr 1fr 1fr; // 1:1:1 비율로 컬럼 3개를 만듦
grid-template-columns: 100px 2fr 1fr; // 첫번째 컬럼은 100px로 고정되고 나머지는 유연하게 1:1비율로 조절

repeat(반복횟수, 반복값) : 반복되는 값을 자동으로 처리할 수 있는 함수(엑셀의 그것과 비슷)
repeat(5, 1fr) → 1fr 1fr 1fr 1fr 1fr
grid-template-columns: repeat(5, 1fr); 이렇게 활용

minmax 함수
최솟값과 최댓값을 지정할 수 있는 함수입니다.
minmax(100px, auto)의 의미는 최소한 100px, 최대는 자동으로(auto) 늘어나게.. 입니다. 즉 아무리 내용의 양이 적더라도 최소한 높이 100px은 확보하고, 내용이 많아 100px이 넘어가면 알아서 늘어나도록 처리해 준 예시입니다.
grid-template-rows: repeat(3, minmax(100px, auto));

- 아이템에 적용하는 속성



https://studiomeal.com/archives/533 참고해서 나중에 시간날때 정리하기

---------------------------------------------------------------------------------------------------

inline/inline-block요소가 넓이 벗어나도 줄 안바뀌게 해주는거 (가로스크롤 만들때 쓸수있음)

부모 요소에
white-space:nowrap

float은 안됨. inline 또는 inline-block만 가능

---------------------------------------------------------------------------------------------------

슬라이드가 되었을때 이벤트

var swiper = new Swiper('.swiper-container', {
  speed: 500,
   navigation: {
    nextEl: '.swiper-button-next',
    prevEl: '.swiper-button-prev',
  },
  pagination: {
    el: '.swiper-pagination',
    type: 'bullets',
    clickable: true,
  },
  on: {
    slideChange: function () {
      alert('슬라이드 변경');
    }
  }
});

---------------------------------------------------------------------------------------------------

라디오버튼 value속성 안넣으면

폼태그 전송(.serialize())시 아무거나체크했다면 'on'이라고 나옴.

<radio> 태그마다 value속성 각각 넣기

---------------------------------------------------------------------------------------------------

form요소 name에 -쓰면
자바스크립트 DOM으로 접근이 안됨. _나 카멜로 쓰기

---------------------------------------------------------------------------------------------------

이미지 업로드 검사 (미리보기 포함)

const writingThumbnail = writingForm.find('#writing-thumbnail-image').val();
const writingThumbnailVal = writingThumbnail.slice(writingThumbnail.indexOf(".") + 1).toLowerCase();
if (writingThumbnailVal != "jpg" && writingThumbnailVal != "png" && writingThumbnailVal != "jpeg" && writingThumbnailVal != "jpe") {
	alert('이미지는 jpg, png, jpeg, jpe 파일로만 업로드 가능합니다.');
	writingThumbnailVal.focus();
	return;
}

const writingFileSize = writingForm.find("input[type='file']")[0].files[0].size;
const writingLimitSize = 4 * 1024 * 1024;
if (writingFileSize > writingLimitSize) {
	alert("4MB 이하 사진 파일만 업로드 가능합니다.");
	return false;
}

// input file 미리보기
function readInputFile(input) {
	if (input.files && input.files[0]) {
		var reader = new FileReader();
		reader.onload = function (e) {
			$('.file-upload-preview').html("<img src=" + e.target.result + ">");
		}
		reader.readAsDataURL(input.files[0]);
	}
}

$(".file-upload").on('change', function () {
	readInputFile(this);
});

---------------------------------------------------------------------------------------------------

한 이벤트에서 ajax로 데이터 수신후 얻은 결과값을

다른 이벤트에서 이용하고싶을때

전역변수로 하면 스코프 문제로 변수이용이 안되는듯 하고
EVD_ID = JSON.parse(result.responseText).body.EVD_ID;
$(body).append("<input type='hidden' id='EVD_ID' value='" + EVD_ID + "'>");

이런식으로 쓰면 됨. (값이 클라이언트에 노출되지 않게 해야하는건 이렇게 하면 안될듯 (비밀번호 등?) )

---------------------------------------------------------------------------------------------------

<meta property="og:url" 

meta태그 카카오톡 앱(pc,m) 링크 공유시 보여지는 제목/내용/이미지 설정

<meta property="og:url" content="https://dev.ktovisitkorea.com/detail/event_detail.do?cotid=<%=ccotid%>" />

-----

카톡에서 공유이미지 안나올경우 og:image 제거하면 나올수도

---------------------------------------------------------------------------------------------------

html 태그들을 다른영역에 옮기기 / 복사하기

(function(){
	var postArea = $(".post_area").clone(); // 복사 말고 그냥 이동을 하려면 .clone() 안써도됨
	console.log("postArea........");
	console.log(postArea);
	$(".tit_cont").hide();
	$("#contents").prepend('<img src="https://cdn.visitkorea.or.kr/img/call?cmd=VIEW&amp;id=3b38f4af-0a2d-47ea-8ea6-064513874b05" style="width:100%; max-width:940px; margin-bottom:1%;">');

	var html = "";

	html += '<div class="bot_post_wrap">';
	html += '</div>';

	$("#contents").append(html);
	postArea.appendTo(".bot_post_wrap");
})();

---------------------------------------------------------------------------------------------------

meta태그로 자동으로 페이지 이동하기

<meta http-equiv="Refresh" content="3;url=이동할주소">


ex) 3초뒤에 login.html로 이동
<meta http-equiv="Refresh" content="3;url=login.html">

ex) 5초뒤에 http://www.naver.com로 이동
<meta http-equiv="refresh" content="5; url=http://www.naver.com">

---------------------------------------------------------------------------------------------------

클릭시 요소를 캡처해서 저장하는 플러그인 - html2canvas
html2canvas.min.js 다운

★클릭시 다운로드 및 서버에 이미지 저장 (base64형식에서 FromData(blob)로 바꿔서 서버에저장함)
$("#btn_download").click(function(e) {
	var imgBase64;
	html2canvas(document.querySelector("#imagetotal")).then(function(canvas) {
		useCORS: true;
		var el = document.createElement("a");
		imgBase64 = canvas.toDataURL("image/png");
		el.href = imgBase64;
		el.download = '나의옷차림.png';
		el.click();
	});
});

★클릭시 서버에 저장
$("#btn_share").click(function(e) {
	imgSave().then((result)=>{
		let imgId = result;
		console.log("imgId: " + imgId);
	});
});

function imgSave(){
	return html2canvas(document.querySelector("#imagetotal")).then(function(canvas) {
		let imgBase64 = canvas.toDataURL("image/png", "image/octet-stream");

		const decodImg = atob(imgBase64.split(',')[1]);
		let array = [];
		for (let i = 0; i < decodImg.length; i++) {
			array.push(decodImg.charCodeAt(i));
		}
		const file = new Blob([new Uint8Array(array)], {type: 'image/png'});
		const fileName = 'canvas_img_' + new Date().getMilliseconds() + '.png';
		let formdata = new FormData();
		formdata.append("file", file, fileName);

		let imgSaveResultData = imgServerSave(formdata);

		let imgPath = JSON.parse(imgSaveResultData.responseText).body.result[0].fullPath;
		if(imgPath === null || imgPath === "") return;
		let result = setUploadImg(imgPath);
		return result.responseJSON.body.imgId;
	});
}

function imgServerSave(image){
	return $.ajax({
		url: "https://dev.ktovisitkorea.com/img/call"+"?isUserUpload=true&inflow=dress",
		// url: mainUploadUrl + "?isUserUpload=true&inflow=dress",
		type: 'POST',
		cache : false,
		contentType: false,
		processData: false,
		data:image,
		success: function (result) {},
		async:false
	});
}

function setUploadImg(imgPath){
	let cmd = "RECOM_IMAGE_SAVE";
	return $.ajax({
		url: mainurl + '/call',
		dataType: 'json',
		type: 'POST',
		data: {
			"cmd" : cmd,
			"imgPath": imgPath
		},
		success: function(result) {
		},
		complete: function() {},
		error: function(xhr, textStatus, errorThrown) {},
		async:false
	});
}

외부 이미지는 캡처가 안됨(앞에 프로토콜 붙은거 → http://~~). 하려면 proxy를 사용해야 한다고 함. css속성중 캡처가 안되는 속성도 있다고 함.
선택한 dom요소 밖의 이미지(background로 뒤에 깔린 이미지)는 캡처가 안됨. 선택한 요소의 내부이미지들만 캡처됨

참고: https://myhappyman.tistory.com/156
참고2: https://tod2.tistory.com/174

---------------------------------------------------------------------------------------------------

사파리에서는 backgroud 속성에 background-image 만 씌워서 배걍이미지를 바꿀 수 없음

background 속성 전체를 바꿔야함

---------------------------------------------------------------------------------------------------

가상선택자(after/before)의 경우 기술적으로 DOM에 속해있지 않아

제이쿼리로는 선택할 수 없음

css에 다른 가상선택자를 미리 정의해두고 클래스를 바꾸거나, 가상선택자 자체를 제이쿼리로 추가하는 등 다른방법을 써야함
https://stackoverflow.com/questions/5041494/selecting-and-manipulating-css-pseudo-elements-such-as-before-and-after-usin/21709814#21709814

---------------------------------------------------------------------------------------------------

배열 뒤집기

obj = {
    a:'aaa',
    arr:[1,2,3]
}

obj.arr.reverse()

---------------------------------------------------------------------------------------------------

현재 포커싱된 요소의 ID/Class 가져오기

var id = $(':focus').attr('id');
var class = $(':focus').attr('class');


탭눌렀을때 가져오기
$(window).on('keyup', (e) => {
	if (e.keyCode === 9) {
		let f = $(':focus');
		console.log(f);
	}
});


자바스크립트 버전

document.activeElement

---------------------------------------------------------------------------------------------------

이벤트 객체


이벤트객체의 toElement 속성 이용해 이벤트에 걸린 요소 가져올 수 있음

$('.ai_travel_list1 ul').on('mouseover',(e)=>{
	console.log('xx');
	console.log(e.toElement);
});


document에 on메소드를 써서 요소에 이벤트를 건 경우 해당 요소를 찾으려면 $(':focus'); 등으로 찾아야함
$(document).on('focus', '.ai_travel_list1 ul.hoverWrap li a', (e) => {

---------------------------------------------------------------------------------------------------

이벤트가 적용되지 않는 경우

선택자로 동적으로 불러오는 요소를 선택할경우
시점문제로 인해 일반적인 방법으로는 이벤트가 적용되지 않음

$('.ai_travel_list1 ul.hoverWrap li').on('mouseover', () => {

위 방식이 안된다면 아래처럼 document에 on 메소드를 쓰고, 두번째 인수로 선택자를 넣기 ( $() 로 안감싸도 됨 )

$(document).on('mouseover', '.ai_travel_list1 ul.hoverWrap li', () => {

----------------------------------------------------------------------------------------------------

아이프레임 내 조작

var textarea = $('iframe').contents().find("iframe").contents().find('.se2_inputarea');

----------------------------------------------------------------------------------------------------

div에 방향키로 스크롤되게하기

div에 overflow-x or y 넣고 (당연히 내용은 이 div보다 더 커야함)

함수 만들고
function scrollCheck(e) {
	if (e.keyCode === 38) e.target.scrollTop = e.target.scrollTop - 10;
	if (e.keyCode === 40) e.target.scrollTop = e.target.scrollTop + 10;
}

쓰고싶은 요소에서 이벤트에 연결해서 쓰기
<div tabindex="0" onkeydown="scrollCheck(event)">

----------------------------------------------------------------------------------------------------

<a href="javascript:"> 에 걸린 함수는 event객체를 쓸 수 없음

ex)아래처럼 하면 e는 undefined가 나옴
<a href="javascript:f1(event)">a태그</a>
function f1(e){
	console.log(e)
}

이벤트 객체가 필요하다면 a href 말고 onclick으로 해야함

------------------------------

자식이벤트에서 이벤트 버블링 막을때

onclick등에 걸린 이벤트는
↓↓↓
이벤트객체.stopPropagation();
이렇게 막는데,


부모에 걸린게 이벤트가 아닌 <a href=> 라면 (<a href="javascript:"> 함수호출 포함)
↓↓↓
이벤트객체.preventDefault();
이렇게 막아야함


즉 부모 이벤트가 a href 인지 onclick등 '이벤트'인지에 따라 막는 방법이 바뀌고,
자식 이벤트는 a href 말고 onclick등의 '이벤트'를 써야됨

ex)
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Document</title>

	<script src="https://korean.visitkorea.or.kr/resources/js/jquery-1.11.2.min.js"></script>

	<style>
		*{margin:10px}
		a{display:inline-block;width:200px;height:200px;background:#FFC19E;cursor:pointer;}
		a p{display: inline-block;width: 100px;height: 100px;background:darkgrey;}
		body > div{display: inline-block; position: relative;}
		div+div{margin-left: 100px;}
		div div{width:100px;height:100px;background:#6799FF;cursor:pointer;}
		h2{display: inline-block;width: 100px;height: 100px;background: lightsalmon;position: absolute;left: 150px;top: 150px;}
	</style>

</head>
<body>
	<!-- 부모이벤트가 onclick으로 걸린경우 -->
	<div>
	<a onclick="f1()">
		a영역
		<p onclick="f3(event)">p영역</p>
	</a>
	<div onclick="f2()">div영역</div>
	<h2 onclick="f5()">h2영역</h2>
	</div>
	
	<!-- 부모이벤트가 href로 걸린경우 -->
	<div>
	<a href="javascript:f1()">
		a영역
		<p onclick="f4(event)">p영역</p>
	</a>
	<div onclick="f2()">div영역</div>
	<h2 onclick="f5()">h2영역</h2>
	</div>

<script>
	function f1(){
		alert("f1");
	}
	function f2(){
		alert("f2");
	}
	function f3(e){
		e.stopPropagation();
		alert("f3")
	}
	function f4(e){
		e.preventDefault();
		alert("f4")
	}
	function f5(){
		alert("f5")
	}
</script>
</body>
</html>

----------------------------------------------------------------------------------------------------

제이쿼리 이벤트 걸때 document에 걸 수 있음. 이렇게 하면 ajax로 늦게 불러온 요소에도 이벤트를 걸기 쉽나?

$(document).on('click', 'p', (e) => {
});

----------------------------------------------------------------------------------------------------

모바일기기 회전될때 새로고침되게할때

resize 이벤트를 쓰면 되는데, 

$(window).resize(function(){
	location.reload();
}

그냥 이렇게 넣으면 모바일기기에서 상단주소창이 올라갈때도(그냥 스크롤을 내렸을때도) 새로고침이 돼버림.

그래서 밖에다가 변수를 하나 넣어서, resize이벤트가 2번 일어날때 새로고침을 시키면 상단창이 움직였을때 새로고침 되는걸 한번은 방지할 수 있음

let check;
$(window).resize(function(){
	if(check)
		location.reload();
	check = true;
}

근데 이건 사실 근본적인 해결책은 아님. 스크롤을 내렸다 올렸다 해서 2번 상단창을 움직이면, 여전히 새로고침이 되기 때문.

그래서 resize가 되었을때 && 윈도우사이즈가 바뀌었을때만 새로고침 되게끔 처리를 하면, 회전시에만 잘 새로고침되게 처리가 가능함

----------------------------------------------------------------------------------------------------

요소 변화를 감지하려면 MutationObserver 를 쓰면 된다고 함

참고: https://jsikim1.tistory.com/154

----------------------------------------------------------------------------------------------------

xpath

우선 CSS Selector는 태그의 패턴을 이용해 탐색하는 선택자이며, 웹 개발자에게 가장 익숙한 선택자일 것이다.
stylesheets나 javascript에서 document.querySelector() 또는 jquery로 많이 접해봤을 것이다. 그만큼 우리에게 익숙하고 널리 사용되고 있는 선택자이다.

하지만 '원하는 범위의 값을 가진 태그'를 선택하는 선택자는 없다. 예를 들어, 'value가 50이상인 input태그를 선택'한다고 했을 때 방법이 없다.
그냥 a태그 전체를 탐색해서 50이상인 태그만 스타일을 적용해주는 스크립트를 작성해야만 했다.
또, 선택한 태그들의 값을 바로 뽑아서 사용하고 싶어도 map으로 한번 가공해줘야했다.

그런데, 그것이 가능해졌다. 바로 XPATH 때문이다. XPATH는 XML 경로 언어라고 하며 Node의 경로를 query로 탐색하는 선택자이다.
위에서 CSS Selector가 하지못했던 일을 XPATH는 할 수 있다. "//input[value>=50]". 매우 간단한 방법으로 처리한다.
또한, 선택된 태그의 값만 가지고 오려면 "//input[value>=50]/@value" 이렇게 사용하면 된다.
이 외에도 4번째에 있는 자식 태그를 탐색하기위해 "div:nth-child(4)"와 같이 복잡한 문법이 아니라, "//div/*[4]" 간결한 문법을 제공한다.

참고 : https://www.w3schools.com/xml/xpath_syntax.asp
참고2 : https://developer.mozilla.org/ko/docs/Web/XPath/Introduction_to_using_XPath_in_JavaScript

----------------------------------------------------------------------------------------------------

스와이퍼 슬라이드 페이지네이션을 다른 슬라이드의 요소와 연결시키기 && 기존 페이지네이션도 사용

중요한것은 thumbs슬라이드는 슬라이드선언을 하면 안된다는것임(안해도 thumbs: { swiper: { 안에 선택자로 연결해놓으면 자동으로 슬라이드가능해짐)

<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Document</title>
	<link rel="stylesheet" href="https://unpkg.com/swiper/swiper-bundle.min.css" />
</head>
<body>

<!-- 슬라이드 컨테이너 (thumbs) -->
<div class="swiper-container thumbs">
	<!-- 슬라이드들 -->
	<div class="swiper-wrapper">
		<!-- 각 슬라이드 -->
		<div class="swiper-slide">
			111
		</div>
		<div class="swiper-slide">
			222
		</div>
		<div class="swiper-slide">
			333
		</div>
		<div class="swiper-slide">
			444
		</div>
	</div>
</div>

<!-- 슬라이드 컨테이너 (main) -->
<div class="swiper-container main">
	<!-- 슬라이드들 -->
	<div class="swiper-wrapper">
		<!-- 각 슬라이드 -->
		<div class="swiper-slide">
			메인111<br>메인111<br>메인111<br>메인111<br>메인111<br>
		</div>
		<div class="swiper-slide">
			메인222<br>메인222<br>메인222<br>메인222<br>메인222<br>
		</div>
		<div class="swiper-slide">
			메인333<br>메인333<br>메인333<br>메인333<br>메인333<br>
		</div>
		<div class="swiper-slide">
			메인444<br>메인444<br>메인444<br>메인444<br>메인444<br>
		</div>
	</div>
	<!-- 페이지네이션 -->
	<div class="swiper-pagination"></div>
</div>

<script src="https://unpkg.com/swiper/swiper-bundle.min.js"></script>
<script>
	// SwiperJS 코드
	var mainSwiper = new Swiper('.main', {
		// 페이지네이션 설정
		pagination: {
			el: '.main .swiper-pagination',
			clickable: true, // 페이지네이션 버튼 클릭 가능하게 설정
		},
		// thumbs 설정
		thumbs: {
			swiper: {
				el: '.thumbs',
				slidesPerView: 2, // thumbs 슬라이드 한 번에 보여질 슬라이드 개수
			}
		}
	});
</script>
</body>
</html>

----------------------------------------------------------------------------------------------------

스와이퍼 슬라이드 fraction & progressbar 둘다 쓰는법

(pagination:{type: 'progressbar' 말고 'fraction'으로})

ex)
<div class="swiper-container">
	<div class="swiper-wrapper">
		<div class="swiper-slide">
			<a href="javascript:;">
				<div class="img"><img src="../resources/images/temp/img_220x300.jpg" alt=""></div>
				<strong>고라니커피클럽 고라니커피클럽고라니커피클럽고라니커피클럽 고라니커피클럽고라니커피클럽</strong>
			</a>
		</div>
		<div class="swiper-slide">
			<a href="javascript:;">
				<div class="img"><img src="../resources/images/temp/img_220x300.jpg" alt=""></div>
				<strong>고라니커피클럽</strong>
			</a>
		</div>
		<div class="swiper-slide">
			<a href="javascript:;">
				<div class="img"><img src="../resources/images/temp/img_220x300.jpg" alt=""></div>
				<strong>고라니커피클럽</strong>
			</a>
		</div>
		<div class="swiper-slide">
			<a href="javascript:;">
				<div class="img"><img src="../resources/images/temp/img_220x300.jpg" alt=""></div>
				<strong>고라니커피클럽</strong>
			</a>
		</div>
		<div class="swiper-slide">
			<a href="javascript:;">
				<div class="img"><img src="../resources/images/temp/img_220x300.jpg" alt=""></div>
				<strong>고라니커피클럽</strong>
			</a>
		</div>
	</div>
	<div class="swiper-button-prev">이전</div>
	<div class="swiper-button-next">다음</div>
	<div class="swiper-pagination"></div>
	<div class="swiper-progressbar" style="height:3px"></div>
</div>

var mySwiper = new Swiper('.swiper-container', {
	pagination: {
		el: '.component30 .swiper-pagination', // .찍어야 함
		type: 'fraction'
	},
	scrollbar: {
		el: '.component30 .swiper-progressbar',  // .찍어야 함
		hide: false,
		draggable: true
	},
	navigation: {
		nextEl: ".component30 .swiper-button-next",
		prevEl: ".component30 .swiper-button-prev",
	}
});

-----

loop 까지 쓸 수도 있음 (다만 스와이프가 끝난 후 움직임)

<div id="festivalCon" class="poster">
	<div class="swiper-container">
		<div class="swiper-wrapper">
		</div>
		<div class="swiper-button-prev">이전</div>
		<div class="swiper-button-next">다음</div>
		<div class="page_box">
			<div class="swiper-pagination"></div>
			<div class="num"><strong class="current"></strong>/<span class="total"></span></div>
		</div>
	</div>

<script>
	let oriSize;
	slFestival = new Swiper(el.find('.poster .swiper-container'), {
		slidesPerView: 'auto',
		watchOverflow:true,
		spaceBetween: 20,
		loop:true,
		pagination: {
			el: '#festivalCon .swiper-pagination',
			type: 'progressbar',
		},
		navigation: {
			nextEl: '.swiper-button-next',
			prevEl: '.swiper-button-prev',
		},
		breakpoints: {
			1023: {
				spaceBetween: 10,
				centeredSlides: true,
			}
		},
		on:{
			beforeInit: function(){
				oriSize = $('#festivalCon .swiper-slide').length;
			},
			activeIndexChange: function(){
				$('#festivalCon .current').text(this.realIndex + 1);
				$('#festivalCon .total').text(oriSize);
			}
		}
	});
</script>

----------------------------------------------------------------------------------------------------

스와이퍼 슬라이드 이벤트 핸들러 함수 내에서 현재 index 확인하는 방법

스와이퍼객체.activeIndex

ex)
let testSl = new Swiper('#testSl', {
	on:{
		slideChangeTransitionEnd:function(){
			console.log('testSl.activeIndex:',testSl.activeIndex);
		}
	}
});

스와이퍼객체 를 this 로 써도 똑같음
ex) this.activeIndex

----------------------------------------------------------------------------------------------------

slideChangeTransitionEnd : 슬라이드 전환이 끝난 후 이벤트
transitionEnd : 스와이프 애니메이션이 끝난 후 이벤트 (넘기지 않았을때도 발생)

----------------------------------------------------------------------------------------------------

슬라이드의 총 개수를 반환

스와이퍼객체.slides.length;

-----

loop기능을 위해 복제된 슬라이드를 제외한 원래의 슬라이드의 개수만 반환

let oriSize;
...
let testSl = new Swiper('#testSl', {
	beforeInit: function(){
		oriSize = $('#testSl .swiper-slide').length;
	},

----------------------------------------------------------------------------------------------------

'넘기기 시작'할때 도착 슬라이드의 index를 가져오는법
activeIndexChange: function(){
	alert(this.realIndex+'번째 slide입니다.');
}


slideChangeTransitionStart: function(){
이 메소드는 바뀌기 전에껄 가져와서 안됨. 꼭 activeIndexChange: function(){로 하기

-----

특정 인덱스의 슬라이드 가져오기

this.slides[인덱스]

이때 this는 스와이퍼 선언변수로 해도됨

----------------------------------------------------------------------------------------------------

서로 다른 슬라이드 2개를 연결하기, 슬라이드 타이머 커스텀

<style>
.main_showcase{transition:all .5s}
.main_showcase .swiper-progress-bar .slide_progress-bar:after{display:none !important}
.main_showcase .swiper-progress-bar .slide_progress-bar .fill{position:absolute;top:0;left:0;background:#000;height:100%}
.main_showcase .swiper-progress-bar.animate .slide_progress-bar .fill{transition:none;animation:move 5s linear;animation-fill-mode:forwards}
.main_showcase.active .swiper-progress-bar.animate .slide_progress-bar .fill{animation-play-state:paused}
</style>

<div class="main_showcase" id="mainTab">
	<div class="cont">
		<div class="swiper-container gallery-thumbs">
			<ul class="swiper-wrapper">
			</ul>
		</div>
	</div>
	<div class="img_wrap">
		<div class="swiper-container gallery-top">
			<div class="swiper-wrapper">
			</div>
		</div>
	</div>
	<div class="page_box">
		<div class="page">
			<div class="swiper-progress-bar">
				<span class="slide_progress-bar"><span class="fill"></span></span>
			</div>
			<div class="swiper-pagination"></div>
			<div class="btn">
				<div class="swiper-button-prev">이전</div>
				<div class="swiper-button-next">다음</div>
				<div class="btn_auto">
					<button class="btn_autoPlay">재생</button>
					<button class="btn_autoStop">멈춤</button>
				</div>
			</div>
		</div>
	</div>
</div>

function scSwiper() {
	const el = $(isSizeM ? '#mainContainerM' : '#mainContainerPC').find('.main_showcase'),
		setBg = ($this) => el.css('background', $($this).data('color')),
		spb = el.find('.swiper-progress-bar'),
		galleryThumbs = new Swiper(el.find('.gallery-thumbs'), {
			spaceBetween: 0,
			slidesPerView: "auto",
			speed: 1000,
			loop: true,
			pagination: {
				el: el.find('.swiper-pagination'),
				type: 'fraction',
				formatFractionCurrent: (number) => ('0' + number).slice(-2),
				formatFractionTotal: (number) => ('0' + number).slice(-2)
			},
			navigation: {
				nextEl: '.swiper-button-next',
				prevEl: '.swiper-button-prev'
			},
			on: {
				init: function () {
					spb.removeClass("animate");
					spb.removeClass("active");
					spb.eq(0).addClass("animate");
					spb.eq(0).addClass("active");
					swiperTabindex(el.selector, this.activeIndex);
					isPossibleChangeBg.call(this);
				},
				slideChangeTransitionStart: function(){
					spb.removeClass("animate");
					spb.removeClass("active");
					spb.eq(0).addClass("active");
				},
				slideChangeTransitionEnd: function(){
					spb.eq(0).addClass("animate");
					swiperTabindex(el.selector, this.activeIndex);
				},
				activeIndexChange: function(){
					isPossibleChangeBg.call(this);
				}
			}
		}),
		galleryTop = new Swiper(el.find('.gallery-top'), { //이미지
			spaceBetween: 30,
			slidesPerView: "auto",
			loop: true,
			speed: 1000,
			on: {
				init: function(){
					isPossibleChangeBg.call(this, true);
				},
				activeIndexChange: function(){
					isPossibleChangeBg.call(this, true);
				},
				transitionEnd: function(){
					// !el.hasClass('active') && this.autoplay.start();
				}
			}
		});

	galleryTop.controller.control = galleryThumbs;
	galleryThumbs.controller.control = galleryTop;
	el.on('focusin', '.swiper-wrapper', function () {
		el.addClass('active');
		galleryThumbs.autoplay.stop();
		galleryTop.autoplay.stop();
	}).on('click', '.btn_auto button', function () {
		if (!el.hasClass('active'))
			el.addClass('active');
		else
			el.removeClass('active');
	}).on('click', '.swiper-pagination button', () => {
		if (el.addClass('active')) {
			$scSwiper.autoplay.stop();
			galleryTop.autoplay.stop();
		}
	});
	setInterval(() => {
		if(spb.find('.fill')[0].offsetWidth / spb.children().width() === 1)
			galleryTop.slideNext();
	}, 500)
	function isPossibleChangeBg(mb){
		!(mb ^ isSizeM) && setBg(this.slides[this.realIndex]);
	}
}

----------------------------------------------------------------------------------------------------

스와이퍼 슬라이드에서 슬라이드를 해도 swiper-slide-active 클래스가 안들어갈땐 수동으로 클래스를 넣어주기

on:{
	slideChange: function() {
		$('.swiper-slide').removeClass('swiper-slide-active');
		el.find('.swiper-container .swiper-slide').eq(this.activeIndex).addClass('swiper-slide-active');
	}
}

----------------------------------------------------------------------------------------------------

스와이퍼 객체 제거

이전에 만들어져 있던 슬라이드 때문에 UI오류가 발생할때가 있음. 이럴땐 이전에 있던 슬라이드객체를 제거하고 다시 만들면 됨


let slCon;

어쩌구저쩌구이벤트나함수(){
	slCon && slCon.destroy()
	slCon = new Swiper(~~~)
}

이러면 이벤트가 실행되기 전에 이미 슬라이드가 만들어져있다면 없애고 다시만들 수 있음

----------------------------------------------------------------------------------------------------

스와이퍼 이벤트 순서

beforeInit
breakpoint
slidesLengthChange
unlock
snapGridLengthChange
slidesGridLengthChange
beforeSlideChangeStart
fromEdge
progress
setTransition
setTranslate
activeIndexChange
snapIndexChange
beforeTransitionStart
transitionStart
slideChangeTransitionStart
slideNextTransitionStart
setTransition
transitionEnd
slideChangeTransitionEnd
slideNextTransitionEnd
init

----------------------------------------------------------------------------------------------------

클릭한 요소가 몇번째 요소인지

요소범위.index(요소)

$("#mainContainerM .main_curation_area .tab li a").click(function () {
	let idx = $("#mainContainerM .main_curation_area li").index($(this).parent());
	console.log('activeTab:',activeTab)
});

----------------------------------------------------------------------------------------------------

제이쿼리로 두번째 부터 끝까지 형제 선택

.siblings().slice(1);

----------------------------------------------------------------------------------------------------

특정 태그안에 있는 <a href="javascript:" 가 작동이 안되고 오류가 날 수 있음

Uncaught Error: Syntax error, unrecognized expression: javascript:

이런 오류가 나면 href="#" 으로 넣어놓고 onclick="함수()" 이렇게 쓰거나

<script> 태그내에서 이벤트 리스너를 등록하기

----------------------------------------------------------------------------------------------------

이벤트 핸들러

특정 이벤트에 대한 콜백 함수를 등록하는 방식
이벤트가 발생했을 때 실행되는 함수를 말함
.on() 또는 .click() 등의 메소드를 사용하여 등록


이벤트 리스너

이벤트 대상에 대한 콜백 함수를 등록하는 방식
이벤트 핸들러를 등록하는 메소드를 말함
.bind() 또는 .addEventListener() 등의 메소드를 사용하여 등록

----------------------------------------------------------------------------------------------------

on 메소드

이벤트 핸들러 등록(이벤트 바인딩)하는 메소드. click()으로 하면 하나밖에 못걸지만 on으로 하면 여러이벤트를 바인딩 할수있음


$(selector).on(event, childSelector, data, function)

selector: 이벤트를 발생시킬 요소를 선택합니다.
event: 등록할 이벤트의 종류를 지정합니다. 예를 들어, 클릭 이벤트를 등록하려면 click을 사용합니다.
childSelector (선택사항): 자식 요소에서 이벤트를 발생시키려면 선택자를 지정합니다.
data (선택사항): 이벤트 핸들러에 전달할 데이터를 지정합니다.
function: 이벤트 핸들러로 등록할 함수를 지정합니다.

1. $(요소).on('이벤트명', 전달할데이터(객체도 가능), function(){...})
2. $(요소).on('이벤트명', 자식요소, 전달할데이터(객체도 가능), function(){...}))

<div class="container">
	<h2>container</h2>
	<div class="box1">box1</div>
	<div class="box2">
		<input type="text" class="inp">
	</div>
	<div class="box3">box3</div>
	<div class="box4">box4</div>
</div>
<script>
	$('.container').on('click', function(){
		console.log('container click');
	}).on('mouseover', '.box1', function(){
		console.log('box1 mouseover');
	}).on('focusin', '.box2 .inp', function(){
		console.log('box2 focusin');
	}).on('click', '.box3', 'asd', function(e){
		console.log('box3', e.data);
	}).on('click', '.box4', {someData: 'zxc'}, function(e){
		console.log('box4', e.data.someData);
	})
</script>

----------------------------------------------------------------------------------------------------

이벤트 리스너를 함수 안에서 등록할때

이벤트 리스너를 등록하는 함수가 2번 호출되면,
이벤트 리스너도 중복해서 적용이됨

이를 방지하기 위해서는

이벤트 리스너가 중복되서 호출됬는지 확인하기
예를들어서 $('.ai_list li div').on('click', function(e){ 이렇게 쓴경우 $('.ai_list li div')요소가 2개 이상있는지 확인하기
<li>
	<div>
		<div></div>
	</div>
</li>
이렇게 되어있을때는 밖에있는 div와 안에있는 div 총 2개의 div가 중복돼서 이벤트리스너로 등록됐는지 확인하기


혹은 이벤트리스너를 등록할때 off() 메서드로 이전 등록된 이벤트 리스너를 먼저 삭제해주면 된다는데 안되는듯
ex)
$('.ai_list li div').off('click').on('click', function(e){ // off() 메서드 추가
        console.log('start...')
})

----------------------------------------------------------------------------------------------------

모바일에서 요소를 클릭했을때

click 이벤트는 1번발생되고,
mouseover 이벤트는 2번발생되고,
focusin 이벤트는 1번발생됨

----------------------------------------------------------------------------------------------------

<br>을 실제로 줄바꿈으로 바꾸려면
.text() 말고 .html() 함수안에 넣어야함

요소.html(`111<br>222`);

-----

html() / append() / prepend() 안에

'요소'를 인수로 넣으면 '복사'가 아니라 '이동'이됨

복사를 하고싶으면 인수로 요소 말고 요소.html() 을 넣기


replaceWith(html내용)

선택 요소를 바꿔치기함 (html()은 요소 안을 교체, replaceWith()는 요소자체를 교체)


<div id=aa></div>

$("#aa").replaceWith('<p id="bb"></p>');

↓↓↓

<p id="bb"></p>

-----

요소.after(html내용)

특정 요소 다음에 추가

-----

요소.before(html내용)

특정 요소 이전에 추가

------------------------------

이전 형제 요소 선택

요소.prev()

-----

다음 형제 요소 선택

요소.next()

-----

이전 형제 요소 모두 선택

요소.prevAll()

-----

다음 형제 요소 모두 선택

요소.nextAll()

-----

요소들 중 특정 클래스가 있는 요소를 다시 선택

요소들.filter(선택자)

----------------------------------------------------------------------------------------------------

제이쿼리 요소 선택자문자열로 가져오는 속성

$("#box") → m.fn.init [div#box.main_contents, context: document, selector: '#box']

$("#box").selector → '#box'

----------------------------------------------------------------------------------------------------

요소들의 순서를 랜덤하게 섞기

elements = $('.asd'); // 선택한 요소들을 배열에 담기
var parent = elements.parent(); // 요소들의 부모 요소 가져오기

// 배열의 순서를 랜덤하게 섞어주는 함수
function shuffleArray(array) {
	for (var i = array.length - 1; i > 0; i--) {
		var j = Math.floor(Math.random() * (i + 1));
		var temp = array[i];
		array[i] = array[j];
		array[j] = temp;
	}
	return array;
}

elements = shuffleArray(elements); // 요소들의 순서 랜덤하게 섞기

// 부모 요소에 랜덤하게 섞은 요소들 추가
$.each(elements, function(i, el) {
	parent.append(el);
});

----------------------------------------------------------------------------------------------------

애니메이션(animation) 일시정지(transition은 안됨)

animation-play-state:paused

----------------------------------------------------------------------------------------------------

attr 함수 다중 적용 가능

attr('', '') → attr({'': '', '': ''})

----------------------------------------------------------------------------------------------------

스와이퍼 슬라이드에서 너비 css 설정한대로 나오게하고싶으면

slidesPerView: 'auto', 를 꼭 넣어야함. 안넣으면 100%로 들어감

----------------------------------------------------------------------------------------------------

trigger()

클릭 이벤트를 발생시키는 함수

$('.switch_wrap .slider').on('click', function(){
	if(!$(this).hasClass('on')){
		$(this).addClass('on');
		$('#switch1').trigger('click');
	}else{
		$(this).removeClass('on');
		$('#switch1').trigger('click');
	}
});

----------------------------------------------------------------------------------------------------

제이쿼리 ajax의

.done(), .fail(), .always() 는 각각 success(), error(), complete()

과 같은 역할을 함.

const pavilion = {
	getSpecialPavilion: function(){
		$.ajax({
			type: ~~~,
			url: ~~~,
			data: ~~~,
			success: function(){},
			error: function(){},
			complete: function(){}
		});
	}
}
pavilion.getSpecialPavilion();

위처럼 쓰던걸, 호출한곳에서 처리가 가능함 (ajax객체 return 필요)

const pavilion = {
	getSpecialPavilion: function(){
		return $.ajax({
			type: ~~~,
			url: ~~~,
			data: ~~~
		});
	}
}
pavilion.getSpecialPavilion().success(function(){}).erroe(function(){}).complete(function(){});


ajax를 두번 호출해야되는데 success/complete만 다르게 해야할경우, 이런 방식으로 분리를 하면 좋음

----------------------------------------------------------------------------------------------------

display:flex 안에 있으면

position:fixed 가 안먹음.

display:flex가 적용된 요소의 바깥으로 빼기

----------------------------------------------------------------------------------------------------

<div class="outer">
	<div class="inner"></div>
	<div class="inner"></div>
</div>

이렇게 있을때

ㅡㅡㅡㅡㅡ // outer

inner
inner

ㅡㅡㅡㅡㅡ // /outer

이렇게  정렬하는법

.outer{display:flex;justify-content:center;align-items:center;flex-direction:column}
.inner{display:flex;align-items:center;line-height:10px}

----------------------------------------------------------------------------------------------------



























