Docker 기본 사용법. ( 강의 생활코딩 ) 

Docker 공식 홈페이지 : https://www.docker.com
				https://hub.docker.com

도움 사이트 : http://pyrasis.com/Docker/Docker-HOWTO#section-4

가장 빨리만나는 Docker  : http://pyrasis.com/docker.html
		       예제파일 : https://github.com/pyrasis/dockerbook

terminal 에서 
명령어 docker version 입력  제대로 설치가 되었는지 확인 
설치를 하였지만 version 정보가 나오지 않는다면. Exit  이후 다시 docker 입력

명령어 docker images 입력 하면 
현재 image로 저장된 목록 확인가능

명령어 docker pull ubuntu:14.04  입력하면
우분투 버전 14.04를 이미지로 넣을수 있음

어떠한 버전들이 있는지 확인하고 싶다면
명령어 docker search ubuntu 치면
우분투에 관해 올라온 이미지들을 확인 가능
이중에서 앞에 개인이름이 없는 것들이 도커에서 지정한 공식적인 이미지

이렇게 보는것이 헤깔리다면  https://hub.docker.com 에서 ubuntu 검색 후 tag에 들어가서 확인가능

도커에는 이미지와 컨테이너가있음
이미지는 일종의 실행파일
컨테이너는 이미지를 실행한 상태(프로세스개념)

명령어 docker run    ( 설치된 운영체제를 부팅하는 개념 )
	  docker run -i -t ubuntu:14.04 /bin/bash
          ( -i interactive의 약자  사용자가 입출력을 할수있는 상태 -t 는 sudo tty 가상터미널환경을 에뮬레이션해주겠다.). 
          ( 일반적으로 i와 t 옵션을 주면된다 )
	 ( bash 위에서 작업을 하게된다 )

실행명령 이후에 ls를 쳐보면 가상환경으로 들어와서 개별적으로 가상공간이 생긴것을 확인? 할수있다.
명령어 ps ax

컨테이너 안은 독립적인 공간이기때문에  바깥공간에서 설치한 예를들어 git 같은것도 개별적으로 필요하다면 설치해주어야한다.

명령어 exit 입력 후 컨테이너를 빠져나와서 명령어 docker ps -a를 쳐보면 실행중이거나 종료된 컨테이너들을 확인할 수 있다.

이름을 따로 지정해주지않으면 도커에서 자동으로 이름을 생성해준다.

명령어 docker start 이미지이름  을 쳐도 컨테이너 실행이 된다. 


명령어 docker run 을 하면 실행한동시에 컨테이너 안으로 들어가고
명령어 docker start 의 경우에는 실행만 한 상태이다. 
명령어 attach 를 치고 엔터를 두번 치면 컨테이너 안으로 들어간다. 

컨테이너에 접속 상태에서 종료하지않고 빠져나오려면 단축키 ^pq 를 누르면 실행상태에서 컨테이너를 빠져나온다.

명령어 docker stop 이미지이름 을 치면  컨테이너를 정지한다.

이미지를 삭제하고싶다면 docker rm 이미지이름(컨테이너) 을 치면 된다.
명령어 docker rmi 이미지ID

명령어 rm 과 rmi 의 차이는 rm은 해당 하나의 컨테이너 이미지를 삭제한다면 rmi는 관련된 예를들어 ubuntu의 모든 이미지를 삭제한다.

컨테이너 안에서 파일을 만들고 설치한것은 컨테이너 레벨에서 저장이 된다.

명령어 docker pull nginx:latest  -> 최신버전 받아짐

명령어 run -d --name hello-nginx nginx:latest 
-> 이미지이름 변경 

호스트의 포트와 도커에서 이미지의 포트가 중복되었을때  충돌이 날수 있음

run -d --name hello-nginx -p 8000:80 nginx:latest   
-> 포트번호 옵션을 설정해줄 수 있다.

명령어 exec 
-> 메인프로세스  메인실행파일 이외에 다른 실행파일을 실행할 수 있도록 해준다.

명령어 docker exec hello touch /hello.txt

