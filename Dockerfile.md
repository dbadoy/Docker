## Dockerfile
```
FROM <이미지:태그>   // 베이스 이미지
MAINTAINER <이름>   // 관리자 정보
COPY <복사할 파일 경로> <이미지 파일이 위치할 절대경로>   // 이미지로 파일, 디렉토리 복사 (URL 불가), 압축 해제X
ADD <복사할 파일 경로> <이미지 파일이 위치할 경로>    // COPY와 유사하나, 상대경로 지정가능 (URL 가능), 압축 해제o
```
```
RUN <명령어>   // 이미지가 만들어지는 과정에서 실행될 명령어

RUN mkdir -p /app 
RUN apt-get install vim
```

```
CMD <명령어>          // 컨테이너가 실행될 때 실행되는 명령어
                     // 여러 개 적어 놓아도 마지막 CMD만 실행됨
                     // 여러 명령어를 사용해야 된다면 run.sh를 만들어 실행
                     // run을 통해 인자값이 전달되면, CMD에 명시된 인자는 무시됨
ENTRYPOINT <명령어>  //  CMD와 유사하나, run을 통해 인자값이 전달돼도 ENTRYPOINT로 지정한 명령어 실행

exam1 - CMD ["echo", "Hello World"]
exam2 - ENTRYPOINT ["echo", "Hello World"]

docker run --it --rm exam1 echo "hi"
--> result : hi

docker run --it --rm exam2 echo "hi"
--> result : Hello World
```

```
WORKDIR <경로>    // COPY, ADD, RUN, CMD 등이 수행될 기본 디렉토리 설정
EXPOSE <포트번호> // 컨테이너와 호스트를 연결할 포트를 지정해주는 명령어
ENV <key>=<value> // RUN, CMD, ENTRYPOINT에서 사용할 환경 변수 지정 명령어, Container에서도 사용 가능 
ARG <key>=<value> // ENV와 유사하나, ARG는 Dockerfile에서만 사용 가능
VOLUME <경로>     // 컨테이너에 외부파일시스템 연결
```

예시 ( hyperledger/fabric/chaincode/Dokerfile ) 
```
ARG GO_VER=1.14.2
ARG ALPINE_VER=3.12

FROM golang:${GO_VER}-alpine${ALPINE_VER}

WORKDIR /go/src/github.com/Hyperledger/fabric-samples/asset-transfer-basic/chaincode-external

COPY ..

RUN go get -d -v ./...
RUN go install -v ./...

EXPOSE 999
CMD ["chaincode-external"]
```
```
