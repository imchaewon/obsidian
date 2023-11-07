★														  ★
★★													     ★★
★★★												 ★★★
★★★★				오류나면 톰캣콘솔 보기.			    ★★★★
★★★★★  휙 사라져버릴수있으니 새로고침 하자마자 보기	★★★★★
★★★★★ 오류메시지봐도 어디서 오류가났는지 모르겠으면,	★★★★★
★★	★★	   메소드 단위로 111,222,333 이렇게 막 찍어보기	    ★★★★
★★★			없는걸 찾고있는 경우가 대부분				 ★★★
★★    메소드를 거슬러올라가서 어디까지되나 한줄씩 확인해보기	     ★★
★														  ★

com.google.gwt.event.shared.UmbrellaException: Exception caught: undefined
↓↓↓
소스트리 가서 HEAD를 옮겨보면서 거꾸로 올라가면서 테스트해보기(트리 점 더블클릭하면 됨. 정말 작업 상태를 변경하시겠습니까? 확인)


★어드민 자바 서버파일이 브라우저에 반영이 안될때 or 404오류뜰때 or
java.lang.ClassNotFoundException: kr.or.visitkorea.admin.server.application.BusinessMappingBuilder 오류날때
or 404는 안뜨지만 무한 로딩될때
(이클립스 톰캣으로 실행한 경우)
↓↓↓
1. 톰캣 종료
2. problems탭 한번 살펴보기
3. 프로젝트폴더 → Beans가 빨간엑스떠있는지 보기
4. 프로젝트 우클릭 → Build Path → Configure Build Path... 에서 오류가 떠있으면 Remove
5. target폴더 제거
6. 메이븐 빌드
7. 톰캣 실행

안되면
8. 프로젝트 → 메이븐 업데이트
9. 톰캣서버 우클릭 → 클린
10. 톰캣 재실행


이클립스gwt창에 항목 안나오면 빨간버튼눌러서 중지하고 톰캣 다시 켜기


com.google.gwt.event.shared.UmbrellaException: Exception caught: (TypeError) : Cannot read properties of undefined (reading 'getValue_2_g$')
↓↓↓
테이블 선언 이전에 값을 넣으려고 한 경우
table = new ContentTable(ContentTable.TABLE_SELECT_TYPE.SELECT_SINGLE);


com.google.gwt.event.shared.UmbrellaException: Exception caught: (TypeError) : Cannot read properties of undefined (reading 'setParameters_0_g$')
at ajc_g$.hA_g$ [as createError_0_g$]
↓↓↓
다이얼로그 만드는데 어플리케이션 파일(ApplicationBase를 상속받는 파일)을 두개를 만들어서 하려고했을때
DialogContent객체가 만들어지지 않은경우


Error: com.google.gwt.event.shared.UmbrellaException: Exception caught: Index: 0, Size: 0
↓↓↓
MaterialComboBox<Object> 에서 선택이 안된상태에서(빈 배열) .get(0)이 실행된 경우(Console.log로 찍은경우도 포함).
if (!mode.getSelectedValue().isEmpty()) { 로 감싸야함


Error: com.google.gwt.event.shared.UmbrellaException: Exception caught: Fri Jun 10 17:54:00 GMT+900 2022
↓↓↓
날짜/시간 포맷을 이상하게 받으려고한 경우.
Date에서 바로 바꾸는경우라면 parse안쓰고 아래처럼 그냥 바꾸면됨
DateTimeFormat.getFormat("HH:mm:ss").format(sTime.getValue())


Uncaught Error: java.lang.IndexOutOfBoundsException: Index: 4, Size: 4
    at Nrg_g$.hA_g$ [as createError_0_g$]
↓↓↓
테이블 만들때 제목으로 넣은 개수보다 많은 열을 넣으려고 했을때


JSONObject에 담겨있는 String형의 JSONObject를
.get()메소드로 꺼내고 다시 JSONObject에 담을 경우 아래처럼 정수배열 형태로 변함
{bytes=[123, 34, 99, 114, 105, 116], empty=false}
↓↓↓
.getString()메소드로 꺼내야함

-----

Uncaught TypeError: Cannot read properties of null (reading 'isString_0_g$')
↓↓↓


1. JSONObject에서 키가 null인걸 get하고, 그거에 .isString() 을 썼을때 발생

아래처럼 분기 처리해야함

String SSRP_ID;
if(resultList.get(i).isObject().containsKey("SSRP_ID")) {
	SSRP_ID = resultList.get(i).isObject().get("SSRP_ID").isString().stringValue();
} else {
	SSRP_ID = "";
}


2. myBatis <if test="">태그에서 연산자 우선순위를 잘못쓴 경우
!mode eq 'ALL'		X
↓
!(mode eq 'ALL')		O

-----

org.apache.ibatis.exceptions.PersistenceException: 
java.lang.IllegalArgumentException: Mapped Statements collection does not contain value for 
kr.or.visitkorea.system.CommentAnalysis.selectCommentListCnt
↓↓↓
mybatis xml파일에서 찾으려는 태그id가 없는경우

-----

개발자도구 콘솔에서 오류나는데 아무리봐도 틀린게 없으면

이클립스 콘솔(톰캣) 에서 sql문 오류나면 sql이 틀린것. 오류메시지 참고해서 문법 확인

SELECT
FROM
WHERE
ORDER BY
LIMIT

-----

디버거에서 일시중지됨

속성명을 케밥표기법으로 썼는지 확인 (콘솔에 잘못된부분 찍힘)

-----

페이지가 반만 나올떄

수정한파일 이클립스에서 한번 열기

----------------------------------------------------------------------------------------------------

GWT (Google Web Toolkit)

Google에서 개발한 자바 기반의 오픈소스 웹 프레임워크

GWT는 웹 애플리케이션 개발을 쉽게 만들어주며, Java 언어와 비슷한 구문을 사용하여 클라이언트 측 JavaScript 코드를 생성함.
이를 통해 웹 개발자들은 Java를 사용하여 웹 애플리케이션을 빠르게 개발할 수 있음
GWT는 특히 큰 규모의 복잡한 웹 애플리케이션을 구축할 때 유용함
GWT는 Java로 작성된 코드를 JavaScript로 컴파일하는 Java-to-JavaScript 컴파일러를 제공함

----------------------------------------------------------------------------------------------------

초기설정(이클립스)

web.xml
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns="http://java.sun.com/xml/ns/javaee"
	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
	version="2.5"web.
↓↓↓
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns="http://JAVA.sun.com/xml/ns/javaee"
	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
	version="2.5">


1. 마켓플레이스에서 gwt다운
2. Preferences → GWT → GWT Settings → Download... 버튼 클릭
3. 2.7버전 다운후 add하기
4. 프로젝트폴더 우클릭 → Run As... → Run Configurations 
5. Maven Build 더블클릭후 name에 visitkorea-admin입력
6. Goals에 아래 입력
clean install -P local (더 빠른거: install -P local gwt:run -f pom.xml)
7. Base directory는 Workspace...버튼 눌러서 루트폴더 선택
8. Skip Tests 체크
9. Run

그러면
약 3분에 걸쳐 빌드가 되고
프로젝트폴더 → target에 폴더들이 생김

만약 빌드도 안되고 아무 반응도 안일어난다면 2~3분좀만더 기다려보고 그래도 반응없으면 이클립스 재설치.
BUILD FAILURE 뜨면 자바버전문제

톰캣 서버 시작

------------------------------

GWT실행 안되고 이상할때 재설정하는법

프로젝트 우클릭 → Run As → Maven install

프로젝트 우클릭 → Run As → Run configurations... → 
좌측에 Maven Build 하위에 visitkorea-admin으로 만들어놓은거(Goals에 clean install -P local gwt:run있는거) 클릭 → Run

한번 해보고 안되면
프로젝트 우클릭 → Run As → Maven build 도 해볼것

1. 프로젝트 폴더 루트에 target폴더 있는데 그 안에
visitKoreaAdmin-3 안에 html 파일들과 WEB-INF폴더가 있는거 확인 후
그 WEB-INF안에 또 폴더들이 들어있는거 확인.

2. 터미널에서 아래 3개 프로세스가 동작되고 있는지 확인도 해보기
ps -ef | grep visit
ps -ef | grep gwt
ps -ef | grep 9876

------------------------------

이클립스에서 GWT 실행 안되면

1. 프로젝트 jdk / jre 버전 설정
프로젝트폴더우클릭 → Build Path → Configure Build Path... → Libraries → JRE 이상한버전 선택후 Remove → Add Library... → 1.8이나 18버전으로 다시 설정

2. maven JRE 설정
프로젝트폴더우클릭 → Run As → Run Configurations... → JRE탭 → Environmnets... → 1.8이나 18버전 등록(Apply and Close) → 셀렉트박스에서 한번더 선택해야함

----------------------------------------------------------------------------------------------------

GWT의 JSONObject (com.google.gwt.json.client)

JSONObject obj = new JSONObject();
obj.put("a", new JSONString("aaa"));

JSONValue val1 = new JSONString("bbb");
obj.put("b", val1);

JSONValue val2 = new JSONNumber(0);
obj.put("c", val2);

JSONValue val3 = new JSONNumber(123);

Console.log(obj+""); // {"a":"aaa", "b":"bbb", "c":0}
Console.log(val1+""); // "bbb"
Console.log(val1.isNumber()+""); // null
Console.log(val2+""); // 0
Console.log(val2.isString()+""); // null
Console.log(val3+""); // 123
Console.log(val3.isString()+""); // null


★JSONNumber에 .isString()을 하면 null로 바뀜
★JSONString에 .isNumber()를 하면 null로 바뀜

★GWT JSONObject에 값을 담으면 자료형이 JSONValue로 변함.
하지만 JSONValue값.getClass.getName() 이렇게 찍어보면 JSONNumber, JSONString 등으로 나오니 안에 있는 값이 뭔지 모를경우 활용하기

JSONValue형을 Date형으로 바꿀때는 아래처럼 (Calendar는 gwt에서 지원안함)
DateTimeFormat.getFormat("HH:mm:ss").parse(VisitKoreaBusinessUtils.removeQuot(obj.get("EXPSR_BGNG_TM")))
더 자세한 Date형변환은 아래쪽 참고

----------------------------------------------------------------------------------------------------

입력값 / 널체크

아무값도 넣거나 선택하지 않았을때

MaterialCheckBox .getValue()		→ == false → .getValue()
MaterialRadioButton .getValue()		→ == false → .getValue()
MaterialTimePicker .getValue()		→ == null
MaterialTextBox .getValue()			→ .equals("")
MaterialTextBox (날짜) .getValue()		→ .equals("")

----------------------------------------------------------------------------------------------------

GWT 날짜/시간 데이터 포맷/자료형 변환
★클라이언트 - com.google.gwt.i18n.client.DateTimeFormat
★서버(일반자바) - java.text.SimpleDateFormat

ex1) 날짜
JSONObject obj = resultList.get(i).isObject();
JSONValue CREATE_DATE = obj.get("STATS_DIV_YMD");

Date date = DateTimeFormat.getFormat("yyyyMMdd").parse(CREATE_DATE.isString().stringValue().toString());
String dateFmt = DateTimeFormat.getFormat("yyyy-MM-dd").format(date);


ex2) 시간
if (componentData.containsKey("EXPSR_BGNG_TM"))
sTime.setValue(DateTimeFormat.getFormat("HH:mm:ss").parse(componentData.get("EXPSR_BGNG_TM").toString()));


ex3) 날짜시간
DateTimeFormat.getFormat("yyyy-MM-dd HH:mm:ss").format(new Date());


JSONObject에 담으면 Date자료형이 JSONValue로 바뀜.
서버쪽에서 Date자료형 쓰지 말고 문자열로 보낸다음 위처럼 클라이언트에서 DateTimeFormat쓰기

써야하는곳은 날짜선택기(input말고 진짜 날짜선택기)나 시간 선택기 에서 값을 set할때 Date자료형이기때문에 씀.

------------------------------

날짜 더하기/빼기

-----

일

Date dateFormat = DateTimeFormat.getFormat("yyyy-MM-dd").parse(date.getText());
CalendarUtil.addDaysToDate(dateFormat, 1);

-----

월

Date dateFormat = DateTimeFormat.getFormat("yyyy-MM-dd").parse(date.getText());
CalendarUtil.addMonthsToDate(dateFormat, 1);

----------------------------------------------------------------------------------------------------

GWT 문법 (회사에서 자체적으로 만든 클래스도 포함)

MaterialPanel를 상속받아 html/css를 넣을 수 있음
객체를 다 만든 후 마지막에 add로 부모에 추가. 같은 객체에 add를 두번쓰면 이전에 add했던 요소가 사라져버리니 주의.

<div>				≒	MaterialPanel
						MaterialRow
<select>				≒	MaterialComboBox<T>
					≒	MaterialListBox
					≒	MaterialListValueBox<T>
<table>				≒	ContentTable
<input-text>			≒	MaterialTextBox
<textarea>			≒	MaterialTextArea
<input>				≒	MaterialInput
<input-checkbox>		≒	MaterialCheckBox
<input-radio>			≒	new MaterialRadioButton("name속성값", "텍스트")
<button>				≒	MaterialButton
<i>					≒	MaterialIcon
label / span			≒	MaterialLabel
텍스트(span)			≒	MaterialLabel tit = new MaterialLabel("aaa");
텍스트(span)			≒	Span s = new Span("aaa");
이미지업로드			≒	UploadPanel
<img>				≒	MaterialImage
grid적용가능			≒	MaterialColumn ( MaterialColumn.setGrid("s12"); MaterualColumn에 add하고 setGrid("")하기. MaterialColumn안에 MaterialColumn를 또 쓰기도 가능 )
날짜					≒	new MaterialTextBox();.setType(InputType.DATE); or MaterialDatePicker
시간					≒	MaterialTimePicker
탭메뉴				≒	SelectionPanel
얼럿메시지			≒	MaterialToast


ex) <div>
MaterialPanel panelTop = new MaterialPanel();
panelTop.setLayoutPosition(Position.RELATIVE);
panelTop.setHeight("100%");

MaterialPanel panelBottom = new MaterialPanel();
panelBottom.setBorder("1px solid #e0e0e0");
panelBottom.setHeight("26px");
panelBottom.setPadding(0);
panelBottom.setTop(-40);
panelBottom.setLayoutPosition(Position.RELATIVE);


ex) <table>
table = new ContentTable(ContentTable.TABLE_SELECT_TYPE.SELECT_SINGLE);

table.appendTitle("cc", 90, TextAlign.CENTER);	// 열 제목 추가
table.appendTitle("aa", 180, TextAlign.CENTER);	// 열 제목 추가
table.appendTitle("xx", 80, TextAlign.CENTER);	// 열 제목 추가

table.clearRows();	// 테이블의 모든 행 지우기 (테이블 내용을 업데이트시킬때 씀. 반복문 안에서 쓰지 않게 주의)

table.addRow(Color.WHITE, list);	// 행 추가 (1행씩)
table.addRow(Color.WHITE, "xxx");	// 행 추가 (1행씩)
table.addRow(Color.WHITE, "zzz");	// 행 추가 (1행씩)

table.addRow(Color.WHITE, "a1", "a2", "a3");	// 행 추가 (여러 행)
★제목으로 지정된(appendTitle()들로 넣은) 열개수를 넘으면 java.lang.IndexOutOfBoundsException: 에러뜸

ex) <MaterialListBox>
MaterialListBox materialListBox = new MaterialListBox();
materialListBox.addItem("옵션1", "값1");
materialListBox.addItem("옵션2", "값2");
materialListBox.addItem("옵션3", "값3");

materialListBox.addValueChangeHandler(event -> {
	int selectedIndex = materialListBox.getSelectedIndex();
	String selectedValue = materialListBox.getValue(selectedIndex);
	Console.log("Selected Index: " + selectedIndex);
	Console.log("Selected Value: " + selectedValue);
});


ex)
for (int i=0; i < resultList.size(); i++) {
	JSONObject obj = resultList.get(i).isObject();
	
	JSONValue CREATE_DATE = obj.get("CREATE_DATE");
	JSONValue RATING = obj.get("RATING");
	
	Date date = DateTimeFormat.getFormat("yyyy-MM-dd HH:mm:ss.S").parse(CREATE_DATE.isString().stringValue().toString());
	String dateFmt = DateTimeFormat.getFormat("yyyy-MM-dd HH:mm:ss").format(date);
	
	tableRow = table.addRow(
		Color.WHITE,
		new int[]{1}, // 밑줄css 적용할 열번호
		COMMENT.isString().stringValue().toString(),
		POSITIVE_YN.isString().stringValue().toString() == "Y" ? "긍정" : "부정",
		NumberFormat.getFormat("0.00").format(RATING.isNumber().doubleValue()) + "%",
		dateFmt
	);
}

위처럼 .get()으로 해도 되지만 아래처럼 getString()으로 하면 null일경우 -로 출력됨
tableRow는 안써도 되지만 클릭시 이벤트를 걸기위해 tableRow에 담아서 씀

for (int i=0; i < resultList.size(); i++) {
	JSONObject obj = resultList.get(i).isObject();

	JSONValue CREATE_DATE = obj.get("CREATE_DATE");
	JSONValue RATING = obj.get("RATING");

	Date date = DateTimeFormat.getFormat("yyyy-MM-dd HH:mm:ss.S").parse(CREATE_DATE.isString().stringValue().toString());
	String dateFmt = DateTimeFormat.getFormat("yyyy-MM-dd HH:mm:ss").format(date);

	ContentTableRow tableRow = null;
	tableRow = table.addRow(
		Color.WHITE,
		getString(obj, "COMMENT"),
		getString(obj, "POSITIVE_YN") == "Y" ? "긍정" : "부정",
		NumberFormat.getFormat("0.00").format(RATING.isNumber().doubleValue()) + "%",
		dateFmt
	);
}


ex) 테이블 한개의셀에 텍스트말고 다른내용 넣기 or 텍스트인데 줄바꿈이 된 텍스트 넣기

MaterialPanel deliveryContainer = new MaterialPanel();

MaterialLabel l1 = new MaterialLabel(data.get("TRS_MN").isString().stringValue());
MaterialLabel l2 = new MaterialLabel(data.get("WYBL_NO").isString().stringValue());
deliveryContainer.add(l1);
deliveryContainer.add(l2);

row = targetTable.addRow(
		.
		.
		.
);
MaterialLabel l = (MaterialLabel) row.getColumnObject(열주소);
l.add(deliveryContainer);


테이블 제목/내용 넓이 자동 조절
table.getHeader().getElement().getStyle().setProperty("width", "auto");
table.getRowContainer().getElement().getStyle().setProperty("width", "auto");

★테이블의 특정컬럼 제어 (0번지주소)
MaterialLabel column = (MaterialLabel) tableRow.getColumnObject(2); (이떄 tableRow는 ContentTableRow클래스의 객체임)
column.setTextAlign(TextAlign.CENTER);

★테이블제목 넓이/정렬 조절 (위치가 이상할경우는 제목들의 넓이의 합계가 부모를 벗어났는지 확인)
this.table.appendTitle("No.", 100, TextAlign.CENTER);

★테이블에 데이터 넣고, 다이얼로그로 '깔끔'하게 보내기
ContentTableRow tableRow = table.addRow(Color.WHITE, new int[]{1},
		getString(dataObj, "GDS_ID"),
		getString(dataObj, "TITLE"),
		getString(dataObj, "PRVD_ENTRPS_NM"),
		getString(dataObj, "AREA_NM"),
		getString(dataObj, "PRC_GDN_CN"),
		getString(dataObj, "CONTENT_STATUS"),
		travledata,
		getString(dataObj, "THEME_LIST")
);

tableRow.put("data",dataObj);
tableRow.addClickHandler(e->{ // 상세다이얼로그로 보내기 위한 이벤트
	ContentTableRow row = (ContentTableRow)e.getSource();
	if(row.getSelectedColumn() == 1) {
		HashMap<String, Object> param = new HashMap<String, Object>();
		param.put("dataObj",row.get("data"));
		param.put("parent",this);
		this.getMaterialExtentsWindow().openDialog(GoodsManagementApplication.ADD_GOODS_DIALOG, param,1000);
	}
});

★ 뷰→모듈→xml로 파라미터전송시 모듈에서 꺼냈다가다시담는 과정없이 그대로 xml로 보내는법
JSONObject에 JSONObject를 또 담아서 보내면됨. 그리고 xml로 보낼때는 .toMap()을 반드시 붙여야함
<뷰>
JSONObject arguments = new JSONObject(), obj = new JSONObject();
obj.put("date", new JSONString(date));
arguments.put("data", obj);
VisitKoreaBusinessUtils.simpleFetch(
	"GET_PROBABILITY_WINNING_DATE"
	, arguments
	, jObject -> {
		Console.log("완료..?");
		Console.log("jObject: "+jObject);
	});
<모듈>
JSONObject param =  parameterObject.getJSONObject("data");
List<Map<String, Object>> result = sqlSession.selectList(
		"kr.or.visitkorea.system.TravSubscrbNewsLetterMapper.getProbabilityWinningDate", param.toMap());


★ ContentTableRow에 들어있는 데이터들을 JSONObject으로 바꾸는 코드 ↓↓↓
ContentTableRow row = table.getSelectedRows().get(0);
Console.log(row.CollectionToJSON());


★ JSONObject를 Map으로 바꾸기 (JSON객체에서 일일이 꺼내서 Map에 옮겨담지 않아도 됨)
(Map) JSON객체.toMap()


ex) <select>
MaterialComboBox<Object> mode = new MaterialComboBox<>();
mode.setLabel("정렬기준");
mode.setLayoutPosition(Position.ABSOLUTE);
mode.setTop(5);
mode.setLeft(10);
mode.setWidth("120px");
mode.addItem("제목", 0);
mode.addItem("CID", 1);
mode.addItem("태그", 2);
mode.addItem("작성자", 3);
mode.setSelectedIndex(0); // 선택시키기
mode.getValues(); // 목록값들 배열로 반환
mode.getSelectedIndex(); // 선택한 index 반환
mode.getSelectedValue(); // 선택한 값(들) 배열로 반환
mode.getSelectedValue().get(0); // 선택한 값 구하는 방법1
mode.getValues().get(mode.getSelectedIndex()); // 선택한 값 구하는 방법2
sort.getSelectedValue().isEmpty() { // 아무것도 선택하지 않았을경우 true


ex) 이미지업로드
imagePanel = new UploadPanel(347, 301, Registry.get("image.server") + "/img/call?cmd=VIEW&id=a9158773-bd4d-49f2-a901-d3a7e204a773&chk=e1b88981-5050-4e79-989d-7006b8b41714");
imagePanel.setButtonPostion(false);
imagePanel.setLayoutPosition(Position.ABSOLUTE);
imagePanel.setLeft(0);
imagePanel.setTop(0);
imagePanel.getUploader().addSuccessHandler(e -> {
	JSONObject resultObj = (JSONObject) JSONParser.parseStrict(e.getResponse().getBody());
	String uploadValue = resultObj.get("body").isObject().get("result").isArray().get(0).isObject().get("saveName").isString().stringValue();
	this.imgId = uploadValue.substring(0, uploadValue.lastIndexOf("."));
	this.imgExt = uploadValue.substring(uploadValue.lastIndexOf("."));
	imagePanel.setImageUrl(Registry.get("image.server") + "/img/call?cmd=TEMP_VIEW&name=" + uploadValue);
});

사용자가 올린 이미지 정보 가져오려면
저장하는 메소드에서 .getImageId() / .getImagePath()

등록된 이미지 보여줄때는
imagePanel.setImageUrl(Registry.get("image.server").toString() + "/img/call?cmd=VIEW&id="+getdata(dataobj,"IMG_ID"));


ex) 이미지 출력
img = new MaterialImage();
img.setClass("imageTest1");
img.setUrl("https://cdn.visitkorea.or.kr/img/call?cmd=VIEW&id=001ffef4-960f-440a-9fc4-229c532c3727");
container.add(img);

ex) 표(ContentTable) 안의 이미지 출력
private MaterialImage image;
for문{
	String imgPath = obj.containsKey("IMG_PATH") ? obj.get("IMG_PATH").isString().stringValue() : "";
	MaterialLabel imageLabel = (MaterialLabel) tableRow.getColumnObject(4);
	
	if(!imgPath.equals("")) {
		image = new MaterialImage(
				Registry.get("image.server") + "/img/call?cmd=VIEW&id=" +
						imgPath.substring(imgPath.lastIndexOf("/") + 1, imgPath.lastIndexOf(".")));
	
		image.setPadding(5);
		image.setHeight("150px");
	
		imageLabel.setText("");
		imageLabel.setHeight("100%");
		imageLabel.setDisplay(Display.FLEX);
		imageLabel.setFlexJustifyContent(FlexJustifyContent.CENTER);
		imageLabel.setFlexAlignItems(FlexAlignItems.CENTER);
		imageLabel.getElement().getStyle().clearOverflowX();
		imageLabel.add(image);
	}
}


ex) 다이얼로그에서 이미지 출력

1. 이미지를 필드변수로 선언
private MaterialImage img;

2. init() 메소드 안에서 임의의 div안에 이미지 생성 후 삽입
MaterialColumn colImg = new MaterialColumn(4,4,4);
colImg.setMargin(0);
colImg.setPadding(0);
colImg.setHeight("150px");
img = new MaterialImage();
colImg.add(img);
mpdetail.add(colImg);

3. onLoad() 메소드 안에서 이미지 경로 지정 (setURL() 이용. 만약 이미지 객체에서 src경로String을 꺼내고 싶을때는 getURL() 이용하기)
String imgPath = toText(this.getParameters().get("image"));
img.setUrl(Registry.get("image.server") + "/img/call?cmd=VIEW&id=" +
				imgPath.substring(imgPath.lastIndexOf("/") + 1, imgPath.lastIndexOf(".")));
img.setPadding(5);
img.setHeight("150px");


ex) <i, 아이콘>
MaterialIcon icon = new MaterialIcon(IconType.SEARCH);

버튼
clb1 = new ContentLinkButton("전체 선택 (시스템 포함)");

목록 (시스템도구 → 사용자 → 왼쪽 사용자 목록)
AccountListItem

트리형태 목록 (시스템도구 → 사용자 → 오른쪽 권한 목록)
MaterialTree tree = new MaterialTree();

로딩 애니메이션 (시스템도구 → 사용자 → 권한 변경시 (DeSelectAllPermissionsForAdmin.java))
MaterialLoader.loading(false, getPanel());


this.mtno = addTextBox(mpdetail, 4, "사용자");
1번째 인수 : 컨테이너
2번째 인수 : 그리드
3번째 인수 : input-text 위에 라벨


ex) input-radio버튼
MaterialRadioButton setType = new MaterialRadioButton("name속성값");
MaterialRadioButton setType = new MaterialRadioButton("name속성값","텍스트");
setType.setEnabled(false); // disabled(비활성화)
setType.setText("요일/시간으로 설정"); // 텍스트
setType.setFormValue("WT"); // value속성값
체크시키기 → this.rdSetWT.setValue(true)
해당버튼체크여부(각각체크함) → rdSetWT.getValue()

ex) 날짜 선택기 (MaterialDatePicker 도 있긴하지만 MaterialtextBox가 더 간편)
MaterialTextBox sDate, eDate;
sDate = new MaterialTextBox();
sDate.setType(InputType.DATE);
sDate.setDisplay(Display.INLINE_BLOCK);
sDate.setWidth("150px");
sDate.setEnabled(false); // disabled(비활성화)
periodWrap.add(sDate);

날짜 세팅은 아래처럼. (setValue같은, 값 세팅하는 메소드에 넣고, JSONObject로 불러올떄 양끝 ""(따옴표) 빼줘야함)
혹은 .isString().stringValue() 붙이기
sDate.setText(VisitKoreaBusinessUtils.removeQuot(componentData.get("EXPSR_BGNG_YMD")));


ex) 시간 선택기
private MaterialTimePicker sTime, eTime;

sTime = new MaterialTimePicker("시작시간");
sTime.isReadOnly();
sTime.setDisplay(Display.INLINE_BLOCK);
sTime.setWidth("100px");
sTime.setOkText("확인"); // 팝업창 확인버튼 텍스트
sTime.setCancelText("취소"); // 팝업창 취소버튼 텍스트
sTime.addMouseDownHandler(e->{
	e.preventDefault();
});
mtDate.addChangeHandler(e -> { // 날짜선택기로 바꾼경우
	rDate.setText(mtDate.getText());
});
timeWrap.add(sTime);

mouseDown 이벤트, preventDefault를 꼭 넣어야함 (안그러면 눌렀다 떼자마자 사라짐)

참고: https://gwtmaterialdesign.github.io/gwt-material-demo/apidocs-addins/gwt/material/design/addins/client/timepicker/MaterialTimePicker.html
참고2: https://material.io/components/time-pickers


ex) MaterialToast
MaterialToast.fireToast("경고메시지");

ex) alert
Window.alert("문자열")

----------------------------------------------------------------------------------------------------

표(ContentTable) 아래에 붙는 아이콘

1. 아이콘을 먼저 만든다
icon1 = new MaterialIcon(IconType.DELETE);
icon1.setTextAlign(TextAlign.CENTER);
icon1.addClickHandler(event->{
	removeMemberTag();
});

2. 영역에 넣는다(.add() 메소드 대신 씀. 사용자클래스임)
(첫번째인수는 버튼객체, 두번째 인수는 버튼에 마우스 오버시 나오는 내용, 세번째 인수는 좌우위치선택가능 left / right / none)
table.getButtomMenu().addIcon(icon1, "삭제", com.google.gwt.dom.client.Style.Float.LEFT);

----------------------------------------------------------------------------------------------------

★이벤트

gwt요소에 클릭 등의 이벤트를 걸 수 있음

.addClickHandler() : 클릭했을때
.addKeyUpHandler() : 키올라갔을때
.addFocusHandler() : 포커스 됐을때
.addBlurHandler() : 포커스가 해제됐을때
.addValueChangeHandler() : 값이 변경되면서 포커스가 해제됐을때
.
.

ex)
MaterialIcon icon = new MaterialIcon(IconType.SEARCH);
icon.addClickHandler(e -> {
	Console.log("클릭함");
});

-----

<테이블 행>
tableRow에 담아야 이벤트를 걸 수 있고, tableRow에 .put()을 하면 화면에 안보이게 데이터를 넣을 수 있음 input-hidden느낌.
tableRow에 put으로 JSONObject를 통으로 넣어놓으면 사용자가 선택한 행의 데이터 조작시 정보를 꺼내 쓰기 좋음

ContentTableRow tableRow = null;
tableRow = table.addRow(
	Color.WHITE,
	getString(obj, "COMMENT"),
	getString(obj, "POSITIVE_YN") == "Y" ? "긍정" : "부정",
	NumberFormat.getFormat("0.00").format(RATING.isNumber().doubleValue()) + "%",
	dateFmt
);

tableRow.put("CMT_ID",getString(obj, "CMT_ID"));	// 이렇게 일부만 넣어놓거나 (★비추천)
tableRow.put("data", obj);						// xml로 받아온 JSONObject를 통째로 다 넣어놔도 됨 (★추천)

tableRow.addClickHandler(event -> {
	ContentTableRow ctr = (ContentTableRow)event.getSource();
	String CMT_ID = ctr.get("CMT_ID").toString();

	Console.log(ctr.toString());
	Console.log(CMT_ID);

	if(ctr.getSelectedColumn() == 0) {
		Console.log("첫번째열 클릭");
	}
});

------------------------------

사용자가 클릭해 선택된 "행" 정보 가져오기

테이블 만들때 ContentTableRow 써서 만들고
거기에 put()메소드로, 사용할 정보를 또 담아놔야함
addrow.put("data",JSON객체); 이런식으로 한번에 담아놓으면 좋음

담았다면
table에 getSelectedRows().get(0).get("담았던 키") 메소드를 쓰면 받아짐

JSONObject dataObj = (JSONObject) table.getSelectedRows().get(0).get("data");
String cotId = dataObj.get("cotId").toString();


행에서 특정 열 정보 가져오기

targetRow.getColumnObject(열index);


텍스트 가져오려면 아래 메소드 붙이면 됨
.getElement().getInnerText()

------------------------------

사용자가 클릭해 선택된 "열" 정보 가져오기

테이블 만들때 ContentTableRow 써서 만들고
addrow = targetTable.addRow(
	Color.WHITE

거기에 클릭이벤트를 걸어서
addrow.addClickHandler(e->{
	ContentTableRow row = (ContentTableRow)e.getSource();
이벤트객체에서 getSource()를 써야함

그리고 다시 그 객체에 getSelectedColumn() 쓰기
row.getSelectedColumn()

------------------------------

★input-text 내용 바뀌었을때(엔터쳤을때 포함) 이벤트

searchText = new MaterialTextBox();
searchText.addValueChangeHandler(e -> {
	Console.log("searchText --> " + searchText.getValue());
});

★키 입력했을때 이벤트
.addKeyUpHandler(e -> {

----------------------------------------------------------------------------------------------------

GWT쓸때 System.out.println() 안나오면

이클립스 콘솔창 메뉴에서 화살표 눌러서 Tomcat으로 바꾸기

----------------------------------------------------------------------------------------------------

권한 있는지 체크

if(Registry.getPermission("547beeb2-f5e8-422e-a63c-fa9323d8242c")){

----------------------------------------------------------------------------------------------------

다이얼로그(dialog) 만드는법

DialogContent 를 만들고 → dialogID로 DialogContent를 찾는다

1-1. DialogContent를 상속받는 파일(이하 다이얼로그)을 만들기

1-2. 생성자 추가
public 클래스명(MaterialExtentsWindow window) {
	super(window);
}

2-1. ApplicationBase을 상속받은, 이미 만들어져있는 파일(부모 페이지를 생성한 자바파일)에서 연결 (필드에 변수 추가)
public static final String SELECT_COMMENT_ANALYSIS_DIALOG = "SELECT_COMMENT_ANALYSIS_DIALOG";

2-2.setWindow메소드에 아래처럼 연결
this.window.addDialog(SELECT_COMMENT_ANALYSIS_DIALOG, new SelectCommentAnalysis(this.window));

3. 기존에 있던 AbstractContentPanel를 상속받은 파일(이하 패널)에서 이벤트 발생시 열기 (데이터안보낼거면 Map 인수는 안넣어도됨)
tableRow.addClickHandler(event -> {
	ContentTableRow ctr = (ContentTableRow)event.getSource();
	String CMT_ID = ctr.get("CMT_ID").toString();

	if(ctr.getSelectedColumn() == 0) {

		HashMap<String, Object> map = new HashMap<>();
		map.put("CMT_ID", CMT_ID);
		map.put("COMMENT", obj.get("COMMENT"));
		map.put("POSITIVE_YN", obj.get("POSITIVE_YN"));
		map.put("RATING", obj.get("RATING"));
		map.put("CREATE_DATE", dateFmt);
		map.put("host", host);

		getMaterialExtentsWindow().openDialog(CommentAnalysisMain.SELECT_COMMENT_ANALYSIS_DIALOG, map, 800);

	}
});


4. 다이얼로그 높이 설정 (너비는 호출하는곳에 3번째 인수로 있음)
@Override
getHeight(){
	return 650;
}

5. 기본닫기버튼 넣기
public void init() {
	addDefaultButtons();
}

6. 띄워진 다이얼로그의 모든 UI는 init(){} 안에서 그리면됨 (init()메소드는 다이얼로그가 띄워지기 전부터 호출됨)

7. 띄워진 다이얼로그에서 파라미터로 받아온 정보를 UI에 담을때는 onLoad(){} 안에서 담아야됨
@Override
	public void onLoad() {

★onLoad() 메소드는 다이얼로그가 띄워졌을때  호출됨. getParameters()를 init()메소드 안에 넣어놓으면 시점문제로 값이 안받아짐 (undefined) )
그리고 onload안에 UI를 생성하는 코드를 넣어놓았을 경우에는 닫았다 열면 UI들이 계속쌓이니 주의.
이때 해결방법은
1. 부모에 .clear()를 먼저 하고 UI&데이터를 한번에 넣는 방법
2. UI는 init(){}메소드 안에 넣고, 데이터는 onLoad(){} 메소드 안에 넣는 방법


다이얼로그 콘텐츠배경색 변경 (좀더밝음)
setBackgroundColor(Color.GREY_LIGHTEN_5);


화면 아래쪽에 다이얼로그 열려있는 목록 동작 관련한 기능을 위한 코드
this.windowLiveFlag = true;
super.window.addCloseHandler(handler -> {
	super.windowLiveFlag = false;
});

??????????????????
host = (CommentAnalysisMainView) getParameters().get("host");

??????????????????
this.window.actionTarget(divisionName);

??????????????????
this.setDivisionName(divisionName);


getHeight 메소드의 리턴값이 0으로 돼있으면 배경이 안나오고 닫기버튼도 안나오니 체크

닫기버튼 안눌러지면(오류나면) MaterialExtentsWindow객체 설정 문제

-----

닫기버튼 사용자설정으로 만들기

private MaterialButton btnClose;

private void buildContent() {
	btnClose = new MaterialButton("닫기");
	btnClose.setLayoutPosition(Position.ABSOLUTE);
	btnClose.setWidth("150px");
	btnClose.setBackgroundColor(Color.GREY_DARKEN_1);
	btnClose.setTop(10); btnClose.setRight(30);
	btnClose.addClickHandler(e->{
		getMaterialExtentsWindow().closeDialog();
	});
	// btnClose.setEnabled(true);
	this.add(btnClose);
}

-----

다이얼로그 클래스내부에서 해당 다이얼로그를 여는 (openDialog메소드가 있는) 클래스에 있는 메소드를 쓰는 방법 

1. 다이얼로그로 Map 보낼때 this도 같이 전송
Map<String, Object> map = new HashMap<>();
map.put("SEQ", finalI + 1);
map.put("ID", obj.containsKey("ID") ? obj.get("ID").isString().stringValue() : "");
map.put("TITLE", obj.containsKey("TITLE") ? obj.get("TITLE").isString().stringValue() : "");
map.put("CONTENT", obj.containsKey("CONTENT") ? obj.get("CONTENT").isString().stringValue() : "");
map.put("CREATE_DATE", obj.containsKey("CREATE_DATE") ? obj.get("CREATE_DATE").isString().stringValue() : "");
map.put("parent", this);

this.meWindow.openDialog(TestBoardApplication.TEST_BOARD_DETAIL, map,800);


2. 다이얼로그 파일 필드에 다이얼로그를 열기 전의 클래스를 선언
private 클래스 hostPanel;

3. 다이얼로그 onLoad메소드 내부에서 객체 대입
if (super.getParameters().containsKey("parent")) {
	this.hostPanel = (TestBoardPannel)super.getParameters().get("parent");
}

4. 필요한 부분에서 메소드 사용
hostPanel.메소드();

----------------------------------------------------------------------------------------------------

테이블 행마다 링크걸기 (테이블 아니여도됨)

Window.open(Registry.get("service.server") + "/trss/intro.do?tnmId=" + 변수, "_blank", "enable");

----------------------------------------------------------------------------------------------------

sql 쿼리문 불러오는 "cmd"키로 불러오는 부분

JSONObject parameterJSON = new JSONObject(); // JSON객체 생성후
parameterJSON.put("cmd", new JSONString("GET_OTHER_DEPARTMENT_MAIN")); // cmd키와 함께 sql쿼리문에 필요한 파라미터들을 담아서

VisitKoreaBusiness.post("call", parameterJSON.toString(), new Func3<Object, String, Object>() { // 2번째 인수로, mybatis와 연결되는 .java파일에 전달함
	@Override
	public void call(Object param1, String param2, Object param3) {

↓↓↓람다로 하면↓↓↓

VisitKoreaBusiness.post("call", checkCmdArguments.toString(), (o1, o2, o3) -> {

----------------------------------------------------------------------------------------------------

mybatis xml파일 새로 추가해야할떄는

그냥 <mapper namespace="XXX"> 만 바꾼다고 끝이 아니라
QueryMappingConfig.xml 에서 <mapper resource="XXX" />추가도 해줘야 연결이 됨

----------------------------------------------------------------------------------------------------

표 만들때 화면에는 안보이게 값만 넣어놓을때
↓↓↓
테이블 생성 이후 tableRow.put("이름",값)

tableRow = table.addRow(
	Color.WHITE,
	new int[]{0},
	getString(obj, "STATS_DIV_YMD"),
	getString(obj, "COOKIE_VAL"),
	getString(obj, dateFmt),
	getString(obj, "SNS_ID"),
	getString(obj, "INQ_NUM"),
	dateFmt
);

tableRow.put("CMT_ID", getString(obj, "CMT_ID"));

----------------------------------------------------------------------------------------------------

view페이지 부터 mybaits까지 파라미터를 넘길때 없으면 처리 안하고 있을때만 처리되게 하려면

<뷰>
JSONObject paramJson = new JSONObject();
	paramJson.put("cmd", new JSONString("GET_EVENT_VISIT_ANALYSIS"));
	if (!mode.getSelectedValue().isEmpty()) { ★★★★★
		paramJson.put("mode", new JSONString((String) mode.getSelectedValue().get(0)));

<모듈>
HashMap<String, Object> paramMap = new HashMap<String, Object>();
if (parameterObject.has("mode")){ ★★★★★
	paramMap.put("mode", parameterObject.getString("mode"));

<xml>
 <sql id="criteria">

        <if test="! mode == null')">
            <trim prefix="WHERE">
            <if test="mode == 'U90'.toString()">
                RATING >= 90
            </if>

----------------------------------------------------------------------------------------------------

MaterialComboBox<Object> 로 선택한 값 받을때


MaterialComboBox<Object> mode;
.
.
.
mode.getSelectedValue()); 이렇게 하면 이상하게 배열로 감싸짐..
.get(0) 으로 벗기기
mode.getSelectedValue()).get(0)

----------------------------------------------------------------------------------------------------

선택한 값 받을때 무슨메소드로 받아야하는지 모르겠는경우 다음 메소드들로 받아지나 해보기


MaterialComboBox<Object> → getSelectedValue()	(이건 배열로 받아지는데 .isEmpty()로 null체크 후 .get(0)으로 받아야함)

MaterialTextBox → getText() or getValue()

SelectionPanel → getSelectedText()


안되면 요소 클래스명 퀵서치 검색 후
그래도 없으면 웹검색

----------------------------------------------------------------------------------------------------

.stringValue()
엔터(줄바꿈) 쳐지도록 (\n을 엔터로 바꾸기)

JSONObject에서 뽑은 JSONValue를 먼저 .isString()으로 JSONString으로 바꾼 후 .stringValue() 메소드를 써야함
String contentTxt = toText(((JSONValue)this.getParameters().get("introCn")).isString().stringValue());
contentTxt = contentTxt.replaceAll("&#63;", "?");

----------------------------------------------------------------------------------------------------

하위/상위 요소 접근 가능

.getElement().getFirstChildElement()
.getElement().getFirstChildElement().getNextSiblingElement()
.getElement().getParentElement()

----------------------------------------------------------------------------------------------------

다이얼로그 닫기

getMaterialExtentsWindow().closeDialog();

----------------------------------------------------------------------------------------------------

JSONNumber객체안에 담긴 숫자는 부모 JSONObject를 toMap으로 바꿨을때 null이 됨

toMap메소드를 쓸때는 JSONNumber쓰면 안되고 JSONString으로 쓰기

----------------------------------------------------------------------------------------------------

엑셀 다운로드

private void databaseImgUrlList(XSSFSheet objSheet, XSSFRow objRow, XSSFCell objCell, CellStyle headStyle, XSSFWorkbook objWorkBook) {
	String type = parameterObject.getString("type");
	String[][] pair = {{"COT_ID", "cotid"}, {"CONTENT_ID", "cid"}, {"CATEGORY", "타입"}, {"TITLE", "콘텐츠명"}, {"TYPE", "분류(기사/DB)"}, {"IMG_ID", "이미지URL"}};
	List<HashMap<String, Object>> list = new ArrayList<>();

	try {
		list = sqlSession.selectList("kr.or.visitkorea.system.DatabaseMapper.SelectImgUrlListExcelDownload", type);
	} catch (Exception e) {
		e.printStackTrace();
	}
	System.out.println("list.size(): "+list.size()); // 테스트용
	System.out.println("list.get(0): "+list.get(0)); // 테스트용

	int sheetCnt = list.size() / 10000; // 시트 분할
	int colSize = pair.length; // 열 개수

	objWorkBook.removeSheetAt(0);
	for (int h = 0; h < sheetCnt; h++) { // 시트수만큼 반복
		objSheet = objWorkBook.createSheet("이미지" + h); // 시트 생성
		objRow = objSheet.createRow(0); // 첫번째 행에 행객체를 생성
		for (int i = 0; i < colSize; i++) { // 컬럼수만큼 반복
			objSheet.setColumnWidth(i, 6000); // 셀너비 설정
			objCell = objRow.createCell(i); // 셀객체 생성
			objCell.setCellStyle(headerStyle1(headStyle, objWorkBook)); // 셀스타일 입히기
			objCell.setCellValue(pair[i][1]); // 셀내용 삽입
		}
		for (int i = 0; i < list.size(); i++) { // 행수만큼 반복
			objRow = objSheet.createRow(i + 1); // 제목행 다음부터 시작. 행객체 생성
			for(int i2 = 0; i2 < colSize; i2++) { // 컬럼수만큼 반복
				objCell = objRow.createCell(i2); // 셀객체 생성
				objCell.setCellValue(list.get(i).get(pair[i2][0]) == null ? "" : list.get(i).get(pair[i2][0]).toString()); // 셀내용 삽입
			}
		}
	}
}

private CellStyle headerStyle1(CellStyle headStyle, XSSFWorkbook objWorkBook) {
	// 테이블 헤더용 스타일
	headStyle = objWorkBook.createCellStyle();

	// 가는 경계선을 가집니다.
	headStyle.setBorderTop(BorderStyle.THIN);
	headStyle.setBorderBottom(BorderStyle.THIN);
	headStyle.setBorderLeft(BorderStyle.THIN);
	headStyle.setBorderRight(BorderStyle.THIN);

	// 배경색은 노란색입니다.
	headStyle.setFillForegroundColor(HSSFColorPredefined.YELLOW.getIndex());
	headStyle.setFillPattern(FillPatternType.SOLID_FOREGROUND);

	// 데이터는 가운데 정렬합니다.
	headStyle.setAlignment(HorizontalAlignment.CENTER);
	return headStyle;
}

----------------------------------------------------------------------------------------------------

부모요소

GWT객체.getElement().getParentNode() → 안되는듯?

------------------------------

자식 요소 계속 탐색하기

형변환(다운캐스팅) 하면 됨

((MaterialWidget)container.getChildren().get(1)).getChildren().get(1)

----------------------------------------------------------------------------------------------------

표에서 정렬이 뭔가 이상하면 각각의 제목넓이값를 높여보기

모두 더한값이 컨테이너 넓이에 근접해야함

컨테이너너비랑 똑같아도 padding때문에 틀어짐(정확히는 컨테이너너비 - 2px 가 되어야함)

----------------------------------------------------------------------------------------------------

지연실행 (자바스크립트의 setTimeout)

Timer timer = new Timer() {
	@Override
	public void run() {
		실행할 내용
	}
};
timer.schedule(1000);

----------------------------------------------------------------------------------------------------

이벤트핸들러에서 this 안될때 파라미터로 하기

s1.addClickHandler(event -> {
	Console.log(this + "");
});

↓↓↓

s1.addClickHandler(event -> {
	Widget clickedWidget = (Widget) event.getSource();
	Console.log(clickedWidget + "");
});

----------------------------------------------------------------------------------------------------

클릭한요소가 부모요소로부터 몇번쨰인지 순번(인덱스) 구하기 (= 제이쿼리 .index())

newItem.addClickHandler(event -> {
	MaterialWidget mw = (MaterialWidget) event.getSource();
	Element parent = mw.getElement().getParentElement();
	int idx = -1;

	for (int i = 0; i < parent.getChildCount(); i++) {
		if (parent.getChild(i).isOrHasChild(mw.getElement())) {
			idx = i;
			break;
		}
	}
	Console.log(idx+"");
});

----------------------------------------------------------------------------------------------------

























