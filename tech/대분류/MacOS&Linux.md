macOS : UNIX 기반의 운영체제

Linux : UNIX와 유사한 운영체제

macOS는 특정 하드웨어와 소프트웨어로 구성된 Apple의 제품군에 최적화되어 있음
반면 Linux는 다양한 배포판(Distribution)으로 제공되며 다양한 하드웨어 및 환경에서 사용할 수 있음

----------------------------------------------------------------------------------------------------

기능						단축키 (opt-option, cmd-command)

한영키					- capslock
CapsLock				- capslock길게
Ctrl						- cmd
Alt						- opt
한자(특수문자X)				- opt + enter
이모지/특수문자				- ctrl + cmd + space (fn키로 바꾸기)
독 숨기기 / 보이기			- opt + cmd + d
Delete					- fn + backspace
Home/End				- cmd + 좌우
단위 이동					- opt + 좌우
단위 선택					- opt + shift  +좌우
PgUp/Down				- fn + 위아래 (커서가 따라오지 않음)
삭제						- cmd + backspase
완전삭제					- opt + cmd + backspace
이름변경					- enter
새로고침					- ctrl + r
최소화					- cmd + m
창닫기/최소화				- cmd + w
창닫기					- cmd + q
프로그램간 전환				- cmd + tab
프로그램간 전환+			- cmd + tab + opt
프로그램내 창 보기			- ctrl + ↓
프로그램내 창 전환			- cmd + `
프로그램내 〃(역방향)			- cmd + shift + `
새탭에서열기				- cmd + enter
검색(Soptlight)				- cmd + space
우클릭					- ctrl + 터치패드클릭
						- 두손가락 클릭
작업 모두 보기				- 세손가락 위로 (터치패드)
런치패드					- 네손가락 모으기
바탕화면					- 네손가락 벌리기(f11)
즉시삭제					- opt + cmd + backspace

화면캡처(전체)				- cmd + shift + 3
화면캡처(영역지정)			- cmd + shift + 4
화면캡처(창선택)			- cmd + shift + 5 (최초 '선택한 윈도우 캡처' 클릭) 같은 프로그램 내 창 선택시 cmd누르고 선택

윈도우탐색기(파인더)			- option + cmd + space (계층아이콘 선택시 윈도우탐색기처럼 ui설정가능) 
루트(내컴퓨터)				- (파인더띄워놓고) cmd + shift + c
사용자/mac/				- (파인더띄워놓고) cmd + shift + h
데스크탑					- (파인더띄워놓고) cmd + shift + d
유틸리티					- (파인더띄워놓고) cmd + shift + u
응용프로그램(앱)			- (파인더띄워놓고) cmd + shift + a
보기 방식 변경				- cmd + 1~4
파일 열기					- cmd + ↓

숨김파일 숨김/해제			- cmd + shift + .
화면전체캡처				- cmd + shift + 3
화면영역캡처				- cmd + shift + 4
설정(preferences)			- cmd + ,
빠른 메모					- fn + q
강제종료도구				- opt + cmd + esc
전체화면					- ctrl + cmd + f
화면 잠금					- ctrl + cmd + q

-----

터미널

프로세스 종료				- ctrl + c
end of file					- ctrl + d
프로세스 일시정지			- ctrl + z
일시정지 프로세스 보기		- jobs
정지 해제					- fg % [job의 대괄호안에 있는 숫자 입력1]

Home					- ctrl + a
End						- ctrl + e
찾기						- cmd + f
다음 찾기					- cmd + g
이전 찾기					- cmd + shift + g
새탭						- cmd + t
창분할 열기				- cmd + d
창분할 닫기				- cmd + shift + d
창분할 세로로 열기(iterm2)		- cmd + shift + d
분할창 이동(iterm2)			- opt + cmd + 방향키
모든 분할창 동시입력(iterm2)	- opt + cmd + i
이전에 입력했던
내용을 검색				- ctrl + r
검색 취소					- esc esc
커서 이전 단어 자르기			- ctrl + w
커서 다음 모두 자르기			- ctrl + k
붙여넣기					- ctrl + y
단어 건너뛰기				- opt + 좌우

입력 취소					- ctrl + u
입력 취소후 엔터				- ctrl + c 아니면 ctrl + g 아니면 cmd + .
화면 clean					- cmd + k
화면 clean					- ctrl + l
(스크롤만 내림)

한줄 지우기				- cmd + l

새탭						- cmd + t

책갈피 추가				- cmd + shift + m
opt + cmd + ↑ , ↓ 로 책갈피 이동가능하며 (cmd+k) 하면 날라감

-----

크롬

새탭						- cmd + t
새창						- cmd + n
주소창					- cmd + l
이전탭/다음탭				- opt + cmd + 좌우
						- ctrl + tab / ctrl + shift + tab
탭닫기					- cmd + w
창닫기					- cmd + shift + w
닫은탭/창 다시열기			- cmd + shift + t
새로고침					- cmd + r
강력새로고침				- cmd + shift + r
찾기						- cmd + f
						- cmd + g
다운로드목록				- opt + cmd + j
						- opt + cmd + l
방문기록					- cmd + y
인터넷사용기록 삭	제		- cmd + shift + backspace
요소검사					- cmd + shift + c
소스보기					- opt + cmd + u
구글 검색창				- /

검색						- opt + cmd + f
s
콘솔창 클리어				- cmd + k
콘솔 입력지우기				- ctrl + u

-----

키노트(Keynote,프레젠테이션,파워포인트)

위 메뉴 숨김/보이기			- opt + cmd + t
오른쪽 메뉴 숨김/보이기		- opt + cmd + i
확대						- cmd + shift + .
축소						- cmd + shift + ,
원래대로					- cmd + 0

----------------------------------------------------------------------------------------------------

iterm 에서 방향키로 단어 이동 되게

1. Preferences → Profiles → Keys → Key Mappings → ⌃← 와 ⌃→ 를 빼기(-)버튼 눌러서 제거
2. Preferences → Keys → 추가(+)버튼 클릭
Keyboard Shortcut : ⌃←
Action : Send Escape Sequence
Esc+ : b

Keyboard Shortcut : ⌃→
Action : Send Escape Sequence
Esc+ : f

----------------------------------------------------------------------------------------------------

맥 추천 프로그램

# HotKey
- 앱 실행 단축키화
Show Clipboard : shift + cmd + space
일 폴더 : opt + `
Terminal.app : cmd + m

# iTerm
- 기본 터미널에 비해 많은 기능을 내장한 터미널 플러그인

# alfred
기존 Spotlight 업그레이드 버전 (단축키: option+space인데 Spotlight랑 바꾸기)
- 웹검색 편리
- Advanced → Force Keyboard: ABC 로 설정하면 영어로 시작되게 가능함 (=엑세스의 IME모드)
- 단점은 로컬 파일검색이 Spotlight에 비해서 떨어짐

# scroll-reverser
- 마우스, 트랙패드 방향 각각 따로설정

# karabiner-elements
- 내장, 외장 키보드 커스터마이징

------------------------------

#brew

- 개발에 관련된 다양한 도구 및 언어, 환경 설치 가능 (리눅스 Debian의 apt-get, 우분투의 apt)
https://brew.sh/index_ko
apt install ~ 명령어 쳐서 쓰던걸 brew install ~ 로 바꾸면 됨

brew ls -l : 설치한 프로그램 목록 조회 (brew ls 또는 brew list도 됨)
brew info 프로그램명 : 설치된 프로그램 경로 조회
brew remove 프로그램명 : 설치된 프로그램 삭제

Formulae / Casks 차이

Formulae
소프트웨어 패키지를 설치하는데 사용됨. 주로 CLI 도구, 라이브러리, 개발 도구 등과 같은 명령줄 프로그램을 포함함
Homebrew의 기본 패키지 유형이며 brew install명령을 사용하여 설치할 수 있음

Casks
MacOS 애플리케이션을 설치하는 데 사용됨
주로 GUI 기반의 애플리케이션(ex. 크롬, atom 등), 응용 프로그램, 게임 등과 같은 사용자 인터페이스를 가진 애플리케이션 설치에 사용됨
Casks는 Homebrew Cask 프로젝트를 통해 제공되며, brew cask install 명령을 사용하여 설치할 수 있음

-----

<cask 설치>
brew install cask

<사용법>
brew cask install atom

brew로 설치한 목록 brewfile로 내보내기
brew bundle dump

------------------------------

utm

윈도우 가상머신 사용가능

------------------------------

★ 키보드 마에스트로
매크로 프로그램 (윈도우는 오토핫키?)

★ gSwitch
brew로 설치해야함. 터미널에서 다음 명령어 입력
brew install --cask gswitch
프로그램 아이콘 클릭 → Integrated Only 클릭 → overwrite once
사과 → 이 Mac에 관하여 누르면 외장그래픽이 사라져있음. 프로그램 끄면 원복됨.
Dynamic switching : 기본값
Integrated Only : 내장 그래픽 칩셋만 사용
Discrete Only : 외장 그래픽 칩셋만 사용

★ giphy capture
gif 혹은 동영상 으로 캡처 프로그램

★ kaleidoscope
파일내 서로다른부분 찾는 프로그램(윈도우의 WinMerge. 윈머지)
텍스트를 드래그 해서 가져와 비교할 수 있음 (2000자까지만 가능)
↓↓↓
https://www.diffnow.com/compare-clips
웹 파일비교 사이트 (FULLSCREEN)

★ DiffMerge (윈머지 비슷한거) (파일을 업로드해야함. 2000자이상 가능)
★ 인텔리제이 Compare Files 도 좋음

----------------------------------------------------------------------------------------------------

기타팁

맥은 윈도우와 달리 창마다 설정이 있는게 아니라, 화면 제일 위쪽좌측에 설정하는 메뉴가 있음
Finder(탐색기) 확장자 표시 : Finder환경설정 → 고급 → 모든 파일 확장자 보기

텍스트편집기에서 20줄이상을 한번에 붙여넣으면 글자가 이상하게 밀리면서 겹쳐짐
이때는 마우스로 전 줄을 클릭한 후 마지막 클릭해 커서를 이동시킨후 delete랑 enter를 한번씩 눌러야함

터미널 vi에디터는 비정상 종료시 .swp파일(백업파일)이 만들어지는데 지워도됨

-----

OS별 파일/폴더명으로 입력 불가능한 문자

Windows(9개) [ \, /, ?, :, *, ", <, >, | ]
Linux Mint(1개) [ / ]
Mac OS X(1개) [ : ]

-----

파일 지울때 권한없어서 Permission denied 뜨면 sudo -s 루트권한

vi편집기 덮어쓸때 권한없어서 Can't open file for writing 뜨면
:w !sudo tee % > /dev/null
하거나 sudo -s 루트권한으로

-----

텍스트 편집기 → 환경설정

- 포맷
일반 텍스트

- 윈도우 크기
너비 : 150
높이 : 60

- 서체
일반 텍스트 서체 : PC명조 12

- 옵션
입력할 때 맞춤법 검사 : 해제
눈금자 보기 : 해제

-----

맥 환경설정

환경설정 → 키보드 → 키보드
키 반복 : 젤 빠르게
반복 지연 시간 : 젤 짧게
Touch Bar에 표시되는 항목 : F1,F2 등의 키
🌎눌러 다음을 실행 : 이모티콘 기호 보기 (fn만 눌러도 특수문자/이모지 뜨게하기) → 굳이 할필요 없는듯

환경설정 → 키보드 → 단축키
키보드 탐색을 사용하여 컨트롤 간에 초점 이동 → 체크
모든 컨트롤에서 마우스 클릭 없이 tab으로 선택할 수 있음
★엔터를 누르면 현재 포커스와 상관없이 파란색으로 표시된 버튼이 눌리게 됨

환경설정 → 키보드 → 단축키 → Mission Control
컨트롤 + ? 로 걸려있는 단축키들 체크해제

환경설정 → 키보드 → 단축키 → 앱 단축키
추가 버튼 → Google Chrome.app 찾아서
메뉴 제목 : 페이지 새로고침
키보드 단축키 : f5
메뉴 제목 : 캐시를 무시하고 페이지 새로고침
키보드 단축키 : ctrl + shift + f5

환경설정 → 키보드 → 텍스트
맞춤법 자동 수정 : 해제
스페이스를 두 번 눌러 마침표 추가 : 해제

Finder 환경설정 → 고급
휴지통에서 30일이 지난 항목 제거

외장키보드쓰고있을때 환경설정 → 키보드
Touch Bar에 표시되는 항목 : 펼쳐진 Control Strip
'외장키보드에서 F1, F2등의 키를 표준 기능으로 사용' 체크

-----

알트탭시 애니메이션 줄이기 (시에라 이상)

환경설정 → 손쉬운 사용 → 디스플레이 → 동작 줄이기

-----

한영변환 capslock키도 쓰고 한영키도 쓰기

1. 카라비너에서 right_option → f13 변경 (right_option이 아닐 수 있음. right~가 들어간 모든키를 f13,f14,f15.. 로 바꾼 후 키보드환경설정에서 한영키를 눌러보기)
2. 환경설정 → 키보드 → 단축키 → 입력 소스 → '입력 메뉴에서 다음 소스 선택' 클릭 → enter → f13

"보안 및 개인정보보호"에서 입력 모니터링에 카라비너가 체크 되어있는지 확인. 안되어있으면 자물쇠 클릭후 체크

-----

로그인시 기타(other)계정 없애기

1. spotlight에서 디렉토리 유틸리티(direct Utility.app)검색
2. 자물쇠 풀기
3. 화면 왼쪽위 편집메뉴 → Root 사용자 비활성화

-----

터미널 환경설정

터미널 → 환경설정 → 프로파일

- 텍스트
Homebrew 스타일로
서체 Hack Regular 12

- 윈도우
윈도우 크기 120 * 40

-----

자바 기본설치경로
Library(라이브러리)/Java/JavaVirtualMachines

이클립스 객체찾아가기 ctrl+클릭 (or f3)했을때 Attach Source 뜨면 눌러서 아래 경로의 파일 설정
Library(라이브러리)/Java/JavaVirtualMachines/jdk1.8.0_321.jdk/Contents/Home/src.zip

-----

finder에서 터미널 열기

키보드 → 단축키 → 서비스
폴더에서 새로운 터미널 열기 ctrl + m

그럼 파인더에서 '폴더를 선택 후' 단축키로 터미널을 열 수 있음

-----

기본프로그램 설정

파일 우클릭 → 정보 가져오기 → 다음으로 열기 → 연결시킬 프로그램 선택 → "모두 변경" 클릭

-----

한영 바꿀때 0,1초 딜레이 생기는데 없애기

Karabiner-Elements 에서
caps_lock을 f13선택해서 바꾸고
cmd + space → 환경설정 → 키보드 → 단축키 → 입력 소스 → '입력 메뉴에서 다음 소스 선택'을 f13으로 바꾸기
(이전입력소스선택은 다른키여야함 + 체크해제하기. 이전입력소스로 한영을 바꾸면 딜레이가 생김)

+++++

캡스락은 한영키에서 본래 캡스락의 기능대로 대소문자전환으로 바꾸고,
우측 커멘드를 한영키로 바꾸고, 윈도우키보드에서는 원래 한영키를 한영키로 설정하는방법

- 키보드
단축키 → 입력 소스 → 입력 메뉴에서 다음 소스 선택 → Enter → F13
입력소스 → Caps Lock 키로 ABC 입력 소스 전환 → 체크해제

- Karabiner-Elements
Apple Internal Keyboard / Trackpad (Apple Inc.) : right_command → f13 (한영키자리의 cmd를 한영키로 이용)
자기 키보드 : left_option → left_command (alt키를 cmd기능으로 이용(원래는 win키가 cmd였음))
자기 키보드 : left_command → left_option (win키를 alt기능으로 이용(원래는 alt키가 alt였음))
자기 키보드 : right_option → f13 (한영키를 한영기능으로 이용)

-----

스페이스 누를때 .(점) 자동 찍힘

환경설정 → 키보드 → 텍스트 → '스페이스를 두 번 눌러 마침표 추가' 체크해제

-----

파일을 새창 말고 새탭으로 열기

데스크탑 및 Dock → 윈도우 및 앱 → 문서를 열 때 탭 사용 → 항상

-----

파일 잘라내기

cmd + c 로 복사한 후 opt + cmd + v로 붙여넣으면 이동됨

-----

스페이스바 눌러서 파일/폴더 미리보기 가능. 다시 스페이스바 누르면 닫힘

아이콘 배열에 맞춰서 방향키를 누르면 옮겨다니면서 다른 파일들을 확인할 수 있음

-----

이미지 자르기

더블클릭해서 미리보기를 열고, 자를 영역 만든 후 cmd + k 누르고, 내보내기를 누르면 원본은 유지할 수 있음

-----

이미지 용량 줄이기

더블클릭해서 미리보기를 열고, 내보내기를 누르고 품질 조절

-----

빠른메모에서 복사/잘라내기 안될때 복사하는법

오른쪽 위에 공유 아이콘 클릭 → 메시지 아이콘 클릭 → 복사

-----

자동 업데이트 알림 끄기

소프트웨어 업데이트 → 자동으로 Mac 최신으로 유지하기 → 체크해제
고급 → 업데이트 확인 → 체크해제

-----

이모지 열때 키보드로 선택 안될떄가 있는데 cmd + tab 두번 누르면 선택 됨.

실수로 ↑키를 눌러서 맨 아래페이지로 내려갔으면 아무 문자나 한글자 입력 했다가 지우고 ↓키 누르면 됨

-----

keypress시 이상한문자 안뜨고 반복입력 되게하기

터미널에서 다음 명령어 입력
defaults write -g ApplePressAndHoldEnabled -bool false

-----

Karabiner 이용해서 한영키 딜레이 없애기

1. 카라비너에서 caps_lock → f13으로 바꾼다
2. cmd+space → 킵enter → 단축키 → 입력 소스 → '입력 메뉴에서 다음 소스 선택' 클릭 → enter → f13

----------------------------------------------------------------------------------------------------

'XXX'은(는) App Store에서 다운로드한 항목이 아니기 때문에 열 수 없습니다

보안 및 개인 정보 보호 → "확인 없이 열기" 클릭

----------------------------------------------------------------------------------------------------

멕에서 윈도우 키보드 쓰기

- 카라비너로 ctrl/alt 키 서로 변경 (외장 키보드에서만 변경하는게 좋음)

1. left_command → left_option 바꾸기
2. left_option → left_command 바꾸기

+++

맥처럼 안하고 윈도우 그대로 ctrl키를 cmd기능으로 쓰려면
(이렇게 하면 단점이 alt+tab기능을 ctrl+tab키로 써야함. 또 윈도우랑 맥의 단축키가 많이 다르기때문에 그냥 윈도우랑 맥이랑 별개로 보는게 더 편한듯)
1. left_control → left_command
2. left_command → left_control

-----

- home/end키 작동 되게 터미널에서 맵핑

cd ~/Library
mkdir KeyBindings
cd KeyBindings
vi DefaultKeyBinding.dict

{
/* Remap Home / End keys to be correct */
"\UF729" = "moveToBeginningOfLine:"; /* Home */
"\UF72B" = "moveToEndOfLine:"; /* End */
"$\UF729" = "moveToBeginningOfLineAndModifySelection:"; /* Shift + Home */
"$\UF72B" = "moveToEndOfLineAndModifySelection:"; /* Shift + End */
"^\UF729" = "moveToBeginningOfDocument:"; /* Ctrl + Home */
"^\UF72B" = "moveToEndOfDocument:"; /* Ctrl + End */
"$^\UF729" = "moveToBeginningOfDocumentAndModifySelection:"; /* Shift + Ctrl + Home */
"$^\UF72B" = "moveToEndOfDocumentAndModifySelection:"; /* Shift + Ctrl + End */
}

:wq! 후 재부팅

-----

이클립스 내에서 자동완성 ctrl+space로 바꾸기

1. Spotlight 키보드 검색 → 단축키 → 입력 소스 → 이전 입력 소스 선택 체크해제
2. 이클립스 Preferences → General → Keys

'Content Assist' → ctrl + space
'Content Assist' → cmd + space (내장키보드용)
'Content Assist' → shift + space (내장키보드용)

-----

propertice : cmd + enter 로 변경
maven update : cmd + f5 로 변경
privious tab / next tab : ctrl + tab / ctrl + shift + tab 로 변경
show in... : cmd + shift + w 로 추가

-----

이클립스 단축키

- home/end 키 제대로 작동되게 설정하기 및 윈도우처럼 변경 (feat.윈도우 키보드)
- when값 올바른지 잘 보기(복제후 바로 바인딩 하고 포커스바꾸면 when값이 바뀜)

Preferences → General → Keys 에서..


이클립스

'현재파일의 위치로 이동' : opt + cmd + w → p → enter
'전체검색(플러그인)' : cmd + shift + l
'파일검색' : cmd + shift + r (파일명의 중간문자를 검색하고싶을때는 *검색어)
'properties' : opt + enter
'이전형제/다음형제태그(xml/html등)' : cmd + shift + 위아래
'다중커서' : opt + cmd + shift 누른상태에서 하나씩 클릭
'열편집모드' : opt + cmd + a 이후 드래그
'간편한찾기' : cmd + j 치고 찾을 문자열 입력 후 다시 쳐서 찾기
'간편한찾기(거꾸로)' : cmd + shift + j
'메소드주석으로설명' : opt + cmd + j
'메소드 쓰는곳 찾기' : ctrl + opt + h
'라이브러리 안에있는 클래스/메소드 찾기' : ctrl + shift + t (그대로)
'Run JUnit Test' : ctrl + cmd + j
'창 포커스 전환' : cmd + f7
'update project' : ctrl + f5
'next word' → 복제 → ctrl + → (맥환경설정 → 키보드 → 단축키 Mission Control 체크해제 먼저 해야함)
'previous word' → 복제 → ctrl + ← (맥환경설정 → 키보드 → 단축키 Mission Control 체크해제 먼저 해야함)
'select next word' → 복제 → ctrl + shift + →
'select previous word' → 복제 → ctrl + shift + ←
'line start' → 복제 → home키
'line end' → 복제 → end키
'select line start' → 복제 → shift + home키
'select line end' → 복제 → shift + end키
'duplicate lines' → 복제 → ctrl + cmd + ↑
'copy lines' → 복제 → ctrl + cmd + ↓
'copy lines' → 복제 → ctrl + shift + d
'delete line' → 복제 → shift + delete
'backward history' → 복제 → ctrl + 1 혹은 ctrl + cmd + ←
'forward history' → 복제 → ctrl + 2 혹은 ctrl + cmd + →
'run java application' → ctrl + shift + j
'organize imports' → 복제 → ctrl + shift + o
'copy - in dialogs and windows' → 복제 → ctrl + c
'copy - terminal control in focus' → 복제 → ctrl + c
'copy - in dialogs and windows' → 복제 → ctrl + v
'copy - terminal control in focus' → 복제 → ctrl + v
'cut - in dialogs and windows' → 복제 → ctrl + x
'select all' → 복제 → ctrl + a
'save' → 복제 → ctrl + s
'undo' → 복제 → ctrl + z
'redo' → 복제 → ctrl + shift + z
'quick fix' → 복제 → ctrl + 1
'close' → 복제 → ctrl + w
'quick search' → ctrl + shift + l
'quick search' → 복제 → cmd + shift + l
'open resource(파일검색)' → ctrl + shift + f
'open resource' → 복제 → cmd+ shift + f
'add block comment - editing in structured text editors' → 복제 → ctrl + /
'Remove Block Comment' → 복제 → ctrl + \
'toggle comment → 복제 → ctrl + /
'cut line' → ctrl + shift + x
'preferences' → ctrl + ,
'find and replace' → ctrl + f
'move lines down' → ctrl + shift + ↓
'move lines up' → ctrl + shift + ↑
★ jsp/xml파일에서 행 이동시킬때는 기본단축키(opt + 위아래) 써야함
'find next' → ctrl + f3 (키보드 → 단축키 → 키보드 → Dock로 초점 이동 체크해제)
'find previous' → shift + f3
'open type - in windows' → ctrl + shift + t
'open type - editing javascript source' → ctrl + shift + t
'rename - refactoring - in windows'(변수일괄수정) → ctrl + shift + r
'save all' → ctrl + cmd + shift + s
'show source quick menu - in windows' → cmd + shift + s
'close all' → ctrl + cmd + shift + w
'show in...' → cmd + shift + w
'convert camel ↔ underscores'(카멜↔스네이크 플러그인: AnyEdit) → ctrl + shift + k
'convert to upper case'(대문자로) → ctrl + u
'convert to lower case'(소문자로) → ctrl + l
'Show Key Assist' → ctrl + cmd + shift + l
'quick search' → ctrl+ shift + l
'replace all'(검색/바꾸기-전체변경) → ctrl + shift + enter
'wrad wrap' → cmd + shift + y
open call hierarchy - 'in windows'(메소드/변수 쓰는곳 찾기) → ctrl + shift + h
open call hierarchy - 'javascript view'(메소드/변수 쓰는곳 찾기) → ctrl + shift + h


단축키에 뭐걸려있는지 확인하려면 아무거나 클릭하고 binding에서 단축키 확인후 취소하면 됨(단, when이 같은것만 나옴)
단축키설정하다 이상해지면 Restore Command(복원) 누르면 됨. 그럼 해당 명령에 설정된 모든 단축키가 기본값으로 돌아감(초기화)

-----

sql디벨로퍼에서 home/end 키 제대로 작동되게 설정하기 및 윈도우처럼 변경 (윈도우 키보드)

Preferences → 단축키

'행 시작' → 복제 → Home
'행 끝' → 복제 → End
'선택사항을 행 시작부분으로 이동' → 복제 → shift + Home
'선택사항을 행 끝부분으로 이동' → 복제 → shift + End
'SQL 스크립트 실행' → ctrl + shift + enter

-----

디비버에서 home/end 키 제대로 작동되게 설정하기 (안되면 디비버 껏다키기) 및 윈도우처럼 변경

환경설정(Preferences) → User Interface → 키

'이전 단어' → ctrl + ←
'이전 단어 선택' → ctrl + shift + ←
'다음 단어' → ctrl + →
'다음 단어 선택' → ctrl + shift + →
'닫기' → 복제 → ctrl + w
'찾기 및 바꾸기' → 복제 → ctrl + f
'복사' → 복제 → ctrl + c
'잘라내기' → 복제 → ctrl + x
'붙여넣기' → 복제 → ctrl + v
'모두 선택' → 복제 → ctrl + a
'행 복사' → 복제 → ctrl + cmd + d
'행 시작' → 복제 → home
'행 시작 선택' → 복제 → shift + home
'행 끝' → 복제 → end
'행 끝 선택' → 복제 → shift + end
'텍스트 시작' → 명령 바인드 해제
'텍스트 끝' → 명령 바인드 해제

'행 잘라내기' → cmd + d & ctrl + d
'실행 취소' → ctrl + z
'저장' → ctrl + s
'환경 설정' → ctrl + ,
'행 복사' → ctrl + shift + d
'다음 찾기' → ctrl + f3
'이전 찾기' → shift + f3
'로우 추가' → ctrl + insert

다 설정했으면 디비버 껏다키기

-----

서브라임 단축키 윈도우처럼 변경 (윈도우 키보드)
[
	{ "keys": ["alt+left"], "command": "move", "args": {"by": "subwords", "forward": false} },
	{ "keys": ["alt+right"], "command": "move", "args": {"by": "subword_ends", "forward": true} },
	{ "keys": ["alt+shift+left"], "command": "move", "args": {"by": "subwords", "forward": false, "extend": true} },
	{ "keys": ["alt+shift+right"], "command": "move", "args": {"by": "subword_ends", "forward": true, "extend": true} },

	{ "keys": ["ctrl+left"], "command": "move", "args": {"by": "words", "forward": false} },
	{ "keys": ["ctrl+right"], "command": "move", "args": {"by": "word_ends", "forward": true} },
	{ "keys": ["ctrl+shift+left"], "command": "move", "args": {"by": "words", "forward": false, "extend": true} },
	{ "keys": ["ctrl+shift+right"], "command": "move", "args": {"by": "word_ends", "forward": true, "extend": true} },

	{ "keys": ["ctrl+shift+p"], "command": "show_overlay", "args": {"overlay": "command_palette"} },
	{ "keys": ["f3"], "command": "find_under" },
	{ "keys": ["shift+f3"], "command": "find_under_prev" },
	{ "keys": ["super+f3"], "command": "find_all_under" },
	{ "keys": ["ctrl+d"], "command": "find_under_expand" },
	{ "keys": ["super+shift+d"], "command": "soft_undo" },
	{ "keys": ["ctrl+k", "ctrl+d"], "command": "find_under_expand_skip" },
	{ "keys": ["ctrl+a"], "command": "select_all" },
	{ "keys": ["ctrl+f"], "command": "show_panel", "args": {"panel": "find", "reverse": false} },
	{ "keys": ["ctrl+a"], "command": "select_all" },
	{ "keys": ["ctrl+s"], "command": "save", "args": { "async": true } },
	{ "keys": ["ctrl+z"], "command": "undo" },
	{ "keys": ["ctrl+shift+z"], "command": "redo" },
	{ "keys": ["ctrl+x"], "command": "cut" },
	{ "keys": ["ctrl+c"], "command": "copy" },
	{ "keys": ["ctrl+v"], "command": "paste" },
	{ "keys": ["ctrl+w"], "command": "close" },
	{ "keys": ["ctrl+o"], "command": "prompt_open" },
	{ "keys": ["ctrl+super+up"], "command": "select_lines", "args": {"forward": false} },
	{ "keys": ["ctrl+super+down"], "command": "select_lines", "args": {"forward": true} },
	{ "keys": ["ctrl+shift+down"], "command": "swap_line_down" },
	{ "keys": ["ctrl+shift+up"], "command": "swap_line_up" },
	{ "keys": ["ctrl+shift+d"], "command": "duplicate_line" },
	{ "keys": ["ctrl+shift+a"], "command": "expand_selection", "args": {"to": "smart"} },
	{ "keys": ["ctrl+u"], "command": "upper_case" },
	{ "keys": ["ctrl+l"], "command": "lower_case" },
	{ "keys": ["ctrl+t"], "command": "new_file" },
	{ "keys": ["ctrl+n"], "command": "new_file" },
	{ "keys": ["super+t"], "command": "new_file" },
	{ "keys": ["ctrl+shift+t"], "command": "reopen_last_file" },
	{ "keys": ["ctrl+enter"], "command": "run_macro_file", "args": {"file": "res://Packages/Default/Add Line.sublime-macro"}, "context":
		[
			{ "key": "overlay_has_focus", "operator": "equal", "operand": false },
		],
	},
	{ "keys": ["ctrl+shift+enter"], "command": "run_macro_file", "args": {"file": "res://Packages/Default/Add Line Before.sublime-macro"} },
	{ "keys": ["ctrl+shift+l"], "command": "split_selection_into_lines" },
	{ "keys": ["shift+delete"], "command": "run_macro_file", "args": {"file": "res://Packages/Default/Delete Line.sublime-macro"} },
	{ "keys": ["super+d"], "command": "run_macro_file", "args": {"file": "res://Packages/Default/Delete Line.sublime-macro"} },
	{ "keys": ["ctrl+forward_slash"], "command": "toggle_comment", "args": { "block": false } },
	{ "keys": ["ctrl+shift+forward_slash"], "command": "toggle_comment", "args": { "block": true } },
	// { "keys": ["ctrl+shift+k"], "command": "Camel case" } // ctrl+alt+c 두번
]

기타 기본 단축키

창분할				- opt + cmd + 1~5
다음 줄 삽입			- cmd + enter
이전 줄 삽입			- cmd + shift + enter
드래그된 영역 다중커서	- cmd + shift + l
스페이스를 탭으로		- cmd + shift + p → itt → enter
코드 접기				- opt + cmd + [
코드 펼치기			- opt + cmd + ]
행 상하 이동			- cmd+ctrl+↕
찾아바꾸기				- cmd+opt+f
여러파일에서 찾기/바꾸기	- cmd+shift+f

-----

인텔리제이 단축키 (윈도우처럼 변경. 추가할때 더하기아이콘 눌러서 추가하고 안쓰는거 겹치면 remove하기)

단축키 뭔지 보려면 아무거나 단축키 추가 누르고 찾고싶은단축키 누르면 해당 단축키를 쓰고있는 단축키목록이 나옴. 확인하고 취소하기

단축키 추가/설명추가/삭제/리셋		: enter (기본값)
Preferences창 저장 후 닫기			: ctrl + enter (기본값)
전체 검색(메소드, 컬럼 등)			: shift, shift (기본값)
Open...							: ctrl + o & cmd + o
new...							: ctrl + n & ctrl + enter (기본값)
Create new directory or package		: ctrl + shift + n
Rename...(클래스/변수/
메소드/파라미터 이름 일괄수정.
다른 파일에서도 쓰고있으면 같이 수정됨)	: f2
다음 오류로 이동						: f2
Rename File...(파일명 보기)			: shift + f2
Recent Files(최근 파일목록)			: cmd + e (기본값)
왼쪽 패키지창으로 이동				: ⌘ + 1 (기본값)
'Tool Windows | Database'			: ⌘ + 2
하단 RUN창으로 이동				: ⌘ + 4 (기본값)
파일 내 필드&메소드(창)				: ⌘ + 7 (기본값) - Structure
DB콘솔							: ⌘ + 8 (기본값)
git 도구창							: ⌘ + 9 (기본값)
git 변경내역/커밋창					: ⌘ + 0 ( 기본값)
파일 내 필드&메소드(팝업)			: ⌘ + f12 (기본값) && ctrl + f12 - File Structure
도구창 최대화/최소화				: cmd + shift + ' (기본값)
마지막에 연 창 닫기					: ctrl + shift + f4 (기본값)
메소드/변수 선언/사용위치 창으로 보기	: opt + f7 (기본값) Find Usages
메소드/변수 선언/사용위치로 이동		: cmd 클릭 (기본값) & cmd + b (기본값) & ctrl + ` - Go to Declaration or Usages
구현으로 이동					: opt + cmd + b
최대화 토글						: ctrl + m - Hide All Tool Windows
탭의 왼쪽으로 이동					: ⌘ + ⇧ + [ (기본값)
탭의 오른쪽으로 이동				: ⌘ + ⇧ + ] (기본값)
열편집모드 토글					: cmd + shift + 8 (기본값)
(드래그 후 사용시 다중커서로 바뀜)
대/소문자 토글						: ctrl + u (기본값)
설명 보기							: f1 (기본값) & ctrl + j (기본값) & ctrl + 휠클릭 (기본값) & 마우스 오버 - Quick Documentation
								  켜진 상태에서 esc누르면 닫힘(마우스 오버 제외)
								  ctrl + j 나 f1을 두번누르면 도움말 창이 켜짐. 도움말 창으로 포커스 이동시키려면 한번 더 누르면 됨
파라미터 힌트 보기/숨기기				: opt + `
불필요한 import 제거				: ctrl + opt + o (기본값) - Optimize Imports

테두리 메뉴 표시					: cmd, cmd (기본값)
엔터(커서그대로)					: cmd + enter (기본값)
엔터(커서만이동)					: shift + enter (기본값)
엔터(윗줄에서)						: opt + cmd + enter (기본값)
문장 자동 마무리						: cmd + shift + enter (기본값)
뒤로가기							: ctrl + cmd + ← & 마우스 4버튼
앞으로가기						: ctrl + cmd + → & 마우스 5버튼
블럭 영역 표시						: cmd + 우클릭
코드 접기							: cmd + - & ctrl + -
코드 펼치기						: cmd + = & ctrl + =
코드 각각 접기						: opt + cmd + - & ctrl + opt + -
코드 각각 펼치기					: opt + cmd + = & ctrl + opt + = 
코드 전체 접기						: cmd + shift + - & - & ctrl + shift + -
코드 전체 펼치기					: cmd + shift + = & - & ctrl + shift + =
함수 위치 이동					: cmd + shift + ↑ / cmd + shift + ↓

'Undo' : ctrl + z
'Redo' : ctrl + shift + z
'Copy' : ctrl + c
'Cut' : ctrl + x
'Copy Paths (파일 풀경로 복사)' : ctrl + shift + c
'Editor Actions | Paste' : ctrl + v
'Main Menu | Edit | Paste | Paste' : ctrl + v
'Paste from History…(인텔리제이에서 복사한것만 history에 저장됨)' : cmd + shift + v (기본값) & ctrl + shift + v
'Editor Actions | Scroll to Center' : ctrl + l (기본값)
'Go to Line:Column…(줄번호로 이동)' : cmd + l (기본값) & ctrl + g
'Find...' : ctrl + f
'Replace...' : cmd + r (기본값)
프로젝트에서 단어 일괄 변경 : cmd + shift + r (기본값) - Replace in Files
'Close Tab' : ctrl + w
'Select Next Tab' : ctrl + tab
'Select Previous Tab' : ctrl + shift + tab
'Previous Project Window' : cmd + `
'Next Project Window' : cmd + shift + `
'Comment with Line Comment' : ctrl + /
'Comment with Block Comment' : ctrl + shift + /
'Fix doc comment (doc코멘트)' : ctrl + opt + cmd + d
'Fold Selection / Remove region' : ctrl + shift + . (기존 단축키 제거)
'Cut up to Line End' : ctrl + k (기본값)
'Parameter Info (파라미터 정보 표시)' : cmd + p (기본값)

'Move Caret to Text Start' : ctrl + home
'Move Caret to Text End' : ctrl + end
'Move Caret to Text Start with Selection' : ctrl + shift + home
'Move Caret to Text End with Selection' : ctrl + shift + end
'Move Caret to Next Word' : ctrl + →
'Move Caret to Previous Word' : ctrl + ←
'Move Caret to Next Word with Selection' : ctrl + shift + →
'Move Caret to Previous Word with Selection' : ctrl + shift + ←
'Move Caret to Next Word in Different "CamelHumps" Mode' : opt + →
'Move Caret to Previous Word in Different "CamelHumps" Mode' : opt + ←
'Move Caret to Next Word with Selection in Different "CamelHumps" Mode' : opt + shift + →
'Move Caret to Previous Word with Selection in Different "CamelHumps" Mode' : opt + shift + ←
'Move Caret to Code Block Start(java/javascript/html 다됨)' : ctrl + [
'Move Caret to Code Block End(java/javascript/html 다됨)' : ctrl + ]
'Move Caret to Code Block Start with Selection' : ctrl + shift + [
'Move Caret to Code Block End with Selection' : ctrl + shift + ]
'Next Highlighted Usage (다음 같은 단어로 이동)' : ctrl + opt + ↓ (기본값)
'Previous Highlighted Usage (이전 같은 단어로 이동)' : ctrl + opt + ↑ (기본값)
'Move to Next Occurrence' : f3 (ctrl+f → esc 한번 하고 써야해서 그냥 Next Highlighted Usage 쓰기)
'Move to Previous Occurrence' : shift + f3 (ctrl+f → esc 한번 하고 써야해서 그냥 Previous Highlighted Usage 쓰기)

'Select All Occurrences' : cmd + f3
'Add Selection for Next Occurrence' : ctrl + d
'Unselect Occurrence' : cmd + shift + d
'Editor Actions | Extend Selection (선택범위 확장)' : ctrl + shift + a (커서가 하나일때는 Add Selection for Next Occurrence로도 같은 가능을 할수있음)
'Editor Actions | Shrink Selection (선택범위 축소)' : ctrl + cmd + shift + a
'Extend Line Selection (한줄선택)' : ctrl + shift + opt + a
'Delete to Word Start' : ctrl + backspace
'Delete to Line Start' : cmd + backspace
'Delete to Word End' : ctrl + delete
'Delete to Word Start in Different "CamelHumps" Mode' : backspace
'Delete to Word End in Different "CamelHumps" Mode' : opt + delete
'Clone Caret Above' : ctrl + cmd + ↑
'Clone Caret Below' : ctrl + cmd + ↓
'Column Selection Mode(드래그 ↔ 멀티 커서 토글)' : cmd + shift + 8
'Duplicate Line or Selection' : ctrl + shift + d
'Delete Line' : cmd + d & shift + delete
'Back' : ctrl + cmd + ←
'Forward' : ctrl + cmd + →
'Find in Files…' : cmd + shift + f (기본값)
'Go to File…' : ctrl + shift + f
'Move Line Up' : remove후 ctrl + shift + ↑
'Move Line Down' : remove후 ctrl + shift + ↓
'Toggle Camel Case (CamelCase플러그인)' : ctrl + shift + k
'Request Mapping (RestfulHelper플러그인)' : ctrl + \
'Go to URL Mapping... (RestfulHelper플러그인)' : ctrl + shift + \
'Copy Paths' : ctrl + shift + c
'Compare Files' : cmd + ctrl + opt + d
'Version Control Systems | Diff & Merge | Open Blank Diff Window' : ctrl + cmd + shift + d
'Go to Declaration or Usages' : ctrl + h
'Database | Database Explorer | Edit Data' : enter
'Database | Database Explorer | Go to DDL' : ctrl + d
'Plugins | Database Tools and SQL | Execute' : ctrl + enter
'Other | Execute Current Statement in Multiline Console' : ctrl + enter & ctrl + s & cmd + s
'Plugins | Database Tools and SQL | Reload Page' : esc
'Plugins | Database Tools and SQL | Next Page' : ctrl + cmd + ↑
'Plugins | Database Tools and SQL | Previous Page' : ctrl + cmd + ↓
'Plugins | Database Tools and SQL | First Page' : ctrl + cmd + home
'Plugins | Database Tools and SQL | Last Page' : ctrl + cmd + en
'Plugins | Database Tools and SQL | Ascending' : ctrl + shift + ↑ (기본값)
'Plugins | Database Tools and SQL | Descending' : ctrl + shift + ↓ (기본값)
'Plugins | Database Tools and SQL | Reload Page' : f5
'Plugins | Database Tools and SQL | Open Query Console(sql문 쿼리콘솔)' : ctrl + shift + q
'Plugins | Database Tools and SQL | Add Row' : ctrl + =
'Plugins | Database Tools and SQL | Delete Selected Rows' : ctrl + -
'Plugins | Database Tools and SQL | Clone Row' : ctrl + shift + d
'Plugins | Database Tools and SQL | Revert Selected' : ctrl + z
'Plugins | Database Tools and SQL | Edit Filter Criteria' (where절 검색) : opt + shift + cmd + f (기본값)
'Main Menu | Run | Stop' (쿼리실행 중지) : cmd+ f2 (기본값. DB창으로 이동 후 ctrl+tab 한번 누르고 해야함)
'Plugins | Diagrams | Show UML Diagram' : ctrl + shift + d (이거랑 Duplicate Line or Selection 이외 단축키 제거)
'Database | Database Explorer | Modify Object… 첫번째꺼' : 제거
'Database | Database Explorer | Modify Object… 두번째꺼' : cmd + f6 (기본값) & ctrl + f6
'Toggle Bookmark 0~9' : ctrl + shift + 0~9(기본값) 
'Go to Bookmark 0~9' : ctrl + 0~9(기본값)
'Show (Line) Bookmarks...' : ctrl + shift + b
'Close Tabs to the Left' : ctrl + opt + cmd + shift + ←
'Close Tabs to the Right' : ctrl + opt + cmd + shift + →

'Split Right' : ctrl + shift + cmd + →
'Split Down' : ctrl + shift + cmd + ↓
'Split and Move Right' : ctrl + shift + cmd + →
'Split and Move Down' : ctrl + shift + cmd + ↓
뺀걸 다시 붙이려면 닫기(ctrl+w)+뒤로가기(ctrl+alt+←) 해야함
'Goto Next Splitter' : opt + tab  (opt + ` 는 한글입력모드에서만 먹혀서 사용X)
'Goto Previous Splitter' :  opt + shift + tab

'Quick Switch Scheme...' : ctrl + esc

'Main Menu | Git | Git | Annotate(좌측에 최종수정자/날짜 표시)' : ctrl + cmd + h
'Show History for Selection(원하는 줄(들)의 모든 수정정보창 열기)' : ctrl + opt + cmd + h
'Reformat Code (코드자동정렬)' : ctrl + shift + l
'Plugins | String Manipulation | Create Sequence' : ctrl + shift + i
'Plugins | String Manipulation | Increment' (1증가) : ctrl + ↑
'Plugins | String Manipulation | Decrement' (1감소) : ctrl + ↓
'Plugins | String Manipulation | Align Carets' : ctrl + cmd + a
'Introduce Variable…(변수로 빼기. 반환값이 있는 메소드가 있는 줄에서 쓸 수 있음)' : opt + cmd + v
'Main Menu | Refactor | Inline...(지역변수를 인라인화. opt + cmd + v 와 반대의 기능)' : opt + cmd + n
'Main Menu | Navigate | Goto by Reference Actions | Go to Test' (클래스의 테스트케이스 자동 생성) : cmd + shift + t → enter
'Introduce Field…(필드로 빼기)' : opt + cmd + f
'Extract Method…(메소드로 빼기)' : opt + cmd + m
'Main Menu | Git | Commit…' : cmd + k (기본값)
'Plugins | Maven | Reload project' : cmd + f5 & ctrl + f5

'Other | Run context configuration(main메소드가있는 (현재클래스 or 클릭한클래스) 실행)' : ctrl + shift + r (기본값)
'Main Menu | Run | Run(최근 실행한 main메소드 실행)' : ctrl + r
'Main Menu | Run | Run...(최근 실행한 main메소드들 선택후 실행)' : ctrl + opt + r (기본값)
'Other | Debug context configuration' : ctrl + cmd + shift + r
'Toggle Line Breakpoint(브레이크 포인트 지정)' : cmd + f8 (기본값)
'Main Menu | Run | Debugging Actions | Step Into(실행하고있는 라인(메소드)로 이동)' : f7 (기본값)
'Main Menu | Run | Debugging Actions | Force Step Into(Stepping에 설정되어있는 스킵을 하지않고 깊은곳까지 들어가기)' : opt+shift+f7 (기본값)
'Main Menu | Run | Debugging Actions | Step Out(다시 빠져나오기)' : shift+f8 (기본값)
'Main Menu | Run | Debugging Actions | Step Over(다음 라인으로 이동)' : f8 (기본값)
'Main Menu | Run | Debugging Actions | Resume Program(다음 브레이크 포인트로 이동)' : f9 (기본값)
'Main Menu | Run | Debugging Actions | Run to Cursor(커서가 있는곳으로 이동)' : opt + f9 (기본값)
'Evaluate Expression...(브레이크&디버깅 모드에서 해당 시점의 변수/객체값을 조회
원하는 구문 드래그 후 단축키 or 단축키 후 직접검색 가능. 크롬 콘솔같은 기능)' : opt + f8 (기본값)


★기타 설정
- 오른쪽 수직선 없애기 → shift * 2 → show right margin 검색 → enter

- 아래부터는 Preferences → Editor 에서 설정가능한 UI설정
탭/공백 문자 표시 : General → Appearance → Show whitespaces 체크

- 아래부터는 Preferences → Editor → Color Scheme → General 에서 설정가능한 UI색상 설정
xml파일의 쿼리문 배경색/음영/녹색/파란색 없애기 : Code → Injected language fragment → Background 체크해제 or 색상 변경
탭/공백 문자 :  Text → Whitespaces #363636
탭 세로선 : Editor → Guides → Indent guide #111111
탭 시작점 : Editor → Tear line selection #FF0000
열려있는탭 배경색 : Editor → Tabs → Selected Tab → Background #1F1136
커서가있는 줄 : Editor → Caret row → background #151515
줄번호 : Code → Line number → Foreground #815B89
커서가있는 줄번호 : Code → Line number on caret row → Foreground #D4A4A4
줄번호 배경 : Editor → Gutter background → #0C0C0C
에디터 배경(콘솔창배경기본값) : Text → Default text → #0C0C0C
사용자 출력 전경 : #9C63CB
변수선언 포커스 : Code → Identifier under caret (write) → Effects : Bordered, #999999
스크롤 : Editor → Vertical Scrollbar → Thumb && Thumb while scrolling → Background #1F1136
같은 단어 하이라이트 : Code → Identifier under caret → Background #400000
같은 단어 하이라이트(변수 선언부) : Code → Identifier under caret (write) → Effects : Bordered, #999999

- 아래부터는 Preferences → Editor → Color Scheme → Console Colors → Console 에서 설정 가능한 콘솔창 내부에서의 색상 설정
콘솔창색깔(기본값은 General → Text → Default text) : Background → Background
기본 출력 : Standard output → Foreground #9C63CB
시스템 출력 : System output → Foreground

- 단어 배경색 없애기 (테마에 의해 적용돼있는걸 수정해야함)
Preferences → Editor → Color Scheme → Java → Classes and Interfaces → Class → 체크해제
Preferences → Editor → Color Scheme → Java → Variables → Local variable → 체크해제

-----

vs코드 단축키 (윈도우처럼 변경. 단축키 변경 후 저장 안해도 되고, 삭제시 실행취소 안됨)

기본단축키
moveFileToTrash : del
editor.action.transposeLetters : ctrl + t

변경
renameFile → f2
editor.action.addSelectionToNextFindMatch → ctrl + d
editor.action.selectHighlights → cmd + f3
cursorWordLeft(단어 점프) : ctrl + ←
cursorWordLeftSelect(단어 점프) : ctrl + shift + ←
cursorWordRight(단어 점프) : ctrl + →
cursorWordRightSelect(단어 점프) : ctrl + shift + →
cursorWordPartLeft(카멜/스네이크 점프) : alt + ←
cursorWordPartLeftSelect(카멜/스네이크 점프) : alt + shift + ←
cursorWordPartRight(카멜/스네이크 점프) : alt + →
cursorWordPartRightSelect(카멜/스네이크 점프) : alt + shift + →
deleteWordLeft(단어 점프) : ctrl + backspase
deleteWordPartLeft(카멜/스네이크 점프) : alt + backspase
cursorTop : ctrl + home & cmd + home
cursorBottom : ctrl + end & cmd + end

아래부터는 키 바인딩 추가로
editor.action.transformToUppercase : ctrl + u
editor.action.transformToLowercase : ctrl + l
workbench.action.openGlobalKeybindings(단축키설정창 열기) : ctrl + k , s
keybindings.editor.addKeybinding(단축키 추가) : ctrl + k , a 이고 설정된 단축키가 없을경우는 enter
keybindings.editor.addKeybinding(단축키 변경) : enter(기본값)
keybindings.editor.removeKeybinding(단축키 제거) : ctrl + del (그냥 del로 하면 위험) & ctrl + backspace
workbench.action.selectTheme(테마 설정창 열기) : ctrl + k , t
workbench.action.terminal.toggleTerminal(터미널 토글) : cmd + 5
editor.action.triggerSuggest(자동완성) : shift + space and ctrl + space
workbench.action.nextEditor(다음탭) : ctrl + tab
workbench.action.quickOpenPreviousRecentlyUsedEditorInGroup 제거
workbench.action.previousEditor(이전탭) : ctrl + shift + tab
workbench.action.quickOpenLeastRecentlyUsedEditorInGroup 제거
workbench.view.explorer(탐색기(익스플로러)로 포커스 토글) : cmd + 1
workbench.debug.action.toggleRepl(디버그콘솔창 토글) : cmd + 4
workbench.action.files.openFileFolder : ctrl + o
explorer.newFile(새파일) : ctrl + n
explorer.newFolder(새폴더) : ctrl + shft + n
deleteFile : ctrl + del
undo : ctrl + z
redo : ctrl + shift + z
editor.action.commentLine : ctrl + z
editor.action.blockComment : ctrl + shift + z
workbench.action.files.save : ctrl + s
workbench.action.closeActiveEditor : ctrl + w
actions.find : ctrl + f
editor.action.clipboardCopyAction : ctrl + c
editor.action.clipboardCutAction : ctrl + x
editor.action.clipboardPasteAction : ctrl + v
editor.action.selectAll : ctrl + a
editor.action.copyLinesDownAction : ctrl + shift + d
editor.action.deleteLines : shift + del & cmd + d
workbench.action.openSettings : ctrl + ,
editor.action.insertCursorBelow : ctrl + cmd + ↓
editor.action.insertCursorAbove : ctrl + cmd + ↑
editor.action.moveLinesDownAction : ctrl + shift + ↓
editor.action.moveLinesUpAction : ctrl + shift + ↑
editor.action.smartSelect.expand : ctrl + shift + a
editor.action.smartSelect.shrink : ctrl + shift + s
workbench.action.reopenClosedEditor : ctrl + shift + t
workbench.action.closeEditorsToTheLeft : ctrl + opt + cmd + shift + ←
workbench.action.closeEditorsToTheRight : ctrl + opt + cmd + shift + →
editor.action.quickFix : opt + enter

----------------------------------------------------------------------------------------------------

이클립스 & 디비버 한글입력후 줄바꿈시 사라짐

Karabiner-Elements 와 json파일 다운받아서 아래 경로로 이동 (파일: https://github.com/taedi90/eclipse_kor_fix/releases)
경로 : ~/.config/karabiner/assets/complex_modifications
이후 Karabiner-Elements Preferences → Complex modifications 탭에서 필요한 규칙들을 추가 후 우선순위가 낮다면 올리기
이후 Karabiner-Elements Preferences → Devices 에서 사용하는 마우스가 체크 되어있는지 확인해야한다.

참고 : https://log.taedi.net/eclipse-mac-kor-fix/

----------------------------------------------------------------------------------------------------

오라클 에러 로케일을 인식 할 수 없습니다.(locale not recognized)

시스템 환경설정 에서 언어 및 지역 → 지역 에서 미국으로 변경 후 다시 대한민국으로 변경

----------------------------------------------------------------------------------------------------

이클립스 2020-06버전 설치시 Failed to create the Java Virtual Machine 오류날때

이클립스 응용프로그램 있는곳 가서 ctrl+클릭 → 패키지 내용 보기(Move to Bin) → 
Contents → Info.plist 열기 → 
아래내용 밑에 내용 추가
<string>-keyring</string>
<string>~/.eclipse_keyring</string>
↓↓↓↓↓
<string>-vm</string>
<string>/Library/Java/JavaVirtualMachines/jdk1.8.0_321.jdk/Contents/Home/bin/java</string>
	(자신의 자바경로)
자바경로 확인은 네손가락 펼쳐서 바탕화면 한번 찍고 → cmd+shift+g → /Library/Java/JavaVirtualMachines →
Enter → 타고 들어가서 home → bin → java를 ctrl+클릭 → 정보 가져오기 → 라이브러리부터 끝까지 복사후 
붙여넣고 /java 추가

-----

이클립스 Explorer창 글자크기 키우기(최신버전으로 Darkest플러그인 다운받아야됨)

Preferences → DevStyle → Color Themes → Explorer font size 체크 후 글자크기설정(기본 11)

-----

이클립스 인텔리제이처럼 위에 현재 경로 나오게하기 (최신버전으로 Darkest플러그인 다운받아야됨)

Preferences → DevStyle → Color Themes → Enable Breadcrumb 체크

하는김에 Icon colors도 Primary Colors 로 바꾸고
Force colors 옆에있는 Browse 클릭하면 웹으로 이동되는데 테마 매우 다양하게 있음. 원하는 테마 XML로 다운후 Import... 눌러서 적용 (Retta테마 추천)

----------------------------------------------------------------------------------------------------

인텔리제이 라이브탬플릿(코드조각)

Preferences → Editor → Live Templates
Define에서 원하는 언어 선택 → 추가버튼 클릭 후 추가

Abbreviation: 단축키
Description: 설명
Template text: 내용
Define버튼: 언어 한번 더 선택 (자바스크립트일경우 JavaScript And TypeScript 선택)


★커서/변수는 $변수명$ 이렇게 넣고, Edit variables(변수 편집) 버튼을 눌러 등록을 해줘야 함.
Expression에서 선택해 클래스명, 사용자명, data("Y-MM-d") 이런식으로 함수 사용 가능하고,
fileNameWithoutExtension / fileName 등
포커스가 있는 초기 문자열만 넣어놓고싶으면 Expression 또는 Default value에 "ASD" 이렇게 큰따옴표 감싼 문자열 넣으면 됨

표현식에 아래와같은 함수들을 넣을 수 있음
variableOfType("") - 가장 가까운 변수명으로 치환
variableOfType("List") / variableOfType("String") - 가까운 특정 타입의 변수명을 치환. 인터페이스 가능

★위/아래 버튼으로 순서를 지정하면 탭을 눌렀을시 커서위치가 이동되는 위치순서를 변경할 수 있음.

★Skip if defined(정의된 경우 건너뛰기) 를 체크하면 포커스 해제 가능함

★Define에서 Everywhere를 체크하면 등록한 항목을 모든 언어에서 단축키를 쓸 수 있으며 user그룹에 들어감

-----

인텔리제이에서 자동완성을 할때

tab을 누르면 커서뒤에 붙어있는 글자가 지워지고(괄호는 빼고), enter를 누르면 붙어있는 글자가 유지됨.

------------------------------

기본 라이브템플릿

-----

가장 가까운 배열/컬렉션 객체를 반복하는 코드 생성

iter 치고 엔터

ex)
List<Integer> l1 = Arrays.asList(1,2,3);
for (Integer integer : l1) {

}

-----

가장 가까운 변수를 출력하는 코드 생성

변수가 선언된 줄의 다음 줄에서

soutv 치고 탭/엔터

그다음 그냥 엔터쳐도 되고
여러 변수들중 어느 변수를 출력할건지 선택한 후 엔터쳐도 됨

ex)
String str = "asdf";
System.out.println("str = " + str);

-----

현재 클래스명과 메서드명을 출력하는 코드 생성

soutm 치고 탭/엔터

ex)
System.out.println("C1.main");

-----

현재 메서드의 파라미터 출력

soutp 치고 탭/엔터

ex)
void m1(String s1, int i1){
	System.out.println("s1 = " + s1 + ", i1 = " + i1);
}

----------------------------------------------------------------------------------------------------

★따옴표를 바꿀때( ` / ' / " ) backspace나 delete로 지웠다 다시쓰지말고
shift로 드래그 시켜서 그냥 바로 쓰면 닫는 따옴표까지 같이 바뀜

------------------------------

커서 주변에 파란테두리 포커스박스가 생겼을때

home / end 를 누르면 박스의 처음과 끝으로 커서를 이동할 수 있음

enter를 누르면 다음 괄호 뒤로 커서가 이동되고 포커스박스가 없어짐

esc를 누르면 커서 이동없이 포커스박스만 제거됨

shift + enter 나 cmd + enter 입력은 포커스박스를 해치지 않음

------------------------------

인텔리제이 환경설정 내보내기 & 가져오기

내보내기 : File → Manage IDE Settings → Export Settings...
가져오기 : File → Manage IDE Settings → Import Settings...

------------------------------

인텔리제이 창을 탭으로 보기

1. 인텔리제이 preferences → System Settings → Open project in → New window

2. 맥 일반(환경설정) → 문서를 열 때 탭에서 열기 → 항상

3. 인텔리제이 재시작

------------------------------

인텔리제이 한글/영어 변환

플러그인에서 한글팩 on/off

------------------------------

인텔리제이 클릭이 안되고 쉬프트키가 눌려서 안빠지는것처럼 클릭시 포커스가 안풀리는 버그

1. 한영키 누르면 정상으로 돌아옴

2. 아래 명령어를 터미널에 입력하면 풀린다고 함 (맥 자체의 악센트 입력 기능 비활성화)
terminal에서 해당 명령어 실행 후 Mac 재실행
OS 전체 적용 : defaults write -g ApplePressAndHoldEnabled -bool false
IntelliJ 만 적용 : defaults write com.jetbrains.intellij ApplePressAndHoldEnabled -bool false
IntelliJ 커뮤니티버전만 적용 : defaults write com.jetbrains.intellij.ce ApplePressAndHoldEnabled -bool false

------------------------------

인텔리제이 컴파일 오류 발생위치 찾기

오류난 파일을 열고 에디터창의 오른쪽위에 보면

1. 오류 아이콘들과 각각의 오류에대한 개수가 있음. 그거 누르면 오류목록창이 출력됨.
	그 오류목록창에서 오류를 클릭해서 오류난 곳으로 이동할 수 있고

2. 오류아이콘들 바로 오른쪽에 위/아래 화살표 눌러도 오류난 곳으로 순차적으로 이동됨

------------------------------

인텔리제이 북마크

ctrl + shift + 0~9 로 부대지정하듯이 북마크 가능
ctrl + 0~9 로 등록된 북마크로 이동 가능
ctrl + shift + b 로 등록된 북마크 조회가능

파일 내에서 말고 프로젝트탐색기에서도 폴더/파일에 북마크 가능

------------------------------

인텔리제이 코드 비교/병합기

★다른 파일과 비교하기
View → Compare With...
or
cmd 누르고 다른 파일 클릭 후 Compare Files단축키(기본:cmd + d → ctrl + opt + cmd + d)

★클립보드와 비교하기
View → Compare with Clipboard
or
우클릭 → Compare with Clipboard

★텍스트끼리 비교하기
Open Blank Diff Window단축키 설정 : ctrl + cmd + shift + d


Do not ignore가 기본값인 셀렉트박스에서 무시안함/공백자르기/공백/공백및빈줄/import및서식지정무시 선택할 수 있음. whitespaces and empty lines 추천

Highlight words가 기본값인 셀렉트박스에서 줄/단어/분리된 단어(Highlight split changes)/문자 단위로 차이를 볼 수 있음. split changes 추천

환경설정(톱니바퀴아이콘) → Align Changes Highliting
체크하면 빈줄이 자리를 차지함

위 설정들 모두 바꾸면 winmerge랑 비슷해짐


오른쪽/왼쪽으로 코드를 붙일 수 있음.
이동할때 ctrl 키를 누른채 클릭하면 → 덮이는게 아니라 밑에줄에 추가가됨

고칠거 끝나면 탭 열린거 닫거나 esc누르면 됨

------------------------------

인텔리제이 누가 언제 수정했는지 찾기

좌측에 최종수정자/날짜 표시 : Git → Current File → Annotate with Git Blame
원하는 줄(들)의 모든 수정정보창 열기 : 코드 우클릭 → Git → Show History for Selection

좌측에 기록 표시해놓은 상태에서 누르면 깃 트리창이 열림

------------------------------

인텔리제이(altimate버전) 디비 & ERD


<DB연결>
1. cmd 두번 누르면 "데이터베이스" 탭 나옴. 클릭
2. DB추가


<쿼리 작성기>
DB우클릭 → 쿼리 콘솔로 이동(cmd + shift + f10) → enter

sql 콘솔창 단축키: cmd + 8

실행할 쿼리문 위에 주석을 달면 실행탭에 주석이 보임
↓↓↓
#실행할쿼리명
SELECT
.
.


<테이블 검색>
DB창 → DB접힌거 테이블 목록 나올때까지 열기 → 그냥 테이블명 입력하면 검색되는데, 다음/이전 검색결과로 이동하려면 아래위 방향키로 이동
복사한걸 붙여넣기로 검색하고싶을때는 DB창 → 아무거나 한글자 치고 → 지웠다가 붙여넣고 → 스페이스 누르면 됨
포커스위치한 테이블 정보 보려면 cmd + enter → ctrl + enter


<컬럼 검색>
방법1. shift, shift (탐색 → 전체 검색) → 해당 컬럼을 정의한 테이블 목록 나옴
방법2. 쿼리로 컬럼검색
방법3. exerd에서 erd파일 불러와서 컬럼검색


<제약조건 검색>
톰캣콘솔오류에 외래키 제약조건 오류가 뜰 경우 오류에 나온 제약조건명(ex. FK_~_TO_~)을 shift, shift로 검색하기
그럼 해당의 테이블의 컬럼을 어느 테이블에서 참조하고 있는지 알 수 있음


<테이블 데이터 보기>
테이블에 포커스 위치시키고(테이블 검색) → cmd + enter
500개까지 LIMIT되어 나오고 더 보려면 페이지 넘겨야됨 (왼쪽위에 버튼있음. alt + cmd + ↓ / ↑ (단축키변경→)  ctrl + cmd + ↓ / ↑)
오름차순/내림차순으로 정렬하려면 해당 컬럼의 아무행에 커서 놓고 ctrl + shift + ↑ / ↓
페이지 새로고침시 ctrl + r (단축키변경→) f5
json으로 보려면 CSV선택되어있는 셀렉트박스에서 json선택 → 오른쪽 눈아이콘(View as) → Text 클릭

데이터 지우려면 행 선택하고 del 혹은 -버튼 누른후
ctrl + enter을 쳐야 삭제됨

데이터 넣으려면 +버튼 누른 후
마찬가지로 ctrl + enter을 해야 추가됨

행 복사 단축키 : Plugins | Database Tools and SQL | Clone Row

★ 컬럼 행 검색은 디비버와 달리 직접 넣어줘야함
필터 아이콘 옆에 입력한 클릭 후 아래처럼 직접 where절 입력
COT_ID="038a96e7-dc66-4d13-9bd1-781f607e727f"


<DDL 보기 / 실행>
DDL버튼 누르기 or 단축키 로 DDL창으로 이동가능
DB 선택하고 DDL 실행 시킬 수 있음


<xml파일에서 쿼리 실행하기>
커서를 쿼리문 중간에 놓고 실행(ctrl+enter)
혹은 실행할 부분만 드래그를 하고 실행(ctrl+enter)


<테이블 수정>
데이터베이스창 → 테이블 우클릭 → 테이블 수정
or
cmd + f6


<ERD>

모든 테이블 조회 : 테이블 들어있는 폴더 우클릭 → (다이어그램 → 시각화 표시 (켜지는데 시간 좀 걸림) or 단축키)
한 테이블 관계 조회 : 테이블 클릭 → 다이어그램 단축키(Plugins | Diagrams | Show UML Diagram)

★외래키 연결선들이 겹쳐져서 1개인것처럼 보일때가 있음. 선을 한번 더 클릭하면 연결선이 다른 외래키 테이블 선으로 바뀜(선을 움직여서 보기 편하게 옮겨놔도 됨)
(참고로 식별관계에서의 화살표방향이 부정확한듯. 테이블 외래키 제약조건이 정확하니 그걸로 보기)

1:1배율		: cmd + /
확대/축소		: ctrl + 스크롤
검색			: ctrl + f / cmd + f
움직이기		: 우드래그
무한무빙		: ctrl + 우드래그
무한무빙 정지	: ctrl + 우클릭
돋보기		: opt (누른상태로 스크롤도 가능)
시작 위치로	: ctrl + 좌그래그 살짝

------------------------------

DB 덤프

-----

테이블 내보내기

원본 테이블 선택 → 우클릭 → 가져오기/내보내기 → DDL 데이터 소스로 덤프 → DDL 데이터 소스 생성 → sql파일 생성시킬 수 있음

-----

테이블 복사하기

원본 테이블 선택 → F5(우클릭 → 가져오기/내보내기 → 다음으로 테이블 복사...)
원하는 DB에 새로 테이블을 만들거나, 기존 테이블에 붙여넣을 수 있음

기존테이블에 붙여넣을때는 기존 테이블의 시퀀스가 유지되고(기존시퀀스가 3인 상황에서 3,4,5,6 이 복사되왔어도 시퀀스는 변화없이 3으로 유지됨)
기존 테이블의 컬럼에 맞춰지고, 복사하기전에 컬럼을 추가할수도 있음. 제약조건에 걸려서 오류발생시 데이터가 안들어가고 오류파일이 로컬에 저장됨

타킷 스키마 : 붙여넣을 DB
테이블 : 붙여넣을 테이블. 새 테이블 or 기존 테이블 표시가 있음

----------------------------------------------------------------------------------------------------

인텔리제이 git


브랜치 & 트리 : cmd + 9
변경사항 & 커밋 : cmd + 0

-----

변경기록 파일목록에서 더블클릭 누르거나 or 우클릭 → Show Diff 누르면

변경소스 확인 및 수정 가능

-----

스태시 추가 : Git → Uncommitted Changes(커밋되지않은 변경내용) → Stash Changes...(변경 내용 스태시...)
스태시 목록(적용/삭제) : Git → Uncommitted Changes(커밋되지않은 변경내용) → Unstash Changes...(변경 내용 스태시 취소...)
	Apply Stash : 스태시 적용
	View : 바꾼 파일
	Drop : 선택한 스태시 삭제
	Clear : 스태시 전체삭제
Pop stash를 체크하면 적용한 스태시는 지워짐

-----

체리픽을 이용하면 다른브랜치의 커밋 변경내역을 쉽게 가져올 수 있음

브랜치 소스 전체병합을 안하고 커밋한 변경내용만 복사하기가 가능

체리픽 쓰기전에
먼저 변경사항들이 있다면 스태시에 넣고 해야 불상사를 방지할 수 있음

-----

커밋 cmd+0누른 후 전체선택 or 일부선택하고 ctrl + enter

-----

브랜치(cmd + 9) 체크아웃후 병합 / 충돌났을때 머지도 가능

변경사항에 충돌병합 에서 Resolve클릭 → merge클릭 → 왼쪽위에 위아래화살표(f7 / shift+f7) 눌러 이동하면서 병합하면됨

혹시 충돌병합이 잘못됐을지 모르니 소스트리에서 한번 확인하는게 좋음
커밋옵션에서(점세개아이콘) Analyze code 체크해제 안하면 커밋하는데 매우 오래걸림

-----

트리에서 초기화/되돌리기 가능

-----

충돌 해결시

"Resolve Simple Conflicts(간단한 충돌 문제 해결)(마법봉아이콘)" 버튼 누르고 하기.

이 기능은 단어 차이를 판단하지 못함
단어차이를 병합해야할때는 수동으로 하는게 안전함(충돌창에서 하거나 or 소스트리 보고 에디터창에서 하거나)

-----

히스토리 보기

파일목록에서(cmd+1) 우클릭 → Local History → Show History

----------------------------------------------------------------------------------------------------

인텔리제이 플러그인

- 테마
Ultra Dark Theme (2022.01버전 지원 안함)
Celestial
Visual Studio Code Monokai HC

- Atom Material Icons
아이콘 예쁘게

- key promoter x
마우스로 버튼을 클릭시 단축키 알려줌

- Rainbow Brackets
헷갈리기 쉬운 괄호 기호에 색을 부여해서 가독성을 높여줌

- nyan progress bar
로딩바 예쁘게

- .ignore
git이나 Docker등을 이용할때 커밋을 할때 제외되는 파일을 설정할 수 있음
프로젝트에서 파일을 생성할 수 있으며 txt파일 형태로 제외하려는 파일명을 등록해두면 제외됨
개인 eclipse 설정 파일등, IDE 고유의 폴더등을 제외할때 아주 유용함 (실수로 커밋, 푸시할 일도 줄어듦)

- CodeGlance
Sublime 처럼 코드 미니맵(코드 보기 및 스크롤 기능)을 제공해줌

- RestfulHelper
Spring MVC 기반 프로젝트에서 엔드포인트 URL 기반의 검색 및 바로가기 기능을 제공한다.
단축키는 ctrl + \ (Plugins | RestfulHelper | Request Mapping 에서 변경가능)

- camel case
케밥→스네이크→파스칼→카멜→등등으로 변환.
단축키는 ctrl + shift + k (플러그인 | CamelCase | Toggle Camel Case 에서 변경 가능)

- iBATIS/MyBatis plugin
설치시 DAO인터페이스에 연결된 XML파일에 자연스럽게 (Ctrl + T) 또는 (Ctrl + 클릭)으로 접근되어짐

------------------------------

인텔리제이 import에서 제거할 패키지 or 클래스 지정하기

Preferences → Editor → General → Auto Import 여기서 +버튼 눌러서 추가하거나

수동으로 선택해서 import하기전에 잘 보면 화살표가 있음 그거 눌러서 제거해도됨

------------------------------

인텔리제이 한줄씩 디버깅

1. 브레이크포인트 설정 (줄번호 옆 클릭하면 빨간동그라미 생김)
2. 실행 → 디버그 'XXX'
3. f7로 한칸씩 실행 (다음 브레이크포인트로 건너뛰려면 f8)

------------------------------

인텔리제이 불필요한 import 제거

1. optimize imports on the fly

2. ctrl + opt + o

------------------------------

인텔리제이 클래스 계층 or 다이어그램 보기

1. 계층
파일 or 에디터창 → ctrl + h
닫기는 ctrl + shift + f4 (or) 들어가서 ctrl + w (or) cmd+2 * 2

2. 다이어그램
파일 or 에디터창 우클릭 → 다이어그램 → 다이어그램 표시 opt + cmd + shift + u, enter
보고싶은것들을 선택할 수 있음 (필드/생성자/메소드/프로퍼티/이너클래스)

------------------------------

로그내용이 길어 앞부분이 짤릴때 더 많이보기 (배치 작업시 편리)
Editor → General → Console 에서 Override console 어쩌고 체크하고 기본값인 1024kb를 수정하면 됨

------------------------------

인텔리제이에서 패키지 통째로 복사할때

그냥 복사한상태 그대로 바로 붙여넣기(ctrl+c, ctrl+v, enter) 하면 패키지 안에 같은 이름의 패키지가 생김.
그 패키지에서 f2 누르고 . (디렉토리) 한단계 지워서 상위폴더로 보내고 원하는 이름으로 바꾸면 복제 완료

------------------------------

Unexpected update count received (Actual: 2, Expected: 1). All changes will be rolled back.
↓↓↓
똑같은 내용의 행이 2개 이상있고 그걸 ui로 수정하려고 할때 발생
같은 내용의 행을 모두 선택한 후 일괄 삭제하고
기본키 만들기 (삭제를 안하고 만드려하면 Duplicate entry 'XXX' for key 'XXX' 발생)

------------------------------

인텔리제이 퀵서치에서 확장자에 해당하는 파일목록만 보거나, 확장자에 해당하지 않는 파일목록만 볼 수 있음

File mask: 콤보박스 클릭후
해당 확장자만 : *.확장자[, *.확장자]
해당 확장자 제외 : !*.확장자[, !*.확장자]

파일마스크 되어있는데 왜 검색안되지 하지 말고 켜져있나 확인하기

------------------------------

인텔리제이 퀵서치에서 떨어진 단어를 검색하는 방법

1. 정규식 아이콘 on 시키기 (ctrl + opt + x)

2. 아래처럼 검색
단어1.*단어2

------------------------------

인텔리제이 실행취소 개수변경

(Help → Find Action...) (= cmd + shift + a) → Registry 검색 → undo.globalUndoLimit과 undo.documentUndoLimit을 수정

undo.globalUndoLimit : 10 → 100
undo.documentUndoLimit : 100 → 1000

확인 누르고 IDE 재실행

undo.globalUndoLimit - 전체 시스템에서 파일 삭제, 이동 취소, 파일 추가 실행취소 등을 되돌리는 history limit 개수
undo.documentUndoLimit - 문서 내 되돌리기

------------------------------

인텔리제이 안드로이드 테스트

preferences → Appearance & Behavior → System Settings → Android SDK → Edit 클릭 → 최신버전으로 하나 설치

설치했으면 인텔리제이 재시작후 Tools → Android → AVD Manager → 실행버튼 클릭

그럼 안드로이드 애뮬레이터가 열리며
안드로이드 앱과 동일한 환경에서 테스트할수있음 (navigator.userAgent.toLowerCase().indexOf('android') > 0 → True)
근데 개발자도구는 안되는듯

----------------------------------------------------------------------------------------------------

서브라임 플러그인

-----

테마 변경

Colorsublime

-----

카멜 표기법 변환
https://github.com/jdavisclark/CaseConversion 에서 다운받고
서브라임 cmd + shift + p → browse packages 하면 파인더가 열림. 거기에 다운받은 폴더(CaseConversion-master) 붙여넣기 → 서브라임 재시작
https://reference-m1.tistory.com/362참고

변환 단축키 (두번 누르기)
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

-----

연속된 번호 만들기

cmd + shift + p → install package → increment selection
설치 이후 숫자 자동증가 단축키 사용 가능		- ctrl +cmd + i

번호0
번호0
번호0
다중커서 0선택 후 ctrl + cmd + i
↓↓↓
번호1
번호2
번호3

번호3
번호3
번호3
다중커서 3선택후 ctrl + cmd + i
↓↓↓
번호3
번호4
번호5

<간격이 있는 연속된 번호 만들기>
번호1
번호3
번호1
번호1
다중커서 번호선택후 ctrl + cmd + i
↓↓↓
번호1
번호3
번호5
번호7

<거꾸로도 가능>
번호3
번호1
번호5
번호5
다중커서 번호선택후 ctrl + cmd + i
↓↓↓
번호3
번호1
번호-1
번호-3
번호-5

-----

코드 자동정렬

Alignment

정렬할 영역 선택후
ctrl + cmd + a

-----

스니펫

Tools → Developer → New Snippet...

<snippet>
    <content><![CDATA[console.log('Hello, ${1:this} is a ${2:snippet}.']]></content>
    <tabTrigger>greeting</tabTrigger>
    <scope>source.js</scope>
</snippet>

<content> : 실제로 삽입될 코드 내용을 작성합니다. <![CDATA[ ... ]]>로 감싸줍니다.
<tabTrigger> : 스니펫을 호출할 키워드를 작성합니다. 위의 예시에서는 greeting을 입력하면 스니펫이 활성화됩니다.
<scope> : 스니펫이 적용될 문서의 유효 범위를 작성합니다. 위의 예시에서는 source.js로 설정되어 JavaScript 파일에서만 스니펫이 동작합니다.

커서 넣고싶으면 $0 이렇게 쓰면됨

파일을 아무이름이나
아무이름.sublime-snippet
이렇게 저장후
cmd + shift + p → Preferences: Browse Packages 엔터쳐서 폴더 열기 → User 폴더 열기 → 아까 만든 아무이름.sublime-snippet 복붙

----------------------------------------------------------------------------------------------------

vs코드 팁

-----

한글설정

cmd + shift + p

language 입력 → Configure Display Language → 한국어 선택 → 재실행

없으면 Install Additional Languages 선택후 Korean 검색 및 설치

-----

테마 변경 : 상단바 제일 왼쪽 Code → 기본 설정 → 색 테마 → 추가 색 테마 찾아보기...
추천: Github Dark Color Default, Ayu Dark, Ayu Dark Bordered, Community Material Theme Ocean High Contrast, Tokyo Night, Material Theme

-----

f3 / shift + f3 / cmd + f3 할때
단어 가운에 커서 놓고ctrl + d 한번 누르고(expand) 해야함

-----

탭 눌렀을때 공백 말고 탭문자열 쓰기
설정 → 일반적으로 사용되는 설정 → Editor: Insert Spaces 체크해제
설정 → 텍스트 편집기 → Detect Indentation 파일마다 설정 다르게 하는건데 이것도 체크해제

-----

cmd + , 누른 후 우측 상단에 '설정 열기(JSON)' 버튼 클릭해 settings.json 파일을 열 수 있음

아래 3줄 추가하면 저장시 자동정렬됨 (특정 포맷에서만 바꾸고 싶으면 editor를 html등으로 바꾸기)

"editor.formatOnSave": true,
"editor.formatOnPaste": true,
"editor.formatOnType": true

-----

vs코드 플러그인

★Auto Rename Tag : HTML / JSX / XML  등의 여는태그와 닫는 태그를 한번에 수정할 수 있게 해줌

★change-case : case 변경플러그인
설치후 extension.changeCase.commands 단축키 ctrl + shift + k 로 추가

★Prettier : 코드 정렬 예쁘게 만들어주는 플러그인
설치후 재실행 하고 ctrl + , 눌러 환경설정 → 사용자 → 확장 메뉴에 Prettier 메뉴가 생겨있음. 거기서 커스텀 하기
설정 → editor format on save 검색 → Editor: Format On Save 체크
설정 → default formatter 검색 → Editor: Default Formatter에 null로 되어있는걸 Prettier - Code formatter로 바꿔야함
setting.json 에서 editor.formatOnSave 가 true인지 체크
https://ux.stories.pe.kr/150 참고

-----

Snippet(스니펫, 코드조각) 만들기

상단바 제일 왼쪽 Code → 기본 설정 → 사용자 코드 조각 구성 → (새 전역 코드 조각 파일... → 파일명 입력 후 엔터) or 기존 코드 조각 선택

그러면 ~.code-snippets 파일이 만들어지는데
주석에 샘플코드가 있으니 복사 붙여넣기 하고 수정

"콘솔로그": {
	"scope": "javascript,typescript",
	"prefix": "cl",
	"body": [
		"console.log($1);",
		"con$3sole.log('$2');",
		"$4"
	],
	"description": "console.log출력"
},										// 2개이상 만들때 ,(쉼표) 사용 (json형식으로 작성)
"함수생성": {								// 단축키 제목
	"scope": "javascript,typescript",			// 코드조각을 쓸 언어
	"prefix": "fu",							// 코드조각을 쓸때 입력하는 축약어
	"body": [								// 코드 내용
		"function ${1:name}(${2:param}){",	// $순번 및 ${순번,이름} 입력해놓으면 커서 시작위치 조정 및 탭으로 커서 이동가능
		"\t$3",							// 내용 줄바꿈은 ,(쉼표)로 구분. espace코드 사용가능
		"}"
	],
	"description": "함수를 생성함"				// 코드조각 이용직전에 목록에 나오는 설명. 안나오면 단축키입력후 제목 오른쪽에 화살표 클릭해놓기
}

$변수명 or ${변수명} 이처럼 사용.

포커스를 넣고싶다면 $1 $1 $2 이렇게 하면 되고
문자에 포커스를 넣고싶을때는 ${1:문자} ${1:문자} ${2:문자} 이런식으로 넣으면 됨
변수에 포커스를 넣고싶을때는 ${1:$변수} ${1:$변수} ${2:$변수} 이런식으로 넣으면 됨
${1가,나,다|} 이런식으로 |(파이프)를 넣어서 선택할 수 있게 할 수 도 있음 

\n(줄바꿈), \t(탭문자) 등 쓸 수 있음

아래 여러가지 변수들을 쓸 수 있음

TM_SELECTED_TEXT : 현재 선택된 텍스트 또는 빈 문자열
TM_CURRENT_LINE : 현재 줄의 내용
TM_CURRENT_WORD : 커서 아래에 있는 단어의 내용 또는 빈 문자열
TM_LINE_INDEX : 제로 인덱스 기반 라인 번호
TM_LINE_NUMBER : 하나의 인덱스 기반 라인 번호
TM_FILENAME : 현재 문서의 파일 이름
TM_FILENAME_BASE : 확장자가 없는 현재 문서의 파일 이름
TM_DIRECTORY : 현재 문서의 디렉토리
TM_FILEPATH : 현재 문서의 전체 파일 경로
RELATIVE_FILEPATH : 현재 문서의 상대(열린 작업 공간 또는 폴더에 대한) 파일 경로
CLIPBOARD : 클립보드의 내용
WORKSPACE_NAME : 열려 있는 작업 공간 또는 폴더의 이름
WORKSPACE_FOLDER : 열려 있는 작업 공간 또는 폴더의 경로

<현재 날짜/시간>
CURRENT_YEAR : 현재 연도
CURRENT_YEAR_SHORT : 현재 연도의 마지막 두 자리
CURRENT_MONTH : 두 자리 숫자로 된 월(예: '02')
CURRENT_MONTH_NAME : 월의 전체 이름(예: 'July')
CURRENT_MONTH_NAME_SHORT : 월의 짧은 이름(예: 'Jul')
CURRENT_DATE : 두 자리 숫자로 된 월의 일(예: '08')
CURRENT_DAY_NAME : 요일 이름(예: '월요일')
CURRENT_DAY_NAME_SHORT : 요일의 짧은 이름(예: '월')
CURRENT_HOUR : 24시간제 형식의 현재 시간
CURRENT_MINUTE : 두 자리 숫자로 된 현재 분
CURRENT_SECOND : 두 자리 숫자로 된 현재 초
CURRENT_SECONDS_UNIX : Unix epoch 이후 경과된 시간(초)

<임의의 값을 삽입하는 경우>
RANDOM : 6개의 임의의 Base-10 숫자
RANDOM_HEX : 6개의 임의의 Base-16 숫자
UUID : 버전 4 UUID

<주석>
BLOCK_COMMENT_START : javascript에서는 /*, HTML에서는 <!-- 이렇게 표시됩니다.
BLOCK_COMMENT_END : javascript에서는 */, HTML에서는 --> 이렇게 표시됩니다.
LINE_COMMENT : javascript에서 // 이렇게 표시됩니다.

자세한 설명은 아래 참고
https://code.visualstudio.com/docs/editor/userdefinedsnippets
https://ux.stories.pe.kr/290

.ts확장자에서 쓰고싶으면 "scope": "typescript"
.tsx확장자에서 쓰고싶으면 "scope": "typescriptreact"

----------------------------------------------------------------------------------------------------

롬복 오류날때 → 롬복 설치

----------------------------------------------------------------------------------------------------

이클립스 maven 설치 pon.xml에 설정 돼있는데 안될때

프로젝트 우클릭 → Maven → Update Project... → OK
프로젝트 우클릭 → Run As → Maven install

----------------------------------------------------------------------------------------------------

터미널(리눅스명령)

man [명령어명] : 명령어를 쓰는법(#도움말#메뉴얼#사용법)을 알려줌
[명령어명] --help : docker, git 등에서 명령어를 쓰는법을 알려줌

tab를 누르면 자동완성 or 파일 목록을 보여줌

/etc : 설정파일들이 모여있는 폴더
/var/log : 로그들이 모여있는 폴더
/usr/shard, /usr/local : 서비스가 구동되기 위하여 필요한 파일들 (설정 파일을 제외한 필수 파일들)
/var/lib : 서비스가 실행되면서 생성되거나 발생한 데이터의 파일들
/proc : 시스템(하드웨어, 스펙) 관련

cd : 경로이동
cd 또는 cd ~ 는 홈디렉토리로, 'mac'이라는 계정으로 접속중이라면/users/mac 폴더가 되고, root계정으로 접속중이라면 / 가 되고
cd /는 루트폴더가 된다 (bin, users, volumes, cores, System 등이 있다)

외장하드/USB 경로 : /volumes

pwd : 현재경로
/usr/libexec/java_home : JDK경로

ls : 디렉토리 목록을 보여줌
ls -a,
ls -all : 숨김파일을 포함하는 옵션
ls -l : 표형식으로 상세정보까지 보여주는 옵션
ls -h : 파일크기를 보기 편하게 단위화해서 보여주는 옵션 (l옵션과 함께 쓰기)
ls -S : 파일크기 내림차순으로 정렬
ls -Sr : 파일크기 오름차순으로 정렬
ls -t : 날짜 내림차순으로 정렬
ls -tr : 날짜 오름차순으로 정렬

옵션순서는 바뀌어도 상관 없음
ex) ls -hla
      ||
    ls -lah
      ||
    ls -ahl

-----

ls -l 첫번째정보 : 파일유형&권한정보&확장된속성 10~11자리
ex) drwxr-xr-x@
ex) -rw-r--r--

첫번쩨 정보에서 1번째자리 글자는
d : 디렉토리(=폴더)
- : 파일
l : 바로가기
b : 블록디바이스
c : 문자디바이스

다음 3개씩 한세트

권한
r는 읽기 w는 쓰기 x는 실행

r = 읽기 = 4
w = 쓰기 = 2
x = 실행 = 1

x,q,x = 7 (모두다)
r,w,- = 6 (읽기&쓰기)
r,-,x = 5 (읽기&실행)
r,-,- = 4 (읽기)
-,w,x = 3 (쓰기&실행)
-,w,- = 2 (쓰기)
-,-,x = 1 (실행)

첫번째 자리 : 소유자
두번째 자리 : 그룹
세번째 자리 : 그외

chmode : 파일/디렉토리의 권한 변경 (파일/폴더 이동/이름변경/삭제 등과는 상관없음)
chmod 755 ./* : 현재 폴더의
 모든 파일에 권한을 부여함 (파일을 만들면 644(rw-r--r--)가 기본)
chmod -r 755 : 폴더및 폴더 내부 모든 폴더/파일도 적용시키는 옵션

첫번째 정보에서 10번째 글자 뒤에 @가 붙어있으면(11번째글자) : 
추가적인 속성값이 있음 (인터넷에서 다운로드받았거나 특정 프로그램으로 만든 파일)
ls -l 에서 추가속성 확인 옵션 : -@

chmod : 파일/디렉토리 소유자 변경

-----

ls -l 두번째 정보 : 링크의 수
ex) 20

ls -l 세번째 정보 : 해당 파일/폴더에 대한 소유권을 가진 소유 사용자의 이름
ex) mac

ls -l 네번째 정보 : 해당 파일/폴더를 소유한 그룹의 이름
ex) staff

ls -l 다섯번째 정보 : 파일/폴더 크기
ex -l)  3392
ex -lh) 3.3K

ls -l 여섯번째 정보 : 파일/폴더 수정 월
ls -l 일곱번째 정보 : 파일/폴더 수정 일
ls -l 여덟번째 정보 : 파일/폴더 수정 시간
ex) 2 20 21:13

ls -l 아홉번째 정보 : 파일/폴더 이름
ex) Desktop

-----

cat /etc/group : 그룹 전체 조회
cat /etc/group | grep staff : 'staff'라는 그룹에 소속된 사용자 조회

-----

rm [파일/폴더명] : 파일/폴더 완전삭제
rm -r [파일/폴더명] : 폴더를(안에있는 파일까지 모두) 삭제하는 옵션 (이 옵션이 없으면 폴더는 삭제되지 않음)
rm -f [파일/폴더명] : 파일을 삭제할건지 메시지를 출력하지 않음
rm -d [파일/폴더명] : 비어있는 폴더들만 삭제하는 옵션
rm -i [파일/폴더명] : 각 파일/폴더를 삭제할때 삭제여부를 묻도록 하는 옵션
rm -v [파일/폴더명] : 모든 처리과정을 출력하는 옵션

rm * : 현재 폴더 있는 폴더/파일 모두 제거

rm -rf /* → 벽돌만들기 (요즘은 sudo rm --no-preserve-root -rf /* 라고 함)

rmdir : 폴더를 삭제하는 명령어인데 rm의 -r 옵션으로 대체가 가능함

-----

mkdir [폴더명] : 폴더 생성
mkdir -p : 경로상에 없는 폴더가 있으면 다 만들어지는 옵션
mkdir -v : 진행상황 메시지 출력

touch 파일명 : 0바이트 파일 생성
touch -m 파일명 : 파일의 수정시각을 서버현재시각으로 설정
touch -t yyyymmddhhmm 파일명 : 파일의 수정시각을 원하는 날짜시각으로 설정 (수정날짜시각을 생성날짜시각보다 이전으로 설정하면 생성일도 수정일로 바뀜)

echo '[파일내용]' > [파일이름] : 파일 생성, 내용 입력 가능

cat 파일명 : 파일 내용 확인
cat 파일명 파일명 : 여러 파일 내용 확인
cat *.py : 여러 파일 내용확인(와일드카드 사용)

head 파일명 : 위에서 20줄까지 보기
head -n 3 note.txt : 위에서 3줄까지 보기
tail : 밑에서 20줄까지 보기

mv [폴더/파일명] [바꿀 새 이름] : 파일/폴더명 변경

mv [원본 폴더/파일명] [도착 폴더명] : 파일/폴더 이동
mv [원본 폴더/파일명] [원본 폴더/파일명] ... [도착 폴더명] : 파일/폴더 일괄 이동
mv *[원본 폴더/파일명]* [도착 폴더명] : 제목에 특정 문자열이 포함된 파일/폴더 일괄 이동 (*를 앞/뒤 한쪽에 붙이기 가능. (~로 시작/~로 끝) )
mv * [도착 폴더명] : 모든 파일 이동 (폴더들이 있어도 파일만 이동됨)

★파일 이동시 확장자까지 꼭 써야되고, 띄어쓰기가 있을경우 따옴표(' or ") 묶기

cp [폴더/파일명] [도착 폴더명] : 파일 복사
cp [폴더/파일명] [도착 폴더명]/[파일명] : 파일 복사(파일명 변경)
cp -r [폴더/파일명] [도착 폴더명] : 폴더 복사

숨김파일 보이기 : defaults write com.apple.finder AppleShowAllFiles YES && killall Finder
숨김파일 숨기기 : defaults write com.apple.finder AppleShowAllFiles NO && killall Finder
탐색기에서 숨김파일 보이기/숨기기 단축키 : cmd + shift + .

wget [tar.gz링크주소복사해온거 붙여넣기] : 웹에서 파일을 다운받아 현재 디렉토리에 저장

tar -cvf [파일명.tar] [폴더명] : tar로 묶기
tar -xvf [파일명.tar] : tar파일 풀기
tar -zcvf [파일명.tar.gz] [폴더명] : tar.gz로 압축하기
tar -xvaf [압축파일명] : tar.gz파일 압축해제 (.zip파일을 압축해제하려면 apt install unzip 로 unzip을 다운받아서 unzip [압축파일명])

ssh imchaewon@[사설ip주소] -p 22222 : 가상원격서버 접속
ssh imchaewon@localhost -p 22222 : 가상원격서버 접속

exit : ssh 연결 끊는 명령어

localhost == 127.0.0.1

| gerp 문자열 : 파이프라인(|) 으로 받은 결과에서 해당 문자열을 검색해줌
	log에서 '404' 등이 포함된줄만 검색할때 쓸 수 있음
| grep -i 문자열 : 대소문자 구분안함
| grep -v 문자열 : 해당 문자열이 없는것만 검색

| grep 'a\|e' : 여러문자 검색 (escape문자 사용, 따옴표감싸야함)
| egrep 'a|b' : 여러문자 검색 (egrep 사용, 따옴표감싸야함)

-----

scp [파일명] [원격지_id]@[원격지_ip]:[받는 위치] : 파일 전송
scp -P [포트포워딩 후 호스트포트번호 입력] [원격지_id]@[원격지_ip]:[받는 위치] : 파일 전송 (포트옵션)
ex) scp -P 22222 ~/Desktop/test root@localhost:/
ex2) scp -P 22222 ~/Desktop/test imchaewon@127.0.0.1:~
ex3) sudo scp -i ~/imchaewon.pem jpashop-0.0.1-SNAPSHOT.jar ec2-user@43.201.248.134:/home/ec2-user/
마지막에 세미콜론(:)을 안쓰면 Read-only file system 뜸

aws ec2에 배포할경우 ssh 접속시 키페어가 필요한데 아래처럼 -i 옵션으로 키파일을 넣으면 됨
imchaewon@imchaewon-ui-MacBookAir libs % sudo scp -i ~/imchaewon.pem jpashop-0.0.1-SNAPSHOT.jar ec2-user@43.201.248.134:/home/ec2-user/

키페어를 안넣으면 아래처럼 권한이 없다는 메시지가 나옴
ec2-user@43.201.248.134: Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
scp: Connection closed

목적지(원격서버)에 파일을 전송할때 루트경로에 전송하려고 할 경우 권한이 없어 전송에 실패됨
scp: dest open "/jpashop-0.0.1-SNAPSHOT.jar": Permission denied
scp: failed to upload file jpashop-0.0.1-SNAPSHOT.jar to /

원격지경로를 아래처럼 특정 사용자 폴더 경로 안의 경로로 지정해야함
imchaewon@imchaewon-ui-MacBookAir libs % sudo scp -i ~/imchaewon.pem jpashop-0.0.1-SNAPSHOT.jar ec2-user@43.201.248.134:/
↓↓↓
imchaewon@imchaewon-ui-MacBookAir libs % sudo scp -i ~/imchaewon.pem jpashop-0.0.1-SNAPSHOT.jar ec2-user@43.201.248.134:/home/ec2-user/

Amazon Linux 운영체제 기준
자바 설치 : sudo yum install java-11-amazon-corretto.x86_64
자바 버전 확인 : java -version
참고) https://kitty-geno.tistory.com/25

기타 운영체제
설치 가능한 자바 검색 : yum list java*
설치 : yum install java-11-amazon-corretto.x86_64

-----

top : cpu점유율
date : 현재날짜

./[쉘스크립트파일명.sh] : 현재폴더에서 쉘스크립트 파일 실행

which 프로그램명 : 프로그램이 설치된 경로 출력

------------------------------

포트번호는 0~65535 까지 쓸 수 있음

------------------------------

curl -XGET "[URL]" : http통신 요청을 했을때 리턴되는 값을 확인 가능

-u 옵션(--user) : 유저 ID/PW 보낼때 씀
curl -XGET 'https://elk.visitkorea.or.kr/logstash-visitkorea_access_log*/_search' -u develop:uniess1208

-H 옵션(--header) : Content-Type:application/json 등
헤더를 여러개 넣고싶을때는 그냥 -H를 여러번 쓰면 됨
ex) -H "accept: */*" -H "두번쨰 헤더: 두번째 헤더 값"

-d 옵션(--data) : POST메소드 요청시 데이터를 보내기위해 씀

-X 옵션(--request) : 요청 메소드 (GET / POST). 붙여써도 됨(-XGET / -XPOST)


1. JSON형식 데이터
curl -XPOST http://localhost:8000/data \
-d '{"key1":"value1", "key2":"value2"}' \
-H "Content-Type: application/json"

2. URL형식 데이터
curl -XPOST http://localhost:8000/data \
-d "key1=value1&key2=value2" \
-H "Content-Type: application/x-www-form-urlencoded"

-----

한줄로 쓰는법
curl -XPOST https://korean.visitkorea.or.kr/api/v1/trss/lottery -H 'X-SSRP-ID: 230661ea-957a-40cf-8315-6e557ce7a1f7' 
-H 'Content-Type:application/json' -H 'accept: */*' -d '{"tnmId": "1d6c84e2-122d-47e1-aa48-098d3fe615b6"}'

줄바꿈 해서 쓰는법 ( \). \앞에 한칸 띄워야함
curl -XPOST https://korean.visitkorea.or.kr/api/v1/trss/lottery \
-H 'X-SSRP-ID: 230661ea-957a-40cf-8315-6e557ce7a1f7' \
-H 'Content-Type:application/json' \                 
-H 'accept: */*' \                                   
-d '{"tnmId": "1d6c84e2-122d-47e1-aa48-098d3fe615b6"}'

-----

원도우 curl에서는
' → " 로,
" → "" 로 변경하고 써야한다고 함
curl -d "{""key1"":""value1"", ""key2"":""value2""}" \

------------------------------

ps : 커널프로세스 조회
ps -e : 커널프로세스를 포함해서 모든 프로세스를 함께 조회해주는 옵션
ps -f : 풀포맷(모든 정보) 옵션
uid / pid / 부모pid / 최근CPU사용량 / 프로세스 시작 시간 / tty제어 / 경과된 CPU사용량 및 관련 명령

ps -u : 사용자까지 표시(f옵션과 함께 씀)

ex) ps -ef | grep ssh : 현재 프로세스에서 'ssh'문자열이 들어있는거 찾기

-----------------------------

| (파이프라인)

| (파이프라인) 앞 명령어를 파이프라인의 뒤 명령어의 입력값으로 사용할 수 있게 해줌

명령어1 | 명령어2 | 명령어3
명령어1의 출력값을 명령어2의 입력값으로 쓰며
그에 따라 나온 명령어2의 출력값을 명령어3의 입력값으로 쓰고
최종 명령어3의 출력값을 반환한다

가장 자주 사용하는것이
ps -ef | grep [찾을단어] 이다

-----------------------------

` (백틱)

쉘 스크립트에서 백틱(`) 사이의 명령은, 실행되고 난 후 그 결과가 앞에 명령에 입력된다

명령4 `명령1 | 명령2 | 명령3`

-----------------------------

줄바꿔서 쓰기

명령어 사용도중 '를 열고 엔터 누르면
quote> 이런게 생기면서 줄이 바뀜

이후 줄바꾸면서 명령어를 치고 마지막에 '를 닫으면 됨

-----------------------------

awk

유닉스에서 개발된 스크립트 언어로, 텍스트가 저장되어 있는 파일을 "원하는대로 필터링하더나 기타 가공을 통해서 나온 결과를 행과 열로 출력"해주는 프로그램이다

Aho Weinberger Kernighan (개발한사람들의 이름임)

awk 패턴 {액션} 원본데이터


<awk_test_file.txt>
name    phone           birth           sex     score
reakwon 010-1234-1234   1981-01-01      M       100
sim     010-4321-4321   1999-09-09      F       88
nara    010-1010-2020   1993-12-12      M       20
yut     010-2323-2323   1988-10-10      F       59
kim     010-1234-4321   1977-07-17      M       69
nam     010-4321-7890   1996-06-20      M       75


1. 열만 출력하기
awk '{print $1}' ./awk_test_file.txt

$0은 행 전체(모든 컬럼),
$1부터는 첫번째 컬럼, $2 두번째 컬럼.. 이런식

여러 열도 가능
awk '${print $1,$2}' ./awk_test_file.txt


2. 특정 패턴이 포함된 행 출력
awk /rea/ ./awk_test_file.txt


3. 출력의 내용 추가
awk '{print "name: " $1 ", phone: " $2}' awk_test_file.txt

4. 특정 행을 검색하기 - if문
~이상, ~이하의 행 출력

	4-1. ~이상, ~이하의 행 출력
	awk '{if($5>=80) print $0}' awk_test_file.txt

	4-2. 남자인 행 출력
	awk '{if($4=="M") print $0}' awk_test_file.txt

	4-3. 남자이면서 80점 이상인 레코드 출력
	awk '{if($4=="M" && $5>=80) print $0}' awk_test_file.txt


5. 내장 함수
awk에는 여러가지 내장함수들이 있음,
단어의 길이: length
부분단어 추출 : substr

이름과 길이와 이름의 3글자까지 출력
awk '{print "name leng: " length($1), "substr(0,3): " substr($1,0,3)}' awk_test_file.txt


6. 반복문
awk '{for(i=0;i<2;i++) print "for loop: " i "\t" $1, $2, $3}' awk_test_file.txt


7. BEGIN, END 패턴
BEGIN은 awk가 모든 행을 돌기 전에 한번 액션을 수행하고, END는 모든 행을 다 돈 후에 마지막으로 정의한 액션이 수행된다

8. 변수 사용
awk역시 언어이기때문에 변수를 사용할 수 있다
만약 위의 파일에서 총점과 평균을 구하고 싶을때 어떻게 하면 좋을까?
레코드를 돌면서 각각의 점수를 더하면서 총점을 구하고, 총점을 사람의 수로 나누면 된다
그래서 구한 결과는 레코드가 끝난 마지막에 출력하면 되니 아까 이야기했던 END패턴을 앞에 명시해준다.
아래의 awk가 그 명령인데, 여기서 cnt가 -1부터 시작인 이유는 데이터가 아닌 열제목이 존재하기 때문이다

BEGIN{
 sum = 0
 cnt = -1
}

{
 sum += $5
 cnt++
}

END{
 avg = sum / cnt
 print "sum: " sum, "avg: " avg
}' awk_test_file.txt


참고
https://reakwon.tistory.com/163

-----------------------------

이름으로 프로세스 찾아서 중지
kill -9 `ps -ef | grep 프로세스이름 | grep -v grep | awk '{print $2}'`

kill -9 `ps -ef | egrep 'webdriver|chromedriver' | grep -v grep | awk '{print $2}'`

------------------------------

lsof -i : 사용중인 프로세스 확인
lsof -i:[포트번호] : 사용중인 특정 프로세스 확인
kill PID값 [PID값 PID값 ..] : 사용중인 프로세스 제거

톰캣실행하는법 : 톰캣폴더 > bin > 디랙토리들어가서 ./startup.sh

-----

find [찾을시작폴더] -name [파일명] : 폴더 내에서 파일 검색
find [찾을시작폴더] -name "*[파일명]*" : 폴더 내에서 파일 검색(와일드 카드(따옴표 꼭 넣어야됨))
ex) find ./ -name "qqq"

find [찾을시작폴더] -type f : 파일만 찾는 옵션
find [찾을시작폴더] -type d : 폴더만 찾는 옵션

find [찾을시작폴더] -name [파일명] -exec ~~~ {} \; : find로 찾은 파일(들)에 대해 추가 명령을 실행(검색결과가 {}위치에 들어감)
find [찾을시작폴더] -name [파일명] -exec vi {} \; : find로 찾은 파일(들)을 vi편집기로 열기
find [찾을시작폴더] -name [파일명] -exec cat {} \; : find로 찾은 파일(들)을 출력

-----

open . : 현재 있는 위치를 finder(탐색기)로 열기
open .. : 현재 있는 위치 부모폴더를 탐색기로 열기
open / : 루트폴더를 탐색기로 열기
open ~ : 사용자폴더(/users/mac) 탐색기로 열기

특정 프로그램으로 파일 열기
[프로그램명] [파일명]
ex) 서브라임텍스트로 파일 열기
subl jenkins_deploy.py

-----

chsh -s /bin/bash : 기본쉘을 bash로 변환
chsh -s /bin/zsh : 기본쉘을 zsh(z쉘)로 변환

history : 히스토리 보기(계정별로 히스토리가 있다(↑눌렀을때 기록불러올수있는거))
history [n] :
	bash : 최근 n개 보기
	zsh : 앞에서 n번째 부터 보기. history 0 하면 모든 기록이 다나옴
history -i : zsh타임스탬프와 같이 표시
history -p : zsh현재세션 기록삭제
history -c : bash현재세션 기록삭제
rm ~/.zsh_history : zsh기록 전체삭제
rm ~/.bash_history : bash기록 전체삭제

ifconfig : ip주소등 정보 확인
ipconfig getifaddr en0 : 로컬/내부/개인/사설(private) ip
환경설정 → 네트워크에 있는 ip주소 : 로컬/내부/개인/사설(private) ip
curl icanhazip.com : 공인/외부/퍼블릭(public) ip

sudo shutdown -h 시:분 : 지정된 시각에 종료
	ex 오후 1시 종료) shutdown -h 13:00
sudo shutdown -h +분 : 지정된 분 이후에 종료
	ex 5분 뒤 종료) shutdown -h +5
sudo killall shutdown : 예약종료 취소

sudo pmset -c disablesleep 0 : 잠자기모드 활성화(기본값)
sudo pmset -c disablesleep 1 : 잠자기모드 비활성화(맥북덮고 음악듣기)
sudo pmset -g : 잠자기모드 상태 확인
	hibernatemode속성 0: 선잠자기, 1: 깊은잠자기(데스크탑기본값), 3: 안전모드로 잠자기(포터블기본값)
sudo pmset -a hibernatemode 번호 : 모드변경

pmset displaysleepnow : 화면끄기
pmset sleepnow : 절전모드로

defaults write com.apple.finder CreateDesktop 0;killall Finder : 바탕화면에 있는 파일/폴더들 숨기기
defaults write com.apple.finder CreateDesktop 1;killall Finder : 바탕화면 파일/폴더들 다시 나오게 하기

sips -r 15 asdf.jpg : 이미지 시계방향 15도 회전
sips -r -15 asdf.jpg : 이미지 반시계방향 15도 회전
sips -r 23 *.jpg : 여러 이미지 회전

networkQuality : 인터넷 속도측정(업로드속도, 다운로드속도, RPM(높을수록좋음), ms단위 레이턴시)
sips -Z [가로사이즈] [파일명] : 이미지 사이즈 변경

say [문자열] : 문자열을 읽어줌
say [문자열] -o ~/Desktop/test.mp4 : 문자열을 읽어서 mp4로 저장
say -v [보이스종류] [문자열] : 다양한 목소리로 문자열을 읽어줌
Albert / Alice / Alva / Anna / Bad / Bahh / Bells / Boing / Bubbles / Carmit / Cellos / Damayanti / Daniel / ellen
ex)
say -v Kyoko coffeecoffee gogo -o ~/Desktop/test.mp4

jot [숫자] : 연속된 숫자 생성
jot -r [개수] : 랜덤 숫자 n개 생성
jot -w [문자열] [숫자] : '문자열+연속된숫자'
jot -w [문자열] -r [숫자] : '문자열+랜덤숫자'

출력결과 | pbcopy : 출력결과를 바로 복사
ex) jot -w 안녕 3 | pbcopy

pbpaste : 해당자리에 붙여넣기

json문자열 | json_pp : json문자열 예쁘게 바꿔줌
ex) curl https://api.coinone.co.kr/ticker | json_pp
ex) 복사해놓은 json문자열을 예쁘게 출력
pbpaste | json_pp

hidutil : 카라비너를 안쓰고도 키를 바꿀수있음 (카라비너 쓰면 설치가 귀찮고, 반응이 좀 느린 이슈)
ex) hidutil property --set '{"UserKeyMapping": [{"HIDKeyboardModifierMappingSrc":[바꾸기전키], "HIDKeyboardModifierMappingDst":[바뀐이후키]}]}'
재부팅시 초기화 되는데 https://hidutil-generator.netlify.app/ 에서 실행스크립트로 등록 가능함

system_profiler SPPowerDataType : 맥북 빠떼리 상태 조회

sudo su or sudo s-
passwd : 관리자로 로그인 후 비밀번호 변경
루트계정 초기 비밀번호는 아무것도 입력하지않고 enter 누르면 됨

sudo powermetrics --samplers smc |grep -i "CPU die temperature" : CPU온도 측정

-----

nslookup vsup.visitkorea.or.kr : DNS 서버에 질의하여 도메인의 정보를 조회함

-----

윈도우는 c: d: 이런식으로 구분되어있지만 맥은 그런거없음 /(루트) 가 최상위폴더고 그 안에 사용자 폴더가 있음

접속된 유저명 확인 : whoami
logout(또는 exit) : 로그아웃후 이전 계정으로 돌아옴
su -c 'apt-get update' : root권한으로 하나의 명령만 실행

계정을 다른계정으로로 변경(정확히는 추가)하고 현재경로는 유지
sudo su :	루트계정으로 변경	root@macui-MacBookPro mac #
su [사용자명] :	계정 변경

계정을 다른계정으로로 변경(정확히는 추가)하고 해당 계정의 홈디렉토리로 이동
sudo -s :	루트계정으로 변경	root@macui-MacBookPro ~ #
su - [사용자명]: 계정 변경

------------------------------

bat (최신식 cat)

문법 강조(stntax highlight), git 통합, 자동 페이징 등 다양한 기능을 갖고 있음

<설치>
우분투 : sudo apt install bat
OSX : brew install bat

<파일 여러개 출력>
bat 파일명 파일명 : 여러 파일 내용 확인

<행 지정하여 출력>
bat --line-range 13:24 파일명 # 13~24행만 출력
bat --line-range 13: 파일명 # 13행부터 끝까지 출력
bat --line-range :24 파일명 # 1~24행 출력

-----

<언어 하이라이트(구문강조) 색깔 변경>

bat --list-themes

목록중 마음에 드는 하이라이트로 변경하고 싶으면 bat 환경변수에 하이라이트명을 등록해주면 됨
bat --theme 테마명 파일명

만약 파이썬파일(.py)을 구문강조하여 터미널에 표시하고싶다면, 앞에 Python이라고 명시해야한다고 함 → 안해도 되는듯
bat -l Python 파일명

-----

bat은 cat의 업그레이드 판이다

따라서 기존의 cat사용법처럼 와일드카드 문자도 쓸 수 있으며, 입출력 재지정, 파이프 문법 조합 역시 그대로 사용이 가능하다

bat *.py # 와일드카드 사용
bat header.md content.md footer.md > document.md # 입출력 재지정 조합
ls -lah | bat # 파이프 조합

-----

tail 과 bat 명령 조합 (로그 파일 보기)
tail 만 사용하는것 보다 가독성 좋게 로그를 출력한다.

$ tail -f /var/log/nginx/server.log | bat --paging=never -l log


명령어와 옵션이 길어서 치기 힘드면 쉘 스크립트로 만들어 활용하는 것도 좋은 방법이다.

function bat_tail {
    tail -f "$@" | bat --paging=never -l log
}

bat_tail /var/log/nginx/error.log

------------------------------

fd (최신식 find)

기존의 find명령어보다 더 사용자친화적이며, 속도도 거의 8배로 빠르다

기본적으로 검색한 파일들에 대한 색상화 출력을 지원하여 가독성을 높여준다

또한 검색시 .gitignore에 지정한 디렉토리는 자동으로 무시하는 기능도 붙어있다(무시하지 않도록 하는 설정도 가능)

fd는 기본적으로 대소문자를 구분하지 않는다
검색 패턴에 대문자가 포함된 경우 fd 대소문자 구분 모드로 작동되게 된다


<설치>
우분투 : apt install fd-find
OSX : brew install fd

<명령어>
fd 찾을단어

------------------------------

fzf

텍스트를 입력하면 파일을 찾아줌

<설치>
우분투 : sudo apt install fzf
OSX : brew install fzf

설치가 끝났으면
~/.zshrc에도 플러그인을 추가하기
plugins=(
	.
	.
	fzf
)
이후 source ~/.zshrc

그럼 단축키를 사용할 수 있음


<명령어>
실행할명령어 $(fzf)
ex) vi $(fzf)

엔터 치면 인덱싱이 돌아가고
계속 입력해서 빠른 검색이 가능함
선택은 방향키로 선택 후 엔터누르면 됨


<단축키>
ctrl + r : 히스토리 목록 조회, 엔터치면 문자열(명령어)이 반환됨
ctrl + t : 하위 디렉토리/파일 목록 검색, 엔터치면 문자열이 반환됨
esc + c : 하위 디렉토리/파일 목록 검색, 엔터치면 경로가 이동됨
esc : 검색 취소

검색 퍼포먼스가 좋지 않다면 find 보다 더 빠른 fd 설치하기

검색할 경로가 ~/git/visitkorea-front 라면,
givfr 만 입력해도 검색이 됨. 근데 될때가 있고 안될때가 있음.
잘 안되면 fzf 쓰기

------------------------------

exa (최신식 ls)

다양한 파일 포맷과 메타 데이터를 화려하게 색상별로 표시해주며, git과 통합되어 있고 속도도 빠르다
Rust 프로그래밍 언어로 작성되었으며 기존의 ls 명령어에서 사용할 수 없는 몇 가지 추가 기능이 함께 제공됨

<설치>
우분투 20.10버전 미만 : 직접 로컬 파일을 받아서 리눅스OS로 옮겨야함
그이상 : sudo apt install exa
OSX : brew install exa

<기본사용법>
exa -l # ls -l 개선버전
exa -T # 트리구조로 출력
exa -alhT # 이것도 가능
exa -l --git # git status 정보도 함께 표시하는 옵션

<필터링>
exa -I='*.txt' # .txt 로 끝나는 파일을 제외하고 출력
	옵션 풀네임 : --ignore-glob

exa -I='open*|???.xml*case*' # 여러 개의 패턴이 있을 경우 |(파이프)로 여러 패턴을 연결


<아이콘 출력>
아이콘을 출력하고 싶으면 Nerd Font를 따로 설치해야함

리눅스는 아래 명령어 복사 후 shift + insert 하면 붙여넣어짐
$ sudo apt install fontconfig
$ cd ~
$ wget https://github.com/ryanoasis/nerd-fonts/releases/download/v2.1.0/Meslo.zip
$ mkdir -p .local/share/fonts
$ unzip Meslo.zip -d .local/share/fonts
$ cd .local/share/fonts
$ rm *Windows*
$ fc-cache -fv # 폰트 캐시 초기화

OSX는 brew install fontconfig

터미널 껏다킨후 아래 명령어 입력
exa --icons

아이콘 안나오면 nerd 폰트 설치해야함
brew tap homebrew/cask-fonts
brew install --cask font-hack-nerd-font
설치 다 됐으면 터미널 preferences(cmd + ,) 에서 프로파일 → 서체 → Hack Nerd Font 선택

------------------------------

jq

json파일을 예쁘게 보여줌. c언어로 작성됨

1. 파일을 지정해서 출력
$ jq . json파일명

2. 파이프라인으로 다른 프로세스의 출력을 넘겨받아 jq의 입력을 보내는 방법
$ cat json파일명 | jq .

3. json문자열을 입력받아서 출력
$ jq . # jq 실행
$ {"a":"aaa"} # 내용을 직접 입력

4. json파일을 만들어서 출력
$ echo '{"a": "aaa"}' > asd.json
$ jq . asd.json


그 외에도

객체에서 특정 키의 값을 가져오거나 ( jq . json파일명 | jq ".키" )
배열에서 n번째 값을 가져오거나 ( jq . json파일명 | jq ".키[인덱스]" )
다수의 입력과 다수의 출력을 다루거나
다수의 출력을 하나의 배열로 만들거나
배열 내를 순회하며 출력하거나
객체의 key들을 순회하며 출력하거나
객체로 만들거나
쉼표 연산자로 하나의 입력을 나누거나
괄호 연산자로 연산 우선순위를 결정하는 등 가능함

참고: https://www.44bits.io/ko/post/cli_json_processor_jq_basic_syntax

------------------------------

oh-my-zshrc

zsh Configuration을 관리하기 위한 프레임워크
oh-my-zshrc에는 많은 플러그인, 테마가 있어 zsh를 좀더 편하게 사용할 수 있음


1. 경로 자동 추론
cd /u/l/b 입력후 탭누르면
cd /usr/local/bin/ /usr/local/bin이 자동으로 입력됨

2. 타이핑 교정
git abd 이렇게 잘못입력하면
git: 'abd'은(는) 깃 명령이 아닙니다. 'git --help'를 참고하십시오.

가장 비슷한 명령은
	add

위처럼 비슷한 명령이 나옴


3. 명령어 추천
git m 입력하고 탭누르면

merge  -- join two or more development histories together
mv     -- move or rename a file, a directory, or a symlink

위처럼 "git m"으로 시작하는 명령어들을 추천해줌


4. 다양한 플러그인
plugins=(
	git
	zsh-autosuggestions
	yarn
	web-search
	jsontools
	macports
	node
	osx
	sudo
	thor
	docker
	zsh-syntax-highlighting
	mouse
	iterm2
)
다양한 플러그인들을 조합할 수 있음 위처럼 git 과 docker 를 추가할경우 명령어를 자동으로 추천해줌


<설치>
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

설치가 되면 기존에 ~/.zshrc파일에 있던 내용들이
python bat ~/.zshrc.pre-oh-my-zsh 로 이동됨
그것들을 ~/.zshrc파일로 다시 가져와 추가해야함

------------------------------

fasd

사용빈도가 높은 파일 또는 디렉토리 검색을 편하게 해서 생산성을 향상시켜주는 도구
열어본 파일이나 디렉토리를 기억하고 우선순위를 정해서 빠르게 검색할 수 있게 도와줌


<설치>
brew install fasd

설치가 완료되었으면 ~/.zshrc에 plugin 추가
plugins=(
	.
	.
	fasd
)

완료되었으면 source ~/.zshrc


<명령어>
명령어를 이용하기위해서는 디렉토리를 좀 이동하고 열어보고 해서 데이터가 어느정도 쌓여야함

디렉토리를 이동할때
z 검색어
이렇게 일부 검색어를 입력하고 tab을 눌러서 이동하면됨
ex) z py 탭

------------------------------

asdf

asdf-vm은 각종 프로그램(nodejs, ruby, python, …)의 버전을 손쉽게 관리해주는 성의 없어 보이는 이름의 도구입니다.
기존에 nvm, rbenv등 언어, 프로그램별로 달랐던 관리 도구를 하나로 통합해서 사용할 수 있습니다.
homebrew도 일부 버전 관리 기능을 제공하지만 asdf만큼 강력하지 않습니다.

<설치>
$ brew install asdf

------------------------------

gtop

터미널용 시스템 모니터링 도구 명령어

<설치>
$ brew install gtop

$ gtop

------------------------------

dust (최신식 du)

디스크 사용량을 한눈에 파악할수 있게 하는 명령어

<설치>
$ brew install dust

<실행>
$ dust

------------------------------

duf (최신식 df)

마운트된 디스크 파일의 크기와 용량을 다채롭게 보여주는 명령어
사용자 친화적인 다채로운 출력
터미널의 테마 및 너비에 맞게 조정
필요에 따라 정렬
그룹 및 필터 장치
JSON을 편하게 출력

<설치>
$ brew install duf

<실행>
$ duf

------------------------------

procs (최신식 ps)

프로세스 상태 목록을 보여줌

<설치>
$ brew install procs

<실행>
$ proces

------------------------------

gping (최신식 ping)

상대 호스트가 살아있는지 ICMP패킷을 보낼 수 있는 명령어로 graph 제공

<설치>
$ brew install gping

<실행>
$ gping google.co.kr
$ gping google.co.kr facebook.com # 두곳에 동시에 보내기

------------------------------

ripgrep (최신식 grep)

grep보다 훨씬 빠르다고하다
regex 친화적인 검색 (Rust 내장 regex엔진 사용)
buffer 대신 mmap(memory mapped file) 사용

<설치>
brew install ripgrep

<사용법>
파일에서 검색 : rg 검색어 파일명
목록에서 검색 : ls | rg 검색어

------------------------------

delta (최신식 more/less/diff)

기존의 more/less 같은 pager기능과 파일간 변경 사항을 표시하는 diff를 대체하는 커멘드
문법 강조(syntax highlighting) 기능이 있으므로 기존 less 나 diff 에 비해서 변경사항을 알아보기 쉬우며
line number 표시나 side-by-side view 기능 등 편리한 기능을 갖추고 있다

<설치>
$ brew install git-delta
★"deleta" 설치하면 안됨 "git-detla" 임

<실행>
delta 파일1 파일2

-----

<git diff 에 적용>
vi ~/.gitconfig
에서 다음 내용 추가

[pager]
    diff = delta
    log = delta
    reflog = delta
    show = delta

[delta]
    plus-style = "syntax #012800"
    minus-style = "syntax #340001"
    syntax-theme = Monokai Extended
    navigate = true

[interactive]
    diffFilter = delta --color-only

------------------------------

vi 에디터

vim 에디터 실행시마다 들여쓰기 4칸으로 적용하기
~/.vimrc 에 아래 내용 입력 후 저장
set ts=4
set sw=4
set sts=4
set smartindent
set cindent

행번호 표시(영구적용)
set nu

vi note.txt 이렇게 없는 파일을 입력하면 파일이 만들어진다 (먼저 vi명령어로 편집기에 들어간 후 나갈때 wq 파일명 이렇게 해도됨)

vim new_dir/new_file.txt
위처럼와 파일을 동시에 만들때는
저장할때 아래와 같이 입력하면
:!mkdir -p %:h
아래와 같은 경고가 나오는데
[No write since last change]
:wq 입력해 빠져나오면 됨

명령 모드 : vi를 실행시키면 가장 먼저 접하는 기본이 되는 모드로 커서의 이동, 수정, 삭제, 복사 붙이기, 탐색 등을 한다.
	입력 모드 전환키인 i,a,o,I,A,O 등을 입력하면 입력 모드로 전환되고, 
	명령 모드로 다시 전환하려면 [Esc] 키를 누르면 된다.
입력 모드 : 입력 모드 이외에도 편집 모드, input mode, insert mode 등으로 불리며, 글자를 입력하는 문서를 만드는 모드이다.
	명령 모드에서 입력 전환키를 눌러서 전환하면 화면 아래에 '-- INSERT --'라고 표시된다. 
마지막 행 모드 : 명령 모드에서 ':'키를 입력했을 때 화면 맨 아랫줄에서 :______ 명령을 수행하는 모드로
	저장, 종료, 탐색, 치환 및 vi 환경 설정 등의 역할을 하는 모드이다.

i : 편집모드 진입
o : end+enter로 줄바꿈후 편집모드 진입
s : 커서위치 글자를 지우고 편집모드 진입
cw : 커서포함 단어끝까지 지우고 편집모드 진입
C : 커서포함 행끝까지 지우고 편집모드 진입
S : 커서행을 지우고 편집모드 진입
r + 문자 : 커서위치 글자를 편집모드 진입하지않고 다른 글자로 바꾸기
a : 한칸 오른쪽으로 이동 후 편집모드 진입
esc : 명령모드 전환
: 키 입력 : ex 명령 모드로 전환

shift + 방향키 : 단어 건너뛰기
ctrl + 방향키 : 문장 건너뛰기
e : 단어의 끝으로 커서 이동
w : 다음 단어의 시작으로 커서 이동
b : 단어의 시작으로 커서 이동
enter : 다음 행의 시작으로 커서 이동
^ : 행의 시작으로 커서 이동
$ : 행의 끝으로 커서 이동
H : 화면의 맨 위로 커서 이동
M : 화면의 중간으로 이동
L : 화면의 맨 밑으로 이동


- 종료 및 저장
:w : 저장
:q : 종료 (변경사항이 있을시 오류메시지 반환됨)
:q! : 저장안하고 강제종료 (!q가 아님)
:e! : 수정한 것을 무시하고 새로고침
:wq, :zz : 저장하고 종료
:wq! : 저장하고 강제종료
:wq [파일이름] : 파일이름 지정해서 저장 후 닫기
:wq! [파일이름] : 파일이름 지정해서 저장 후 닫기


- 커서/화면 이동
h/j/k/l : 좌/하/상/우 커서 이동 (방향키가 없는 키보드에서 씀)
^ : 행 처음으로 이동
$ : 행 끝으로 이동
w : 다음 단어의 첫글자로 이동
b : 이전 단어의 첫글자로 이동
{ : 문단 시작으로 이동
} : 문단 끝으로 이동
gg, [[ : 첫 행으로 가기
G, :$, ]] : 마지막 행으로 가기
:set number : 행번호 표시
:숫자 : 지정한 숫자 행으로 이동
숫자gg : 지정한 숫자 행으로 이동
숫자G : 지정한 숫자 행으로 이동
ctrl + g : 현재파일의 이름과 커서의 행 정보
# : 이전 같은 단어로 이동
* : 다음 같은 단어로 이동
% : 짝 괄호로 이동
/검색어 : 검색
검색후 n : 다음 검색
ctrl + y : 화면을 한줄 위로 이동
ctrl + e : 화면을 한줄 아래로 이동
ctrl + u : 화면을 반 화면 위로 이동
ctrl + d : 화면을 반 화면 아래로 이동
ctrl + b : 화면을 한 화면 위로 이동 (= PageUp)
ctrl + f : 화면을 한 화면 아래로 이동 (= PageDown)


- 잘라내기
x : 커서에 있는 글자 잘라내기
X : 커서 앞에 있는 글자 잘라내기
dw : 커서포함 단어 끝까지 잘라내기(마지막공백까지)
de : 커서포함 단어 끝까지 잘라내기
db : 커서미포함 단어 왼쪽까지 잘라내기
D : 커서 포함 행끝까지 잘라내기
dd : 한줄 잘라내기
숫자dw, 숫자db, 숫자dd 혹은
d숫자w, d숫자b, d숫자d 이렇게 해서 잘라낼 개수를 지정 가능
ggdG : 첫번째 줄로 이동 후 모두 잘라내기


- 복사
yw : 커서 뒤에 있는 단어 복사(커서 포함)
yb : 커서 앞에 있는 단어 복사
yy : 커서가 있는 줄 복사
yw, yb, yy 명령 앞에도 복사할 숫자를 지정 가능 ex) 3yw, 2yb, 4yy

ctrl + q, v : 비주얼 모드로 전환. d / y 눌러서 복사 / 잘라내기 가능. esc로 빠져나오기 가능
ctrl키와 같이 누르면 끝까지 드래그 가능

V : 비주얼 라인 모드


- 붙여넣기(복사/삭제된 내용을 붙여넣기 가능)
p : 커서 오른쪽에 붙여넣기
P, . : 커서 이전에 붙여넣기


- 찾기
/문자열 : 앞에서부터 문자열을 검색
?문자열 : 뒤에서부터 문자열을 검색
n : 뒤로 검색
N : 앞으로 검색


- 바꾸기
:%s/old/new : 각 행의 처음 나오는 old를 찾아 new로 바꾼다.
:%s/old/new/g : 모든 old를 찾아 new로 바꾼다.
:%s/old/new/gc : 모든 old를 찾아 new로 바꾸기 전에 물어본다.


- 실행취소, 재실행
u : 실행취소
ctrl + r : 재실행


- 기타
:set nu : 행번호를 출력 (= :set number)
:set nonu: 행번호를 숨긴다. (= :set nonumber)
:cd: 현재 디렉토리를 출력
r + Enter : 행 분리. 커서에있던 글자는 사라짐
xp : 커서 위치와 오른쪽 문자 교환
~ : 커서에 있는 문자 대소문자 변경
:new 파일경로, :sp 파일경로 : 세로로 화면이 분할되어 기존 파일과 새로 불러온 파일 2개를 동시에 볼 수 있음
:vs 파일경로 : 가로로 화면이 분할되어 기존 파일과 새로 불러온 파일 2개를 동시에 볼 수 있음
ctrl + w w : 분할된 창 간 이동
:q : 분할된 창에서 실행하면 닫아짐

-----

나노 에디터

설치 안돼있으면 아래 명령어로 설치
$ sudo yum install nano

도움말 : ctrl + g
잘라내기 : ctrl + k
붙여넣기 : ctrl + u
찾기 : ctrl + w
저장 : ctrl + o , enter

-----

터미널 매크로 등록하는법
vi ~/.zshrc → alias ll="ls -alh" 이런식으로 입력 → ese 누른후 :!wq → enter
하고 터미널 껏다키면 됨

zsh 말고 bash에서 매크로 등록
~/.profile 에서 똑같이 alias로 하면 됨. 없으면 파일 만들기

전체유저에개 등록하려면 /etc 폴더 안에다 하기

★별칭으로 프로그램 실행시 permission denied이 발생할 경우
시스템 환결설정 → 보안 및 개인 정보 보호 → 전체 디스크 접근 권한 → 터미널app 체크

-----

터미널을 켜면 프로그램 자동 실행시키기
python3 schedule/works_in.py &
python3 schedule/works_out.py &
python3 schedule/report.py &
python3 schedule/p2p.py &

참고로 뒤에 &를 붙이는 이유는 백그라운드에서 명령을 수행하기 위함. 해당 명령의 출력을 볼 수 는 없으니 주의

-----

zsh/bash에서 폴더/파일 색깔 바꾸기
매크로 등록했던 파일에서

export TERM=xterm-color
export CLICOLOR=1
export LSCOLORS=GxFxCxDxBxegedabagaced
export GREP_OPTIONS='--color=auto'
alias ls='ls -GFh'
alias ll='ls -lah'ex

-----

~/.bashrc 등의 스크립트 파일은 수정후 저장하여도 수정한 내용이 바로 적용되지 않는데
그 이유는 ~/.bashrc 파일은 유저가 로그인 할 때 읽어들이는 파일이여서, 로그아웃 후 로그인하거나 리눅스를 재시작해야 적용이된다
재로그인을 하지 않고도 적용 시키는 명령어

source [환경 설정 파일명]

-----

VirtualBox가상머신 CLI에서 키보드로 빠져나가는법

1. cmd를 한번 누른다
2. cmd + tab을 누른다

----------------------------------------------------------------------------------------------------

Ubuntu(리눅스 우분투)

------------------------------

사설 ip 확인

$ ip a
or
$ ip addr
inet 뒤에 나오는 IP주소가 사설 IP주소

------------------------------

포트를 사용하고있는 서비스 정보 조회

$ ss -tln | grep :포트번호

톰캣이 실행중인 상태라면 아래처럼 뜰탠데
LISTEN 0      100                     *:8080            *:*
여기서 LISTEN 은 포트가 현재 열려있고, 해당 포트로 들어오는 연결을 기다리고 있다는 것을 의미함

------------------------------

방화벽 설정 조회

$ sudo ufw status

-----

방화벽이 활성화 되어있는경우 출력되는 내용

Status: active

To                         Action      From
--                         ------      ----
22                         ALLOW       Anywhere
80                         ALLOW       Anywhere
443                        ALLOW       Anywhere

위 예시에서는 22(SSH), 80(HTTP), 443(HTTPS)에 대한 허용 규칙이 설정되어 있음을 알 수 있음

-----

방화벽이 비활성화 되어있는경우 출력되는 내용

Status: inactive

-----

방화벽을 활성화 하는 명령어

$ sudo ufw enable

-----

방화벽을 추가하는 명령어

ex)
$ sudo ufw allow 8080

------------------------------

-hollywood (시각적 연출)

$ sudo apt-add-repository ppa:hollywood/ppa
$ sudo apt-get update
$ sudo apt-get install byobu hollywood

$ hollywood


- sl (증기 기관차)

$ sudo apt-get install sl

$ sl

----------------------------------------------------------------------------------------------------

맥에서 사진 크기 조절

미리보기.app으로 열고 오른쪽위에 연필모양동그라미 버튼 클릭 → 크기조절아이콘 클릭 → 원하는 크기로 조절(★이미지 리샘플 체크 해제하기)

------------------------------

사진 용량 조절

사진파일 우클릭 → 빠른 동작 → 이미지 변환

포맷 및 용량 변경 가능

----------------------------------------------------------------------------------------------------

맥에서 사진 회전

'미리보기' 말고 '사진' 앱으로 열어서
편집 → 자르기 → 수평 맞추기 로 조절 가능

----------------------------------------------------------------------------------------------------

맥에서 동영상 회전

파인더로 영상이 있는 경로로 이동

파일 클릭하면 '왼쪽으로 회전' 이 있음

----------------------------------------------------------------------------------------------------

맥에서 프린터검색 안되면 와이파이를 껏다키기

----------------------------------------------------------------------------------------------------

ssh키 생성

1. 터미널 들어가서
$ ssh-keygen
입력후 엔터 엔터 엔터

2. 파일 확인
$ sudo cat ~/.ssh/id_rsa.pub

3. 전체 복사 후 필요한 곳에서 쓰기

4. 삭제 시
cd ~/.ssh
rm -rf ./*

----------------------------------------------------------------------------------------------------

jsp페이지 자동 저장 / 톰캣 자동반영시 cmd + tab 눌렀을떄 로딩바가 사라져야 반영이 된것

----------------------------------------------------------------------------------------------------

맥에서 아이폰 테스트 (사파리만 써도 비슷하게 되는듯)


앱스토어에서 Xcode 설치

Xcode 실행 후 약관 동의

터미널 열고 아래 명령어 입력
open -a simulator

----------------------------------------------------------------------------------------------------

맥 기본 오디오 녹음 / 동영상 녹화 프로그램

QuickTime Player


내장 소리를 녹음하려면 BlackHole 2ch 를 깔아야함
이후 내장프로그램인 오디오MIDI 설정에서 다중출력설정을 해야함(인터넷 참고)

-----

MP3 커터 사이트

https://mp3cut.net/ko/

----------------------------------------------------------------------------------------------------

터미널에서 파일경로에 띄어쓰기가 있으면 escape를 붙여서 '\ ' 로 써야함

ex) 터미널에서 iClude Drive로 이동
cd ~/Library/Mobile\ Documents/com~apple~CloudDocs/

----------------------------------------------------------------------------------------------------

로컬호스트 휴대폰으로 접속하는 방법

ifconfig로 사설ip 주소 확인 (ex. 192.168.0.205)

로컬호스트 서버를 띄워놓고,
아까 찾은 ip에 포트번호 붙여서 접속 (ex. 192.168.0.2105:5500/~~.html)

맥의 방화벽은 기본적으로 꺼져있음. 윈도우는 따로 설정 필요

----------------------------------------------------------------------------------------------------

맥 알림 안나올때

알림 → 알림 센터 → 디스플레이를 미러링하거나 공유할 때 알림 허용

알림 → 응용프로그램 알림 → 알림을 받을 앱 클릭 → 없음/배너/알림 중 알림 선택

2가지 다 해보기

----------------------------------------------------------------------------------------------------

postman 요청할때 URI의 같은 부분을 환경변수로 설정해놓고, 환경만 선택해서 쓸 수 있음


Environments → 추가버튼(Create new environment)

Variable : 변수로 쓸 문자열
Initial value : URI 공통문자열
Current value : URI 공통문자열

이렇게 넣고

쓸때는 아래와 같이 쓰면 되는데, 오른쪽 위에 환경을 설정할 수 있는 셀렉트박스가 있음. 원하는 환경으로 바꾸기

{{변수}}dashboard/home-exposed


위처럼 하면

로컬
	요청1
dev서버
	요청1
stg서버
	요청1

이렇게 같은 요청을 3개씩 만들 필요가 없어짐. 요청할때 환경만 바꾸면 됨

----------------------------------------------------------------------------------------------------




























