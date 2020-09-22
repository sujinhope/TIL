### [특화] Django Nginx 설정하기



##### 프로젝트 구조

```python
test_aws
 └─ sub2
 	 ├─ frontend		# frontend project
 	 │
 	 └─ backend			# backend project
 	 	  ├─ manage.py	# runserver 위치
 	 	  ├─ .config
          │		├─ nginx
          │  	│    └─ backend.conf
          │  	└─ uwsgi
          │      	 ├─ backend.ini
          │      	 └─ uwsgi.service
 	 	  └─ backend
 	 	  		└─ wsgi.py
```





##### 1. nginx 설치

```bash
$ sudo apt-get install nginx
```



##### 2. /etc/nginx/nginx.conf 설정

앞선 과정에서 배포를 위해 생성한 deploy 계정을 nginx에 등록

```bash
$ sudo vi /etc/nginx/nginx.conf
```



i를 눌러서 맨 첫 줄 `www-data -> deploy`로 수정 후 :wq를 눌러서 저장+종료

![image](https://user-images.githubusercontent.com/33229855/93848314-3038e700-fce4-11ea-8975-745934dff783.png)





##### 3. 프로젝트 내 .config 폴더 아래에 nginx 폴더 생성, backend.conf 파일 설정

```bash
# 디렉토리 생성 위치 - test_aws/sub2/backend/.config/
$ sudo mkdir nginx

# backend.conf 파일 생성
# 파일 위치 - test_aws/sub2/backend/.config/nginx/backend.conf
$ sudo vi backend.conf
```

- listen : 요청을 받을 포트 번호(80: http 기본 포트)
- server_name : 요청받을 서버 주소 (앞에서 settings.py에서 ALLOWED_HOSTS에 등록했던 주소)
- location / {} : 해당 주소(*t3coach12.p.ssafy.io/*)로 요청이 들어올 경우 처리할 내용

```python
server {
	listen 80;
	server_name t3coach12.p.ssafy.io; # 여기에 팀 도메인 사용
	charset utf-8;
	client_max_body_size 128M;
    
    location /api/ {
        uwsgi_pass		unix:///tmp/backend.sock;
        include			uwsgi_params;
    }
}
```

![image](https://user-images.githubusercontent.com/33229855/93848899-cb7e8c00-fce5-11ea-8aa7-d1efc3563560.png)





##### 4. .config/uw

.config/uwsgi/backend.ini에는 8080포트로 지정되어 있는데 위에서 포트가 80으로 변경되었기 때문에 .config/uwsgi/backend.ini 파일 수정 필요

> 기존 내용에서 http = :8080을 삭제하고 소켓 정보와 소유자, 권한을 서술한 세 줄 추가

![image-20200922151753521](C:\Users\multicampus\AppData\Roaming\Typora\typora-user-images\image-20200922151753521.png)





##### 5. uwsgi가 백그라운드에서 항상 켜질 수 있도록 설정

Nginx는 항상 켜져있어야 함. uwsgi는 명령어를 통해 실행시켜 주어야 하는데, uwsgi와 nginx를 연결해야 한다면 uwsgi도 항상 백그라운드에서 켜져 있어야 한다.

> ∴ uwsgi를 백그라운드에서 계속 켜둘 수 있도록 설정 파일 추가



5-1.   *.config/uwsgi/uwsgi.service* 생성

```bash
# 실행 위치 test_aws/sub2/backend/.config/uwsgi
$ sudo vi uwsgi.service
```



- ExecStart : uwsgi를 관리자 권한으로 실행하기 위한 명령어

  각 파일, 디렉토리 경로들은 **절대경로**로 설정(안 될 경우 뒤쪽 **프로젝트 경로** 상대경로로 바꿔보기 - ex) */test_aws/sub2/backend/.config/uwsgi/backend.ini*)

```service
[Unit]
Description=uWSGI service
After=syslog.target

[Service]
ExecStart=/home/ubuntu/myvenv/bin/uwsgi -i /home/ubuntu/test_aws/sub2/backend/.config/uwsgi/backend.ini

Restart=always
KillSignal=SIGNOUT
Type=notify
StandardError=syslog
NotifyAccess=all

[Install]
WantedBy=multi-user.target
```

![image](https://user-images.githubusercontent.com/33229855/93849581-6a57b800-fce7-11ea-9b74-c69442ca6e39.png)





##### 6. uwsgi.service 파일을 데몬(백그라운드에 실행)에 등록

###### 6-1. /etc/systemd/system/에 링크 걸기

```bash
$ sudo ln -f ~/test_aws/sub2/backend/.config/uwsgi/uwsgi.service /etc/systemd/system/uwsgi.service
```



###### 6-2. 데몬 새로고침

```bash
$ sudo systemctl daemon-reload
```



###### 6-2. uwsgi 사용가능하게 변경 후 restart

```bash
$ sudo systemctl enable uwsgi
$ sudo systemctl restar uwsgi
```



































