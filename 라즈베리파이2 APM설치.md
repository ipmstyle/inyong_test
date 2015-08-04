# 라즈베리파이2 APM설치
### 여기서는 root를 예로 든다.

##### apt 최신 업데이트
```sh
$ apt-get update
```
##### 아파치 서버 설치
```sh
$ apt-get install apache2
```
##### MySQL설치
```sh
$ apt-get install mysql-server mysql-client
```
##### php설치
```sh
$ apt-get install php5 php5-common libapache2-mod-php5
```
##### 웹 서버에 올릴 디렉토리 생성
```sh
$ mkdir /home/pi/www
```
##### 디렉토리 권한 설정
```sh
$ chmod 755 /home/pi/www
```
##### php파일 하나를 생성
```sh
$ nano /home/pi/www/index.php
```
##### index.php
```sh
<? 
    phpinfo(); 
?>
```

##### 웹서버 디렉토리 설정 변경
```sh
$ cd /etc/apache2/sites-enabled
$ nano 000-default
```
##### 000-default
```sh
$ <VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /home/pi/www
    <Directory />
         Options FollowSymLinks
         AllowOverride None
    </Directory>
    <Directory /home/pi/www/>
         Options Indexes FollowSymLinks MultiViews
         AllowOverride None
         Order allow,deny
         allow from all
    </Directory>
```
중간의 var/www로 되 있는 두 부분을 '/home/pi/www' 과 '/home/pi/www/'로 바꿔준다.(두번째껀 뒤에 '/'가 붙는것을 주의할것!
##### 아파치 서버 재시작
```sh
<? 
$ /etc/init.d/apache2 restart 
?>
```
##### apm설치완료
웹 주소창에 'http://localhost/index.php'
입력해서 php 정보화면이 뜨면 설치완료.
이제 /home/pi/www에다가 php파일 올리면 됩니다.
