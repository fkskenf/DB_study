# Mac 기준

1. Xcode 설치
> 앱스토어에서 다운

2. HomeBrew 설치
```terminal
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
> 맥북 비밀번호 입력 

3. cask 설치
> HomeBrew를 통해 그래픽 기반으로 동작하는 프로그램(사파리,크롬,워드 등)을 설치하게 해주는 패키지
```terminal
brew install cask
```
```terminal
mysql.server start # 시작

mysql.server status # 상태확인

mysql.server stop # 정지
```

4. 프로세스 죽이기
```terminal
ps -ef | grep mysql
sudo kill [pid] [pid]
```

5. 대신쓰는 명령어
```terminal
mysql.server start --> brew services start mariadb
mysql.server stop --> brew services stop mariadb
mysql.server status --> brew services list
```

6. MariaDB 접속
```terminal
mysql -u root -p
// DB 비밀번
```
> Access Denied for user root오류가 뜨면
```terminal
sudo mysql -uroot
```
>  접속한 뒤에 root 계정의 비밀번호를 바꿔주면 됩니다. <br>
>  root 계정의 비밀번호를 바꾸려면 기본적으로 구축되어 있는 mysql이라는 데이터베이스에 접속한 뒤에 root 계정의 비밀번호를 변경

7. 시도
```terminal
use mysql; # mysql이라는 데이터베이스를 사용하겠다는 의미.
set password=password('root'); # MariaDB 10.4 버전 이상에서 사용가능한 명령어
```

## 8. 비밀번호 Error
```terminal
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
> MariaDB가 MySQL기반으로 둘다 사용가능한것으로 보임

<br>

![image](https://user-images.githubusercontent.com/60438691/213624477-07158e29-4050-4390-8488-4cd5f7aed3ac.png)

