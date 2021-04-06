## Dockerfile
```
FROM <이미지:태그>   // 베이스 이미지
MAINTAINER <이름>   // 관리자 정보
COPY <복사할 파일 경로> <이미지 파일이 위치할 절대경로>   // 이미지로 파일, 디렉토리 복사 (URL 불가), 압축 해제X
ADD <복사할 파일 경로> <이미지 파일이 위치할 경로>    // COPY와 유사하나, 상대경로 지정가능 (URL 가능), 압축 해제o

RUN <명령어>   // 이미지가 만들어지는 과정에서 실행될 명령어
RUN mkdir -p /app 
RUN apt-get install vim

CMD <명령어>   // 컨테이너가 실행될 때 실행되는 명령어
