1. 의존 라이브러리 설치
```
yum install -y 

gcc-c++yun
libtermcap-devel
gdbm-devel
zlib*
libxml*
freetype*
libpng*
libjpeg*
glibc
flex
gmp
ncurses-devel
cmake.x86_64
libaio
```

2. 계정 생성
```
groupadd mysql

useradd -M -g mysql mysql
```

3. 소스 다운로드

```
wget https://downloads.mariadb.org/interstitial/mariadb-10.1.38/source/mariadb-10.1.38.tar.gz/from/https%3A//archive.mariadb.org/

mv index.html mariadb-10.1.38.tar.gz

tar xvfz mariadb-10.1.38.tar.gz
```

4. 빌드 
```

cd mariadb-10.1.38 

cmake -DCMAKE_INSTALL_PREFIX=/usr/local/javafullstack/mariadb -DMYSQL_USER=mysql -DMYSQL_TCP_PORT=3307 -DMYSQL_DATADIR=/usr/local/javafullstack/mariadb/data -DMYSQL_UNIX_ADDR=/usr/local/javafullstack/mariadb/tmp/mariadb.sock -DINSTALL_SYSCONFDIR=/usr/local/javafullstack/mariadb/etc -DINSTALL_SYSCONF2DIR=/usr/local/javafullstack/mariadb/etc/my.cnf.d -DDEFAULT_CHARSET=utf8 -DDEFAULT_COLLATION=utf8_general_ci -DWITH_EXTRA_CHARSETS=all -DWITH_ARIA_STORAGE_ENGINE=1 -DWITH_XTRADB_STORAGE_ENGINE=1 -DWITH_ARCHIVE_STORAGE_ENGINE=1 -DWITH_INNOBASE_STORAGE_ENGINE=1 -DWITH_PARTITION_STORAGE_ENGINE=1 -DWITH_BLACKHOLE_STORAGE_ENGINE=1 -DWITH_FEDERATEDX_STORAGE_ENGINE=1 -DWITH_PERFSCHEMA_STORAGE_ENGINE=1 -DWITH_READLINE=1 -DWITH_SSL=bundled -DWITH_ZLIB=system

make && make install
```


5. 설정
5-1 설치 디렉토리 및 파일 권한 변경
```
chown -R mysql:mysql /usr/local/javafullstack/mariadb
```

5-2. 설정파일 /etc로 옮긴다
```
cp -R /usr/local/javafullstack/mariadb/etc/my.cnf.d /etc
```

5-3 기본 데이터베이스 생성
```
/usr/local/javafullstack/mariadb/scripts/mysql_install_db --user=mysql --basedir=/usr/local/javafullstack/mariadb --defaults-file=/usr/local/javafullstack/mariadb/etc/my.cnf --datadir=/usr/local/javafullstack/mariadb/data
```

5-4 tmp 디렉토리 생성
```
# mkdir /usr/local/javafullstack/mariadb/tmp
# chown mysql:mysql /usr/local/javafullstack/mariadb/tmp
```

yes y 치면됨
```
cp: overwrite `/etc/my.cnf.d/tokudb.cnf'? y
cp: overwrite `/etc/my.cnf.d/client.cnf'? y
cp: overwrite `/etc/my.cnf.d/mysql-clients.cnf'? y
cp: overwrite `/etc/my.cnf.d/server.cnf'? y
cp: overwrite `/etc/my.cnf.d/enable_encryption.preset'? y
```

5-5. 서버 실행해보기
# /usr/local/javafullstack/mariadb/bin/mysqld_safe &
# ps -ef | grep mysql

5-6. root 패쓰워드 설정하기
# /usr/local/javafullstack/mariadb/bin/mysqladmin -u root password '비밀번호'

5-7. 접속하기
# /usr/local/javafullstack/mariadb/bin/mysql -p

6. 서비스 등록
#vi /etc/systemd/system/mariadb.service

===========================================================
[Unit]
Description=MariaDB Database Server
After=syslog.target
After=network.target

[Service]
User=mysql
Group=mysql

KillMode=process
KillSignal=SIGTERM
SendSIGKILL=no

LimitNOFILE=infinity
LimitNPROC=4096
LimitCORE=infinity
PermissionsStartOnly=true
PrivateTmp=true
OOMScoreAdjust=-1000
ExecStartPre=sync
ExecStartPre=sysctl -q -w vm.drop_caches=3
ExecStart=/usr/local/javafullstack/mariadb/bin/mysqld --defaults-file=/usr/local/javafullstack/mariadb/etc/my.cnf --plugin-dir=/usr/local/javafullstack/mariadb/lib/plugin --pid-file=/usr/local/javafullstack/mariadb/mysqld.pid
Restart=always
RestartSec=1
TimeoutSec=300

[Install]
WantedBy=multi-user.target
===========================================================

# systemctl enable mariadb
# systemctl status mariadb
# systemctl start mariadb
# systemctl stop mariadb
# systemctl start mariadb

# reboot

7. /usr/local/javafullstack/mariadb/bin 디레토리를 PATH 환경변수 설정
# vi /etc/profile
PATH 변수에 /usr/local/javafullstack/mariadb/bin 추가
===========================================================

# mariadb
export PATH=$PATH:/usr/local/javafullstack/mariadb/bin

===========================================================


8. webdb 데이터베이스 생성
create database webdb;

9. 사용자 생성
create user 'webdb'@'localhost' identified by 'webdb';
create user 'webdb'@'192.168.1.%' identified by 'webdb';

10. 권한부여
grant all privileges on webdb.* to 'webdb'@'localhost';
grant all privileges on webdb.* to 'webdb'@'192.168.1.%';

flush privileges;
flush privileges;
flush privileges;

테스트
```
source /etc/profile
```

```
mysql -p
```

```
show databases;
```


8. 
webdb 생성


```
mysql -u webdb -D webdb -p
```

```
mysql -p
```

```
create database webdb;
create user 'webdb'@'localhost' identified by 'webdb';
grant all privileges on webdb.* to 'webdb'@'localhost';
flush privileges;

create database webdb;
create user 'webdb'@' 192.168.%' identified by 'webdb';
grant all privileges on webdb.* to 'webdb'@'localhost';
flush privileges;
exit
```


window workbench 사용

Setup New Connection
Name : dba
Hostname 192.168.1.12 (리눅스 ifconfig inet)
port : 3307
user name : root
Default Schema : mysql


```

```

```

```

or use https://mariadb.com/resources/blog/installing-mariadb-10-on-centos-7-rhel-7/
