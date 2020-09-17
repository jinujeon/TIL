# git시작



## git 사전 준비

> git을 사용하기 전에 커밋을 남기는 사람에 대한 정보를 설정(최초)

```bash
$ git config --global user.name '내 username을 입력'
$ git config --global user.email '내 email을 입력'
```

* 추후에 commit을 하면, 작성한 사람(author)로 저장된다.

* email 정보는 github에 등록된 이메일로 설정을 하는것을 추천(잔디밭)

* 절정 내용을 확인하기 위해서는 아래의 명령어를 입력한다.

* ```bash
  $ git config --global -l
  # 결과-----------------------------------------
  filter.lfs.required=true
  filter.lfs.clean=git-lfs clean -- %f
  filter.lfs.smudge=git-lfs smudge -- %f
  filter.lfs.process=git-lfs filter-process
  user.name=ruldy99
  user.email=ruldy99@naver.com
  ```

  > git bahs 설치 [링크](https://gitforwindows.org/)



## 기초 흐름

### 0. 저장소 설정

```bash
$ git init
# 결과-----------------------------------------
Initialized empty Git repository in C:/Users/ruldy/Desktop/gittest2/.git/
```

* git 설정을 원하는 폴더에 들어가서 위 명령어 실행.
* git 저장소를 만들게 되면 해당 디렉토리 내에 `.git/` 폴더가 생성
* git bash내에서는 `(master)`로 현재 작업중인 브랜치가 표기된다.

### 1. `add`

> 커밋을 위한 파일 목록(staging area)

```bash
$ git add . 			# 현재 디렉토리의 모든 파일 및 폴더
$ git add a.txt			# 특정 파일
$ git add md-images/	# 특정 폴더
$ git status
# 결과-----------------------------------------

# add . 후 status-----------------------------
# master 브랜치에 있다.
On branch master

No commits yet
# 커밋이 될 변경사항들(changes)
# Staging area 단계
Changes to be committed:
	# unstage를 하기 위해선 아래의 .... 명령어를 입력
	# working directory 단계
  (use "git rm --cached <file>..." to unstage)
        new file:   a.txt

# add 하지 않고 status-------------------------
On branch master

No commits yet
# add 되었지만 commit되지 않은 파일 목록
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   a.txt
# 아직 add되지 않은 파일목록(트래킹 되지 않은 파일들)
# git으로 관리하지 않기 때문에 아직 working directory단계
Untracked files:
	# 커밋이 될 것에 추가하려면 아래의 ... 명령어를 입력
  (use "git add <file>..." to include in what will be committed)
        b.txt

```

### 2.`commit`

> 버전을 기록(스냅샷)

```bash
$ git commit -m '커밋내용 메세지 입력'
# 결과-----------------------------------------
[master (root-commit) 3bf34e5] First commit
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 a.txt
 create mode 100644 b.txt

```

* 커밋 메시지는 현재 버전을 알 수 있도록 명확하게 작성한다.
* 커밋 이력을 남기기 위해서는 아래의 명령어를 입력한다.

```bash
$ git log
# 결과-----------------------------------------
commit 3bf34e582c249a750ffa48bff533655f7acfd136 (HEAD -> master)
Author: ruldy99 <ruldy99@naver.com>
Date:   Thu Sep 17 13:25:16 2020 +0900

    First commit

$ git log -1			# 최근 한개의 버전
$ git log --oneline		# 한줄로 간단하게 표현
# 결과-----------------------------------------
3bf34e5 (HEAD -> master) First commit

$ git log -1 --oneline	
```

## status - 상태 확인

> git에 대한 모든 정보는 status에서 확인할 수 있다.

```bash
$ git status
```



## 원격 저장소 활용하기

> 원격 저장소를 제공하는 서비스는 github, gitlab, bitbucket등이 있다.

### 1. 원격 저장소 설정하기

```bash
$ git remote add origin {url}
```

* 깃아, 원격(remote(내가 쓸 것은 github))저장소로 추가해줘(add). origin이라는 이름으로 URL을

* 원격저장소 삭제를 위해서는 아래 명령어 사용

  ```bash
  $ git remote rm origin
  ```

  

### 2. 원격 저장소 확인하기

```bash
$ git remote -v
# 결과-----------------------------------------
origin  https://github.com/ruldy99/git-test.git (fetch)
origin  https://github.com/ruldy99/git-test.git (push)
```

### 3. push

```bash
$ git push origin master
# 결과-----------------------------------------
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 209 bytes | 209.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/ruldy99/git-test.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

* origin 원격저장소의 master 브랜치로 push