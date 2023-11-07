깃에서 HEAD(헤드)는 현재 작업 위치를 말함. 작업 트리에 변화를 주는 git 명령은 대부분 HEAD를 변경하는 것으로 시작함


git bash 명령어

cd 이동할 하위 디렉토리명 : 디렉토리 이동
git rm -r 삭제할 디렉토리명 : 디렉토리 삭제
dir : 디렉토리 목록 조회
ls : 디렉토리 목록 조회
cat 파일명 : 파일 내용 조회

<깃허브 계정정보 세팅>
git config [--global] user.name "이름"					: 리모트 저장소에 github 사용자 정보 세팅
git config [--global] user.email "이메일"				: 리모트 저장소에 github 사용자 정보 세팅
git config --list										: 사용자 정보 조회

<로컬에 프로젝트 clone>
git clone [자신의 원격저장소 주소]						: 로컬에 clone
ex) cd로 폴더를 만들 경로로 이동한 후 git clone https://gitlab.uniess.co.kr/visitkorea/visitkorea-tourapi-batch.git

<리모트 저장소 연결>
git init											: 로컬 디렉토리를 Git 저장소로 만듦 (git폴더를 생성함)
git remote add [새 원격브랜치명] [자신의 원격저장소 주소]	: 리모트 저장소에 github 원격 저장소 연결정보 추가
git config -l (or --list)								: Git 저장소 각종 정보 조회
git remote show [원격브랜치명]						: 리모트 저장소 연결정보 조회
git config --get romote.[원격브랜치명].url				: 리모트 저장소 연결정보 url만 조회
git remote set-url [원격브랜치명] [새 url]				: 리모트 저장소 연결정보 url 수정
git remote -v										: 리모트 저장소 연결조회
git remote rename [기존 저장소 이름] [변경할 저장소 이름]	: 리모트 저장소 이름 변경
git remote rm [삭제할 저장소 이름]						: 리모트 저장소 삭제
git push [리모트 저장소 이름] --delete [삭제할 브랜치 이름]	: 리모트 브랜치 삭제


<체크아웃, head 이동>
git checkout 브랜치명								: 로컬브랜치가 있는 위치로 이동
git checkout -f 브랜치명								: 충돌이 났을때 변경사항을 버리고 이동함(스태시를 이용하면 안버리고 이동후 충돌병합 가능)
git checkout origin/브랜치명							: 원격브랜치가 있는 위치로 이동
git checkout -b 브랜치명								: 브랜치를 복사하고 체크아웃까지 함
git checkout 커밋ID									: 지정한 위치로 이동
git checkout head									: 현재 헤드 위치 확인
git checkout head^	^^								: 개수만큼 이전 커밋으로 이동
git checkout head~5								: 개수만큼 이전 커밋으로 이동
git checkout -										: 한단계 최근 위치으로 이동


<커밋 이력 조회>
git log											: 현재위치(head)의 커밋기록부터 과거 커밋기록 조회. 커밋ID/작성자/날짜/커밋메시지
												아직 푸쉬하지 않은것도 포함, 스태시에 있는것도 포함
<옵션>
	-p											: 커밋한 파일 변경내용 보기
	--grep='검색어'								: 커밋메시지로 검색기능
	--graph										: 트리를 보기 편하게 그래프로 보여줌
	--all											: 현재 브랜치와 연결된 모든 브랜치 커밋 이력 조회
	--since=yyyy-mm-dd --until=yyyy-mm-dd			: 날짜사이 검색
	파일경로(src/~)								: 파일로 검색
	--author ='사용자ID'							: 작성자 검색
	--oneline										: 커밋ID/커밋메시지 만 조회 (작성자/날짜는 제외)
	--shortlog									: 저장소에 참여한 모든 사용자가 만들어낸 커밋횟수/커밋메시지를 사용자명 오름차순으로 정렬해 출력
	--shortlog -n									: 저장소에 참여한 모든 사용자가 만들어낸 커밋횟수/커밋메시지를 커밋횟수 내림차순으로 정렬해 출력
	--shortlog -s									: 커밋횟수, 사용자명만 출력
	--shortlog -e									: 사용자명 뒤에 이메일 표시
	--shortlog -n -s -e								: 옵션들 한꺼번에 적용 가능. 커밋횟수/사용자명/이메일을 커밋횟수 내림차순으로 출력

git show											: 현재위치(head)의 커밋 내용 조회. 커밋ID/작성자/수정파일목록/수정내용
git show 커밋ID									: 원하는 커밋의 내용 조회
git show head^^^									: 현재위치(head)의 3개 전
git show head~5									: 현재위치(head)의 5개 전
git show head~3^^								: 현재위치(head)의 5개 전(혼합 사용 가능)
git show head^^~3								: 현재위치(head)의 5개 전(혼합 사용 가능)


<커밋/리셋 이력 조회>
git reflog											: 모든 commit, ★reset 등 이력 조회


<삭제한 브랜치 복구>
git reflog로 먼저 조회 후 원하는 시점의 HEAD@{번호} 복사
git checkout -b '새로만들브랜치명' HEAD@{번호}


<워킹디렉토리 & 스테이지 / 트리의 상태 조회>
git status											: 워킹디렉토리 파일 목록("커밋하도록 정하지 않은 변경사항(add하기 전,빨간색)") &
												스테이지 파일 목록("커밋할 변경 사항(add한 이후 초록색)") /
												트리의 상태정보(갈라짐유무 / 원격브랜치 시점 / 헤드 시점) 조회


<워킹디렉토리(add하기 전)에 있는 파일 / 커밋내역끼리 비교>
git diff											: 워킹디렉토리(add전)에 있는 파일들 수정내용 조회
	d		: pageDown
	u		: pageUp
	g or <	: home
	/검색어	: 찾기
	h		: 도움말
	q		: 나가기
git diff --staged									: 스테이지(add후)에 있는 파일들의 변경내역

git diff '버전id(기준)' '버전id2(바뀐버전)'				: 커밋내역간의 차이 비교. 거리가 한칸일때의 비교는 git show와 동일하고, 2칸이상 비교할때 씀


<스테이지 추가>
git add .											: 워킹디렉토리 → 스테이징영역으로 옮김 (COMMIT 이전에 수행해야함)


<스테이지 리셋>
git restore 파일경로(src/~)							: 워킹디렉토리에 있는 파일을 초기화함
git restore . 										: 워킹디렉토리에 있는 파일들을 모두 초기화함
git restore --stage 파일경로(src/~)						: 스테이지에 올라가 있는 파일을 내림
git restore --stage .									: 스테이지에 올라가있는 파일들을 모두 내림


<커밋 / 푸쉬>
git commit										: 변경사항 저장 (COMMIT) 커밋메시지를 입력후 wq로나오면 저장됨
git commit -m '커밋메시지'							: 커밋시 들어가서 메시지입력후 wq로 안나오고 바로 커밋가능
git commit --amend								: 직전 커밋을 고쳐서 커밋함, 스테이지에 올라가있는것들이 있으면 같이 합쳐서 커밋함
GIT_COMMITTER_DATE='Sun 1 Mar 2021 20:11:22 KST' git commit --amend --no-edit
												: 커밋 날짜 수정
git push [원격 저장소 이름] [로컬 브랜치 이름]				: 로컬저장소→원격저장소 변경사항 올리기
git push origin feature/travelPlaylist -f					: 강제 푸쉬는 뒤에 -f 붙이기. (확인하려면 소스트리 새로고침(ctrl+r)하기)
git push origin develop -f
설명 - 원격저장소 브랜치를 로컬브랜치로 강제로 옮김(소스트리에서 원격브랜치가 로컬브랜치보다 위에있을때 push하려고 하면
현재 브랜치의 끝이 리모트 브랜치보다 뒤에 있으므로 업데이트가 거부되었습니다. 푸시하기 전에 ('git pull ...' 등 명령으로) 리모트..
위같은 메시지가 나오면서 안되는데
터미널에서 이 force 명령어로 push를 하면 원격브랜치를 강제로 덮기 가능. 되도록 혼자작업하는 브랜치에서만 쓰기)
★브랜치의 강제 푸쉬를 막을 수 있는 설정이 있는데 이게 설정되어있으면 아래처럼 나오면서 강제푸쉬가 안됨
You are not allowed to force push code to a protected branch on this project.
이걸 푸는 방법은 깃랩기준으로
프로젝트 메뉴 → Settings → Repository → Protected branches → Expand → Unprotect 누르면 됨

push의 -u 옵션
git push -u origin master
-u 옵션을 넣어주면 앞으로 master라는 브랜치를 자동으로 origin이라는 원격저장소의 master 브랜치로 연결해
간단히 git push 만 입력하여 반영하거나
git pull 입력시 origin이라는 원격저장소의 master브랜치를 로컬 저장소의 master브랜치로 merge할 수 있게 해주겠다는 의미
따라서 간단히 아래와 같은 식으로 원격저장소와 로컬 저장소를 자동 연결하여 쓸 수 있음. (.git폴더의 config파일에 옵션이 저장됨)
git push
git pull


<풀>
git fetch											: 원격 저장소의 최신 정보를 가져옴
git pull [원격 저장소명] [원격 브랜치]					: 원격 저장소 변경사항을 불러와 로컬브랜치 변경사항과 합침.

pull은 내부적으로 fetch + merge인데,
fetch는 원격 저장소에 올라온 최신 변경사항을 가져오는것이고
merge는 가져온 원격 브랜치 변경사항을 로컬 브랜치로 합치는 작업임
git pull은 git fetch + git merge origin/develop 이렇게 하는것과 동일함


<병합>
git merge [끌려갈 브랜치]							: 끌어올 시점으로 체크아웃된 상태에서 병합
git merge [끌려갈 브랜치] --no-edit					: 병합시 커밋 메시지 기본으로 설정
git merge --abort									: 병합하다가 충돌났을때 병합을 취소가능(git merge명령어를 치기 전으로 돌아감)
git merge [끌려갈 브랜치] --squash						: 병합커밋이 아닌 브랜치의 커밋들을 하나로 합쳐서 새로운 커밋을 따로 만듬(연결선이 안만들어짐)


<재배치>
하기 전에 워킹디렉토리&스테이지가 비어있어야함
git rebase [현재브랜치를 갖다 붙일 기존 브랜치]			: 현재 브랜치를 기존의 다른 브랜치에 새로 붙임
git rebase --continue								: (충돌난경우) 처리하고 add 후 commit 대신 씀
git rebase --abort									: (충돌난경우) 재배치를 취소함
git rebase -i head^ or ~n							: 편집할 개수를 정함

그럼 vi편집창이 띄워지고 커밋이 역순으로 나오는데..

커밋들을 하나의 커밋으로 통합하려면 마지막에 있는 항목(제일 최근 커밋임)에 pick이라고 써있는걸 squash로 바꾸고 저장후닫기
이후 커밋메시지를 수정할 수 있음. 그대로 저장후닫기하면 커밋메시지가 합쳐져서 여러줄로 나옴

n번째 커밋을 수정을 하려면 처음에 명령어 입력시 head~n 으로 하고,  첫번째 항목(제일 마지막 커밋임)에 pick이라고 써있는걸 edit로 바꾸고 저장후닫기
이후 파일수정을 하고, add, commit --amend -m 커밋메시지 를 함. --amend옵션 안넣으면 커밋 수정이 아닌 커밋이 하나 더 생겨버림.
마지막으로 rebase --continue를 하면 되는데 그럼 이후 커밋들과 병합이 됨.
만약 이때 충돌이 나면 다시 파일수정을 하고, add, 다시 rebase --continue 를 한다음 편집커밋 바로이후커밋의 커밋메시지를 수정할수 있는데 수정할거면 수정하기

rebase로 수정한것도 git reset --hard ORIG_HEAD 로 되돌리기 가능


<커밋 되돌리기>
git revert head									: 가장 최근 커밋 되돌리기
git revert 커밋ID									: 특정 커밋 되돌리기
git revert 머지커밋ID -m 인덱스						: 머지 커밋 되돌리기
												  git show에서 보여지는 Merge: 뒤에 순번이 1,2 로 붙음. 어느쪽 커밋으로 되돌릴지 정해야함

<커밋 초기화>
git reset											: 스테이지에 올라가 있는 내용들 모두 내림(git restore --stage . 와 동일)
git reset --hard									: 워킹디렉토리/스테이지 모두 초기화(git restore --stage . & git restore . 와 동일)

git reset --hard/mixed/soft HEAD@{헤드숫자}			: 조회된 헤드숫자를 확인하여 해당 시점으로 초기화
												hard 옵션 : 되돌리고, 변경했던 파일들을 작업트리에서도 지움
												mixed 옵션 : 되돌리고, 변경했던 파일들은 워킹디렉토리로 보냄 (옵션을 안넣을경우 mixed가 기본값)
												soft 옵션 : 되돌리고, 변경했던 파일들은 스테이지로 보냄

git reset --hard head^								: 1단계 전으로 강력 초기화
git reset --mixed head~3							: 3단계 전으로 믹스 초기화
git reset --soft 커밋ID								: 특정 커밋으로 소프트 초기화

git reset --hard ORIG_HEAD							: reset/pull/push/commit/merge를 하기 직전으로 되돌림(hard리셋했던것도 복구 가능)
												연속으로 명령어를 입력하면 git reset --hard ORIG_HEAD 가 다시 취소됨


<브랜치>
git branch										: 로컬 브랜치 확인
git branch -r										: 원격 브랜치 확인
git branch -a										: 로컬 브랜치 & 원격 브랜치 확인
git branch 브랜치명									: 현재 체크아웃된 브랜치 복사 (복사&체크아웃은 git checkout -b 브랜치명)
git branch -c 원본브랜치명 복사할브랜치명				: 원하는 브랜치 복사
git branch -d 브랜치명								: 브랜치 삭제(병합된 브랜치일때만)
git branch -D 브랜치명								: 브랜치 삭제(병합하지 않았더라도)


<스태시>
git stash											: 현재 작업을 스태시에 추가. 워킹디렉토리/스테이지 모두 저장
git stash -m 제목									: 스태시저장시 메시지(제목) 입력가능
git stash list										: 스태시 목록
git stash show										: 가장 최근 스태시의 파일목록 조회
git stash show -p									: 가장 최근 스태시의 파일별 변경사항 조회
git stash show -p | git apply -R						: 스태시 적용했던거 되돌리기 (바로 안되돌아가고 뭔가 스테이지 이동을 해야 돌아가는 오류가 있음)
git stash apply										: 가장 최근 스태시 적용. 모든 파일이 워킹 디렉토리로 감). 스태시는 제거되지 않음
git stash apply	 --index								: 가장 최근 스태시 적용. 스태시했을때의 워킹디렉토리/스테이지 유지. 스태시는 제거되지 않음
git stash pop										: 가장 최근 스태시 적용 후 삭제
git stash pop stash@{숫자}							: 원하는 스태시 꺼내기
git stash drop										: 가장 최근 스태시 삭제
git stash drop stash@{숫자}							: 원하는 스태시 삭제
git stash clear										: 스태시 전체 삭제


<태그>
git tag											: 태그 목록 조회
git tag -n											: 태그 목록 조회(상세정보 포함)
git tag -n 태그명									: 태그 조회(상세정보 포함)
git tag 태그명										: 현재 시점에 태그를 붙임. 태그로 간편하게 checkout / reset 가능
git tag -a 태그명									: 태그에 주석을 붙임(Annotated tag)
git tag 태그명 -am 메시지							: 주석메시지 바로 입력 가능
git tag -d 태그명									: 태그 삭제


<체리픽>
git cherry-pick 커밋ID								: 다른브랜치의 커밋 1개 복사해서 워킹디렉토리로 갖고오거나 바로 커밋할 수 있음


<Access Token Settings>
git remote set-url origin https://[APPLICATION]:[NEW 
TOKEN]@github.com/[ORGANISATION]/[REPO].git		: 깃 clone은 받아져 있는 상태 - token이 만료되었을때 토큰 정보만 업데이트


<추적 방지 파일 설정> (스테이지에 올라가지 않은상태의 특정 파일을 숨김)
git update-index --skip-worktree 파일경로(절대경로(cmd + shift + c) or src/~ 경로)
git update-index --assume-unchanged 파일경로 (이 방법도 가능)

<추적 방지 파일 해제>
git update-index --no-skip-worktree 파일경로(절대경로(cmd + shift + c) or src/~ 경로)
git update-index --no-assume-unchanged 파일경로 (이 방법도 가능)


<추적 방지 파일 목록>
git ls-files -v | grep ^S (skip-worktree로 한 경우. 대문자S)
git ls-files -v | grep ^h (assume으로 한 경우. 소문자h)

-----

터미널로 원격저장소에 접근시
remote repo의 주소가 ssl로 되어있으면 상관없지만, https로 되어있는경우에는
clone, push, pull 등 동작마다 remote repo에 접근하기 위한 로그인 정보를 입력해 주어야 한다.
이 과정을 생략하는 방법


방법1. 쉽지만 위험한 방법
remote repo 주소 자체에 접속정보를 직접 넣는 방법

아래와 같이 하면 별도로 접속 정보를 입력하지 않아도 된다고 함
git clone https://<ID>:<PASSWORD>@myrepo.github.com/coolproject.git


방법2. 안전하고 공식적인 방법
git에서 제공하는 credential 이라는 기능 이용
이 기능을 사용하면 로그인 정보를 저장해 두었다가 다시 입력하지 않아도 사용할 수 있게 해 준다. 크게 cache와 store 두 가지 방법이 있다


방법 2-1
만약 id와 password를 짧은 시간 동안 반복적으로 입력하는 일을 피하고 싶다면 credential.helper를 cache로 설정할 수 있다.
git config --global credential.helper cache

이렇게 하면 ID와 PASSWORD 같은 인증정보를 Disk에 저장하지는 않고 메모리에서 15분 까지만 유지한다. 한 번 입력된 인증 정보는 15분 동안 다시 묻지 않는다.

시간을 연장하려면 다음과 같은 옵션을 붙인다
git config credential.helper 'cache --timeout=300'


방법2-2
사용자이름과 암호 같은 인증정보를 Disk에 저장하고 계속 유지하고 싶을 때도 있다.
이 때는 credential.helper를 store로 지정한다.

아래와 같이 옵션을 수정해 주면 한 번 로그인 된 정보는 자동으로 저장되어 다음부터 묻지 않는다. 로그인 정보는 ~/.git-credentials에 저장되게 된다.
git config --global credential.helper store


방법2-2 선택사항
credential.helper를 store로 지정했을 때의 문제는 파일에 로그인 정보가 그대로 저장된다는 점이다
이를 좀 더 안전하게 사용하려면 OS 자체에서 지원한는 Keychain 시스템을 이용하면 된다.
mac이나 windows에는 OS 자체에서 제공하는 Keychain 시스템이 있다. git credential 정보를 이곳에 저장할 수 있다.

store로 설정한상태에서 아래 명령어 추가로 입력
git config --global credential.helper wincred

이 정보는 windows의 “자격 증명 관리자(Credential Manager)”에서 확인할 수 있다.
만약 remote repo의 비밀번호를 수정하였다면 이 “자격 증명 관리자”에서 해당 정보를 삭제해 주어야 한다.

<계정 설정 상태 확인>
git config --list
git config --global --list

credential.helper=cache 가 있으면 cache로 설정되어있는것이고,
credential.helper=store 가 있으면 store로 설정되어있는것이고,
credential.helper=wincred 가 있으면 store + wincred로 설정된것.


<로컬에 저장되어있는 계정 정보 삭제>
git config --global --unset credential.helper
git config --system --unset credential.helper

----------------------------------------------------------------------------------------------------

깃허브/깃랩 클론

방법1. 이클립스 import git → 소스트리 불러오기
방법2. 소스트리 new → 이클립스 Projects from Folder or Archive
방법3. 저장할 폴더 cd로 들어가서 git clone 저장소주소 → 이클립스 Projects from Folder or Archive → 소스트리 불러오기

----------------------------------------------------------------------------------------------------

브랜치

독립적으로 어떤 작업을 진행하기 위한 개념.
필요에 의해 만들어지는 각각의 브랜치는 다른 브랜치의 영향을 받지 않기 때문에, 여러 작업을 동시에 진행할 수 있음(릴리스 버전 이력 / 기능 추가 이력 / 버그 수정 이력)

여러명이서 동시에 작업을 할 때 다른 사람의 작업에 영향을 주거나 받지 않도록, 먼저 메인 브랜치에서 자신의 작업 전용 브랜치를 만듦.
그리고 각자 작업을 진행한 후, 작업이 끝난 사람은 메인 브랜치에 자신의 브랜치의 변경 사항을 적용함.
이렇게 함으로써 다른 사람의 작업에 영향을 받지 않고 독립적으로 특정 작업을 수행하고 그 결과를 하나로 모아 나가게 됨.
이런 방식으로 작업할 경우 '작업 단위', 즉 브랜치로 그 작업의 기록을 중간 중간에 남기게 되므로 문제가 발생했을 경우
원인이 되는 작업을 찾아내거나 그에 따른 대책을 세우기 쉬워짐

통합 브랜치
언제든지 배포할 수 있는 버전을 만들 수 있어야 하는 브랜치.
그렇기 떄문에 늘 안정적인 상태를 유지하는것이 중요한데, 여기서 '안정적인 상태'란 현재 작업중인 소스코드가 모바일에서 동작하는 어플리케이션을 개발하기 위한 것이라면,
'그 어플리케이션의 모든 기능이 정상적으로 동작하는 상태'를 의미함
일반적으로 저장소를 처음 만들었을때 생기는 'master'브랜치를 통합 브랜치로 사용함

토픽 브랜치
기능 추가나 버그 수정과 같은 단위 작업을 위한 브랜치.
여러 개의 작업을 동시에 진행할 때는 그 수만큼 토픽 브랜치를 생성할 수 있음
토픽 브랜치는 보통 통합브랜치로부터 만들어 내며, 토픽 브랜치에서 특정 작업이 완료되면 다시 통합브랜치에 병합하는 방식으로 진행됨
이러한 토픽 브랜치는 '피처 브랜치(Feature branch)' 라고 부르기도 함


저장소를 처음 만들면 Git은 'master'라는 이름의 브랜치를 만들어둠

----------------------------------------------------------------------------------------------------

한 브랜치를 빼서 작업할때,
원격브랜치 만들지 말기(뺀 브랜치를 push 하지 않고 로컬에만 저장)

원격 브랜치를 실수로 push했으면 원격브랜치 강제삭제 해도됨(로컬브랜치에 영향 X)

브랜치를 만들어서 푸쉬하면 원격브랜치에 저장되는데
생성된 원격브랜치를 삭제시, 그 원격브랜치를 체크아웃했던 사람PC에서만, 소스트리에서 원격브랜치가 남아있는 버그? 가 있음 (git에서는 정상 삭제되어있음)
해당 브랜치를 체크아웃 하지 않은 사람들에게는 잘 삭제돼서 브랜치가 보이지않음.
해당 브랜치를 체크아웃한 사람PC에서만 원격브랜치를 지우든 말든 하면 됨

-----

스태시(stash)

브랜치1에서 작업한걸 브랜치2에 체크아웃해서 커밋을 할 수있음. 하지만 충돌이 날경우 체크아웃이 안되는데,
이때 "스태시"를 이용해서 브랜치2로 옮길 수 있음

스태시에서 꺼낼때,
스태시로 등록한 파일과 같은파일이 <스테이지에 올라가지 않은파일> 에 있을경우, 자동병합이 안되기때문에
그 파일을 스테이지로 이동시킨 후 스태시에서 꺼내야함

-----

병합(merge)

다른 브랜치를 현재 체크아웃중인 브랜치로 가져와서 합침


master와 master에서 딴 bugfix가 있다고 할 때
master에 체크아웃후 bugfix에서 수정한것들을 가져올경우 (병합),

master에서는 수정을 안하고 bugfix에서만 수정을 했다면
master의 head를 bugfix로 옮기기만 하면 됨. 이걸 'fast-foward(빨리감기) 병합'이라고 함 (그래프로 보면 갈라짐이 없음. 포인터만 옮긴것이기 때문에)


하지만 bugfix를 분기한 이후에 master에 여러가지 변경사항이 적용될경우,
master의 변경내용과 bugfix의 변경내용을 하나로 통합할 필요가 있음.
따라서 양쪽 변경을 가져온 'merge commit(병합 커밋)'을 실행하게 됨.
이를 'non fast-foward 병합'이라고 함 (그래프가 갈라졌다가 합쳐짐. 나뉘어졌다가 합쳐진것이기때문에)

fast-foward 병합이 가능한 경우라도, non fast-forward 병합을 한것처럼 만들 수도 있음.
non fast-forward 병합을 하면브랜치가 그대로 남기 때문에 그 브랜치로 실행한 작업 확인 및 브랜치 관리 면에서 더 유용할 수 있음


결과물을 가지고 합치는 방법

git checkout [병합한 결과가 있을 브랜치]
git merge [끌려갈 브랜치]

아래와 같이 한줄로 작성가능
git merge [병합한 결과가 있을 브랜치] [끌려갈 브랜치]


각각의 브랜치에서 변경한 내용이 같은 파일의 같은 행에 포함되어 있을경우 충돌이 발생함.

그럼 자동으로 충돌 정보를 포함해서 충돌난 파일이 아래와 같이 변경됨
<<<<<<< HEAD
최초 커밋된 내용입니다. 마스터브랜치에서 행수정함
=======
최초 커밋된 내용입니다. 브랜치1에서 행수정함
>>>>>>> branch1

그러면 어느쪽 브랜치의 수정 내용을 유지할지 선택해서 내용 및 <<<===>>> 구분자까지 직접 제거해야함

수정한 결과
↓↓↓
최초 커밋된 내용입니다. 마스터브랜치에서 행수정함
or
최초 커밋된 내용입니다. 브랜치1에서 행수정함

충돌 수정을 완료했으면 수정완료된 파일을 add 하고 commit 하기


충돌난 파일명을 다시 확인하려면 git status


만약 중간에 병합을 취소하고싶으면(merge명령어 치기전으로 돌아가려면)
git merge --abort

------------------------------

재배치(rebase)

브랜치 이력 재정렬하기

기준을 재지정하여 브랜치를 합침

git checkout [이동될 브랜치]
git rebase [현재브랜치를 갖다 붙일 기존 브랜치]

충돌났으면 수정하고

git add .

git rebase --continue

-----

커밋 메시지 수정

1. 스테이지 비우기(commit or stash)

2. 재배치할 개수 선택. 최신순부터 1-based index
git rebase -i HEAD~번호

3. 그럼 과거순으로 조회됨. 변경할 커밋을 찾아 'pick'을 'edit'로 변경후 저장닫기 (커밋메시지는 지금 수정하는게 아님)

-4. git commit --amend 입력 후 커밋메시지 수정
git commit --amend -m '커밋메시지' 로 바로 수정가능

5. git rebase --continue

6. git push -f

-----

커밋 날짜 수정

1. 깃 로그 열기
$ git log
수정하고 싶은 날짜 이전의 커밋을 골라 해당 커밋 해쉬값을 복사
15일의 커밋 기록을 13일로 바꾸고 싶다면 그 이전인 10일의 커밋 해쉬를 복사
닫기 : q


2. 리베이스
$ git rebase -i {복사한 커밋 해쉬}

i를 눌러 insert모드로 진입
가장 윗 줄의 pick을 edit으로 바꾼 후
esc → :wq (저장 후 종료)


3 . 어멘드
$ git commit --amend --no-edit --date="날짜형식"

ex)
$git commit --amend --no-edit --date="Jul 26 22:00:01 2022 +0900"
잔디를 못심은 날짜/시각으로 지정
1-Jan, 2-Feb, 3-Mar, 4-Apr, 5-May, 7-Jun
8-Aug, 9-Sep, 10-Oct, 11-Nov, 12-Dec 


4. 날짜 수정 후 rebase --continue
$ git rebase --continue

5. 수정한 rebase 내용을 master에 강제 푸쉬
$ git push -f origin master

6. 잔디가 잘 심어진 것을 확인

깃허브 계정명과 이메일이 다르면 잔디가 안심어짐
푸쉬했는데도 잔디가 안심어지면 계정명이랑 이메일 깃허브랑 맞추기
월만 바꿔서 복사붙여넣기하면 편함. 푸쉬는 각각 해줘야함 ↑ 두번 눌러서 과거 명령어 쓰기
git commit --amend --no-edit --date="Jun 1 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 2 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 3 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 4 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 5 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 6 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 7 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 8 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 9 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 10 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 11 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 12 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 13 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 14 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 15 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 16 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 17 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 18 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 19 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 20 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 21 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 22 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 23 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 24 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 25 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 26 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 27 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 28 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 29 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 30 22:00:02 2023 +0900"
git commit --amend --no-edit --date="Jun 31 22:00:02 2023 +0900"

------------------------------

체리 픽(Cherry-Pick)

커밋 하나만 rebase하는 것

병합하면 해당 브랜치의 소스가 모두 병합되는데
체리 픽을 하면 해당 커밋내용만 갖고와짐

-----

소스트리에서 트리그래프가 복잡할때는
현재 브랜치 체크하고 보면 아주 편함

-----

하다가 꼬였을때는 원격브랜치랑 로컬브랜치 위치 확인 후

다른브랜치로 체크아웃 후 로컬브랜치 강제삭제 하기

-----

같은 브랜치에서 두명이상이 동시에 수정해서 푸쉬했을경우 갈래가 뻗어짐.

이후 내가 pull을 받으면, 다른 사람들이 그동안 푸쉬했던게 자동으로 merge됨. 놀라지 말기
푸쉬해주면됨.

-----

소스트리로

스테이지에 올라가지 않은 어느 한 파일의 변경사항들 중 "특정 코드뭉치" or "특정 줄(들)"만 스테이지에 올리거나 버리기(reset) 할 수 있고
스테이지에 올라가있는 어느 한 파일의 변경사항들 중 "특정 코드뭉치" or "특정 줄(들)"만 스테이지에서 내일 수도 있음

----------------------------------------------------------------------------------------------------

★★★병합할때 주의★★★

병합기능을 이용해놓고, 원하는 파일빼고 나머지를 초기화 시킨 후 확인을 누르면,
그 파일 이외의 초기화 시킨 파일들은 다시 병합이 안됨.

이걸 방지하려면 병합기능을 쓰지 말고 직접 병합할 브랜치에서 직접 내용을 수정해야함

----------------------------------------------------------------------------------------------------

git 커맨드창 단축키

Alt + f8 : 커맨드창 화면 초기화
Ctrl + L : 커맨드창 밀기
Ctrl + A : 명령어 맨앞으로 이동
Ctrl + E : 명령어 맨뒤로 이동

----------------------------------------------------------------------------------------------------

기타팁

명령창의 제목을 보면 현재 위치한 경로가 써있음
루트는 c/Users/유저명 (사용자폴더)이고,
루트(사용자폴더)로 이동하려면 cd만 치거나 cd ~
c로 이동은 cd /c 혹은 cd c:
사용자폴더의 git 폴더로 이동하려면 cd ~/git

----------------------------------------------------------------------------------------------------

오류 모음

From https://gitlab.uniess.co.kr/visitkorea/visitkorea-front
 * branch                master     -> FETCH_HEAD
git -c diff.mnemonicprefix=false -c core.quotepath=false --no-optional-locks push -v --tags origin main:main
Pushing to https://gitlab.uniess.co.kr/pilot/first-project-icw.git
To https://gitlab.uniess.co.kr/pilot/first-project-icw.git
 ! [rejected]        main -> main (non-fast-forward)
error: failed to push some refs to 'https://gitlab.uniess.co.kr/pilot/first-project-icw.git'
↓↓↓
브랜치지웠다가 다시만들거나 원격브랜치로 hard merge하기


오류가 나면서 완료됨. 
↓↓↓
pull할게 있는 상태에서 push를 할경우 발생.
이때는 pull을 먼저 누르고, 병합후 push해야함


src refspec main does not match any
↓↓↓
push하려고 하는데 보낼 원격저장소 연결을 안했을때 발생.
remote명령어로 원격저장소와 연결해야함


현재 브랜치 master에 업스트림 브랜치가 없습니다.
↓↓↓
git push 말고 풀 명령어 입력
git push origin master


Authentication failed for
↓↓↓
무조건 개인 토큰을 이용하여 인증하도록 Git hub 정책이 바뀌었음.
git hub의 2021년 8월 13일 부로 Git hub 정책이 변경되었다는 것을 알 수 있었다.
인증 과정에서 더 이상 비밀 번호를 사용하여 인증할 수 없게 됨.
개인 토큰(Personal Access Token)을 발급 받아 사용해야한다. (https로 remote할 시에만 이런듯?)
↓↓↓
1. 깃허브 사이트 오른쪽위의  자신의 프로필을 눌러서 Settings에 들어감
2. 좌측메뉴 아래쪽에 Developer settings 클릭
3. 다시 Personal access tokens 클릭
4. 토큰을 재발급받거나 새로 발급받는다 (발급받을때 repo권한을 체크한다)
5. 명령어에 비밀번호대신 토큰값을 입력
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

소스트리에서 github비밀번호 계속 입력하라고 뜨면 깃허브 비밀번호 말고 이 토큰을 입력하면 됨


키체인에서 git-credential-osxkeychain이(가)
'github.com'에 저장된 비밀 정보를 사용하려고 합니다.
이를 허용하려면, '로그인' 키체인 암호를 입력하십시오.
↓↓↓
맥 비밀번호 입력후 '항상 허용' 버튼 클릭

-----

pull할것이 있는데 pull이전에 commit을 했을 경우, pull도 안되고 push도 안됨
이때는 트리에서 원격브랜치 우클릭 → 병합 눌러서 병합을 하면 됨

-----

어떤 원격브랜치를 다른 이름으로 받은 후 이름을 원격브랜치랑 똑같이 바꿔서 푸쉬를 하면?
그 브랜치를 commit만 해놓고 push를 안하고있는 상태에서,
누군가 해당 원격 브랜치에 push를 해버리면
pull도 못하고 push도 못함

이때 해결 방법은

최신 원격 브랜치를 체크아웃 하는데 이때 이름을 바꿔서 하기(뒤에 _붙이기)

그리고 수동으로 병합하면 병합이 잘된다

그 후 원래 있던 브랜치를 지우고 (원격브랜치는 지우면 안됨)

새로운 브랜치를 원래있던 브랜치 이름으로 바꾸고 push하기

-----

error: Your local changes to the following files would be overwritten by checkout:
	src/main/webapp/login.html
Please commit your changes or stash them before you switch branches.
↓↓↓↓↓
다른 브랜치로 체크아웃할때 발생.
src/main/webapp/login.html 이라는 파일이 변경되어있는데 커밋을 안했다는 뜻.
커밋하거나 스태시에 넣기

ignore한 파일도 우선 풀어서 스태시에 넣었다가 체크아웃을 한 후에 다시 ignore해야함

cd ~/git/visitkorea-admin

git update-index --skip-worktree src/main/webapp/login.html
git update-index --skip-worktree src/main/java/kr/or/visitkorea/admin/client/application/ApplicationView.java

git update-index --no-skip-worktree src/main/webapp/login.html
git update-index --no-skip-worktree src/main/java/kr/or/visitkorea/admin/client/application/ApplicationView.java

새로 만든 파일은 위 방법으로 안됨

----------------------------------------------------------------------------------------------------

깃허브 페이지생성법

① 저장소(repository) 생성
1. github.com/유저ID 페이지로 이동한다
2. Repositories 탭으로 이동한다
3. New 버튼을 눌러 새 저장소를 만든다
	- Repository name에는 프로젝트명을 적는다
	- Public은 소스를 전체공개 , Private는 비공개다
	- Initialize this repository with a README 체크박스 체크한다
	(체크하지 않고 만든다면 git repository를 처음 만든 이후 local repository와 연결하는 방법을 알려주는 안내 글이 뜬다. 이를 읽어 봐도 괜찮다)


② 파일 생성
1. github.com/유저ID/저장소명 페이지로 이동한다
2. uploading an existing file 를 누른다
3. choose your files 를 누른 후 업로드 할 파일을 선택한다
4. Commit changes 를 눌러 업로드를 시작한다


③ 웹페이지 서비스
1. github.com/유저ID/저장소명 페이지로 이동한다
2. Settings 탭으로 이동한다
3. Pages 탭으로 이동한다
4. Source 항목에서 master branch 또는 main 을 선택하고 Save 버튼을 누른다
5. 표시된 주소로 이동하면 자신이 만든 웹페이지가 나온다

참고: https://opentutorials.org/course/3084/18891

----------------------------------------------------------------------------------------------------

비주얼스튜디오 등으로 가져오기 (로컬로 가져오기)
github.com/사용자명/프로젝트명 에서
1. 프로젝트 최초 생성시
	- Set up in Desktop 버튼 클릭
2. 프로젝트에 내용이 있을시
	-  Code 버튼 클릭 Open with GitHub Desktop

----------------------------------------------------------------------------------------------------

이클립스에서 프로젝트로 가져오는법
Package Explorer 빈공간 → 우클릭 → Import → Git → Projects from Git
→ Next → Clone URI → github.com/사용자명/프로젝트명 에서 Code버튼 → HTTPS 주소 복사
→ 이클립스로 돌아와서 URI에 붙이기 → Next → Next → Import as general project → Next → Finish

----------------------------------------------------------------------------------------------------

GitHub Desktop 과 연동법
좌측 Current repository화살표 클릭 → Add → Add existing repository... → Choose... → 폴더 선택

----------------------------------------------------------------------------------------------------

깃허브 메인에 자기소개 영역 넣기 (숨겨진 기능)

Repositories → New버튼 → Repository name에 이름과 똑같이 입력 →
add a README file 체크 → Create repository버튼

이후 md(마크다운)문법이나 html문법으로 꾸미기 가능

-----

깃허브 랭크 / 기술비율 넣기

랭크 컬러 - ![Anurag's GitHub stats](https://github-readme-stats.vercel.app/api?username=사용자명&show_icons=true)
랭크 흰바탕 - ![Anurag's GitHub stats](https://github-readme-stats.vercel.app/api?username=사용자명&show_icons=true&theme=radical)
랭크 다크테마 - ![Anurag's GitHub stats](https://github-readme-stats.vercel.app/api?username=사용자명&show_icons=true&theme=dark)
언어 통계 - ![Anurag's GitHub stats](https://github-readme-stats.vercel.app/api/top-langs/?username=사용자명&langs_count=8)

-----

스택이나 sns 배지 만들기

<a href="연결할 링크" target="_blank"><img src="https://img.shields.io/badge/배지제목-배경색?style=뱃지모양&logo=로고&logoColor=로고색"/></a>

ex)<img src="https://img.shields.io/badge/Scss-green?style=flat&logo=Sass&logoColor=CC6699"/>

색깔 넣을때 : #는 빼야함 ★★★
배지 아이콘 : https://simpleicons.org/
뱃지 모양 : plastic / flat / flat-square / for-the-badge / social
배지제목 : 원하는 글자입력
로고아이콘 : https://simpleicons.org/ 에서 쓰고싶은 아이콘제목 복붙

배지 만드는 사이트? : https://shields.io/ 에서 make badge버튼 있음

-----

커밋시각 통계 노출하기

1. github.com/techinpark/productive-box 들어가서 fork

2. 오른쪽위 +버튼 클릭 → new gist 클릭 → 내용 아무렇게나 작성

3. Create public gist 로 gist 를 생성 (제목/내용은 아무렇게나)
이때 중요한건 Create secret gist 로 하면 안되고 화살표눌러서 Create public gist 로 해야 결과를 다른사람에게 보여줄수 있음

4. URL에 보이는
gist.github.com/사용자ID/GIST_ID
에서 GIST_ID 를 메모장에 적어놓기

5. Github 로 돌아가 Setting > Developer settings > Personal access tokens 로 들어가서 (혹은 https://github.com/settings/tokens/new)
Generate new token 클릭 → Note에 아무거나 작성후 repo와 gist에 체크한 후 Generate token 으로 토큰을 생성

6. 토큰값 또 적어놓기 (토큰은 한번밖에 보여주지 않으니 잘 적어놓기)

7. fork했던 내저장소로 돌아가서 왼쪽메뉴에 Secrets → New repository secret로 환경변수를 생성

8. 다음과같이 적고 저장
Name: GIST_ID
Value: 아까 첫번째로 복사한거

9. 한번더 New repository secret클릭후 다음과같이 적고 저장
Name: GH_TOKEN
Value: 아까 두번째로 복사한거

10. Fork한 내저장소의 Actions 탭에 들어가 action을 활성화시키기

11. 왼쪽에 Update gist → Enable workflow 클릭

12. README.md 편집버튼 → 공백입력 → 커밋 → Actions탭으로 가면 뭔가가 올라와있고
내 gists로 가면 workflows의 정상 작동을 확인할 수 있음
(주소창에 https://gist.github.com/깃아이디 로도 내gist 들어갈수있음)

13. 내 프로필로 와서 Popular repositories 영역에있는 Customize your pins 클릭후 추가된항목(방금업데이트된 내gist) 체크

-----

배경

![header](https://capsule-render.vercel.app/api?type=디자인종류)

디자인종류 : Wave / Egg / Shark / Slice / Rect / Soft / Rounded / Cylinder / Waving / Transparent / 
미리보기 - https://github.com/kyechan99/capsule-render#waving-

-----

참고:
https://codesyun.tistory.com/98
https://80000coding.oopy.io/865f4b2a-5198-49e8-a173-0f893a4fed45

----------------------------------------------------------------------------------------------------

소스트리에서 병합하는방법
먼저 병합할게 있는지 Pull을 눌러보고

있다면

1. 병합을 누른다.
2. 왼쪽에 파일 이름을 더블클릭해 연다??
3. 내용을 수정한다
4. 스테이지에 올리고 커밋&푸쉬를 한다

----------------------------------------------------------------------------------------------------

소스트리

스테이지 올라가지 않은 파일에서 반영시킬 파일들만을 스테이지에 올림

필요없는 파일은 파일 우클릭 → 초기화



브랜치 안하고 마스터에서 한건..

풀을 함 → 안됨

마스터 우클릭 → 브랜치 만듬

커밋 메시지 입력후 커밋을 하고 풀을 함

마스터에다 커밋을 하면 안됨


개발계에 반영할때 먼저
내가 만든 브랜치 우클릭 → 영어 머지 머시기..

같은 가지를 가지고 브랜치를 했는데
같은 파일을 수정했고, 수정한 라인도 비슷하면 충돌이 남.
충돌나면
파일 아무 에디터로 열어서
헤드가 원래 있던거..
밑에가 새로 바뀐거..

잘 보고 추가할건 추가하고 없앨건 없앤다음
<<<<<======>>>>>>이런 틀은 제거해주기

전체 검색해서 찌꺼기 남아있는지 확인하기
<<<<
====
>>>>

충돌난거 인텔리제이로 해결할때는 "Resolve Simple Conflicts(간단한 충돌 문제 해결)(마법봉아이콘)" 버튼 누르고 하기. 아니면 소스트리 보면서 하기



개발 서버에 배포할떄는 젠킨스로 함


master 브랜치에다 반영하는건 운영서버에 배포할때 함




체크 아웃 : 해당 브랜치로 접속하는거

로컬 변경사항을 폐기할때(지울때)는 (스테이지에 올리기 전에, 스테이지에 올라가지 않은 파일 탭에서) 제거가 아닌 '초기화'

푸쉬할때는 어디에 체크아웃돼있든(들어와있든) 상관없이 푸쉬 아이콘 누르고 체크 해주면 된다
꼭 체크아웃된 상태에서 푸쉬를 누를 필요가 없음. 체크아웃된상태에서 풀을 누르면 그냥 단순히 체크가 되어있는게 다임

추가(add) : 파일들을 스테이지에 올림
커밋(commit) : 스테이지에 올라가있는 파일들을 로컬 저장소의 해당 브랜치로 변경 사항들을 적용시킴(저장되는곳 : .git폴더안에 object폴더)
푸쉬(push) : 로컬 저장소 → 원격 저장소의 해당 브랜치 로 변경 사항들을 적용시킴
풀(pull) : 특정 원격 저장소에 있는걸 로컬 저장소의 현재 브랜치로 가져옴 + 워크스페이스에 적용시킴
병합(merge) : 로컬 저장소의 다른 브랜치거를 현재 체크아웃중인 브랜치로 가져와서 합침
	받을브랜치체크아웃후 보내는브랜치에 커서갖다대고 우클릭 → Merge OOO into OOO 이거 눌러도 됨


원격 브랜치를 직접 수정하지는 못하고 무조건 로컬로 풀 받거나 병합한 후 다시 푸쉬해줘야함


기능에 따라 브랜치를 뽑아서 작업해야함

마스터에서 따온 기능1을 개발하기 위한 브랜치와,
마스터에서 따온 기능2를 개발하기 위한 브랜치가 있다고 할때.
각각의 브랜치에서 수정을 하던 중, 한쪽으로 합칠경우 다시 브랜치를 분리할수 없어진다
때문에 한쪽브랜치에서 더 이상 수정할게 없는게 아닌이상, 각각의 브랜치(기능)들을 따로 관리하고 developer / master 에 병합시켜야한다

-----

.git/objects/

objects_tree

git에서 활용하는 데이터들이 저장되는 곳이다. tree 명령어를 실행시켜 보면 위와 같은 구조를 가진다. 2글자의 폴더 밑에 38글자의 파일명을 가지는 특이한 구조를 가진다.

objects의 구성은 실제 파일에 담긴 값들을 SHA1 해시한 값 40자 중
2자는 폴더명 38자는 파일명으로 두어 식별자로 활용한다.
해싱을 사용했을 때, 소스 코드의 일부만을 바꾸더라도 별개의 해시값이 되기 때문에, 파일 식별이 쉬워지게 된다. (추가로 SHA1 해시 처리 전, zlib으로 한번의 압축이 진행된다.)

저장되는 파일의 형태는 크게 3가지 blob, tree, commit으로 분리된다.

----------------------------------------------------------------------------------------------------

소스트리 브랜치 지웠는데 안지워지고 이상하면 그냥 로컬 브랜치를 삭제하고 다시 따오기.
(내변경사항이 있다면 스태시에 저장해놓고 왼쪽에 '치워두기' 메뉴에서 다시 변경사항들만 불러올 수 있음)

스태시 파일이름은 날짜_시간으로 만들면 편함

----------------------------------------------------------------------------------------------------

소스트리에서

브랜치라고 써있는게 → 로컬 브랜치고
구름모양에 원격이라고 써있는게 → 원격 브랜치임 (깃랩/깃허브 사이트에서 확인 가능한..)

트리 그래프에서.. 커밋제목앞에 버튼모양으로 색깔칠해져있는 브랜치중
앞에 원격브랜치명(origin/) 이 붙은건 원격 저장소에 있는 브랜치라고 생각하면됨.

푸쉬를 하면 원격브랜치가 밑에있다가 로컬브랜치 위치로 이동(올라올)될것임

----------------------------------------------------------------------------------------------------

커밋 되돌리기(revert) : 브랜치의 선택한 커밋만을 취소시킴.
(취소했다는 기록이 새로 남음. 언제든지 원상복구 가능. 병합커밋에는 못쓰는듯
commit 5e7c5a5d9d46b0e170c572b42cc07866ac7dd47d is a merge but no -m option was given. 오류)

ㅇㅇ를 이 커밋으로 초기화(reset) : 브랜치의 선택한 포인트로 완전히 돌아갈 수 있음
Soft : 변경했던 파일들이 스테이지에 올라가있음
Mixed : 변경했던 파일들이 스테이지에 안올라가있음
Hard : 변경했던 파일들이 완전히 제거됨 (원상복구 불가. 완전히 필요없어졌을때만 이용)

----------------------------------------------------------------------------------------------------

소스트리에서 변경한파일명/파일변경내용/커밋메시지/사용자 로 검색하는법

워크스페이스 → 검색 → 검색창 우측에 검색기준/날짜 선택후 → 돋보기 옆 검색창에 검색할 문자열 입력 후 엔터

★ 파일명으로 검색이 잘 안되는 듯 함
검색 창에서 하지말고 오른쪽 아래 검색입력창에 파일명 쳐놓고
수동으로 최근트리부터 하나씩 내려가면서 변경사항이 있는지 찾는게 더 정확함

----------------------------------------------------------------------------------------------------

스태시 붙이기 or 병합 시 충돌이 났을때

				.
				.
				.
<<<<<<< HEAD
					aaa
=======
                    			bbb
>>>>>>> feature/xxx
				.
				.
				.

위처럼 되어있다면

남이한것 → aaa

이랑 ,

내가한것 (feature/xxx에서 수정한것) → bbb

모두 살려놓거나, 둘중 하나를 지워야하는데,

둘 다 필요한것이면 둘다 살리면 되고, (거의 java/jsp/xml/js)
둘 중 하나만 필요한 것이면 둘중 하나를 지우면 됨 (거의 css. css의 경우 더 최신의 css를 남기면 됨)

헷갈릴때는
내 코드는 소스트리가서, 병합하기 전 브랜치에서, 해당 파일을 마지막으로 수정한 커밋날짜/커밋내용을 확인하고,
타인의 코드는 ctrl+cmd+h / ctrl+opt+cmd+h로 git 내역의 커밋날짜/커밋내용을 확인해서
둘 중 더 최신의 코드나, 더 중요한 코드를 남기면 됨

----------------------------------------------------------------------------------------------------

풀이 안될때

develop 브랜치를 pull받아야하는데 현재브랜치의 커밋이 더 앞에 있을때
별도의 옵션없이 pull 하는경우 원하지 않는 방향으로 pull될 수 있다는 뜻.

pull을 받지 않은상태에서 commit을 할 경우 오류 발생
or
commit까지만 하고 push는 안했을때 누군가 push를 한경우 pull받을게 생기면 발생???

↓↓↓↓↓

git pull 전략

git config pull.rebase false (기본값)
- pull 할때 rebase를 하지 않고 merge 한다.

git config pull.rebase true
- pull할 때 rebase 한다. → 체리픽 한것처럼 됨. 불필요한 커밋이 생기지 않음. 이걸로 바꿨는데도 안되면 git pull --rebase

git config pull.ff only
- fast-foward일때만 pull을 허용한다

----------------------------------------------------------------------------------------------------

풀을 안받고 커밋을 하면, 풀도 안되고 푸쉬도 안되는 듯

이때는 soft reset → 풀 → 커밋 → 푸쉬하기

----------------------------------------------------------------------------------------------------

develop 브랜치를 master브랜치와 다르게 하지않기

다르게 할경우 다른사람이 master브랜치에서딴 브랜치를 병합할경우 충돌이 생김

----------------------------------------------------------------------------------------------------

병합 커밋 revert 하기

병합커밋만 보기
git log --merges

꼭 CLI에서 안하고 소스트리에서 '태그'같은거 눌러서 커밋id복사해도 됨

# git revert --mainline [남길 line] [병합 commit]
git revert --mainline 1 cb70c2d
(--mainline 대신에 -m 써도 됨)

왼쪽 그래프가 1번라인, 오른쪽 그래프가 2번라인이다


취소커밋을 다시 취소할 수 있음

----------------------------------------------------------------------------------------------------

마스터 병합커밋을 되돌려야할때는, 되도록 revert를 하지말고 다른 방법을 이용하기

★특히, 마스터랑 디벨롭이랑 차이가 나면 안된다고 디벨롭을 마스터껄(병합revert한걸로) 가져와 병합해버린경우
↓↓↓
이경우가 발생되면 병합커밋을 revert를 한 후 하나하나 고친부분을 수정해줘야하는 매우 성가신일이 발생
또한 그냥 성가실뿐만 아니라, 따로따로 revert를 해야하기때문에 작업브랜치 → develop==master 이랬던 일관성도 깨짐

reset을 하던가 작업브랜치를 하나 복사해서,
과거 커밋으로 reset시키고(이게 되나 테스트는 아직 안해봄)

----------------------------------------------------------------------------------------------------

재배치할때는 브랜치를 하나 따서 백업해놓는게 좋음

----------------------------------------------------------------------------------------------------

























