# Git 사용법
> 필자는 Git Bash를 이용

> git 설치가 완료되었다는 전제 하에 진행.


### git version 확인
 설치가 잘 되었다면 git 버전이 잘 출력된다.
```git
  $ git --version
```
### 디렉터리 생성

```
  $ mkdir [디렉터리명]
  $ cd [생성한 디렉터리명]
```

### git 초기화하기

 디렉터리 안의 내용을 살펴보기 위해 먼저 'ls -la'로 확인.
```
  $ ls -la
```
 디렉터리에 저장소를 만들기 위해 'git init'을 입력해 깃을 사용할 수 있도록 초기화.
```
  $ git init
```
 다시 'ls -al'을 통해서 디렉터리 안의 내용을 살펴보면 '.git'이라는 디렉터리가 생성되어 있다.
```
  $ ls -al
```
* 'ls -al'과 'ls -la' 는 같은 명령어이다. 둘다 상관 없음.

> 여기서 윈도우 탐색기나 맥Finder에서 생성한 디렉토리를 열었을 때, .git디렉터리가 화면에 나타나지 않을 수 있다.
> 
> 이는 사용자가 실수로 .git디렉터리를 지우지 않도록 숨어 있기 때문이다.

> **윈도우 탐색기** 에서는 [보기]탭에서 '숨긴 항목'을 체크
> 
> **맥** 에서는 Shift + Commend + . 을 눌러서 숨은 파일을 확인해보자.

### 스테이지와 커밋
> **작업트리**
  
**작업트리(working tree)** 는 파일 수정, 저장 등의 작업을 하는 디렉터리. (=작업 디렉터리(working directory))

> **스테이지**

**스테이지(stage)** 는 버전으로 만든 파일이 대기하는 곳 (=스테이징 영역(staging area))

> **저장소**

**저장소(repository)** 는 스테이지에서 대기하고 있던 파일들을 버전으로 만들어 저장하는 곳

* 여기서 스테이지와 저장소는 눈에 보이지 않는다. 깃 초기화시 만들어지는 .git 디렉터리 안에 숨은 파일로 존재.

>> 예를 들어서 'hello.txt'파일을 수정하고 저장하면, 이 파일은 작업트리에 존재. 이 파일을 버전으로 만들고 싶다면 스테이지에 넣고, 깃에게 커밋(commit)하면 된다. 

### 작업트리에서 vim으로 문서 수정하기

#### git 상태 확인
```
  $ git status
```
* On branch main : 현재 main 브랜치에 있다.
* No commits yet : 아직 커밋한 파일이 없다.
* nothing to commit : 현재 커밋할 파일이 없다.

#### vim으로 파일 생성하기
```
  $ vim [파일명]
```
> vim화면이 나타나면 'ㅣ' 또는 'A'를 눌러 입력 모드로 변환.
> 파일 작성
> 'Esc'를 눌러 ex모드로 돌아간 다음, ':wq'를 입력하고 'Enter'

'git status'를 통해 보면, 현재 untracked file (아직 한번도 버전 관리하지 않은 파일) 확인가능
```
  $ git status
```

#### 수정한 파일 스테이징 -git add
```
  $ git add [파일명]
```

#### 스테이지에 올라온 파일 커밋 - git commit
```
  $ git commit -m "[커밋메시지]"
```

#### 방금 커밋한 메시지 수정하기 - git commit --amend
방금 커밋한 메시지를 수정하고 싶다면 아래 코드를 사용하면 된다.
'ㅣ' 또는 'A'를 눌러 입력모드 전환 후 수정.

'Esc'를 누르고 ':wq'를 입력해 ex모드로 전환 후 저장하면 수정완료.
```
  $ git commit --amend
```

#### 버전이 제대로 만들어졌는지 확인 - git log
```
  $ git log
```

#### 스테이징과 커밋 한번에 처리하기 - git commit -am
```
  $ git commit -am "[커밋메시지]"
```
* 단 이 방법은 한 번이라도 커밋한 적 있는 파일을 다시 커밋할 때만 사용할 수 있다.
* 한 번도 커밋한 적 없다면, git add 후 git commit 

'git commit -a-m 사용해도 결과는 같다.
```
  $ git commit -a-m "[커밋메시지]"
```

#### 변경사항 확인하기 -git diff
방금 수정한 파일(작업트리에 있는 파일)과 저장소에 있는 파일의 차이점 찾기
```
  $ git diff
```

#### 작업트리에서 수정한 파일 되돌리기 - git checkout
파일을 수정한 뒤 파일이 정상동작하지 않는 등의 이유로 수정 내용을 취소하고, 가장 최신 버전 상태로 되돌릴 때 사용.
```
  $ git checkout -- [파일명]
```
* 단 checkout으로 수정한 파일을 되돌리면 그 파일은 다시 복구할 수 없으니 주의.

#### 스테이징 되돌리기 - git reset HEAD 파일명
수정한 파일을 이미 스테이징했다면, 스테이징을 취소하고 checkout 해야 한다. 이 경우 사용.
```
  $ git reset HEAD [파일명]
```

#### 최신 커밋 되돌리기 - git reset HEAD^
수정된 파일을 스테이징하고 커밋까지 했을 때, 가장 마지막에 한 커밋을 취소
```
  $ git reset HEAD^
```
최근 커밋 하기 전 상태로 작업 트리 되돌리기.
```
  $ git reset --soft HEAD^
```
최근 커밋과 스테이징을 하기 전 상태로 작업 트리 되돌리기. 옵션없이 git reset 명령 사용 시 이 옵션 기본 적용
```
  $ git reset --mixed HEAD^
```
최근 커밋과 스테이징, 파일 수정을 하기 전 상태로 작업 트리 되돌리기. --> 이 옵션 사용 시 되돌린 내용 복구 불가
```
  $ git reset --hard HEAD^
```

#### 특정 커밋으로 되돌리기 - git reset 커밋 해시
최신 버전이 아니라 특정 버전으로 되돌리고, 그 이후 버전을 삭제할 경우 사용
```
  $ git reset [커밋해시]
```
* 위 git reset 명령 옵션 사용 가능 (--hard, --soft, --mixed)

#### 커밋 삭제하지 않고 되돌리기 - git revert
나중에 사용할 것을 대비해 커밋을 되돌리더라도 소한 커밋을 남겨두어야 할 때 사용
```
  $ git revert [커밋해시]
```
### GitHub에서 협업하기

#### GitHub과 연결
```git
  $ git clone [github 주소]
```

#### GitHub에서 파일 가져오기
협업 시에는 첫번째 커밋이 아니라면, push하기 전 최신 커밋을 pull한 후 push 해야 한다. 
```
  $ git pull
```
#### 브랜치 체크아웃
브랜치 변경 시 사용
```
  $ git checkout [브랜치명]
```

#### 브랜치 생성 및 체크아웃 한꺼번에
브랜치 생성과 체크아웃을 한번에 하고 싶을 때 사용.
```
  $ git checkout -b [브랜치명]
```
* 만일 checkout -b [브랜치명]을 실행했을 때, 이미 해당 브랜치가 존재한다면 생성하지 않고 해당 브랜치로 체크아웃 된다.


#### GitHub으로 파일 올리기
```
  $ git push origin [브랜치명]
```
