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
<br />
<br />
<br />
## 시작

- ## git init
깃 저장소 생성

![git-02-init.jpg]({{site.baseurl}}/images/git-02-init.jpg)
<br />
<br />
- ## git clone (주소)
저장소를 복제해 가져온다

![git-03-clone.jpg]({{site.baseurl}}/images/git-03-clone.jpg)
<br />
<br />
<br />
## 변경사항

- ## git add (파일)
파일이나 디렉터리를 인덱스에 올린다

![git-05-mv.jpg]({{site.baseurl}}/images/git-05-mv.jpg)
<br />
<br />
- ## git mv (파일) 
파일, 디렉터리, 심볼릭 링크를 이동

![vim-01-insert.jpg]({{site.baseurl}}/images/vim-01-insert.jpg)
<br />
<br />
- ## git reset (옵션) (커밋)
헤드를 이전 커밋으로 재설정한다 <br />1. hard: 재설정한 커밋 이후의 모든 이력을 삭제 <br />2. soft: 재설정한 커밋으로 돌아가고 해당하는 인덱스가 남는다 <br />3. mixed(default): 재설정한 커밋으로 돌아가고 해당하는 인덱스는 초기화 된다

![git-06-reset.jpg]({{site.baseurl}}/images/git-06-reset.jpg)
<br />
<br />
- ## git revert (커밋)
특정 커밋을 삭제한다. 그 커밋 이력은 남아있고 취소사항이 추가 커밋된다.

![git-07-revert.jpg]({{site.baseurl}}/images/git-07-revert.jpg)
<br />
<br />
- ## git rm (파일) 
파일이나 디렉토리를 작업 디렉토리와 인덱스에서 삭제

![git-08-rm.jpg]({{site.baseurl}}/images/git-08-rm.jpg)
<br />
![git-09-rm2.jpg]({{site.baseurl}}/images/git-09-rm2.jpg)
<br />
<br />
<br />
## 커밋 내역/상태 확인

- ## git log (옵션) 또는 git log (파일)
커밋 로그 확인 <br />옵션 <br />-숫자: 최근 몇 개를 보일건지 <br />-p: 차이점 표시

![git-10-log.jpg]({{site.baseurl}}/images/git-10-log.jpg)
<br />
![git-11-log-2-p.jpg]({{site.baseurl}}/images/git-11-log-2-p.jpg)
<br />
<br />
- ## git status 
작업 디렉터리에서 어떤 파일이 트래킹 되고 안 되는지, 스테이지 됐는지 안 됐는지 확인

![git-12-status.jpg]({{site.baseurl}}/images/git-12-status.jpg)
<br />
<br />
- ## git show
커밋 정보 확인 (최근커밋/특정커밋/HEAD 확인 가능)

![git-13-show.jpg]({{site.baseurl}}/images/git-13-show.jpg)
<br />
<br />
<br />
## 커밋 작업

브랜치: 격리된 환경에서 따로 작업을 진행해야 할 때 브랜치를 만든다.<br />
나중에 master 브랜치와 병합하면 된다.

- ## git commit -m "(설명)"
커밋 실행 (최종 확정)

![git-13-commit.jpg]({{site.baseurl}}/images/git-13-commit.jpg)
<br />
<br />
- ## git branch (이름)
새 브랜치 생성 <br />(git branch만 입력하면 브랜치 목록을 볼 수 있다. * 표시된 것이 현재 브랜치)

![git-14-branch.jpg]({{site.baseurl}}/images/git-14-branch.jpg)
<br />
<br />
- ## git checkout (브랜치)
해당 브랜치로 전환

![git-16-merge.jpg]({{site.baseurl}}/images/git-16-merge.jpg)
<br />
<br />
- ## git merge (브랜치)
커밋간, 브랜치간, 또는 커밋과 작업 내용 사이의 바뀐 점 확인 <br />git diff (브랜치1) (브랜치2) : 두 브랜치의 차이점 <br />git diff (커밋1) (커밋2) : 두 커밋의 차이점 <br />git diff HEAD HEAD^ : 마지막 커밋과 그 이전 커밋의 차이점 <br />git diff : 스테이지 되지않은 변경 사항만 확인

![git-17-diff.jpg]({{site.baseurl}}/images/git-17-diff.jpg)
<br />
<br />
- ## git tag (태그)
참고할 수 있는 꼬리표를 붙임

![git-18-tag.jpg]({{site.baseurl}}/images/git-18-tag.jpg)
<br />
<br />
<br />
## 원격 저장소 작업

- ## git fetch (저장소) 
원격 저장소에서 파일 가져오기 

![git-19-fetch.jpg]({{site.baseurl}}/images/git-19-fetch.jpg)
<br />
<br />
- ## git pull (저장소/브랜치)
원격 저장소나 브랜치에서 파일을 가져오고 병합

![git-20-pull.jpg]({{site.baseurl}}/images/git-20-pull.jpg)
<br />
<br />
- ## git push (저장소)
로컬 저장소의 HEAD의 변경 사항을 원격 저장소로 올림

![git-21-push.jpg]({{site.baseurl}}/images/git-21-push.jpg)
<br />
<br />
<br />