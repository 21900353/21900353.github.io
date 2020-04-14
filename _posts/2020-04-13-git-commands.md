---
layout: post
title: vim 명령어 연습/정리
published: true
---
# Git Command 정리

git은 세 단계를 통해 관리된다.
1. 작업 디렉토리: 실제 파일
2. 인덱스: 최종화 하기 전 준비 영역 (staging area라고도 한다)
3. 헤드: 최종 확정본

## 사용자 설정

- ## git config --global user.name "(이름)" <br />git config --global user.email "(메일주소)"
사용자 이름/메일주소 설정

![git-01-config.jpg]({{site.baseurl}}/images/git-01-config.jpg)

사용자 이름과 메일주소를 "Byun Sangjin"/"21900353......"로 한 것을 볼 수 있다.
<br />
<br />
<br />
## 시작

- ## git init
깃 저장소 생성

![git-02-init.jpg]({{site.baseurl}}/images/git-02-init.jpg)

저장소가 재생성 되었다는 메시지가 나왔다 (이미 생성된 저장소였기 때문)
<br />
<br />
- ## git clone (주소)
저장소를 복제해 가져온다

![git-03-clone.jpg]({{site.baseurl}}/images/git-03-clone.jpg)

다른 디렉터리에서 git clone을 실행하자 원격 저장소가 복제되었다
<br />
<br />
<br />
## 변경사항

- ## git add (파일)
파일이나 디렉터리를 인덱스에 올린다

![git-05-mv.jpg]({{site.baseurl}}/images/git-05-mv.jpg)

git_test.c 를 만들고 add 했다. git status의 "new file: git_test.c"라는 메시지는 파일이 잘 추가되었음을 알려준다. 
<br />
<br />
- ## git mv (파일) 
파일, 디렉터리, 심볼릭 링크를 이동

![vim-05-mv.jpg]({{site.baseurl}}/images/vim-05-mv.jpg)

git_test.c 파일을 git_test_dir라는 디렉터리로 이동시켰다. git status에서 "renamed: git_test.c -> git_test_dir/git_test.c"라는 메시지를 확인할 수 있다 (파일경로 앞에 git_test_dir/가 붙었기 때문에 결국 rename 결과가 이동한 것과 같다).
<br />
<br />
- ## git reset (옵션) (커밋)
헤드를 이전 커밋으로 재설정한다 <br />1. hard: 재설정한 커밋 이후의 모든 이력을 삭제 <br />2. soft: 재설정한 커밋으로 돌아가고 해당하는 인덱스가 남는다 <br />3. mixed(default): 재설정한 커밋으로 돌아가고 해당하는 인덱스는 초기화 된다

![git-06-reset.jpg]({{site.baseurl}}/images/git-06-reset.jpg)

사진에서는 git reset --hard HEAD^를 실행했다. HEAD 직전의 커밋으로 재설정되었다. 
<br />
<br />
- ## git revert (커밋)
특정 커밋을 삭제한다. 그 커밋 이력은 남아있고 취소사항이 추가 커밋된다.

![git-07-revert.jpg]({{site.baseurl}}/images/git-07-revert.jpg)

커밋 'e801610'을 revert 한 결과이다. "Revert "deleted git_test.c"" 했다는 커밋이 추가되었다.
<br />
<br />
- ## git rm (파일) 
파일이나 디렉토리를 작업 디렉토리와 인덱스에서 삭제

![git-08-rm.jpg]({{site.baseurl}}/images/git-08-rm.jpg)
stats.txt를 삭제했다.

![git-09-rm2.jpg]({{site.baseurl}}/images/git-09-rm2.jpg)
git diff --staged에서 파일이 삭제됐음을 확인할 수 있다. 
<br />
<br />
<br />
## 커밋 내역/상태 확인

- ## git log (옵션) 또는 git log (파일)
커밋 로그 확인 <br />옵션 <br />-숫자: 최근 몇 개를 보일건지 <br />-p: 차이점 표시

![git-10-log.jpg]({{site.baseurl}}/images/git-10-log.jpg)

git log만 실행한 결과

![git-11-log-2-p.jpg]({{site.baseurl}}/images/git-11-log-2-p.jpg)

git log -p -2 (차이점 표시 + 2줄만 표시) 실행 결과
<br />
<br />
- ## git status 
작업 디렉터리에서 어떤 파일이 트래킹 되고 안 되는지, 스테이지 됐는지 안 됐는지 확인

![git-12-status.jpg]({{site.baseurl}}/images/git-12-status.jpg)

git status에서 stats.txt 파일이 삭제되었고, 트래킹 되지 않는 파일들이 2 개 있는 걸 확인했다.
<br />
<br />
- ## git show
커밋 정보 확인 (최근커밋/특정커밋/HEAD 확인 가능)

![git-13-show.jpg]({{site.baseurl}}/images/git-13-show.jpg)

최근 커밋인 c74577f을 확인할 수 있다.
<br />
<br />
<br />
## 커밋 작업

브랜치: 격리된 환경에서 따로 작업을 진행해야 할 때 브랜치를 만든다.<br />
나중에 master 브랜치와 병합하면 된다.

- ## git commit -m "(설명)"
커밋 실행 (최종 확정)

![git-13-commit.jpg]({{site.baseurl}}/images/git-13-commit.jpg)

저장소를 만들고 파일 추가 후 커밋하는 상황이다. 여기에서는 "first commit"이라는 설명을 붙여 커밋하였다.
<br />
<br />
- ## git branch (이름)
새 브랜치 생성 <br />(git branch만 입력하면 브랜치 목록을 볼 수 있다. * 표시된 것이 현재 브랜치)

![git-14-branch.jpg]({{site.baseurl}}/images/git-14-branch.jpg)

test_branch라는 브랜치를 만들었다. git branch로 확인하니 현재 master 브랜치에 있고 그 아래 test_branch가 있다.
<br />
<br />
- ## git checkout (브랜치)
해당 브랜치로 전환

![git-15-checkout.jpg]({{site.baseurl}}/images/git-15-checkout.jpg)

test_branch 생성 후 git checkout test_branch를 실행했다. 'test_branch'로 스위치 되었다는 메시지를 확인했다. 
<br />
<br />
- ## git merge (브랜치)
커밋간, 브랜치간, 또는 커밋과 작업 내용 사이의 바뀐 점 확인 <br />git diff (브랜치1) (브랜치2) : 두 브랜치의 차이점 <br />git diff (커밋1) (커밋2) : 두 커밋의 차이점 <br />git diff HEAD HEAD^ : 마지막 커밋과 그 이전 커밋의 차이점 <br />git diff : 스테이지 되지않은 변경 사항만 확인


![git-16-merge.jpg]({{site.baseurl}}/images/git-16-merge.jpg)

test_branch에서 stats.txt를 수정하고 커밋했다. 그 다음 master 브랜치로 전환하고 git merge test_branch 했다. 그 결과 master 브랜치에서 stats.txt 파일이 바뀌었다는 것을 확인할 수 있다. 
<br />
<br />
- ## git diff
파일이나 커밋간 차이점을 확인

![git-17-diff.jpg]({{site.baseurl}}/images/git-17-diff.jpg)

git diff을 실행하니, git_test.c 파일에 printf("Hello World!");가 추가된 것을 확인할 수 있다.
<br />
<br />
- ## git tag (태그)
참고할 수 있는 꼬리표를 붙임

![git-18-tag.jpg]({{site.baseurl}}/images/git-18-tag.jpg)

CRUD 라는 태그를 추가했다.
<br />
<br />
<br />
## 원격 저장소 작업

- ## git fetch (저장소) 
원격 저장소에서 파일 가져오기 

![git-19-fetch.jpg]({{site.baseurl}}/images/git-19-fetch.jpg)

GitHub 저장소를 가져왔다. HEAD가 FETCH_HEAD로 전환되었다 (외부 저장소에서 무엇이 fetch 되었는지 알기 위함이다).
<br />
<br />
- ## git pull (저장소/브랜치)
원격 저장소나 브랜치에서 파일을 가져오고 병합

![git-20-pull.jpg]({{site.baseurl}}/images/git-20-pull.jpg)

같은 GitHub 저장소를 pull 했더니 이미 최신이라는 메시지가 나온다.
<br />
<br />
- ## git push (저장소)
로컬 저장소의 HEAD의 변경 사항을 원격 저장소로 올림

![git-21-push.jpg]({{site.baseurl}}/images/git-21-push.jpg)

저장소를 초기화하고 파일 추가 후 커밋까지 한 상황이다. git push origin master를 실행해서 origin(GitHub 저장소)의 master 브랜치로 푸쉬했다. 
<br />
