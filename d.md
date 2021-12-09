# SSH 포트 변경
> SSH 보안 강화를 위해서는 포트 번호를 수정하는 것이 필수입니다.   
  흔한 22번 포트로 SSH를 이용하는 경우 온갖 종류의 공격에 시달리는 불상사가 발생합니다.

## SSH 설정 변경
> 아래 명령어를 입력해 ssh 설정파일로 접속합니다.

```
vi /etc/ssh/sshd_config
```
![image](https://user-images.githubusercontent.com/69878816/145315717-0b80ec51-f8e6-40bc-b59a-23660216e90b.png)   
그리고 #port 22 부분의 주석을 해제하고 ssh로 사용할 포트를 입력합니다. (해당 사진의 경우 10000번 포트 사용)

## SELinux 포트 사용 허용
> SELinux를 사용할 경우 포트를 설정하더라도 SELinux에서 포트 허용을 해줘야 접속이 가능합니다.

![image](https://user-images.githubusercontent.com/69878816/145316022-058def58-1142-4415-8562-90f1c9a9f2ea.png)   
이미지의 명령어를 이용하여 포트를 추가하고 정상적으로 추가됬는지 확인합니다.

## ssh 서비스 재시작 
> 변경된 설정파일을 적용시키기 위해 ssh service를 재시작합니다.

![image](https://user-images.githubusercontent.com/69878816/145316220-0e5387f4-55f4-4438-8a45-cede248db930.png)   
위 사진처럼 재시작 이후 status를 사용해 10000포트로 수신중인지 확인합니다.

## 방화벽 포트 사용 허용
> SELinux와 마찬가지로 방화벽에서도 포트를 허용합니다.

![image](https://user-images.githubusercontent.com/69878816/145316429-8874d1c6-c70c-412c-be68-cb6483f99a9b.png)   
방화벽에 포트를 추가하고 재시작하여 변경된 설정을 적용합니다.

## ssh 접속
> 이제 ssh 접속을 변경된 포트로 하면 정상 접속이 가능합니다.
