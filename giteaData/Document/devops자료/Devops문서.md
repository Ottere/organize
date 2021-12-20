# #DevOps

## #DevOps의 정의
DevOps는 Development and Operations의 약자이며, 소프트웨어 및 컴퓨터 시스템 개발 기술.<mark> 개발(Development) 담당자와 운용(Operations) 담당자가 긴밀하게 협력·제휴해</mark><br> 애플리케이션 개발의 품질과 속도를 더 빠르게 하고 신규 또는 수정된 소프트웨어 기능이나 제품의 릴리즈 주기 단축을 장려하는 새로운 철학입니다

## #DevOps의 이점
* 속도
    * <mark>작업 속도가 빨라지므로 고객을 위해 더 빠르게 혁신하고</mark>, 시장 변화에 더 잘 적응하고, 좀 더 효율적으로 비즈니스 성과를 창출할 수 있습니다

* 신속한 제공
    * <mark>릴리스의 빈도와 속도를 개선하여 제품을 더 빠르게 혁신하고 개선할 수 있습니다.</mark> 새로운 기능의 릴리스와 버그 수정 속도가 빨라질수록 고객의 요구에 더 빠르게 대응하여 경쟁 우위를 강화할 수 있습니다

* 안정성
    * 최종 사용자에게 지속적으로 긍정적인 경험을 제공하는 한편 <mark>더욱 빠르게 안정적으로 제공할 수 있도록 애플리케이션 업데이트와 인프라 변경의 품질을 보장합니다</mark>

* 확장
    * 규모에 따라 인프라와 개발 프로세스를 운영 및 관리합니다. <mark>자동화와 일관성이 지원</mark>되므로 위험을 줄이면서 복잡한 시스템 또는 변화하는 시스템을 효율적으로 관리할 수 있습니다

* 협업 강화
    * <mark>주인의식 및 책임과 같은 가치를 강조하는 DevOps 문화 모델에서 좀 더 효과적인 팀을 구축합니다.</mark> 개발자와 운영팀은 긴밀하게 협력하고, 많은 책임을 공유하며, 워크플로를 결합합니다.

* 보안
    * 제어를 유지하고 규정을 준수하면서 신속하게 진행할 수 있습니다. <mark>자동화된 규정 준수 정책, 세분화된 제어 및 구성 관리 기술</mark>을 사용함으로써 보안을 그대로 유지하면서 DevOps 모델을 도입할 수 있습니다
***

## #DevOps의 툴체인

![image](https://mblogthumb-phinf.pstatic.net/MjAxOTA0MjJfNDkg/MDAxNTU1OTE5MTQxNTYz.x27cIz_skLfoLu6fmpaa8WgOATYpR2kreJ584oq4jtwg.7eraCTdUja3mZ2ufs_yWYGiOIkZ6Er0NeaWwJWU253Eg.PNG.acornedu/%EC%9D%B4%EB%AF%B8%EC%A7%802.png?type=w800)

* <b>계획</b>: <br>이 단계는 <mark>비즈니스 가치 및 요구사항을 정의</mark>하는 데 도움이 됩니다.<br>샘플 툴로는(Jira 또는 Git)가 있습니다.

* <b>코딩</b>:<br> 이 단계에는 <mark>소프트웨어 설계 및 소프트웨어 코드 생성이 포함됩니다</mark>. <br>샘플 툴로는 (GitHub, GitLab, Bitbucket, Stash)가 있습니다.

* <b>구축</b>:<br> 이 단계에서는 <mark>소프트웨어 빌드 및 버전을 관리하고 자동화된 툴을 사용하여 코드를 컴파일하고 패키징하여 향후 제품 릴리즈에 제공합니다</mark>.<br> 샘플 툴로는 (Docker, Ansible, Puppet, Chef, Gradle, Maven 또는 JFrog Artifactory)가 있습니다.

* <b>테스트</b>:<br> 이 단계에서는 <mark>최적의 코드 품질을 보장하기 위해 지속적인 테스트(수동 또는 자동)를 수행합니다</mark>. <br>샘플 툴로는 (JUnit, Codeception, Selenium, Vagrant, TestNG 또는 BlazeMeter)가 있습니다.

* <b>릴리즈</b>: <br> 완성된 결과물을 개발서버에 이관합니다

* <b>배포</b>:<br> 이 단계에는 <mark>제품 릴리즈를 운영 단계로 관리, 조정, 예약 및 자동화</mark>를 합니다<br> 샘플 툴로는 (Puppet, Chef, Ansible, Jenkins, Kubernetes, OpenShift, OpenStack, Docker 또는 Jira)가 있습니다.

* <b>운영</b>:<br> 이 단계에서는 <mark>운영 중인 소프트웨어를 관리합니다</mark>.<br> 샘플 툴로는( Anabilities, Puppet, PowerShell, Chef, Salt 또는 Otter)가 있습니다.

* <b>모니터링</b>:<br> 이 단계에서는 운영 환경의 <mark>특정 소프트웨어 릴리즈에서 발생하는 문제에 대한 정보를 식별하고 수집합니다</mark>.<br> 샘플 툴로는 (New Relic, Datadog, Grafana, Wireshark, Splunk, Nagios 또는 Slack)이 있습니다.

## #devops CI/CD의 정의
![img](https://k21academy.com/wp-content/uploads/2020/08/CI-CD_BlogImage.png)

* <b>CI</b>란  개발자를 위한 자동화 프로세스인 지속적인 통합(Continuous Integration)을 의미합니다<br>
<mark>테스트와 개발 간의 신속한 피드백을 통해 코드 문제를 신속하게 파악하고 해결하는 작업이 포함됩니다.</mark>

* <b>CD</b>란 지속적인 서비스 제공(Continuous Delivery) 및/또는 지속적인 배포(Continuous Deployment)를 의미하며 이 두 용어는 상호 교환적으로 사용됩니다<br><mark>Docker, Kubernetes 및 기타 컨테이너 기술을 사용하면 서로 다른 구축 플랫폼 및 환경에서 코드의 일관성을 유지하여 지속적인 구축을 지원할 수 있습니다.</maark>

즉 정리하면 빌드·테스트·배포라고 말한 개발에 관련된 각종 작업을 자동화해, 계속적으로 실시하는 구조를 「CI/CD」라고 부릅니다<br>
CI/CD를 채용하면, 개발 담당자가 소스를 수정했을 때도, 프로덕션 환경에 릴리스할 때까지의 일련의 작업이 자동화되는 것입니다. CI/CD를 도입함으로써 담당자가 수개월에 걸쳐 실시한 작업을 몇 시간 안에 완료할 수 있는 일도 적지 않습니다.

## #참조 사이트
1. https://www.netapp.com/ko/devops-solutions/what-is-devops/
2. https://aws.amazon.com/ko/devops/what-is-devops/
3. https://www.kagoya.jp/howto/it-glossary/develop/devops/