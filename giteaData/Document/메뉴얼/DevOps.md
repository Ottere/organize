# DevOps

## 목차 
1. 데브옵스 DevOps란?
2. DevOps의 이점
3. DevOps 툴체인
4. CI/CD란?

### 데브옵스 DevOps란?
> 'DevOps'는 'development(개발)'와 'operations(운영)'가 합쳐진 단어이지만,   
  단순히 각각의 용어를 결합한 이상의 포괄적인 아이디어와 방식을 나타냅니다. 

- 애플리케이션 개발의 품질과 속도를 개선하고 신규 또는 수정된 소프트웨어 기능이나   
  제품의 릴리즈 주기 단축을 장려하는 새로운 철학이자 프레임워크입니다.   
- DevOps 사례는 애플리케이션 개발 팀(Dev)과 해당 IT 운영 팀(Ops) 팀 간의 원활하고   
  지속적인 커뮤니케이션, 협업, 통합, 가시성 및 투명성을 장려합니다.   

### DevOps의 이점
> DevOps 사용자들이 설명하는 비즈니스 및 기술적 이점 중 다수는 고객 만족도의 개선입니다.   
  DevOps의 몇가지 이점에 대해 알아보겠습니다.

- 더 우수한 제품을 더 빠르게 제공
- 더 빠른 문제 해결 및 복잡성 감소
- 확장성 및 가용성 향상
- 보다 안정적인 운영 환경
- 향상된 리소스 활용률
- 자동화 향상
- 시스템 결과에 대한 가시성 개선

### DevOps 툴체인
> DevOps 사례를 따르는 사람들은 종종 DevOps “툴체인”의 일부로 DevOps 친화적인 툴을 사용합니다.

이러한 툴의 목표는 소프트웨어 전송 워크플로(또는 "파이프라인")의 다양한 단계를 추가로 간소화하고, 단축하고, 자동화하는 것입니다.   
또한 이러한 툴 중 다수는 자동화, 협업 및 개발-운영 팀 간의 통합에 대한 핵심 DevOps 원칙을 손쉽게 준수할 수 있도록 합니다.   
다음은 다양한 DevOps 라이프사이클 단계에서 사용되는 툴의 예입니다.


![image](https://mblogthumb-phinf.pstatic.net/MjAyMTA3MDFfMTYy/MDAxNjI1MTQwNjA4MDE5.rQehbiimIminpPJMU7FsJphdwREjTn8sAO6JoaC38wsg.2e2LjYaUTs1_gImZlHiw-yLA8AR0OujUg1CX9eQWShUg.JPEG.agapeuni/d668b94e2e6b3d9dfe842f6c4c44a9c3.jpg?type=w800)
- 계획 (PLAN)
  <p>SR을 접수하거나 이슈를 생성, 단위 기능이나 서비스를 계획, 분석하고 설계 (Jira, Git)</p>

- 개발 (CODE)
  <p>코드를 작성하여 버전관리 시스템에 등록, 내용 정리, 공유 <br>
  상황에 따라 신규 Branch 생성하거나 코드 수정, 코드를 merge (GitHub, GitLab, Bitbucket)</p>

- 빌드 (BUILD)
  <p>작성한 코드를 정적분석, 보안분석을 수행하고 빌드 <br>
  자동화 도구로 빌드하여 문제가 없는지 주기적으로 확인 (Docker,Puppet,Maven,Ansible)</p>

- 테스트 (TEST)
  <p>빌드 한 기능이 문제가 없는지 테스트 및 요구사항에 따라 계획한 기능을 수행하는지 검증 (Vagrant,Selenium)</p>

- 구현 (RELEASE)
  <p>완성된 결과물을 개발서버나 품질서버에 이관</p>

- 배포 (DEPLOY)
  <p>서비스할 운영서버나 클라우드에 배포 (Jenkins,Kubenetes,Docker)</p>

- 운영 (OPERATE)
  <p>실제 업무에 적용하여 협업 </p>

- 모니터 (MONITOR)
  <p>안정적인 운영을 위해 지속적인 모니터링 (Grafana,New Relic, Nagios)</p>

### CI/CD란?
- **CI (Continuous Integration)** 다수의 개발자가 작성·수정한 소스코드를 지속적으로 통합·테스트하는 것을 의미
- **CD (Continuous Delivery/Deployment)** 개발, 통합, 배포, 릴리즈, 테스트를 자동화하여 지속적으로 배포하는 것을 의미   

전통적인 방식으로는 코드수정하고 배포하는데 까지 많은 시간이 소요되었습니다. 특히 QA테스팅에서 많은 버그가 발생되었습니다.
![CI/CD](https://blog.oursky.com/wp-content/uploads/2019/08/image-1160x553.png)   

CI/CD를 통해 지속적으로 통합·테스트·배포를 하고 이 흐름을 자동화하여 효율적으로 일을 처리할 수 있습니다.   
![CI/CD](https://blog.oursky.com/wp-content/uploads/2019/08/image-1-1160x571.png)

#### 참조사이트
- https://www.atlassian.com/devops   
- https://simsimjae.medium.com/devops%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-c50f4d86666b   
- https://www.netapp.com/ko/devops-solutions/what-is-devops/   
- [DevOps 구축을 위한 7가지 고려사항](https://media.fastcampus.co.kr/newsletter/wennews/%EA%B0%9C%EB%B0%9C%EC%9E%90-%ED%95%84%EB%8F%85-%EC%B6%94%EC%B2%9C-%EC%98%AC%EB%B0%94%EB%A5%B8-%EB%8D%B0%EB%B8%8C%EC%98%B5%EC%8A%A4-%EA%B5%AC%EC%B6%95%EC%9D%84-%EC%9C%84%ED%95%9C-7%EA%B0%80%EC%A7%80/)
