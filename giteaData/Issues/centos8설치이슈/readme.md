# #증상 및 현상

1. centos 8 설치시 파티션 분배하는 과정에서 RAID 된 디스크를 찾지못함    
   
   * 구형서버에 신형OS를 설치시 일어나는 현상(호환문제)
   * CentOS 8 / RHEL 8 넘어오면서 오래된 컨트롤러에 대한 지원을 제거
> 참조: [11장. 하드웨어 지원](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/considerations_in_adopting_rhel_8/hardware-enablement_considerations-in-adopting-rhel-8#removed-hardware-support_hardware-enablement)

# #서버 정보
* 이름: supermicro x8dtl-3/-i/-3f/-if
* 버전: 2.1a
* 사용중인 레이드카드: LSI megaraid software

# #조치방법

1. 해당 서버에서 사용중인 Megaraid RAID 컨트롤러를 다운후 설치중인 서버에 삽입
   * 참고 1 확인

* 레이드 설정
  * RAID 해제 후 재부팅 
    * centos 7 에서는 로컬 표준 디스크에 디스크가 3개가 인식되는것을 확인
    * centos 8 에서는 로컬 표준 디스크에 디스크가 인식되지 않은것을 확인

  * RAID 설정 후 재부팅 
    * centos 7 에서는 로컬 표준 디스크에 RAID가 된 디스크 2개를 제외한 나머지 1개가 인식되는것을 확인
    * centos 8 에서는 로컬 표준 디스크에 디스크가 인식되지 않은것을 확인

* BIOS SATA 변경
  * IDE방식을 RAID 방식으로 변경
    * centos 7 에서는 로컬 표준 디스크에 디스크가 3개가 인식되는것을 확인
    * centos 8 에서는 로컬 표준 디스크에 디스크가 인식되지 않은것을 확인

# #레이드컨트롤러 install 하는법

* [이곳에서 레이드 컨트롤러 다운로드](https://elrepo.org/linux/dud/el8/x86_64/)
* 위 사이트 진입후 centos 8 버전에 맞는 iso 파일 다운로드
  * 예시 (dd-megaraid_sas-07.717.02.00-1.el8_5.elrepo.iso) 다운로드 후 usb에 삽입
1. <p>부팅후 Install Centos 8 출력시 [Tab]키를 눌러 명령어 창에 진입</p>
2. <p>스페이스바 한번 입력후 modprobe.blacklist=ahci inst.dd 입력</p>
3. <p>usb 선택후 설치 진행</p>
> 참조: [CentOS 8/Redhat 8 설치시 RAID DISK](https://atelier-house.tistory.com/5)

## 참고 사이트
* https://m.blog.naver.com/harvana/222071666904
* https://atelier-house.tistory.com/5
* https://centosfaq.org/centos/centos-8-installation-not-recognizing-local-disk/
 
# #결론
<mark></mark>