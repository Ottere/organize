# CentOS 7 Cockpit install

# 목차
1. Cockpit이란?
2. 설치방법
3. 참조사이트

## 1. Cockpit이란?
>Cockpit 은 Fedora Project 에서 나온 웹 UI 기반의 모니터링 및 관리 툴입니다.
Fedora 에서 개발됬지만 CentOS 의 경우 RHEL기반에 Kernel도 비슷하여 호환성이 보장되므로 사용이 가능합니다.

## 2. 설치방법
```
# yum 으로 Cockpit 설치
yum install cockpit
```
```
# 자동실행 등록
systemctl enable cockpit.socket
```
```
# 방화벽에 Cockpit 등록
firewall-cmd --permanent --zone=public --add-service=cockpit

```
```
# 방화벽 재실행
firewall-cmd --reload
```
```
# 방화벽 서비스 확인
firewall-cmd --list-services
```
```
# 데몬 시작
systemctl start cockpit
```
```
# 데몬 재시작
systemctl daemon-reload
```
```
# Cockpit 재시작
systemctl restart cockpit
```
접속 방법: https://localhost:9090/

## #참조사이트
1. https://newstars.cloud/334
2. https://idchowto.com/web-ui-%EA%B8%B0%EB%B0%98%EC%9D%98-%EB%AA%A8%EB%8B%88%ED%84%B0%EB%A7%81-%EB%B0%8F-%EA%B4%80%EB%A6%AC-%ED%88%B4-cockpit/
3. https://msg.soledot.com/blog/fo/7524/blogview.sd