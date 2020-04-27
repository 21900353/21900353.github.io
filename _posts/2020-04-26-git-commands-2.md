---
published: false
---
# git 협업

branch는 독립된 환경에서 기능을 추가하고 테스트 해야할 때 유용하다. branch에서 작업을 완료하면 master 브랜치와 merge 과정을 통해 병합한다.

협업에서 branch와 merge는 중요한 개념이다. 이번 포스트에서는 예제 시나리오를 통해 branch와 merge를 어떻게 사용하는지 알아보겠다. 그리고 커밋을 취소하는 reset, revert, rebase의 차이점을 알아보겠다. 

## branch, merge 명령어 설명

- ## git branch
git branch (이름): 새 브랜치 생성<br />
git branch: 브랜치 목록 확인. * 표시된 것이 현재 브랜치이다.


- ## git checkout (브랜치)
해당 브랜치로 전환<br />


- ## git log
git log (옵션): 커밋 로그 확인<br />
git log (파일): 특정 파일에 대한 로그 확인<br />
옵션:<br />
-숫자: 최근 몇 개를 보일 것인지<br />
-p: 차이점 표시<br />

(예: git log -p -2 = 최근 2 개의 커밋에 대한 로그를 보여주고 추가적으로 차이점도 표시된다.)<br />


- ## git merge (브랜치)
현재 브랜치로 해당 브랜치에서 한 작업을 병합<br />
<br />
<br />
## 시나리오

master 브랜치에서 파생된 second 브랜치가 있다. master와 second를 전환하며 작업하고, second에서 작업이 완료되면 second를 master에 No fast forward 방법으로 병합할 것이다. 시나리오를 그림으로 나타내면 다음과 같다:

![git2-01-diagram.png]({{site.baseurl}}/images/git2-01-diagram.png)<br />
그림과 같이 파일을 추가하고, 수정하고, 브랜치가 (no fast forward)병합될 것이다. 

## second branch 
v2 커밋에서는 git_test1.txt를 만들어 추가했고, v3 커밋에서는 git_test2.txt를 만들어 추가했다.

![git2-02-v1.jpg]({{site.baseurl}}/images/git2-02-v1.jpg)<br />
(초기 커밋 v1)

![git2-03-v2.jpg]({{site.baseurl}}/images/git2-03-v2.jpg)<br />
![git2-04-v3.jpg]({{site.baseurl}}/images/git2-04-v3.jpg)<br />
v2, v3: 각 커밋에서는 새로 만들어진 git_test1.txt, git_test2.txt 파일을 추가했다.<br />
<br />
<br />
v3 커밋 후 second 브랜치를 생성했다.<br />
그리고 second 브랜치로 전환해 적업을 시작했다.

![git2-05-branch,checkout.jpg]({{site.baseurl}}/images/git2-05-branch,checkout.jpg)
git branch second를 실행하면 second라는 브랜치가 생성된다. 현재 master 브랜치에 있기 때문에 git checkout second를 실행해 second 브랜치로 전환했다.<br />
<br />
<br />
![git2-06-v4.jpg]({{site.baseurl}}/images/git2-06-v4.jpg)
v4 커밋에서는 git_test_second.txt라는 파일을 만들고 추가했다.<br />
<br />
<br />
second 브랜치에서 작업을 끝냈고, 이제 master 브랜치로 전환해 작업할 차례이다.

![git2-07-checkout.jpg]({{site.baseurl}}/images/git2-07-checkout.jpg)<br />
git checkout master를 실행해 master로 전환했다. 이후 vim에서 git_test1.txt를 수정한 후 커밋했다.<br />
(두 번째 줄 "edited"를 추가했다)<br />

![git2-08-v5.jpg]({{site.baseurl}}/images/git2-08-v5.jpg)<br />
v5: 수정한 파일 커밋

v6에서도 마찬가지로 수정하고 커밋했다.

![git2-09-v6.jpg]({{site.baseurl}}/images/git2-09-v6.jpg)<br />
v6 커밋<br />
<br />
<br />
다시 second로 전환해 작업할 차례이다. git checkout second를 실행해 second로 전환했고, git_test_second.txt 수정 후 커밋했다. 

![git2-10-v7.jpg]({{site.baseurl}}/images/git2-10-v7.jpg)<br />
v7 커밋<br />
<br />
<br />
second에서 할 작업은 완료되었기 때문에, master로 병합할 차례이다. <br />
master로 전환한 후, git merge --no-ff second를 실행해 No fast forward 방법으로 second 브랜치를 병합했다.

![git2-11-v8,merge.jpg]({{site.baseurl}}/images/git2-11-v8,merge.jpg)<br />
v8 커밋: second를 master로 병합<br />

(Fast forward란 포인터를 앞으로 당기는 일을 뜻한다. master에서 변경사항이 없다면, fast forward 병합을 하는 경우 second에 있던 모든 커밋이 master로 합쳐지게 된다.<br />
No fast forward 병합을 하면 브랜치는 브랜치대로 유지가 되면서 변경사항만 합쳐지는 커밋이 추가된다.)<br />
아래 그림에서 시각적으로 설명하고 있다: 

![git2-merging.png]({{site.baseurl}}/images/git2-merging.png)<br />
왼쪽 FF, 오른쪽 No-FF<br />
<br />
<br />
마지막으로 git_test_second.txt를 수정 후 커밋하면서 시나리오를 완료했다.

![git2-12-v9.jpg]({{site.baseurl}}/images/git2-12-v9.jpg)<br />
v9 커밋<br />
<br />
<br />
## 깃 로그

![git2-concl.jpg]({{site.baseurl}}/images/git2-concl.jpg)<br />
<br />
<br />
<br />

## * git rebase 
rebase는 공통조상이 되는 base를 다른 브랜치가 가리키는 지점으로 바꾸는 일입니다. 그러면 base부터 현재 브랜치까지의 변경사항이 다른 브랜치의 앞에 합쳐지게 됩니다.<br />
예를 들어 v7까지 커밋한 후 second 브랜치에서 git rebase master를 실행했다면, v4와 v7이 v6 앞에 위치하게 될 것입니다. <br />
<br />
<br />
## git revert 
revert는 특정 커밋의 변경사항을 취소한다. 커밋 이력은 남아있고 취소사항이 추가적으로 커밋된다.<br />
예를 들어 v9까지 커밋한 후, git revert e778ef(v3커밋)을 실행했다면 v3 커밋에서 일어난 변경사항은 취소되고, 'Revert "add git_test2.txt"'라는 메시지의 커밋이 추가될 것이다.<br />
<br />
<br />
## git reset
reset은 head 포인터를 지정한 커밋으로 재설정한다.<br />
git reset (옵션) (커밋)에서 옵션에 대한 설명은 다음과 같다: <br />
1. hard: 재설정한 커밋 이후의 모든 이력을 삭제<br />
2. soft: 재설정한 커밋으로 돌아가고 해당하는 인덱스가 남는다<br />
3. mixed(default): 재설정한 커밋으로 돌아가고 해당하는 인덱스는 초기화 된다<br />
예를 들어 v9까지 커밋한 후, git reset --hard 558e9e(v6)를 실행하면 v7에서부터 v9까지의 커밋 이력은 모두 삭제될 것이다.