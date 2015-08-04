# MySQL 외부 연동 방법 - 특정 사용자 계정의 외부 접속 허용하기
### 여기서는 root를 예로 든다.

##### 1.MySQL 접속 후 mysql database 선택
```sh
$ mysql -u root -p
패스워드 입력
mysql> use mysql;
```
##### 2.user 테이블 살펴보기
```sh
mysql> select host, user, password from user;
```

root의 host 값들은 localhost, 127.0.0.1 등으로 기본 등록 되어 있지만 외부접속을 나타내는 값이 없다. 외부접속을 특정 IP로만 하게 할 수도 있고 전체적으로 접속하도록 할 수도 있다.

##### 3.권한 설정
```sh
mysql> grant all privileges on *.* to 'root'@'%' identified by 'root의 패스워드';
Query OK, 0 rows affected (0.03 sec)
```
전체적으로 접속을 허용하려면 그대로 쓰면 된다.
특정 IP만 접속하게 하려면, 중간의 'root'@'%'부분에서 % 대신 접속을 허용할 IP를 적어주면 된다. 

##### 4. 등록 확인하기
```sh
mysql> select host, user, password from user;
```
root 계정의 host 필드에 % 또는 접속을 허용할 IP가 등록되었는지 확인한다.

##### 5.refrash
```sh
mysql> flush privileges;
Query OK, 0 rows affected (0.00 sec)
```
위 단계는 mycnf 파일 수정 후 서버를 재시작할 것이기 때문에 굳이 안해도 된다.

##### my.cnf 에서 외부접속 관련사항 변경하기
```sh
$ sudo vim /etc/mysql/my.cnf
```
파일 내용 중
bind-address = 172.0.0.1  
부분 주석처리 후 저장하기

##### mysql 재시작
```sh
$ sudo /etc/init.d/mysql restart
```

##### 8.완료

 이제 외부, 클라이언트에서 접속이 가능하다
