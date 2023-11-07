sql 로그를 보이게 하고 싶을때 (System.out.println)

logback.xml 에서 <appender-ref 태그 아래처럼 변경

<root level="info">
	<!--<appender-ref ref="CONSOLE" />-->	안나오게
	<appender-ref ref="FILE" />				안나오게
↓↓↓
	<appender-ref ref="CONSOLE" />			나오게
	<!--<appender-ref ref="FILE" />-->			나오게
</root>

----------------------------------------------------------------------------------------------------

투어API에 올렸다는 콘텐츠가 대구석에서 안나오면

투어API사이트로 들어가서 컨텐츠 데이터가 잘 올라와있는가 확인. https://api.visitkorea.or.kr/ 에서 검색.
텍스트(엑셀)다운로드로 받으면 텍스트를 편하게 볼수있음(로그인필요)

컨텐츠가 정상으로 나오고있는지 확인
안나오면?
	1. 젠킨스 로그에서 처음부분에 getMasterURL --> 이렇게 되어있는거 처음부터 URL 들어가보기
	2. 이상있는 콘텐츠 제목 검색
		안나오면?
			투어api에서 안올렸거나 늦게(스케줄러 동작이후 → ex.아침에) 올린것.
			투어api에서 올려놓은걸 새벽에 배치프로그램으로 다운받는데
			아침에 수정한건 그 다음날새벽에 반영되기때문에 수동으로 반영해줘야함
		나오면?
			프로그램실행중 오류가 났는지 확인.
				안났으면?
					1. CONTENT_MASTER 테이블에서 TITLE / DISPLAY_TITLE 컬럼으로 검색해서 데이터가 있는지 확인
					2. DATABASE_MASTER 테이블에서 COT_ID 컬럼으로 검색해서 데이터가 있는지 확인
					3. IMAGE 테이블에서 COT_ID 컬럼으로 검색해서 데이터가 있는지 확인
					4. <img src="https://cdn.visitkorea.or.kr/img/call?cmd=VIEW&id=이미지ID"> id value로 IMG_ID값 넣어보기
						나오면?
							정상적으로 받아진거
						안나오면?
							Firefox브라우저로 들어가보기
								나오면?
									CDN의 문제
								안나오면?
									IMAGE 테이블의 URL 컬럼값을 브라우저로 들어가보기 (http://tong.visitkorea.or.kr/~~)
										나오면?
											CDN의 문제
										안나오면?
											투어API의 문제
				났으면?
					왜 났는지 로컬로 돌려보기
					이경우는 투어api에 정상적으로 요청을 했는데 안나오는 경우임
					좀 있다가 다시 run 하면 오류가 안나는 경우가 있음

투어api 낚시 주의
★★★젠킨스 로그에 있는 URL을 브라우저로 들어갔을때 나오는건 과거 로그가 아니고 들어간 현재 요청한것임★★★

----------------------------------------------------------------------------------------------------

투어api에서 샘플데이터에 문제가 있을때 먼저 연관된 테이블 싹 json으로 복사 후
서브라임같은데 붙여넣어놓고
젠킨스로 해당날짜 실행해서
다 되면 다시 연관된 테이블들 싹 json으로 복사후 서브라임 새탭에 붙여넣어서
인텔리제이로 테이블별로 데이터의 차이 (바뀐 데이터를)를 비교하기

----------------------------------------------------------------------------------------------------

오류모음

<errMsg>SERVICE ERROR</errMsg>
<returnAuthMsg>APPLICATION_ERROR</returnAuthMsg>
<returnReasonCode>01</returnReasonCode>
or
<errMsg>SERVICE ERROR</errMsg>
<returnAuthMsg>SERVICE_KEY_IS_NOT_REGISTERED_ERROR</returnAuthMsg>
<returnReasonCode>30</returnReasonCode>
↓↓↓
짧은 시간에 너무 많은 호출시 발생.
1시간 후에 다시 시도하기

----------------------------------------------------------------------------------------------------

인텔리제이 기준

Run/Debug Configurations(실행/디버그 구성) → Build and run(빌드 및 실행) 부분 → Modify options(옵션 수정) → Program Parameter(프로그램 인수)
여기서 옵션을 지정 할 수 있는데,

옵션설정을 하면 ApplicationArguments 인터페이스 변수에 배열로 담김.

프로그램인수: update

아래처럼 이용
return (ApplicationArguments args) -> {
	Arrays.stream(args.getSourceArgs())
			.forEach(arg -> {
				System.out.println("arg --> " + arg);
			});
	if (args.getSourceArgs().length == 0) {
		printVersion();
		printHelp();
		return;
	} else if (args.containsOption(VERSION)) {
		printVersion();
		return;
	} else if (args.containsOption(HELP)) {
		printHelp();
		return;
	}

	if (args.getSourceArgs()[0].equals("fetch")) {


또 뒤에 --를 붙여 옵션을 추가 할 수 있는데
프로그램인수: update --dates=20220810

그러면 아래처럼 쓸 수 있음
if (args.containsOption("dates")) {

이걸 젠킨스에서 "구성" 페이지에서
프로젝트를 특정 옵션을 넣어서 실행하는 코드를 만든 후
특정 시각마다 자동으로 실행되게 설정 할 수 있음

운영계에서 실행하고싶으면 젠킨스(Jenkins → 'scheduler' → Server_PNM_WEB → scheduler-batch-tourapi) 에서 Build Now 누르면 되고
개발계에서 테스트하고싶으면 application.properties에서 db정보(spring.datasource.url) 바꿔서 로컬실행하면됨

운영계 "실행" 말고 "배포"는 권한 미부여 상태. 경로는 다음과 같음
Jenkins → 'scheduler' → Server_PNM_WEB → scheduler-batch-tourapi

----------------------------------------------------------------------------------------------------

api 요청실패시 1초 단위로 5번까지 재요청

/**
 * 요청에 실패시 최대 5번까지만 재요청한다.
 */
private static JsonNode readTreeRetry(URL url) throws InterruptedException {
	ObjectMapper mapper = new ObjectMapper();
	JsonNode root = null;
	boolean isSuccess = false;
	for (int i = 0; i < 5; i++) {
		if (isSuccess) {
			return root;
		}
		if (i != 0) {
			System.out.println("retry count --> " + i);
		}
		try {
			root = mapper.readTree(url);
			validate(root);
			isSuccess = true;
		} catch (IOException e) {
			e.printStackTrace();
		}
		Thread.sleep(1000);
	}
	return root;
}

----------------------------------------------------------------------------------------------------

api 요청 실패시 요청실패했다는 예외 메시지 출력

private static void validate(JsonNode root) {
	String resultCode = root.findPath("resultCode").asText();
	if (!resultCode.equals("0000")) {
		throw new RuntimeException("API 요청에 실패했습니다.");
	}
}

----------------------------------------------------------------------------------------------------

투어api호출과정

공공데이터포털(data.go.kr)의
"한국관광공사_국문 관광정보 서비스_GW" - ~~/KorService/areaBasedList
"한국관광공사_무장애 여행 정보_GW" - ~~/KorWithService/areaBasedList
"한국관광공사_생태 관광 정보_GW" - ~~/GreenTourService/areaBasedList


로 정보를 요청함 (아래는 "한국관광공사_국문 관광정보 서비스_GW"에 필요한 파라미터들임)

BASE_URL = "https://apis.data.go.kr/B551011";
SERVICE_KEY = "A%2BycgFhk2eYE6mEw%2B6%2FhcCbRDaCPGJf3aLCdYyfzuqRx6iY2b%2F04BmXgnQoTrGhm1FBQ%2BOVA5mbMogKlHFcDgw%3D%3D";
MOBILE_OS = "ETC";
MOBILE_APP = "BatchApp";
path = KorService/areaBasedList
pageNo=1&numOfRows=100&arrange=C&_type=json

https://apis.data.go.kr/B551011/KorService/areaBasedList?ServiceKey=A%2BycgFhk2eYE6mEw%2B6%2FhcCbRDaCPGJf3aLCdYyfzuqRx6iY2b%2F04BmXgnQoTrGhm1FBQ%2BOVA5mbMogKlHFcDgw%3D%3D&MobileOS=ETC&MobileApp=BatchApp&pageNo=1&numOfRows=100&arrange=C&_type=json

------------------------------

Jenkins → 'visitkoreatourapibatch' → visitkorea-tourapi-batch-prod
https://jenkins.visitkorea.or.kr/view/'visitkoreatourapibatch'/job/visitkorea-tourapi-batch-prod/changes
소스는 여기에 올라가고

Jenkins → 'scheduler' → Server_PNM_WEB → scheduler-batch-tourapi
https://jenkins.visitkorea.or.kr/view/'scheduler'/job/Server_PNM_WEB/job/scheduler-batch-tourapi/1160/changes
젠킨스 스케줄러로 오전4시마다 자동으로 실행됨

----------

1. 메인메소드 대신 Bean 어노테이션 사용

@Bean
@Profile("!test")
public ApplicationRunner applicationRunner(ApplicationContext context) {


2. 프로그램 인수 & --옵션 에 따라 처리

if (args.getSourceArgs()[0].equals("fetch")) {
      if (args.containsOption("dates")) {
         String dates = args.getOptionValues("dates").get(0);
         if (dates.contains(",")) {
            String[] startEnd = dates.split(",");
            fetchRunner.execute(startEnd[0], startEnd[1]);
         } else {
            fetchRunner.execute(dates, dates);
         }
         writeToFile(fetchRunner.getResultList(), args);
      } else if (args.containsOption("cid-file")) {
         String cidFileName = args.getOptionValues("cid-file").get(0);
         filteredFetchRunner.execute(loadContentIdArray(cidFileName));
         writeToFile(filteredFetchRunner.getResultList(), args);
      } else if (args.containsOption("cid")) {
         filteredFetchRunner.execute(args.getOptionValues("cid").get(0).split(","));
         writeToFile(filteredFetchRunner.getResultList(), args);
      } else {
         printHelp();
      }
   } else if (args.getSourceArgs()[0].equals("update")) {
.
.


3. FetchRunner의 execute 메소드

공공데이터포털에서 컨텐츠 간략정보 목록을 받아오는 역할
TourApiClient.TourApiClientBuilder 로 URL을 만들어서 요청함

<FetchRunner.java>
@Override
public void execute(String... args) {
.
.
   ExecutorService threadPool = Executors.newFixedThreadPool(10);
   Future<List<Master>> listFuture1 = threadPool.submit(TourApiClientCallableFactory.getKorServiceMasterCallable(start, end)); // 국문 관광
   Future<List<Master>> listFuture2 = threadPool.submit(TourApiClientCallableFactory.getKorWithServiceMasterCallable(start, end)); // 무장애 여행
   Future<List<Master>> listFuture3 = threadPool.submit(TourApiClientCallableFactory.getGreenTourServiceMasterCallable(start, end)); // 생태 관광

↓↓↓

<TourApiClientCallableFactory.java> - 국문 관광
public static Callable<List<Master>> getKorServiceMasterCallable(long start, long end) {
	return createTourAPIMasterCallable(TourApiClient.builder().listYN("Y").path("KorService/areaBasedList"), start, end);
}

↓↓↓

<TourApiClientCallableFactory.java> - 국문관광
private static Callable<List<Master>> createTourAPIMasterCallable(TourApiClient.TourApiClientBuilder builder, long start, long end) {

이때 List<Master>는 아래와 같음
[
    {readcount=17931, modifiedtime=20220915155736, contentid=2458348, contenttypeid=12},
    {readcount=2553, modifiedtime=20220915154906, contentid=2366217, contenttypeid=14},
    {readcount=24458, modifiedtime=20220915153947, contentid=1541165, contenttypeid=12},
    .
    .
]
↓↓↓
TourApiClientCallableFactory 에서 base가 되는 데이터를, 날짜 상관없이 모두 '수정일' 순으로, 날짜범위에 들어오는지 확인하면서 기본정보목록이 있는URL을 한페이지씩 계속 요청한다 (수정일 내림차순 조회 파라미터 → arrange=C)
배열목록을 받으면 그 안의 기본정보 항목들을 jsonArray로 변환 후 `TypeReference` 로 원하는 속성("contentid","contenttypeid","modifiedtime","readcount","withtour","greentour”)들만 취해서 `List<Master>` 에 담는다 
그리고 항목이 날짜를 벗어날 경우 기본정보목록URL 호출을 종료하고. ③으로 List를 돌려준다

private static Callable<List<Master>> createTourAPIMasterCallable(TourApiClient.TourApiClientBuilder builder, long start, long end) {
   ObjectMapper mapper = new ObjectMapper();
   TypeReference<List<Master>> typeReference = new TypeReference<List<Master>>() {};
   return () -> {
      List<Master> resultList = new ArrayList<>();

      boolean tracking = false;
      boolean needToFetchMore = true;
      while (needToFetchMore) {
         TourApiClient client = builder.build();
         System.out.println("getMasterURL --> " + client.getMasterURL());
         JsonNode root =readTreeRetry(client.getMasterURL());
         JsonNode item = root.findPath("item");
         if (item.isArray()) {
            String itemString = item.toString();
            List<Master> items = mapper.readValue(itemString, typeReference);
            for (Master i : items) {
               if (i.getModifiedDate() <= end) {
                  tracking = true;
               }

               if (tracking) {
                  if (i.getModifiedDate() >= start) {
                     resultList.add(i);
                  } else {
                     needToFetchMore = false;
                  }
               }
            }
         }

         final int totalCount = root.findPath("totalCount").asInt();
         if ((int) Math.ceil((double) totalCount / client.getRowsPerPage()) < client.getPageNo()) {
            break;
         }

         if (needToFetchMore) {
            builder.pageNo(client.getPageNo() + 1); // increase page!!
         }
      }
      System.out.println("resultList0000000000"+resultList);
      return resultList;
   };
}

이때 돌려주는 간략정보 목록인 List<Master>는 아래와 같음
[
    {readcount=17931, modifiedtime=20220915155736, contentid=2458348, contenttypeid=12},
    {readcount=2553, modifiedtime=20220915154906, contentid=2366217, contenttypeid=14},
    {readcount=24458, modifiedtime=20220915153947, contentid=1541165, contenttypeid=12},
    .
    .
]


4. 컨텐츠기초정보 목록을 통해 각각의 콘텐츠id에 대한 상세 정보들을 요청

<FetchRunner.java>
for (Master master : result) {
	try {
		Map<String, Object> item = new HashMap<>();
		if (master.isGreenTour()) {
			item.put("master", master);
		} else {
			final String contentId = master.getContentId();
			final int contentTypeId = master.getContentTypeId();
			/**
			 *  @URL /KorService/detailCommon  */
			Future<Map<String, Object>> futureCommon = threadPool.submit(
					TourApiClientCallableFactory.getKorServiceCommonCallable(contentId, contentTypeId));
			/**
			 *  @URL /KorService/detailIntro  */
			Future<Map<String, Object>> futureIntro = threadPool.submit(
					TourApiClientCallableFactory.getKorServiceIntroCallable(contentId, contentTypeId));
			/**
			 *  @URL /KorService/detailInfo  */
			Future<List<Map<String, Object>>> futureInfoList = threadPool.submit(
					TourApiClientCallableFactory.getKorServiceInfoCallable(contentId, contentTypeId));
			/**
			 *  @URL /KorService/detailImage  */
			Future<List<Map<String, Object>>> futureImageList = threadPool.submit(
					TourApiClientCallableFactory.getKorServiceImageCallable(contentId));
			/**
			 *  @URL /KorWithService/detailWithTour  */
			Future<Map<String, Object>> futureWithTour = threadPool.submit(
					TourApiClientCallableFactory.getKorWithServiceDetailWithTourCallable(contentId, contentTypeId));

			item.put("master", master);
			item.put("common", futureCommon.get());
			if (futureIntro.get() != null) {
				item.put("intro", futureIntro.get());
			}
			if (futureInfoList.get() != null && !futureInfoList.get().isEmpty()) {
				item.put("info", futureInfoList.get());
			}
			if (futureImageList.get() != null && !futureImageList.get().isEmpty()) {
				item.put("image", futureImageList.get());
			}
			if (futureWithTour.get() != null) {
				item.put("withtour", futureWithTour.get());
			}
		}
		aggregationList.add(item);
	} catch(Exception e) {
		// ignore and skip..
		logger.error("SKIPPED CID: " + master.getContentId(), e);
	}
}

↓↓↓

<TourApiClientCallableFactory.java>
public static Callable<Map<String, Object>> getKorServiceCommonCallable(String contentId, int contentTypeId) {
	return createTourAPICommonCallable(TourApiClient.builder().contentId(contentId).contentTypeId(contentTypeId));
}

↓↓↓

private static Callable<Map<String, Object>> createTourAPICommonCallable(TourApiClient.TourApiClientBuilder builder) {
	ObjectMapper mapper = new ObjectMapper();
	return () -> {
		TourApiClient client = builder.build();
		System.out.println("getDetailCommonURL --> " + client.getDetailCommonURL());
		JsonNode root = readTreeRetry(client.getDetailCommonURL()); // 요청
		JsonNode item = root.findPath("item");
		if (item.isObject()) {
			return mapper.readValue(item.toString(), new TypeReference<Map<String, Object>>() {});
		} else {
			if (item.size() == 0) {
				return null;
			}
			return mapper.readValue(item.get(0).toString(), new TypeReference<Map<String, Object>>() {});
		}
	};
}

↓↓↓

return 받은 데이터를 갖고 <FetchRunner.java> 로 돌아가서
Map<String, Object> item = new HashMap<>(); 에 엔티티별로 저장
item을 필드 변수인 aggregationList 에 담음

모아진 aggregationList를 <Main.java> 에서 fetchRunner 객체에 대한 getResultList() 메소드로 가져옴. 아래 참고
} else if (args.getSourceArgs()[0].equals("update")) {
	if (args.containsOption("dates")) {                        // fetch and update
		String dates = args.getOptionValues("dates").get(0);
		if (dates.contains(",")) {
			String[] startEnd = dates.split(",");
			fetchRunner.execute(startEnd[0], startEnd[1]);
		} else {
			fetchRunner.execute(dates, dates);
		}
		writeToFile(fetchRunner.getResultList(), args); // 파일로 저장
		dataManipulateRunner.execute(fetchRunner.getResultList()); // DB에 저장


getMasterURL를 이용해 요청한 결과 응답json 모음
https://www.notion.so/getMasterURL-JSON-fd9230b754b74cdc9a676488c729735a


5. DB에 저장

<Main.java>
dataManipulateRunner.execute(fetchRunner.getResultList());

execute 메소드로 KTOController.java의 process메소드에 List<Map<String, Object>> 전달해 실행
(이때 Collections.unmodifiableList메소드로 컬렉션의 추가/삭제를 금지시킴)

process 메소드는 받은 전체리스트의 크기만큼 순회하면서

"master" 키 안의 "contentid" 를
SELECT COT_ID FROM CONTENT_MASTER WHERE CONTENT_ID = #{contentId}
DB조회후 COT_ID를 반환시켜서
null이면 COT_ID를 생성해서 item을 insert,
있으면 해당 COT_ID의 데이터를 item으로 (새로운 정보로) update를 함

이때 update,insert 메소드에 파라미터로 들어가는 list의 item(Map<String,Object>)각각의 정보는 아래와 같음

![FireShot Capture 002 - Json Parser Online - json.parser.online.fr.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d7bd18f4-70a8-4d83-96d4-919834319750/FireShot_Capture_002_-_Json_Parser_Online_-_json.parser.online.fr.png)


6. insert / update 메소드에서 각각의 서비스를 이용해 각각의 테이블에 insert / update

메소드 안에서 각각의 서비스를 이용해서 insert / update 함
private void insert(String newCotId, Map<String, Object> item) {

contentMasterService.insert(content); → CONTENT_MASTER
imageService.insert(imageVo); → IMAGE
databaseMasterService.insert(dataBaseMasterVo); → DATABASE_MASTER
introService.insertTouristIntro(TouristIntroVO.*valueOf*(newCotId, introMap)); → TOURIST_SPOT_INTRO
infoService.insertCourseInfoList(list); → COURSE_INFO
departmentContentService.insert(DepartmentContentVO.*valueOf*(otdId, newCotId)); → OTHER_DEPARTMENT_CONTENT
contentTagsService.insert(ContentTagsVO.*valueOf*(newCotId, tagId)); → CONTENT_TAGS

update도 마찬가지

이때 이미지는 common에 있는이미지도 IMAGE테이블에 넣고,
image에 있는 이미지들도 IMAGE테이블이 들어감

---------------------------

투어api 특정 컨텐츠 조회 방법 (투어api에 있는 데이터가 DB로 반영안되는 컨텐츠가 있을때)
운영팀에서 특정 날짜에 올렸는데 그 날짜에 투어API로 반영이 안된 경우 발생 가능

1. contentId 로 찾기
<common>
https://apis.data.go.kr/B551011/KorService/detailCommon?ServiceKey=A%2BycgFhk2eYE6mEw%2B6%2FhcCbRDaCPGJf3aLCdYyfzuqRx6iY2b%2F04BmXgnQoTrGhm1FBQ%2BOVA5mbMogKlHFcDgw%3D%3D&MobileOS=ETC&MobileApp=BatchApp&contentId=콘텐츠아이디&defaultYN=Y&firstImageYN=Y&areacodeYN=Y&catcodeYN=Y&addrinfoYN=Y&mapinfoYN=Y&overviewYN=Y&_type=json

createdtime / modifiedtime 으로 tourAPI에 최초업로드 / 최종업데이트 된 날짜를 알 수 있음.

<추가image>
https://apis.data.go.kr/B551011/KorService/detailImage?MobileOS=ETC&ServiceKey=A%2BycgFhk2eYE6mEw%2B6%2FhcCbRDaCPGJf3aLCdYyfzuqRx6iY2b%2F04BmXgnQoTrGhm1FBQ%2BOVA5mbMogKlHFcDgw%3D%3D&MobileOS=ETC&MobileApp=BatchApp&contentId= 콘텐츠아이디&imageYN=Y&subImageYN=Y&_type=json

옵션으로 아래처럼 넣으됨. 쉼표(,) 다음에 띄어쓰기 하면 안됨
update --cid=2568667,585522


2. 업로드 / 업데이트 날짜로 찾기

옵션에 찾고싶은 컨텐츠를 업로드날짜(or 업데이트날짜) 넣고 배치프로그램 돌린 후 직접 검색후 contentId로 다시 검색해 요청보낸주소 찾기
update --dates=20230110

---------------------------

소스를 수정한 경우 로컬에서 실행하면 개발계 DB에 반영됨.
1. 로컬에서 정상적으로 동작하는지 테스트해보고
2. 마스터 브랜치에 푸쉬한 후
3. 운영계에 반영해달라고 하기

---------------------------

신규 콘텐츠가 DB에 들어오면 1~2시간 사이에 검색엔진에 업데이트 되서(?) 대구석에서 검색이 가능

이미지가 엑박뜰경우 요청하고있는 id를
IMAGE 테이블에서 IMG_ID에 검색한 후 URL값을 브라우저로 들어가보기

이미지가 잘 나온다면
30분~1시간 정도 지나면 엑박안뜨고 반영되는듯

---------------------------

이미지는 최초 한번 상세페이지에 접속을 해야 IMAGE테이블에 있는 이미지가 이미지서버에 저장된다고 함. 이후 저장된 이미지를 다시 불러옴.
만약 이미지가 잘 안나온다 하면 IMAGE테이블에 이미지가 잘 들어있는지 먼저 확인하고 들어있으면
https://csp30.ktcdn.com 에서 MANAGEMENT → PURGE → 이미지경로 입력 → Purge요청 으로 이미지서버 캐시삭제를 수동으로 해줘야함

상세페이지에 메인 이미지 뿌려주는곳

1. ms_detail.jsp

//명소상세 가져오기
function getContentList() {

   showLoding();
   //참고
   $.ajax({
      url :mainurl+ '/call',
      dataType : 'json',
      type : 'POST',
      data : {
         cmd : 'TOUR_CONTENT_BODY_DETAIL',
         cotId:cotId,
         locationx :locationx+ '',
         locationy :locationy+ '',
         stampId :stampId
},
      success : function(data) {

         goContentListView(data);
         goStampView(data);
      },
      complete : function() {
         getContentMapList('Tour');
         killerBanner();
         TrssMissionCheck();
         getSafetyWeek();
         hideLoding();
      },
      error : function(xhr, textStatus, errorThrown) {
      }
   });
}


2. newDetailCommon.js - goContentListView()

// 이미지 부분 시작
var pImg = data.body.publicImage;	// 공사 사진
pImgCnt = pImg.length;
var pImgListHtml = '';

var videohtml='';

if(data.body.video != undefined){

if(data.body.video.viewyn != undefined){
		var mainYoutubeTag = document.createElement('script');
		mainYoutubeTag.src = "https://www.youtube.com/player_api";
		var firstScriptTag = document.getElementsByTagName('script')[0];
		firstScriptTag.parentNode.insertBefore(mainYoutubeTag, firstScriptTag);

		videoId = data.body.video.url;

		videohtml += '<div class="db_detail_youtube" id="youtubeGo">';
		videohtml += '<div class="video_wrap">';
		videohtml += '<img src="../resources/images/temp/temp_video.jpg" alt="video dummy">';
		videohtml += '<div class="video_area">';
		videohtml += '<div id="youtube" style="height: 100%;"></div>';
		videohtml += '</div>';
		if(data.body.video.type == '1'){
			videohtml += '<div class="iosLayer">';
			videohtml += '<div>';
			if(getDevice()=='iOS'){
				videohtml += '<p>해당 동영상은 VR 동영상으로<br/>';
				videohtml += '아이폰 Youtube APP을 통해서만<br/>';
				videohtml += '원활한 재생이 가능합니다.</p>'
				videohtml += '<a href="javascript:ios_go_url(\''+videoId+'\');">Youtube APP 으로 시청</a>';
			} else{
				videohtml += '<p>본 동영상은 VR기능을 지원합니다<br/>';
				videohtml += '화면을 상/하/좌/우로 이동하여 감상해 보세요.<br/>';
				if(mobileYn == 'N')
					videohtml += '(단, IE브라우저는 지원하지 않습니다.)</p>';

			}

			videohtml += '</div>';
			videohtml += '<button type="button" onclick="closeIosLayer();">닫기</button>';
			videohtml += '</div>';

		}
	videohtml += '</div></div>';
	$('.detail_tab').after(videohtml);
	$('#photoTab span').text('동영상/사진');
	}
}

$.each(pImg, function(index, items){
	//pImgListHtml += '<div class="swiper-slide" style="background-image: url('+mainimgurl+items.imgPath+');"><a href="javascript:openPhotoView('+index+');">'+items.imgAlt+'</a></div>';
	pImgListHtml += '<div class="swiper-slide" >';
	pImgListHtml += '	<img class="swiper-lazy" data-src="'+mainimgurl+items.imgPath+'" alt="'+items.imgAlt+'" onclick="openPhotoView('+index+')" style="width:100%; height:100%;object-fit: contain;"><div class="swiper-lazy-preloader"></div>';
	pImgListHtml += '</div>';
});

----------------------------------------------------------------------------------------------------

변경사항 조회용 쿼리

SELECT
    '' as '-----CONTENT_MASTER-----',
    CM.*,
    '' as '-----DATABASE_MASTER-----',
    DM.*,
    '' as '-----DETAIL_INFO-----',
    DI.*,
    '' as '-----TOURIST_SPOT_INTRO-----',
    TSI.*,
    '' as '-----COURSE_INFO-----',
    CI.*,
    '' as '-----OTHER_DEPARTMENT_CONTENT-----',
    ODC.*,
    '' as '-----CONTENT_TAGS-----',
    CT.*
FROM
CONTENT_MASTER CM
LEFT JOIN DATABASE_MASTER DM
    USING(COT_ID)
LEFT JOIN DETAIL_INFO DI
    USING(COT_ID)
LEFT JOIN TOURIST_SPOT_INTRO TSI
    USING(COT_ID)
LEFT JOIN COURSE_INFO CI
    USING(COT_ID)
LEFT JOIN OTHER_DEPARTMENT_CONTENT ODC
    USING(COT_ID)
LEFT JOIN CONTENT_TAGS CT
    USING(COT_ID)
WHERE COT_ID in (
    SELECT COT_ID FROM CONTENT_MASTER WHERE CONTENT_ID IN('2871057','2871026','2871003','2870986')
)

바뀌었는지 안바뀌었는지 수동으로 비교툴로 확인할 수도 있지만
CONTENT_MASTER의 MODIFIED_DATE가 옛날 날짜면 수정이 안된거라고 보는 방법도 있음

----------------------------------------------------------------------------------------------------

프로그램 인수로 날짜 대신 콘텐츠 아이디로 검색 가능

날짜 검색 : --dates=[data]
콘텐츠id 검색 : --cid=[cid1],[cid2],..,[cidn]

콘텐츠id검색시 쉼표옆에 띄어쓰기가 있으면 안됨

----------------------------------------------------------------------------------------------------
























