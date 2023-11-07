[[Python]]에서 애플스크립트 쓰는법 (osascript)

import os 후 os.system("""osascript -e" """") 이안에 담으면 됨


ex)
import os

os.system("""
osascript -e "set Volume 10"
""")


밝기 1단계 높이기 : -e 'tell application "System Events"' -e 'key code 113' -e ' end tell' (만약안되면 144)
밝기 1단계 낮추기 : -e 'tell application "System Events"' -e 'key code 107' -e ' end tell' (만약안되면 145)
소리 최대로 : -e 'set Volume 10'
소리 최저로 : -e 'set Volume 0'

밝기 최저로 :
for i in range(2):
        os.system("""
        osascript -e 'tell application "System Events"' -e 'repeat 30 times' -e 'key code 107' -e 'end repeat' -e 'end tell'
        """)


ctrl 키와 다른 키를 동시에 누르기
osascript -e 'tell application "System Events"' -e 'keystroke "u" using control down' -e 'end tell'


애플리케이션(터미널)창을 제일 앞으로 가져오기
osascript -e 'tell application "Terminal" to activate'


애플리케이션(터미널) 새창열기
osascript -e 'tell application "Terminal"' -e 'DO script "" ACTIVATE' -e 'end tell'


애플리케이션(터미널)이 실행중일때 실행?
if application "Terminal" is running then
    tell application "Terminal"
        do script ""
        activate
    end tell


애플리케이션창에 포커스가 있을때 실행
tell application "System Events"
	if frontmost of process "TextEdit" is true then
	else #선택
	end if
end tell


첫번째 윈도우에 실행중인 응용프로그램이 있는지 확인
if window 1 is busy then
















