# gitea ssh 주소로 git 사용
> ssh로 사용하는경우 gitea 계정에 로컬(본인 컴퓨터)의 ssh key가 등록되어있어야합니다.

## ssh keygen
> 사용자의 ssh key를 생성하겠습니다.

바탕화면에서 마우스 우클릭 이후 Git Bash Here을 클릭하여 git Bash로 이동합니다.   
![image](https://user-images.githubusercontent.com/69878816/145323836-6aa939c4-d5d2-41c6-a0e2-bd0160c0b053.png)  

   
이후 Git Bash에서 cd ~ 를 이용해 홈 디렉토리로 이동합니다.      
![image](https://user-images.githubusercontent.com/69878816/145324193-fd593cc7-0200-4ef4-b3b1-540b8ef6c1e5.png)   
이후 나오는 메시지는 모두 엔터를 눌러 패스합니다.   

![image](https://user-images.githubusercontent.com/69878816/145324386-93be8c5c-0744-4397-8fed-04d2cb73a6b0.png)   
~/.ssh로 이동해 파일들을 보면 id_rsa.pub이라는 파일이 있습니다.   
해당 파일의 내용을 복사해줍니다. ex) ssh-rsa AAAAB3NzaC1yc2EA....

## gitea에서 공개키 등록
> 로컬에서 생성한 공개키를 gtea에 등록하겠습니다.

![image](https://user-images.githubusercontent.com/69878816/145324650-d8d3273c-3d8a-4d62-a4e2-85e207ff7fa4.png)   
우측 상단의 프로필을 누르고 설정으로 이동합니다.   
![image](https://user-images.githubusercontent.com/69878816/145324834-4c886649-84b0-4039-a3cf-335656fa442b.png)   
이후 SSH/GDG 키로 이동합니다.   
![image](https://user-images.githubusercontent.com/69878816/145324855-4cf06deb-ca7d-4bf6-a5a9-d031abff0bac.png)   
SSH 키 관리의 키 추가를 누릅니다.

![image](https://user-images.githubusercontent.com/69878816/145325203-fac5c0b7-1666-4eac-a5e9-e300418c9ea7.png)   
이후 컨텐츠 부분에 위에서 복사한 id_rsa.pub의 내용을 전부 붙여넣습니다. (...없이 모두 붙여넣습니다.)   
그리고 키 추가를 누르면 본인의 공개키가 추가되고 ssh 주소를 이용해 gitea의 사용이 가능합니다.
