쉘 스크립트
- Shell이나 command line 인터프리터에서 구동되도록 작성된 스크립트
- 윈도우에서는 batch파일, .bat 이 사용됨
- shell script가 인터프리터 방식이므로 한줄한줄 읽어 실행함으로 다소 속도가 느림
- 터미널에서 실행 가능


<파일 생성>
vi에디터로 파일 생성
vi [파일명.sh]

i 눌러 입력모드로 변경 후 내용 작성

echo "Hello, World!"

작성 완료후 명령모드로 전환 : esc
저장 후 닫기 : :wq
저장할때 wq! 뒤에 파일명 써도 됨


<권한 부여>
파일을 작성한 뒤 아래 명령어로 실행권한을 부여해야해야 실행됨(-rw-r--r--에서 -rwxr-xr-x로 바뀌고, 이름색깔도 바뀐걸 확인하기)
chmod 755 [파일명]
or
chmod +x [파일명]


<실행>
sh [파일명]


<변수 선언>
변수의 타입에는 "로컬변수"와 "환경변수(전역)"이 존재한다.

----------------------------------------------------------------------------------------------------

cpu사용량아 80%이상일때 터미널 종료

#!/bin/bash

# 임계값 (이 값 이상이면 종료)
THRESHOLD=80

# 무한 반복
while true; do
# 현재 CPU 점유율을 추출하여 변수에 할당
CPU=$(top -n 1 -l 1 | grep "CPU usage" | awk '{print $3}' | cut -d. -f1)
echo $CPU

# CPU 점유율이 임계값을 초과한 경우
if [ "$CPU" -gt "$THRESHOLD" ]; then
    echo "CPU usage is above the threshold of ${THRESHOLD}%. Closing terminal..."
    sleep 3
    osascript -e 'tell application "Terminal" to close first window' & exit
fi

# 5초 대기 후 다시 검사
sleep 5
done

----------------------------------------------------------------------------------------------------


