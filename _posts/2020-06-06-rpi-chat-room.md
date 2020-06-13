---
layout: post
title: 라즈베리파이에서 Chat-room, 워드프레스 서비스하기
published: true
---
## DB 설치 및 설정
### 설치
PHP-MySQL과 MariaDB를 설치할 것입니다. 라즈베리파이에서 `sudo su -` 를 입력하여 루트가 된 다음

    apt-get -y install mariadb-server
    apt-get install php-mysql

위 명령어를 입력하여 패키지를 설치합니다. <br/>
다음 두 개의 파일에 아래 내용을 추가해야 합니다:

 - */etc/mysql/mariadb.conf.d/50-server.cnf*
Character sets에서 기본 설정 되어있는 두 줄은 주석처리 합니다.
    `#character-set-server = utf8mb4
    #collation-server = utf8mb4_general_ci`
<br/>
    그리고 아래 내용을 추가합니다:
   `init_connect=SET collation_connection = utf8_general_ci
    init_connect=SET NAMES utf8
    character-set-server=utf8
    collation-server=utf8_general_ci
    lower_case_table_names = 1`

 - */etc/mysql/mariadb.conf.d/50-client.cnf*
Character sets에서 기본 설정 되어있는 아래 줄을 주석처리 하고:
`#default-character-set = utf8mb4`
<br/>
   그 아래에 다음 내용을 추가합니다:
`default-character-set = utf8`
<br/>
파일 수정을 마치면 MySQL을 재시작 합니다: 
`service mysql restart` 
<br/>
<br/>
### 설정
MariaDB를 root로 실행하기 위해 `mysql -u root -p`를 입력합니다. *-u* 옵션은 사용자, *-p* 옵션은 비밀번호를 뜻합니다. root는 초기 비밀번호가 없기 때문에 비밀번호를 입력하지 않아도 접속할 수 있습니다. <br/>
<br/>
MariaDB의 root 비밀번호를 만들기 위해 다음과 같이 입력합니다.
`update mysql.user set authentication_string=password('비밀번호') where user=('root');`
잘 되면 *Query OK* 메시지와 *Rows matched: 1 Changed: 0 Warnings: 0* 메시지가 나옵니다. <br/>
<br/>
Chat-Room과 워드프레스에서 사용할 데이터베이스를 만들겠습니다. 데이터베이스 이름은 *byundb*로 하고, *byun* 사용자를 만들어 권한을 주겠습니다. <br/>
데이터베이스를 생성합니다:
`create database byundb;`
<br/><br/>
*byun* 사용자를 만들고 동시에 *byundb*에 대한 권한을 주려면:
`grant all privileges on byundb.* to 'byun'@'localhost' identified by '비밀번호';`
 <br/> <br/>
변경사항을 적용하기 위해: 
`flush privileges;`
<br/><br/>
모두 *Query OK* 메시지가 나왔으면 `quit`을 입력해 종료합니다.<br/>
 <br/>
*byun* 사용자 테스트를 하기 위해 라즈베리파이에 일반사용자로 접속합니다. 그리고 MariaDB에 *byun* 사용자로 접속합니다:
`mysql -u byun -p`
비밀번호 입력문이 나오기 때문에 입력해서 들어갑니다.<br/>

![mariadb]({{site.baseurl}}/images/rpi401.jpg)
(MariaDB에 root로 접속한 화면)<br/>
<br/>
byundb 데이터베이스에 접속 가능하고, mysql 데이터베이스에 접속이 불허되는 걸 확인하기 위해 다음 두 개의 명령어를 입력합니다:
`use byundb;`
`use mysql;`
<br/>
첫 번째 명령어는 가능해야 하기 때문에 *Database changed* 메시지와 나오고 프롬프트가 *MariaDB [byundb]>* 로 바뀌어야 합니다. 두 번째 명령어는 안 돼야 하기 때문에 *Access denied* 메시지가 나와야 합니다.<br/>
<br/>
잘 되는 걸 확인하면 라즈베리파이에 다시 루트사용자로 접속합니다. *byun* 사용자가 사용하는 도메인에 맞는 nginx 설정파일을 편집할 것입니다. 도메인은 *21900353.com* 이기 때문에, */etc/nginx/sites-available/21900353.com* 파일을 열고, 다음과 같이 수정합니다: 

    server {
      listen 80;
      listen[::]:80;
      
      server_name 21900353.com;

      root /html/byun/html;
      index index.html index.php;
      location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.3-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
      }
    }

수정이 끝나면 `service nginx restart` 해서 nginx를 재시작합니다.
<br/><br/>
## Chat-Room 서비스
다시 Chat-Room을 서비스할 계정으로 라즈베리파이에 접속합니다. 그리고 서버 루트디렉터리(*/home/byun/html*)로 작업 디렉터리를 변경합니다. 그 디렉터리에 Chat-Room 포크 저장소를 가져옵니다: 
`git clone https://github.com/21900353/Chat-Room.git`

그리고 Chat-Room 디렉터리의 connection.php 파일에 본인 정보를 넣어 편집합니다: 

    <?php
    $host = "localhost";
    $user = "byun";       // 수정
    $pass = "비밀번호";    // 수정
    $db_name = "byundb";  // 수정
    $con = new mysqli($host, $user, $pass, $db_name);
    function formatDate($date){
      return date('g:i a', strtotime($date));
    }
    ?>

마지막으로 데이터베이스에 chat 테이블을 추가하기 위해 다음을 입력합니다: 
`mysql -u byun -p byundb < Chat-Room/database/chat.sql`

이제 로컬 PC 브라우저에서 도메인/Chat-Room/ (예제의 경우 21900353.com/Chat-Room/)으로 접속하면 채팅방을 사용할 수 있습니다.

### 테스트 
![chat1]({{site.baseurl}}/images/rpi402.png)
채팅방에 byun1, byun2 사용자가 보낸 메시지가 보입니다. 왼쪽에 byun1 사용자이름으로 "OSS"라는 메시지를 보내려고 하고 있습니다. 
<br/><br/>
![chat2]({{site.baseurl}}/images/rpi403.png)
메시지를 보내자 양 쪽에서 메시지가 보입니다.

## 서버 백업
서버에 사고가 일어날 우려가 있기 때문에 반드시 백업을 해 대비해야 합니다. 백업을 매일 04시에 백업하도록 자동화하겠습니다. 먼저 라즈베리파이에 루트사용자로 접속합니다. 그리고 루트에 backup 디렉터리를 만들고, 권한을 읽기/쓰기/실행을 줍니다:
`mkdir /backup`
`chmod 700 /backup`

그 다음 루트에 backup.sh 파일을 만들고 내용을 다음과 같이 합니다:

    #!/bin/bash
    tar -czpf /backup/userdata_`date +%Y%m%d%H%M%S`.tgz /home 1>>/backup/log_`date +%Y%m%d` 2>>error_log_`date +%Y%m%d`
    mysqldump -uroot -p비밀번호 byundb |gzip > /backup/userdb_`date +%Y%m%d%H%M%S`.sql.gz
    find /backup/ -type f -mtime +7 | sort | xargs rm -f
    
![backup.sh]({{site.baseurl}}/images/rpi404.jpg)
<br/>
<br/>
그리고 이 파일에 같은 권한을 줍니다: 
`chmod 700 backup.sh`
<br/>
<br/>

![backup test]({{site.baseurl}}/images/rpi405.jpg)

백업 스크립트 실행 결과, 백업 파일이 잘 만들어졌습니다.<br/>
<br/>
백업을 자동화하기 위해서 *cron*을 사용할 것입니다. 초기에는 아무것도 설정되어 있지 않으니 `crontab -e` 입력 후 편집기를 선택하면 새 크론탭을 만들 수 있습니다. 긴 주석이 있는데 마지막 줄에 다음과 같이 추가하면 됩니다:
`0 4 * * * /root/backup.sh 1>/dev/null 2>/dev/null`<br/>
<br/>
![crontab]({{site.baseurl}}/images/rpi406.jpg)
순서대로 (분) (초) (일) (월) (요일) (명령어)입니다. 이렇게 해서 백업 자동화가 끝났습니다.<br/>
<br/>

## 워드프레스 서비스
워드프레스에 사용할 데이터베이스 계정과 이름은 Chat-Room에 사용된 동일한 것을 사용하겠습니다. <br/>
*html* 디렉터리에서 워드프레스 파일을 받습니다:
`wget https://ko.wordpress.org/latest-ko_KR.tar.gz`

파일 압축을 풉니다:
`tar -xzvf latest-ko_KR.tar.gz`

로컬 PC 브라우저에서 워드프레스 주소로 접속합니다: *도메인/wordpress/* (예제의 경우 21900353.com/wordpress/)

![wp install]({{site.baseurl}}/images/rpi407.jpg)
설치 페이지 화면입니다. 데이터베이스 정보를 입력하세요.

![wp-config]({{site.baseurl}}/images/rpi408.jpg)

넘어가면 이런 화면이 나오면서 wp-config.php가 자동으로 추가되지 않았을 것입니다. 라즈베리파이에서 직접 파일을 만들고 내용을 붙여넣기 하세요: 
`cat > wp-config.php`
`복사 후 붙여넣기`

![wp install 2]({{site.baseurl}}/images/rpi409.jpg)

넘어가면 이런 화면이 나옵니다. 입력하고 설치를 마치면 됩니다. <br/>
<br/>
![index]({{site.baseurl}}/images/rpi410.jpg)

설치는 끝났고, 테마나 모듈을 설치하기 위한 마지막 설정이 필요합니다. 라즈베리파이에서 워드프레스의 *www-data*, *wp-content* 디렉터리 권한과 그룹을 다음과 같이 변경합니다:
`sudo chgrp -R www-data ~/html/wordpress/wp-content`
`sudo chmod -R 775 ~/html/wordpress/wp-content`

그리고 *html* 디렉터리의 *wp-config.php* 파일의 마지막 줄에 다음을 추가합니다:
`define('FS_METHOD', 'direct');`

 
## 관리자 페이지
관리자 페이지는 *도메인/wordpress/wp-admin/* (예제의 경우 21900353.com/wordpress/wp-admin/)으로 들어갈 수 있습니다. 제가 변경한 설정은 테마 변경, 일반 설정 > 제목, 태그라인 변경, 이미지 로고 적용입니다.

 - 테마 적용

테마 디자인 메뉴 > 테마 > 새로 추가 에서 Go 테마를 찾아 설치한 후 적용했습니다.<br/>
그리고 
테마 디자인 메뉴 > 사용자 적용하기 > 사이트 아이덴티티 에서 로고에 이미지파일을 추가했습니다. 

![theme1]({{site.baseurl}}/images/rpi411.jpg)<br/>
<br/>
![theme2]({{site.baseurl}}/images/rpi412.jpg)<br/>
<br/>
<br/>
- 제목, 태그라인

설정 메뉴 > 일반 설정 에서 제목, 태그라인을 다음과 같이 변경했습니다.

![settings]({{site.baseurl}}/images/rpi413.jpg)<br/>
<br/>
<br/>
