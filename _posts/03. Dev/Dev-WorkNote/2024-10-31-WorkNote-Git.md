---
title: 자주 활용되는 Git
layout: single
categories: Dev
tags:
  - WorkNote
  - Git
toc: true
toc_sticky: true
toc_label: 목차
author_profile: false
sidebar: 
    nav: "counts"
search: true
use_math: true
---
# Git Note




## Commit clean history
commit 후 env와 같은 보안에 위반되는 내용 발견 시 특정 commit 내용을 삭제하거나 브랜치 자체를 갈아끼우는 방법으로 history를 제거할 수 있다.
<h3> 방법 1 : 특정 commit 내용 삭제 </h3>
```shell

```

<h3> 방법 2 : history 전체 삭제 </h3>
```shell
git checkout --orphan new-main  # 기존 브랜치 내역이 없는 새로운 브랜치 생성
git add -A  # 모든 파일을 새 브랜치에 추가
git commit -m "Initialize repository with a clean commit"  # 새로운 커밋 생성
git branch -D main  # 기존 main 브랜치 삭제
git branch -m main  # 새 브랜치 이름을 main으로 변경
git push -f origin main
```

<br>

# Git 사용 시 발생하는 Error 정리
## 1) push 자격증명 Error
로컬에서 push 사용 시 발생할 수 있는 에러이다.
<div class="notice--danger">
<h4> 자격증명 에러 </h4>
  PS C:\github_blog\MeteorNote.github.io> git push -f origin main
  remote: Permission to MeteorNote/MeteorNote.github.io.git denied to [타계정].
  fatal: unable to access 'https://github.com/MeteorNote/MeteorNote.github.io.git/': The requested URL returned error: 403
</div>

<div class="notice--success">
  Windows 자격 증명 관리자에서 GitHub 관련 자격 증명 삭제
</div>

## 2) Github Desktop : Fetch 수행 후 충돌 문제
  모든 Commit clean history 를 진행할 때 Github Desktop을 사용하는 경우 아래와 같은 문구가 나오는데 이는 commit 기록을 제거하는 취지와는 다른 문구이며 강제 push를 하여 clean을 할거면 Git Bash를 사용해야한다. 해당 문구에 대한 해결 방법은 아래와 같다.
<div class="notice--danger">
<h4> Github Desktop 사용 시 </h4>
  Desktop is unable to push commits to this branch because there are commits on the remote that are not present on your local branch. Fetch these new commits before pushing in order to reconcile then with your local commits
</div>

<div class="notice--info">
<h4> Fetch 수행 후 충돌 해결 </h4>
<ul>
  <li> 원격 브랜치에 있는 커밋 내역이 로컬 브랜치와 다르기 때문에 발생하며 GitHub Desktop은 기본적으로 원격 저장소와 로컬 저장소가 일치하지 않을 경우 푸시를 차단한다. </li>
  <li> Fetch 버튼을 클릭하여 원격 저장소의 최신 커밋을 로컬로 가져온다. </li>
  <li> 원격 저장소와 로컬 저장소 간의 변경 사항이 표시되면 충돌이 발생한 파일들을 GitHub Desktop의 지시에 따라 수정하고 충돌을 해결한 뒤에 commit한다. </li>
  <li> 충돌을 해결한 후 Push 버튼을 클릭하여 변경 사항을 원격 저장소에 push한다. </li>
</ul>
</div>
Fetch 후 충돌 해결은 커밋 내역을 그대로 두고 로컬과 원격 간의 차이를 조정하여 푸시하는 방법이기 때문에 기존 커밋 내역을 삭제하지 않고 유지하는 것이 된다. 위에 작성한 모든 commit history를 제거하는 과정에서 발생하는 Warning 문구이지만 모든 commit history를 삭제하는 것과는 목적이 다르다.