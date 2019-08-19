## 설치
 - 설치시, 에디터를 선택해주면 좋다. 
 - git bash only는 불편해서 2번째꺼 prompt를 선택하는 것이 좋다.

## 개념
 - git server repository <-> local repository < --add, commit- working direcotry
 - 서버와 로컬을 연결하는 것 : git remote add origin
 - origin 붙은 것은 다 서버이다.

## bash
 - /는 루트 디렉토리 cd /   cd /c   cd /c/worspace
 - pwd : 현재디렉토리 경로
 - ls
 - alias ll='ls -al'

## 설정
 - git config --list : 설정 리스트 확인
    - git config --list | grep "user.name" : | grep을 통해 해당사항만 필터링 해서 볼 수 있다. 
 - git config user.name : 설정된 이름 확인 : “ChoJaeSeong” 
    - --global : 모든 디렉토리에 이 설정을 박아버리겠다.
    - git config --global user.name <github-name> : 깃허브 주소에 보이는 주소 
 - git config user.email : 설정 이메일 확인 : “tingstyle1@gmail.com”
    - git config --global user.email <email> : 프로필에 확인되는이메일 
 - cat ~/.gitconfig : 좀 더 정리되서 설정파일
    - ~은 내 홈디렉토리다.  / 바로 아래에 .gitconfig 파일이 있고, 설정시 이 파일이 변경된다. 

## 로컬저장소 만들어 서버저장소와 연결하기
1. 해당폴더에서 git init : 로컬저장소가 생김
2. .gitignore 파일 만들기 - 약속된 파일명
 - 파일명을 그냥 엔터로 그냥 입력해주면 된다.
3. git add --all : add --all은 .gitignore빼고 올라간다.
 - 파일한개 : git add  *.py
 - add다음에 git status를 확인하자.
3. git status : 뭐가 add됬는지를 확인한다. 
4. git commit -am "first commit"
 - -am : 혹시나 몰라서 a dd하고, m: add한 것을 몽땅 
 - 만약, 같은파일을 수정하고 또 commit해야한다면, add는 할필요없다. 이미 ㄹ올라가 있다. 
5. git remote add origin <git-remote-url>
 - 로컬의 메인줄기가 : origin master이며, 이것도 branch이다.
 - 서버의 메인줄기는 remote origin master라고 한다.
 - git branch : 현재의 branch들을 볼 수 있다. 

6. git push -u origin master
 - 최초에만 -u origin master 를 붙혀준다.
 - -u : 위로 올린다. up
 - origin master : 메인줄기에다가 올린다.

7. git pull
 - 현재 원격저장소에 readme.MD가 있어서 sync가 안맞아서 push가 안된다.

8. git push -fu origin master
 - -fu : 강제로 올린다. 

9. git clone <https>
 - 다른pc에서 작업할때, 해당 디렉토리로 이동 후 가져온다. 
 - 폴더 자체가 내려온다.
 - pull 후에, 작업후 push 한다.
 - remote add origin은 최초의 컴퓨터에서만 하고.. 다음 작업장에서는 git clone만 하면 알아서 다 연결된다.


## 참고
touch 파일명 : 파일생성
mkdir : 디렉토리 생성
git log
git status  # staging 상태 확인

## git log
 - git log
 - :이 보이면 q누르면 나와진다.
 - git log --graph --oneline
    : 그래프로, 한개당 1줄로 로그를 보여줘
    - HEAD : 마지막 커밋한 소스
    - 각 revision id가 보인다. 이것으로 돌아갈 수 있다.
    - commit하고 확인한다.

## reset과 revert 
 - git reset --hard: 돌아감
    - git reset --hard/soft/mixed
    - hard : 완전히 다돌린다. 정말 위험함. 동료가 수정한 것도 없어진다. 정말 reset을 해야한다면, hard를 써야한다. 
 - git revert : 취소인데, 완전히 취소는 아니다. 
     - history내역이 쌓이면서, 돌아간다.
 - github에서 commit메세지 클릭시 소스리뷰가 가능해진다. 
    - +버튼으로 바로 주석을 달 수 도 있다.  우상단에 show commnet 체크를 풀면 안보인다.
 - github에서 파일클릭후 history버튼 > git log와 비슷, revision(돌아가고자하는 id)가 보인다. 

## git lens 설치
 - 5번째 아이콘 extensions > git검색 > gitlens 설치

## 돌아가기 실습
1. 커맨드 창 reset ( 거의 안쓴다 )
 - git reset cdef65f(git log의 revision아이디 복붙)
    : git log를 확인하면, history는 돌아갔지만, 실제 소스는 그대로다.
    : 옵션을 주지 않은 reset은 hard도 soft도 아니다. 
    : reset은 흔적이 없어지면서 돌아간다. 
 - git commit -am "rollback 222" 
   : reset한 것을 commit다시 해줘야한다. 
 - git push
    : 서버 레파지토리랑 다른 내용을,, git push하면 reject이 뜬다. 
    : 이 때는 강제로 push해야한다.
 - git push -fu origin master
 - git push origin +master 
    : 2개가 똑같다.

2. 커맨드창 revert (흔적남기고 돌아가기) -> conflict가 기본적으로 난다. 
 - git revert cdef65f
    : conflict = 현재의 revision과 돌아가는 revision 사이의   1개의 파일의 소스가 달른 것. 
  - vscode에서 파일을 보면, conflict 현재변경사항수락/수신변경사항수락/두 변경사항 모두수락의 3가지가 있다.
    : 대부분 두 변경사항 모두수락을 이용해서 수정하여 저장한다.

3. 커맨드창 reset hard
 - git log 로 revision번호 확인후 
 - git reset --hard ed6904f
 - git log --graph --oneline
    : 기록 모두 삭제됨..
    : mixed와 다르게 기록삭제 + 파일소스도 변함

## 다른사람이 수정 & 나도 다르게 수정한 상태에서 pull reject처리후 commit -> push
1. 깃허브에서 연필버튼으로 수정해서 다른사람이 수정한 것5555을 가정해보자.
2. 나도 같은라인을 로컬에서 7777수정해보자.
3. 로컬777 을 add  /  commit   /  push
4. git pull...하라고하면서 reject당한다 
    - git pull -> 서버에 다른 소스가 있다.
5. git pull 
     - 나도 수정했으니, 가져올 때 conflict가 난다. 
     - 직접 그 파일로가서 수정하자.
6. git commit -am " "
    - pull과정에서 conflict를 냈다면, conflict해결 후 commit, push하면 잘된다.
7. git push


master : 메인줄기 - 서비스 되고 있는 소스
 - br1 : 브랜치 1 - 브랜치를 따는 이유? 각 사람들이 수정하고, 서비스로 나가지 않는 소스 
 - br2 : 브랜치 2 - 어떠한 기능추가가 됬으면, 메인에 집어놓고 브랜치를 없앤다. 

## branch
 - git branch : 로컬 branch 확인
    - git branch -r : 서버에 있는 브랜치 확인 
    - gir branch -a  : 로컬, 서버 브랜치 모두 확인 
 - git branch 브랜치명 : branch생성
 - git checkout 브랜치명 : branch왔다 갔다하는 것
 - git push origin 브랜치명 
    : branch가 없으면, 그냥 git push만 해줬었다. 서버의 근원에 브랜치를 추가해준다. 
 - git branch -d 브랜치명 : 로컬의 branch 삭제 
    - git push --delete origin 브랜치명 : 서버의 branch 삭제 
 - 서버의 특정 브랜치 가져오기
    - git checkout -t origin/브랜치명 

## branch를 merge하기
 1. git checkout xxx(master, br2): 일단 수정된 파일을 받을 수신branch로 이동한다. 
 2. git merge br1 : br1의 코드를 가져온다. 
 3. conflict이 날 경우, git status를 통해 충돌내역을 확인한다. 


## branch 실습해보기
1. git add -all   &   git commit -am " " : checkout전 commit해놓고 branch 옮기기 
2. git branch 확인
3. git branch br1 : 작업할 브랜치로 생성
4. git checkout br1 : 작업할 브랜치로 이동
5. br1상태에서 소스(a.py) 수정한 뒤, add/commit
6. git branch -a(or -r) : push전에 서버에도 해당 branch가 있나 확인
7. git push origin br1 : 서버에 br1이라는 브랜치를 생성해서 push 
8. git branch master 
 - master로 돌아온 순간 수정파일이 그대로 있음.
9. git diff br1 을 통해, 현재(master)와 가져올브랜치(br1)의 차이점을 항상 본다.
 - 빨간색 : 현재의 입장에서 없다
 - 초록색 : 추가됬다. 
10. git diff br1 a.py 를 통해, 특정파일만 차이점을 본다. 
11. git checkout -p br1 a.py
 - br1브랜치의 a.py를 나한테 patch시킨다는 의미이다. 브랜치 것을 그대로 가져와서 바꾼다.
 - 다 가져오고 싶으면, 파일명 없이 git checkout -p br1
 - 물음표창이 뜨면, a을 해주면 되는데 여기서는 y를 해보자.
12. git add a.py & git status
  - master에서 patch한 br1의 파일을 commit해줘야한다.
13. git commit -am "br1 patch"
14. git push origin master

## 다른사람이 push한 최근 파일 받기
1. a가 br1을 통해 a.py를 수정
2. a가 br1으로 서버에 push  ( 집에서 해당 branch를 가져와 계속 작업하기 위함 )
3. a가 master로 이동 후 br1에서 작업한 a.py의 diff 확인 후 patch
4. a가 master에 push 
5. c가 br3을 통해 c.py를 수정중에, 최신 a.py을 받고 싶음
6. c가 master에서 서버의 최근a.py를 pull
 - 주의! pull은 서버의 master만 온다. 
7. c가 br3에서 master것을 patch

## 집에서 서버의 특정 branch 받아서 작업하기
pull은 master것만 가져온다.
1. git branch -r(-a) 을 통해서, 서버의 branch들을 확인한다.
2. git checkout -t origin/브랜치명
 - 확인한 branch에서 복붙해서 긁어온다 .
 - 해당 branch만 pull해올 수 있다.
 - 또다른방법 
    - git pull origin br1 : master건, br1이건, 서버br1 -> 로컬br1으로 
3. 다시 받은 br1을 수정 한뒤 add/commit후 , git push origin br1으로 push 

## github에서 협업하기
1. 해당 레파지토리 > collaborators > 초대
2. 초대받은 사용자는 처음에 프로젝트가 안보인다.
    - 만약, 파일 통채로 받아보고 싶다면, fork를 통해 가져와야한다.
    - fork의 특징 : 포크받은 repository의 url은, 최초 repository랑 url이 다르다. 
3. 원본url로 git clone을 받아야한다. 

## 정리
1. working directory에서 git init
 - .git폴더가 생기는데 local repository가 된다.
 - origin 은 server repository를 말하고, origin master는 서버의 메인줄기.
 - git push -u origin master를 통해 최초에 뚫기만 해주면 된다. 다음부터는 git push만 해주면 알아서 origin master에 push된다.
 - wd와 local repository 사이에는 stage가 있다. 
 - add시 stage로 넘어간다. git add --all or git add 파일명, 확인은 git status
 - commit은 이 stage에 대기중인 파일이 local repostory로 간다.

2. .git 라는 local rep에는 
 - branch가 최초에 master가 있다. 
 - 여기서 branch를 딸 수 있다. 복사는 아니지만 master의 파일들이 연결된다.
 - br1, b2에서 a.py을 수정한다면, 각 branch마다 파일이 달라진다. 각각이 stage와 repository를 가진다. 
 - 각각의 br1, br2에서 add, commit하면 각각의 stage, repository로 갈 것이다.

3. branch를 master이외에 파는 순간 git push만 해서는 안된다.
 - push할 branch를 정해주어야한다. 
 - git push origin 브랜치명(master, br1, br2) -> 서브에도 똑같은 branch가 존재할 것이다.

4. master와 br1만 있다면?
 - git checkout br1 을 통해 branch 위치를 바꾼다.
 - wd와 에디터에서는 branch중 1개만 보인다. 그래서 commit한 뒤 branch를 바꿔야한다. 

5. 다른브랜치의 파일을 가져올 때
 - git diff 비교할branch명 파일명 : 차이점을 확인한다.
 - git checkout -p branch명 파일명 : 그파일로 patch해서 가져온다.(merge나 똑같은 말)


 ## 처음부터 다시 정리
 1. 현재 github과 내가 작업중인 폴더가 따로 존재하는 상태
  - git config
  - git init
  - git add commit
  - git remote add origin url
  - git push -u origin master
    : 다음부터는 git push

2. 만약 새로운PC에서 다른사람이 작업해야한다면?
 - 작업폴더로 간다음, git clone url : 폴더채로 가져오니 조심
 - 상위폴더에서 git init하면 안된다. 

3. 서버에 누가 수정해놓은 상태에서, 내껏을 올리고 싶다.
 - git pull을 먼저하고, 생기는 conflict를 처리한다.
 - git add commit 후 git push

4. branch
 - 회사에서 br1 branch를 딴다.
    - git branch br1
    - git commit -am (in master)
    - git checkout br1
    - 수정
    - git add, commit
    - git push origin br1 (서버에 br1으로 push) -> 서버에 br1 브랜치가 생긴다.

 - 집에서 
    - git pull 해보니까, master만 내려온다.
    - git pull origin br1 해보니까, 안내려온다. 왜냐면... local에 br1이 없는 상태이기 때문에
        - pull이라는 것은, local에 있는 branch것을 가져오는 것이다.
        - 이미 존재하는 branch에 pull받아서, diff도 비교한다.
        - pull에는 conflict까지 확인한다는 의미이다.
    - git checkout -t origin/브랜치명 : 서버branch만 따와서 branch를 생성한다.
        - (git branch -r을통해 확인한 서버branch)
    - git pull origin br1 : 이제서야 local에서도 br1이 존재하는 상태로서, pull해온다.

 - master에 br1을 합칠 때
    - git checkout matser
    - git diff br1 : 차이점 확인
        - git checkout -p br1 파일명 : 특정 파일만 받아올 때
        - git merge br1 : br1전체를 가져올 때 
        - conflict나면 처리
    - git add, commit 
    - git push origin master

5. 다른사람들은 pull하면 master를 받기 때문에, 작업완료된 것을 가져온다.
