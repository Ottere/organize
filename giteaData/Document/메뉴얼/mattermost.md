[공통] mattermost 설치 가이드 라인
======================
## 목차
- [시스템 업데이트]
- [비교 PostgreSQL VS Mariadb]
- [PostgreSQL 데이터베이스 설치]
    1. [PostgreSQL 데이터베이스 설치](#2-postgresql-install)
- [mariaDB 설치]
    1. [mariaDB 설치](#2-mariadb-install)
- [Mattermost 서버 설치]
    1. [Mattermost 서버 설치](#3-mattermost-install)

## 시작하기전 알아야 할것
### 1. 데이터베이스는 PostgreSQL과 mariaDB중 하나를 골라 '하나'만 설치한다

## 참조
1. [mattermost 공식 홈페이지](https://docs.mattermost.com/install/install-rhel-8.html#installing-mattermost-server)
***
# 1.시스템 업데이트

```
1.1. 시스템이 업데이트되었는지 확인하십시오.
sudo yum -y update

1.2. nano, wget 설치
yum install nano
yum install wget
```

# 비교 PostgreSQL VS Mariadb
## PostgreSQL, Mariadb 공통 장점:
### 1. 영구적인 무료 데이터베이스
### 2. 윈도우 기반으로 설치가 가능
### 3. 엔지니어가 없이 간편히 설치 및 유지보수가 가능
### 4. 대용량 자료를 취급가능
***
![스크린샷1](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdkIQiJ%2FbtqENAQMqt7%2FJzP5qkUgCpMHTDk5mmUgd0%2Fimg.png)
## PostgreSQL 특장점
### 1. 라이선스에 대한 비용문제가 전혀 없음
### 2. 오래된 오픈소스의 안정성
### 3. 여전히 발전중인 데이터베이스
### 4. mattermost 에서 정식 지원(설정방법,기초설정등이 나와있어 찾아보기 쉬움)
### 5. 일본 및 해외에서는 국가기관에서도 사용하고, Skype, 인스타그램 등에서도 PostgreSQL을 사용
> 참조:     [PostgreSQL을 선택한 이유](https://codecamp.tistory.com/2)

## 단점
### 1. 읽기가 많은 간단한 작업의 경우 PostgreSQL은 일반적으로 MySQL과 같은 다른 RDBMS보다 성능이 떨어진다.

> 참조:     [[DBMS] SQLite vs MySQL vs PostgreSql: 관계형 DB 시스템의 비교. - (3) PostgreSql](https://smoh.tistory.com/370)

***

![스크린샷1](https://t1.daumcdn.net/cfile/tistory/2366E84358EA426C1D)
## MariaDB 특장점
### 1. MySQL보다 가볍고 빠름
### 2. 본질적으로 사용 가능한 모든 기능 사용을 포함하여 MariaDB를 무료로 사용할 수 있음
### 3.  사용자 또는 사용자가 동시에 사용할 수 있음
> 참조:     [MariaDB : 정의, 기능, 강점 및 약점](https://altitudetvm.com/ko/komputer/1481-mariadb-pengertian-fungsi-kelebihan-dan-kekurangan.html)

## 단점
### mattermost의 페이지에선 정식으로 지원하지 않음(자료가 부족함)
### 서버가 수용 할 수있는 용량을 초과하는 경우 데이터 저장에 제한
> 참조:     [MariaDB : 정의, 기능, 강점 및 약점](https://altitudetvm.com/ko/komputer/1481-mariadb-pengertian-fungsi-kelebihan-dan-kekurangan.html)
***
# 2.(선택사항)PostgreSQL 데이터베이스 설치
## 2 postgresql install
### 1. 데이터베이스를 호스팅할 서버에 로그인하고 터미널 창을 엽니다.
### 2. PostgreSQL을 설치합니다.
```
a.mattermost 업데이트
rpm -Uvh https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm

b. mattermost 10버전 다운로드
sudo yum install postgresql10-server postgresql10-contrib

Is this ok [y/d/N]: y
이 버전이 PostgreSQL 버전 10 이상인지 확인합니다

psql -V
```
### 만약 버전이 10이상이 아니면 
1. [이곳에서 확인](https://www.postgresql.org/download/linux/redhat/ )
***

### 3. 데이터베이스를 초기화합니다.
```
sudo postgresql-10-setup initdb
```

###  4.부팅 시 PostgreSQL을 시작하도록 설정합니다.
```
sudo systemctl enable postgresql-10
```
### 5.PostgreSQL 서버를 시작합니다.
```
sudo systemctl start postgresql-10
```
### 6. 설치 중에 생성된 postgres Linux 사용자 계정으로 전환 합니다.
```
sudo -iu postgres
```

### 7. PostgreSQL 대화형 터미널을 시작합니다.
```
psql
```

### 8. Mattermost 데이터베이스를 생성합니다.
```
postgres=# CREATE DATABASE mattermost WITH ENCODING 'UTF8' LC_COLLATE='en_US.UTF-8' LC_CTYPE='en_US.UTF-8' TEMPLATE=template0;
```

### 9. Mattermost 사용자를 만듭니다 .
```
postgres=# CREATE USER mmuser WITH PASSWORD 'mmuser-password';

*참고 mmuser은 유저이름 , mmuser-password는 패스워드 비밀번호 자유롭게 생성
```

### 10. 사용자에게 Mattermost 데이터베이스에 대한 액세스 권한을 부여합니다.
```
postgres=# GRANT ALL PRIVILEGES ON DATABASE mattermost to mmuser;
```
### 11. PostgreSQL 대화형 터미널을 종료합니다.
```
postgres=# \q
```

### 12. 포스트그레스 계정 에서 로그아웃 합니다.
```
exit
```

### 13 .Mattermost 서버가 데이터베이스와 통신할 수 있도록 파일 을 수정 합니다.

```
Mattermost 서버와 데이터베이스가 동일한 시스템에 있는 경우:
a. /var/lib/pgsql/10/data/pg_hba.conf 텍스트 편집기에서 루트로 엽니다 .

nano /var/lib/pgsql/10/data/pg_hba.conf

b. 다음 행을 찾으십시오.

local   all             all                        peer

host    all             all         ::1/128        ident

c. peer와 ident를 trust로 변경합니다.
local   all             all                        trust

host    all             all         ::1/128        trust

Mattermost 서버와 데이터베이스가 다른 시스템에 있는 경우:
a.  /var/lib/pgsql/data/pg_hba.conf 텍스트 편집기에서 루트로 엽니다
b. 파일 끝에 다음 줄을 추가합니다. 여기서 {mattermost-server-IP} 는 Mattermost 서버가 포함된 시스템의 IP 주소입니다.

host all all {mattermost-server-IP}/32 md5
```
### 14. PostgreSQL 다시 로드
```
sudo systemctl reload postgresql-10
```

### 15. mmuser 사용자와 연결할 수 있는지 확인합니다 .

```
a. Mattermost 서버와 데이터베이스가 동일한 시스템에 있는 경우 다음 명령을 사용합니다.

--username과 --password는 9번에서 설정한 이름과 패스워드 입니다

psql --dbname=mattermost --username=mmuser --password

b. Mattermost 서버가 다른 컴퓨터에 있는 경우 해당 컴퓨터에 로그인하고 다음 명령을 사용합니다.

psql --host={postgres-server-IP} --dbname=mattermost --username=mmuser --password

연결 된지 확인후 \q로 나가기
```
### 명령을 사용하려면 PostgreSQL 클라이언트 소프트웨어를 설치해야 할 수 있습니다.
### PostgreSQL 대화형 터미널이 시작됩니다. PostgreSQL 대화형 터미널을 종료하려면 를 입력 \q하고 Enter 키를 누릅니다 .
***
# 2.(선택사항)mariadb 데이터베이스 설치
## 2 mariadb install
### 1. Mariadb 저장소 생성 및 접속
```
nano /etc/yum.repos.d/MariaDB.repo
```

###  2.아래 내용 기입

```
[mariadb]  
name=MariaDB
baseurl=http://yum.mariadb.org/10.5/centos7-amd64 
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB 
gpgcheck=1
```
### 3. Mariadb install
```
yum install MariaDB-server MariaDB-client
```

### 4. Mariadb 자동시작
```
sudo systemctl enable --now mariadb
```
### 5. Mariadb 설정
```
sudo mysql_secure_installation

나중에 다시 설정할수 있으니 간단하게 하고 다음단계 진행

```
### 6. Mattermost에 대한 데이터베이스와 사용자를 생성

```
mysql -u root -p
비밀번호는 5번 Mariadb 설정한 곳에서 설정한 비밀번호
```

### 접속후 아래 내용 한줄씩 기입 mattermost는 아이디 StrOngPass는 비밀번호

```
CREATE DATABASE mattermost;

GRANT ALL PRIVILEGES ON mattermost.* TO mattermost@localhost IDENTIFIED BY 'Str0ngPass';

FLUSH PRIVILEGES;

QUIT;
```

# 3.mattermost 서버 설치
## 3 mattermost install
### 64비트 시스템에 Mattermost 서버를 설치합니다.

### 1. Mattermost Server를 호스팅할 서버에 로그인하고 터미널 창을 엽니다.
### 2. 다운로드 합니다
```
wget https://releases.mattermost.com/6.1.0/mattermost-team-6.1.0-linux-amd64.tar.gz
```

### 3. 압축을 풀어줍니다
```
tar -xvzf *.gz
```

### 4. 압축을 푼 파일을 /opt디렉터리로 이동시킵니다
```
sudo mv mattermost /opt
```

### 5. 파일의 저장소 디렉토리를 만듭니다.
```
sudo mkdir /opt/mattermost/data

스토리지 디렉토리에는 사용자가 Mattermost에 게시하는 모든 파일과 이미지가 포함되므로 드라이브가 업로드된 파일 및 이미지의 예상 수를 저장할 만큼 충분히 큰지 확인해야 합니다.
```

### 6. mattermost이 서비스를 실행할 시스템 사용자 및 그룹을 설정하고 소유권 및 권한을 설정합니다.

```
a. sudo useradd -d /opt/mattermost -U -M mattermost

b. sudo chown -R mattermost:mattermost /opt/mattermost

c. sudo chmod -R g+w /opt/mattermost
```

### 7. 파일에서 데이터베이스 드라이버를 설정합니다 /opt/mattermost/config/config.json. 텍스트 편집기에서 루트 로 파일을 열고 다음과 같이 변경합니다.

```
PostgreSQL을 사용하는 경우:

sudo nano /opt/mattermost/config/config.json

1. sqlSettings를 찾은다음 
2 "DriverName"을 "postgres"로 변경
3.DataSource에 아래 코드 삽입

"postgres://mmuser:<mmuser-password>@<host-name-or-IP>:5432/mattermost?sslmode=disable&connect_timeout=10"

<mmuser-password>는 사용자 만들었을때 만들었던 비밀번호 예)mmuser-password

동일 기계 설치의 경우 <host-name-or-IP>를 localhost 또는 127.0.0.1 로 바꿉니다
-----------------------------------------------------------------------------
mariaDB 사용하는 경우:

sudo nano /opt/mattermost/config/config.json

1. sqlSettings를 찾은다음 
2 "DriverName"을 "mysql"로 변경
3.DataSource에 아래 코드 삽입

"mattermost:Str0ngPass@tcp(localhost:3306)/mattermost?charset=utf8mb4,utf8\u0026readTimeout=30s\u0026writeTimeout=30s"

```

### 8. Mattermost 서버를 테스트하여 모든 것이 제대로 작동하는지 확인하십시오.
```
디렉토리 이동:

cd /opt/mattermost

사용자로 Mattermost 서버 시작:
sudo -u mattermost ./bin/mattermost

터미널 창에서 CTRL+C를 눌러 서버를 중지할 수 있습니다
```

### 10. Mattermost 프로세스의 감독을 처리 하는 데몬 을 사용하도록 Mattermost를 설정합니다 .
```
a. Mattermost 구성 파일 생성:

sudo touch /etc/systemd/system/mattermost.service

sudo nano /etc/systemd/system/mattermost.service

b.(postgresql 경우) 텍스트 편집기에서 구성 파일을 열고 다음 줄을 파일에 복사합니다.

[Unit]
Description=Mattermost
After=syslog.target network.target postgresql.service

[Service]
Type=notify
WorkingDirectory=/opt/mattermost
User=mattermost
ExecStart=/opt/mattermost/bin/mattermost
PIDFile=/var/spool/mattermost/pid/master.pid
TimeoutStartSec=3600
KillMode=mixed
LimitNOFILE=49152

[Install]
WantedBy=multi-user.target

b.(mariadb 경우) 텍스트 편집기에서 구성 파일을 열고 다음 줄을 파일에 복사합니다.

[Unit]
Description=Mattermost
After=syslog.target network.target mariadb.service

[Service]
Type=notify
WorkingDirectory=/opt/mattermost
User=mattermost
ExecStart=/opt/mattermost/bin/mattermost
PIDFile=/var/spool/mattermost/pid/master.pid
TimeoutStartSec=3600
KillMode=mixed
LimitNOFILE=49152

[Install]
WantedBy=multi-user.target

c. 서비스 파일 권한을 설정합니다.

sudo chmod 644 /etc/systemd/system/mattermost.service

d. 시스템 서비스를 다시 로드합니다.

sudo systemctl daemon-reload

e. Mattermost를 부팅 시 시작하도록 설정합니다.

sudo systemctl enable mattermost
```
### 11 . Mattermost 서버를 시작합니다.
```
sudo systemctl start mattermost
```

### Mattermost가 실행 중인지 확인합니다.
```
curl http://localhost:8065

Mattermost 서버에서 반환한 HTML이 표시되어야 합니다.
```

## 접속하기
```
(서버ip):8065로 접속
```

## 4. 선택사항
### 데이터베이스와 Mattermost 앱 서버에 다른 서버를 사용하는 경우 PostgreSQL이 할당된 모든 IP 주소에서 수신 대기하도록 허용할 수 있습니다

```
1. config 파일을 열고
nano /var/lib/pgsql/data/postgresql.conf

2. listen_addresses를 찾은 다음에
#listen_addresses = 'localhost'

3.행의 주석을 제거하고 localhost를 *로 변경합니다 
listen_addresses = '*'

4. PostgreSQL 다시 시작
sudo systemctl restart postgresql
```
