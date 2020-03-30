---
published: true
---
# vim을 실행하면 Command mode에서 시작한다.

## Insert mode 진입
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
O: 현재 커서 위에 새로운 줄을 추가하고 편집을 시작한다.<br />

![vim-02-insert.jpg]({{site.baseurl}}/images/vim-02-insert.jpg)
<br />
<br />