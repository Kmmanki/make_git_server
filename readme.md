## NAS 서버에 Git Server 구축하기 (SSH통신)

NAS에 Git을 구축해야 할 일이 생겼다.
Pc에서 버추얼 박스를 이용해 가상 리눅스를 만들어 테스트를 먼저 진행 하기로 했다.

pc에 버추얼박스와 ubuntu를 설치 

<img width="720" alt="스크린샷 2020-07-29 오전 10 40 48" src="https://user-images.githubusercontent.com/50133267/88746705-1b2e5480-d188-11ea-8942-2b2c4570d43a.png">

pc와 ssh통신을 하기위한 포트 설정 
>버추얼 박스 pc 우클릭 -> 설정 -> 네트워크 -> 고급 -> 포트포워딩 -> ssh를 사용할 포트를 설정 
>즉 ssh 유저명@내아이피:설정포트 를하면 가상 리눅스로 ssh 통신이 연결된다.
추후 ssh git@127.0.0.1:9090로 진행하면 git이란 유저의 이름으로 리눅스와 연결

<img width="678" alt="스크린샷 2020-07-29 오전 10 47 33" src="https://user-images.githubusercontent.com/50133267/88747137-259d1e00-d189-11ea-86b0-88c3be442958.png">

깃을 접속할 때 사용 될 user 생성 
>sudo useradd git 
>이미 테스트 과정에서 만들어 둠

![스크린샷 2020-07-29 오전 10 55 49](https://user-images.githubusercontent.com/50133267/88747598-166aa000-d18a-11ea-8cde-c9aea44ab2eb.png)
