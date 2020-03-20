---
layout: post
title: 리눅스 명령어 연습/정리
published: true
---

## 1. date
날짜 표시

![스크린샷(116).jpg]({{site.baseurl}}/images/스크린샷(116).jpg)




## 2. df
시스템 전체의 디스크 사용량 표시

![스크린샷(117).jpg]({{site.baseurl}}/images/스크린샷(117).jpg)




## 3. pwd
현재 작업위치 표시

![스크린샷(118).jpg]({{site.baseurl}}/images/스크린샷(118).jpg)




## 4. ls
파일과 디렉토리 표시

![-la 옵션: 자세히 출력, 숨겨진 파일과 디렉토리를 출력]({{site.baseurl}}/images/스크린샷(119).jpg)
-la 옵션: 자세히 출력, 숨겨진 파일과 디렉토리를 출력
<br />
<br />
<br />
## 5. cd
작업위치 변경

![스크린샷(120).jpg]({{site.baseurl}}/images/스크린샷(120).jpg)

<br />
<br />
<br />
## 6. cat
파일 내용 출력

![-n 옵션: 행번호 표시 / ">" : redirect 하여 화면에 쓰는 내용을 파일에 쓸 수 있다]({{site.baseurl}}/images/스크린샷(123).jpg)
-n 옵션: 행번호 표시 / ">" : redirect 하여 화면에 쓰는 내용을 파일에 쓸 수 있다
<br />
<br />
<br />
## 7. less
파일 내용을 보여주는 창. 화살표키로 스크롤

![스크린샷(128).jpg]({{site.baseurl}}/images/스크린샷(128).jpg)
![less 화면]({{site.baseurl}}/images/스크린샷(129).jpg)
less 화면
<br />
<br />
<br />
## 8. cp
파일 복사

![스크린샷(130).jpg]({{site.baseurl}}/images/스크린샷(130).jpg)

<br />
<br />
<br />
## 9. mkdir
디렉토리 만들기

![스크린샷(131).jpg]({{site.baseurl}}/images/스크린샷(131).jpg)

<br />
<br />
<br />
## 10. mv
파일 이동

![스크린샷(132).jpg]({{site.baseurl}}/images/스크린샷(132).jpg)

<br />
<br />
<br />
## 11. rm
파일 삭제

![-r 옵션: 디렉토리와 그 안에 있는 파일들을 모두 삭제한다]({{site.baseurl}}/images/스크린샷(133).jpg)
-r 옵션: 디렉토리와 그 안에 있는 파일들을 모두 삭제한다
<br />
<br />
<br />
## 12. ln
링크 생성
1. 하드링크: 원본과 동일한 내용의 다른 파일
2. 심볼릭링크 (-s 옵션): 파일을 가리키기만 하는 링크

![sample.txt의 링크 두 개를 만들었다. 하드링크는 원본과 inode가 같은 것을 보아 같은 파일을 가리키고, 심볼릭링크는 원본과 inode가 다른 것을 보아 원본을 가리키는 다른 파일이다.]({{site.baseurl}}/images/스크린샷(135).jpg)
sample.txt의 링크 두 개를 만들었다. 하드링크는 원본과 inode가 같은 것을 보아 같은 파일을 가리키고, 심볼릭링크는 원본과 inode가 다른 것을 보아 원본을 가리키는 다른 파일이다.
<br />
<br />
<br />
## 13. file
파일 종류 표시

![스크린샷(136).jpg]({{site.baseurl}}/images/스크린샷(136).jpg)

<br />
<br />
<br />
## 14. type
명령어 종류 표시

![스크린샷(137).jpg]({{site.baseurl}}/images/스크린샷(137).jpg)

<br />
<br />
<br />
## 15. which
명령어의 위치 표시

![스크린샷(138).jpg]({{site.baseurl}}/images/스크린샷(138).jpg)

<br />
<br />
<br />
## 16. help
특정 명령어 도움말. 명령어 뒤에 --help를 붙여 사용

![스크린샷(139).jpg]({{site.baseurl}}/images/스크린샷(139).jpg)
![less의 help 창]({{site.baseurl}}/images/스크린샷(140).jpg)
less의 help 창
<br />
<br />
<br />
## 17. man
특정 명령어 도움말

![스크린샷(141).jpg]({{site.baseurl}}/images/스크린샷(141).jpg)
![cp의 man 창]({{site.baseurl}}/images/스크린샷(142).jpg)
cp의 man 창
<br />
<br />
<br />
## 18. sort
파일의 내용을 행단위로 정렬

![스크린샷(143).jpg]({{site.baseurl}}/images/스크린샷(143).jpg)

<br />
<br />
<br />
## 19. uniq
연속으로 중복된 행은 하나만 남겨서 표시. sort와 같이 사용하면 유용하다
-c 옵션: 중복된 개수 표시

![distros.txt.의 내용을 sort로 정렬하고, uniq 로 전달하였다. 그 결과 각 distro가 몇 개 있는지 표시되었다.]({{site.baseurl}}/images/스크린샷(144).jpg)
distros.txt.의 내용을 sort로 정렬하고, uniq 로 전달하였다. 그 결과 각 distro가 몇 개 있는지 표시되었다.
<br />
<br />
<br />
## 20. grep
문자열 검색

![grep "검색어" 검색할파일]({{site.baseurl}}/images/스크린샷(145).jpg)
grep "검색어" 검색할파일
<br />
<br />
<br />
## 21. wc
파일의 행, 단어, 문자 표시

![옵션이 없다면 기본으로 행, 단어, 문자 순으로 표시된다]({{site.baseurl}}/images/스크린샷(146).jpg)
옵션이 없다면 기본으로 행, 단어, 문자 순으로 표시된다
<br />
<br />
<br />
## 22. head
파일의 앞부분 출력 (기본 10줄)

![스크린샷(147).jpg]({{site.baseurl}}/images/스크린샷(147).jpg)

<br />
<br />
<br />
## 23. tail
파일의 뒤부분 출력 (기본 10줄)

![스크린샷(148).jpg]({{site.baseurl}}/images/스크린샷(148).jpg)

<br />
<br />
<br />
## 26. echo
화면에 출력

![스크린샷(150).jpg]({{site.baseurl}}/images/스크린샷(150).jpg)

<br />
<br />
<br />
## 25. tee
화면에 출력된 내용을 파일로 저장

![echo 화면에 출력한 내용을 tee로 전달하여 tee.txt에 저장했다.]({{site.baseurl}}/images/스크린샷(151).jpg)
echo 화면에 출력한 내용을 tee로 전달하여 tee.txt에 저장했다.
<br />
<br />
<br />
## 26. clear
이전 명령어를 화면에서 지워 깨끗하게 한다

![스크린샷(152).jpg]({{site.baseurl}}/images/스크린샷(152).jpg)
![clear 실행 후]({{site.baseurl}}/images/스크린샷(153).jpg)
clear 실행 후
<br />
<br />
<br />
## 27. history
이전에 입력한 명령어 목록을 출력

![history 실행 후]({{site.baseurl}}/images/스크린샷(154).jpg)
history 실행 후
<br />
<br />
<br />
## 28. chmod
파일 권한 변경
첫번째 변수에서 권한을 설정한다.
1. u 사용자, g 그룹, o 다른 사용자
2. + 추가, - 삭제, = 명시한대로 설정
3. r 읽기, w 쓰기, x 실행

![chmod 실행 후 파일 권한이 rw-rw-r--에서  rw-r--r--으로 변경되었다]({{site.baseurl}}/images/스크린샷(155).jpg)
chmod 실행 후 파일 권한이 rw-rw-r--에서  rw-r--r--으로 변경되었다
<br />
<br />
<br />
## 29. umask
기본 권한 설정
1. 숫자모드: 초기 권한에서 삭제할 권한을 쓴다
(0: rwx, 1: rw-, 2: r-x, 3: r--, 4: -wx, 5: -w-, 6: --x, 7: ---)

2. 문자모드: chmod와 사용법이 동일

![umask 133 실행 후 만든 파일은 권한이 rw-r--r--이고, umask u=rw,g=rw,o=r 실행 후 만든 파일은 권한이 rw-rw-r--이 된다.]({{site.baseurl}}/images/스크린샷(156).jpg)
umask 133 실행 후 만든 파일은 권한이 rw-r--r--이고, umask u=rw,g=rw,o=r 실행 후 만든 파일은 권한이 rw-rw-r--이 된다.
<br />
<br />
<br />
## 30. chown
파일 소유 계정 변경
chown (소유권자):(그룹) 파일 을 입력한다

![없는 사용자이기 때문에 저런 결과가 나왔다. 존재하는 사용자였다면 잘 됐을 것이라고 생각한다.]({{site.baseurl}}/images/스크린샷(157).jpg)
없는 사용자이기 때문에 저런 결과가 나왔다. 존재하는 사용자였다면 잘 됐을 것이라고 생각한다.
<br />
<br />
<br />
## 31. chgrp
파일 소유 그룹 변경

![없는 그룹이기 때문에 저런 결과가 나왔다.]({{site.baseurl}}/images/스크린샷(158).jpg)
없는 그룹이기 때문에 저런 결과가 나왔다.
<br />
<br />
<br />
## 32. ps
프로세스 확인

![스크린샷(159).jpg]({{site.baseurl}}/images/스크린샷(159).jpg)
스크린샷(159).jpg
<br />
<br />
<br />
## 33. top
시스템 상태 확인

![top 실행 결과]({{site.baseurl}}/images/스크린샷(160).jpg)
top 실행 결과
<br />
<br />
<br />
## 34. jobs
백그라운드 작업 확인

![하나의 작업이 Stopped 되어 있는 것을 확인했다.]({{site.baseurl}}/images/스크린샷(161).jpg)
하나의 작업이 Stopped 되어 있는 것을 확인했다.
<br />
<br />
<br />
## 35. kill
프로세스 종료

![kill 실행 후 1번 작업이 종료되었다.]({{site.baseurl}}/images/스크린샷(162).jpg)
kill 실행 후 1번 작업이 종료되었다.
