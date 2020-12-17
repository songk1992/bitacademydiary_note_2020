


1. 의존 라이브러리 설치

yum install -y
gcc-c++
libtermcap-devel
gdbm-devel
zlib*
libxml*
freetype*
libpng*
libjpeg*
iconv
flex
gmp
nucurses-devel
cmake.x86_64
libaio

2. 계정 생성
groupadd mysql
useradd -M -g mysql mysql

3. 소스 다운로드
wget https://downloads.mariadb.org/interstitial/
