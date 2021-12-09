# gitea 설치
> rocky linux 서버에서 gitea를 설치하고 실행하는법을 알아보겠습니다.

## 목차
1. 시스템 설정
2. git 설정 및 디렉토리 설정
3. Mariadb 설치 및 설정 
4. gitea 설치

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
