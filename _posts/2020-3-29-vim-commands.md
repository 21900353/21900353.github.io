---
layout: post
title: vim 명령어 연습/정리
published: true
---
# vim을 실행하면 Command mode에서 시작한다.

## Insert mode 진입
내용을 편집할 때 사용하는 모드이다.

- ## i
Command mode에서 Insert mode로 진입할 때 i를 누른다.<br />
현재 커서에서 편집을 시작한다.

![vim-01-insert.jpg]({{site.baseurl}}/images/vim-01-insert.jpg)
<br />
<br />
- ## i 외
커서 위치를 현재 위치가 아닌 다른 위치에서 편집을 시작할 수 있다.<br />
커서 위치는 우측하단에 (행,글자번호)로 확인할 수 있다.<br />
a: 현재 커서의 다음 위치에서부터 편집을 시작한다.<br />
A: 현재 행의 맨 끝으로 커서를 이동시키고 편집을 시작한다.<br />
o: 현재 커서 아래에 새로운 줄을 추가하고 편집을 시작한다.<br />
O: 현재 커서 위에 새로운 줄을 추가하고 편집을 시작한다.

![vim-02-insert.jpg]({{site.baseurl}}/images/vim-02-insert.jpg)
<br />
<br />
<br />
## Command mode 에서
- ## 지우기
x: 현재 커서 위치에서 한 글자를 지운다.<br />
dw: 현재 커서 위치에서 그 단어의 끝까지 지운다<br />
dd: 현재 행을 지운다.
사진에서 현재 커서 위치는 3행 e 앞이다.

![vim-03-delete.jpg]({{site.baseurl}}/images/vim-03-delete.jpg)
<br />
<br />
숫자+dd: 현재 커서 위치에서 입력한 숫자만큼의 행을 지운다.<br />
아래 사진의 커서는 첫번째 행에 있고, 2dd를 입력했으므로 1~2행이 삭제되었다.

![vim-04-delete.jpg]({{site.baseurl}}/images/vim-04-delete.jpg)
<br />
<br />
<br />
- ## 실행 취소/다시 실행
u: 마지막으로 실행한 명령을 취소한다.

![vim-05-undo.jpg]({{site.baseurl}}/images/vim-05-undo.jpg)
<br />
<br />
U: 현재 행의 모든 수정사항을 취소한다.<br />
Ctrl+r: 실행 취소한 명령을 다시 실행한다. 사진에서 U 입력 후 Ctrl+r을 했기 때문에 1번으로 돌아온다.<br />
![vim-06-undo,redo.jpg]({{site.baseurl}}/images/vim-06-undo,redo.jpg)
<br />
<br />
<br />
- ## 내용 변경
r: 현재 커서의 글자를 변경한다.

![vim-07-replace.jpg]({{site.baseurl}}/images/vim-07-replace.jpg)
<br />
<br />
cw: 현재 커서에서부터 단어 끝까지를 변경한다. 명령을 입력하면 그 부분이 삭제된 후 Insert mode로 진입한다.<br />
c$: 현재 커서에서부터 행 끝까지를 변경한다. 명령을 입력하면 그 부분이 삭제된 후 Insert mode로 진입한다.

![vim-08-cw.jpg]({{site.baseurl}}/images/vim-08-cw.jpg)
<br />
<br />
<br />
- ## 붙여넣기, 이동하기
p: 복사된 내용이나 마지막으로 지운 내용을 붙여넣는다. (y: 복사)<br />
행번호+Shift+g: 번호를 입력한 행으로 이동한다. 3+Shift+g를 입력했기 때문에 3 번째 행으로 이동한다.<br />
Shift+g: 마지막 행으로 이동한다. <br />
Ctrl+g: 파일 상태, 행 개수, 현재 커서 위치를 확인할 수 있다.

![vim-09-paste,nav.jpg]({{site.baseurl}}/images/vim-09-paste,nav.jpg)
<br />
<br />
<br />
- ## 검색
/검색어: 현재 위치에서 아래로 검색어를 찾는다. 사진에서 1번은 커서가 첫 번째 행 첫 번째 글자에 있었기 때문에, /member를 입력했을 때 가장 먼저 나타나는 member(7행) 앞으로 커서가 이동했다.<br />
?검색어: 현재 위치에서 위로 검색어를 찾는다. 사진에서 2번은 커서가 7행에 있었기 때문에, ?member를 입력했을 때 가장 먼저 나타나는 include(3행) 앞으로 커서가 이동했다.<br />
n: 검색한 후 아래쪽으로 다음 나타나는 검색어로 이동한다. 사진에서 3번은 7행 member를 찾은 상황이기 때문에, n을 입력하면 10행 member 앞으로 커서가 이동한다.<br />
Shift+n: 검색한 후 위쪽으로 나타나는 검색어로 이동한다. 사진에서 4번은 검색어를 두 번째 찾은 상황이기 때문에, Shift+n을 입력하면 첫 번째 검색어 앞으로 커서가 이동한다.

![vim-10-find.jpg]({{site.baseurl}}/images/vim-10-find.jpg)
<br />
<br />
<br />
## Command-line mode
복잡한 명령을 실행할 때 쓰는 모드이다.

- ## 내용 변경
":s/찾는단어/새단어": 현재 행에서 찾는단어를 새단어 한 개만 변경한다.<br />
":s/찾는단어/새단어/g": 현재 행에서 찾는단어를 모두 새단어로 변경한다.<br />
":%s/찾는단어/새단어/g": 파일 내 모든 찾는단어를 새단어로 변경한다.<br />
":%s/찾는단어/새단어/gc": 파일 내 모든 찾는단어를 물어보면서 새단어로 변경한다.

![vim-11-cl_replace.jpg]({{site.baseurl}}/images/vim-11-cl_replace.jpg)
<br />
<br />
":행번호,행번호s/찾는단어/새단어/g": 두 행 사이에서 모든 찾는단어를 새단어로 변경한다.

![vim-12-cl_replace.jpg]({{site.baseurl}}/images/vim-12-cl_replace.jpg)
<br />
<br />
<br />
- ## 창 나눔
":vs 파일이름": 수직으로 창을 나눠 파일을 읽어온다.

![vim-13-vs.jpg]({{site.baseurl}}/images/vim-13-vs.jpg)
<br />
<br />
":split 파일이름": 수평으로 창을 나눠 파일을 읽어온다.

![vim-13-split.jpg]({{site.baseurl}}/images/vim-13-split.jpg)
<br />
<br />
<br />
- ## 외부 명령어 실행
":!명령어": 쉘 명령어를 실행한다. 확인 창에서 엔터를 입력하면 다시 vim으로 돌아온다.

![vim-14-shell.jpg]({{site.baseurl}}/images/vim-14-shell.jpg)
<br />
<br />
<br />
- ## 파일 내용 끼워넣기
":r 파일이름": 현재 커서에 파일 내용을 가져온다.

![vim-15-r.jpg]({{site.baseurl}}/images/vim-15-r.jpg)
<br />
<br />
<br />
- ## 파일 일부를 다른 이름의 파일로 저장
":행번호,행번호w 파일이름": 두 행 사이의 내용을 다른 이름의 파일로 저장한다.

![vim-16-write.jpg]({{site.baseurl}}/images/vim-16-write.jpg)
<br />
<br />
<br />
## Visual mode
구간을 블록으로 설정할 때 쓰는 모드이다. 복사/자르기/붙여넣기 할 때 유용하다.<br />
v를 입력해 Visual mode로 진입한다.

사진에서 1번은 현재 커서 위치에서 v를 입력해 Visual mode로 진입한 후, k(위로 이동)를 4번 눌러 네 개의 행을 선택했다. 그 이후 2번 처럼 y를 입력해 복사한 후 p를 입력해 현재 커서 위치에 붙여넣었다. 

![vim-17-visual.jpg]({{site.baseurl}}/images/vim-17-visual.jpg)
<br />