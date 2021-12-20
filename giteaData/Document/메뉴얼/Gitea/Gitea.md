# gitea 설치
> rocky linux 서버에서 gitea를 설치하고 실행하는법을 알아보겠습니다.

## 목차
1. 시스템 설정
2. git 설정 및 디렉토리 설정
3. Mariadb 설치 및 설정 
4. gitea 설치 및 실행
5. gitea 설정

### 1. 시스템 설정
> 시작하기전 필요한 설정을 구성하겠습니다.

```bash
  # yum update
  # yum install wget git nano epel-release
```
yum을 최신 버전으로 업데이트 해주고, wget과 git 등 필요한 라이브러리를 설치합니다.

### 2. git 설정 및 디렉토리 설정
> gitea 구축에 필요한 git을 설정하겠습니다.

```bash
  # useradd git
```
user에 git을 추가해줍니다. 다른 이름으로 설정해도 무관합니다.   
또한 Gitea에서 데이터를 저장할 디렉토리를 만들겠습니다.
```bash
  # mkdir -p /etc/gitea /var/lib/gitea/{custom,data,indexers,public,log}
  # chown git:git /var/lib/gitea/{data,indexers,log}
  # chmod 750 /var/lib/gitea/{data,indexers,log}
  # chown root:git /etc/gitea
  # chmod 770 /etc/gitea
```

### 3. Mariadb 설치 및 설정
> Gitea를 실행하기 위해선 MySQL을 서버에 설치해야 합니다.

```bash
  # yum install mariadb-server
  설치 이후 
  # systemctl enable mariadb
  # systemctl start mariadb
```
해당 부분에서 Failed to start MariaDB database server 에러 발생시 [여기](http://gotopark.blogspot.com/2015/01/centos-7.html)를 참조해주세요.   

그리고 MariaDB의 설정을 하겠습니다.   
루트 암호를 만들고, 테스트 데이터베이스를 제거하고, 익명 사용자를 제거한 후 권한을 다시 로드합니다.
```bash
  # mysql_secure_installation
  
  Enter current password for root (enter for none): Press the [Enter] key on your keyboard. No password is set by default
  Set root password? [Y/n]: Y
  New password: Enter a new password
  Re-enter new password: Repeat the new password
  Remove anonymous users? [Y/n]: Y
  Disallow root login remotely? [Y/n]: N   
  Remove test database and access to it? [Y/n]: Y
  Reload privilege tables now? [Y/n]: Y
```

#### 3-1. Gitea용 DB 생성
```bash
  # mysql -u root -p
  
  mysql> create database gitea;
  mysql> grant all on gitea.* gitea@localhost identified by 'm0d1fyth15';
  mysql> flush privilieges;
  mysql> quit
```
localhost를 서버의 ip로 변경하여 작성합니다. ex) gitea@192.168.0.1

### 4. Gitea 설치 및 실행
> Gitea를 설치하기에 앞서 [여기](https://github.com/go-gitea/gitea/releases)에서 최신 안정 버전을 확인합니다.

```bash
  # export GITEAVER=1.15.7
  작성일자 기준 최신버전입니다.`
  
  # wget https://github.com/go-gitea/gitea/releases/download/v${GITEAVER}/gitea-${GITEAVER}-linux-amd64 -O /usr/local/bin/gitea
  # chmod +x /usr/local/bin/gitea
  # gitea -v
```
wget을 통해 gitea를 다운받고 실행 권한을 부여합니다.   
그리고 이제 Gitea용 systemd 파일을 생성하겠습니다.
```bash 
  # nano /etc/systemd/system/gitea.service
  
  [Unit]
  Description=Gitea
  After=syslog.target
  After=network.target
  After=mariadb.service

  [Service]
  RestartSec=2s
  Type=simple
  User=git
  Group=git
  WorkingDirectory=/var/lib/gitea/
  ExecStart=/usr/local/bin/gitea web -c /etc/gitea/app.ini
  Restart=always
  Environment=USER=git HOME=/home/git GITEA_WORK_DIR=/var/lib/gitea

  [Install]
  WantedBy=multi-user.target
```

```bash
  systemctl daemon-reload
  systemctl start gitea
  systemctl status gitea
```

status 명령어를 입력하면 현재 3000번 포트로 gitea가 실행된것을 확인 할 수 있습니다.   
이후 서버에서 3000번 포트를 허용해주고 url 창에 http://ip:3000/ 을 통해 gitea에 접속이 가능합니다.

### 5. Gitea 설정
![image](https://user-images.githubusercontent.com/69878816/145341646-baaa5b30-31db-4c8b-a6ee-9a698cbed5b1.png)   
이미지와 같이 초기 설정 화면이 나옵니다.   
![image](https://user-images.githubusercontent.com/69878816/145342219-c96697f2-fc8c-4a7d-808d-df6e338216ad.png)   
<mark>이름은 root로 설정합니다</mark>
   
그리고 하단으로 내려와서 ssh와 사용할 포트를 설정합니다.
![image](https://user-images.githubusercontent.com/69878816/145342764-7f939cab-70dc-4598-953c-94063c7b0697.png)
![image](https://user-images.githubusercontent.com/69878816/145342892-6acf4c7d-9573-4d39-aa77-f62a19c7a8ab.png)   

이후 최하단의 Gitea 설치하기를 하고 다시 서버에서 3000번 포트를 닫아줍니다. (포트를 설정한경우)   
그리고 설정한 포트를 서버에서 열어주고 http://ip:설정한 포트/를 통해 gitea에 접속합니다.   

![image](https://user-images.githubusercontent.com/69878816/145344781-0cd29b15-1892-41a0-846b-4c98f73f54ea.png)   
Gitea가 정상 설치되었으며 우측 상단의 회원가입을 통해 로그인을하고 git처럼 사용할 수 있습니다.   

상단에서 했던 초기 설정은 /etc/gitea/app.ini 파일에서 수정할 수 있습니다.

### 참조
1. [Gitea 설치](https://www.linuxcloudvps.com/blog/how-to-install-gitea-on-centos-7/)
2. [초기설정](https://blog.naver.com/PostView.naver?blogId=browniz1004&logNo=221403209991&parentCategoryNo=&categoryNo=&viewDate=&isShowPopularPosts=false&from=postView)