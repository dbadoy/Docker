## Image
Docker Hub - https://hub.docker.com/

```
$ docker search <Image name> // Docker Hub
$ docker search ubuntu

$ docker search -f "stars=3" hyperledger
$ docker search --filter=stars=3 hyperledger
// 필터링 [ stars (int) / is-automated (bool) / is-official (bool) ]
$ docker search --limit=5 ubuntu
// 결과 개수 지정 ( default = 25 )
```
```
$ docker pull <Image name>:<Tag>
$ docker pull ubuntu:16.09  // or latest 

//Tag 생략시 latest 
$ docker pull -a ubuntu
// ubuntu 모든 태그 이미지 다운로드
```
```
$ docker images
$ docker image ls

$ docker images -a 
$ docker images --digests

$ docker images -q
// 이미지 ID만 표시 

$ docker images --format "{{.ID}}: {{.Respository}}"
// 선택 출력 
```
```
$ docker run <Option> <Container name> <Imagename> <shell>

-d 데몬모드 / 백그라운드

--device=[]:[] 
--device="/home/user/myData:/home/data"  호스트 /home/user/myData 디렉터리를 컨테이너 /home/data 와 연결

-e, --env 컨테이너 환경 변수 설정 ( 설정값, 비밀번호 ... )
-e MYSQL_ROOT_PASSWORD=mypassword

--expose 컨테이너 포트를 호스트와 연결, 외부노출 x
--expose="8080"

--link=[] 컨테이너끼리 연결
--link="db:db" ( 컨테이너 이름:별칭 )

-p, --publish 컨테이너의 특정 포트 외부 노출
-p 80:80  ( 호스트 포트:컨테이너 포트 )
          ( IP:호스트 포트:컨테이너 포트)
  

-i, -t 실행된 bash shell에 입력 및 출력 설정 ( i - 입력 t - 출력 )
--name 컨테이너의 이름 지정 . 없을시 임의 지정

$ docker run -i -t --name test ubuntu /bin/bash
$ docker run -d -p 80:80 nginx:latest
```

```
$ docker rmi <Image name>:<Tag>

전부 삭제
$ docker rm `sudo docker images -aq`
$ docker rm $(sudo docker images -aq)

-f 강제 삭제 
```

## 참고
Link : http://pyrasis.com/book/DockerForTheReallyImpatient/Chapter20/28

