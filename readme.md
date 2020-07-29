## NAS 서버에 Git Server 구축하기 (SSH통신)

NAS에 Git을 구축해야 할 일이 생겼다.
Pc에서 버추얼 박스를 이용해 가상 리눅스를 만들어 테스트를 먼저 진행 하기로 했다.

>pc에 버추얼박스와 ubuntu를 설치 

<img width="720" alt="스크린샷 2020-07-29 오전 10 40 48" src="https://user-images.githubusercontent.com/50133267/88746705-1b2e5480-d188-11ea-8942-2b2c4570d43a.png">

>pc와 ssh통신을 하기위한 포트 설정 
버추얼 박스 pc 우클릭 -> 설정 -> 네트워크 -> 고급 -> 포트포워딩 -> ssh를 사용할 포트를 설정 
즉 ssh 유저명@내아이피:설정포트 를하면 가상 리눅스로 ssh 통신이 연결된다.
추후 ssh git@127.0.0.1:9090로 진행하면 git이란 유저의 이름으로 리눅스와 연결

<img width="678" alt="스크린샷 2020-07-29 오전 10 47 33" src="https://user-images.githubusercontent.com/50133267/88747137-259d1e00-d189-11ea-86b0-88c3be442958.png">

>깃을 접속할 때 사용 될 user 생성 
터미널 접속해서
sudo useradd git 
이미 테스트 과정에서 만들어 둠

![스크린샷 2020-07-29 오전 10 55 49](https://user-images.githubusercontent.com/50133267/88747598-166aa000-d18a-11ea-8cde-c9aea44ab2eb.png)


>git을 인스톨 해야한다.
sudo add-apt-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get install git-core
위 명령어를 통해 깃을 설치한다.

git version
깃 설치 확인 

<img width="887" alt="스크린샷 2020-07-29 오전 11 11 08" src="https://user-images.githubusercontent.com/50133267/88748551-4450e400-d18c-11ea-9a80-2cd5ea460119.png">

> git Repository 만들기
su git 
cd ~
mkdir test.git

깃 디렉토리 생성

<img width="892" alt="스크린샷 2020-07-29 오전 11 16 24" src="https://user-images.githubusercontent.com/50133267/88748831-f8526f00-d18c-11ea-9eff-a6713db12845.png">

cd test.git
git init --bare --shared

<img width="895" alt="스크린샷 2020-07-29 오전 11 18 21" src="https://user-images.githubusercontent.com/50133267/88748960-3fd8fb00-d18d-11ea-8dac-18c249243821.png">

깃 저장소가 초기호 된 것을 확인 할 수 있다.

>클론 받아보기
내 pc에서 클론을 받아보자
다운 받을 디렉토리로 이동 한 뒤  
git clone ssh://git@127.0.0.1:9090/git/home/test.git

pingerprint 어쩌구 나오면서 클론이 안된다면 ssh git@127.0.0.1:9090으로 한번 정상 접근한 뒤 다시 진행해보자


![스크린샷 2020-07-29 오전 11 23 41](https://user-images.githubusercontent.com/50133267/88749376-1ec4da00-d18e-11ea-9edf-71c3bee517a6.png)

정상적으로 클론을 받으 것을 확인했다.

>푸쉬 후 다시 클론 받아보기
디렉토리에 접근하여 파일을 하나 만든 뒤 푸쉬해보자
test 폴더에 파일을 하나 만들었다면
git add *
git commit -m "test commit"
git push origin master

![스크린샷 2020-07-29 오전 11 30 04](https://user-images.githubusercontent.com/50133267/88749731-dfe35400-d18e-11ea-9f9b-3324ef4e9789.png)

>재대로 푸쉬 되었는지 확인하기 위해 내 pc에 있던 test 디렉토리를 삭제 한 뒤 다시 클론 받기

![스크린샷 2020-07-29 오전 11 33 12](https://user-images.githubusercontent.com/50133267/88749919-508a7080-d18f-11ea-9ea9-e9610d7bf740.png)

깃에서 클론 받을 디렉토리에 내가 만들었던 doc 파일이 들어있는 것을 확인 할 수 있었다.

추가적으로 접근 시 비밀번호를 계속하여 적는 것이 불편하다면 클라이언트의 RSA키를 서버에 등록하면 된다.

