# docker 명령어

## 이미지 관련 명령어
### 이미지 검색
- `docker search`
### 이미지 다운로드
- `docker pull centos:latest`
- `docker pull centos:7`
- `-a` 모든 버전 다운로드
### 다운로드된 이미지 목록 조회 
- `docker image ls`
- `docker images`
### 이미지 삭제
- `docker image rm`
- `ex) docker image rm webserver:1.0`
## 컨테이너 관련 명령어
### 컨테이너 생성
- `docker create`
### 컨테이너 구동
- `docker start`
### 컨테이너 중지
- `docker stop`
### 컨테이너 삭제
- `docker rm`
- 컨테이너만 삭제되고 이미지는 삭제되지 않음
- 구동되고있는 컨테이너는 -f 옵션을 사용해 강제로 종료 + 
### 컨테이너에 표준 입력(stdin)과 표준 출력(stdout)을 연결
- `docker attach`
### 컨테이너 생성 및  구동
- `docker run`
- 먼저 로컬에 이미지가 있는지 확인하고 없으면 자동으로 `pull` 하여 생성
- `docker run`이라는 명령어에는 `docker pull`, `docker create`, `docker start`, `docker attach`(`-it` 옵션을 사용했다면)이 포함  
- `docker run -dit --name "test" centos /bin/cal`
- `-it` : 현재 터미널이나 콘솔에 결과를 출력- 
-  `--rm` : docker stop 하면 컨테이너 삭제
-  `--name "<NAME>"` :컨테이너 이름
-  `centos` : 이미지 이름
-  `/bin/cal` : 컨테이너에서 실행하는 커맨드
- `-d` 컨테이너를 백그라운드에서 계속 실행하겠다
- `-p` 컨테이너의 내부 포트와 호스트 컴퓨터의 포트를 연결하기 하기 위한 명령어로 호스트와 컨테이너의 포트를 적어주면 된다. `docker run -d -p 8080:80 httpd`, `-p [Host]:[Container]`
```
docker run -dit -p 8080:80 httpd --name apache /bin/bash
```

### 컨테이너 로그 확인
- `docker log -f apache`

### 일괄 처리
- windows는 powershell에서만 작동함
#### 모든 컨테이너 정지
- `docker stop $(docker ps -a -q)`
#### 모든 컨테이너 삭제
- `docker rm $(docker ps -a -q)`



#### 모든 이미지 삭제

- `docker rmi $(docker images -q)`



#### Exit 상태의 모든 컨테이너 삭제

`docker rm $(docker ps --filter 'status=exited' -a -q)`

## 잡다한 기술
### 해당 컨테이너의 포트를 확인하는 방법
```
docker port httpd
80/tcp -> 0.0.0.0:8080
```
### 검색
`netstat -ano | findstr :873`
- 각 포트별로 연결된 
```
 TCP    0.0.0.0:873            0.0.0.0:0              LISTENING       328
 TCP    [::]:873               [::]:0                 LISTENING       328
```
`tasklist | findstr 328`
```
rsync.exe                      328 Services                   0      4,880 K

```
