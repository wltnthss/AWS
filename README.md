# AWS

## AWS 개념 

AWS를 알기 전에 **클라우드 컴퓨팅**이라는 개념에 대해 먼저 알아가고자 합니다.

**클라우드 컴퓨팅**

일반적으로 사용하는 서버는 크게 2가지 **온프레미스**와 **클라우드** 방식이 있습니다.

**온프레미스 (on-Premise)**

- 데이터센터나 서버실에 서버를 직접 관리하는 방식입니다.
- 집에 있는 pc로 작은 서버를 돌리는 경우도 온프레미스에 속합니다.
- 서버, 네트워크장비, os, 스토리지 등.. 직접 구매, 설치, 관리해야하므로 사용량이 적어도 유지비용이 발생하는 단점이 존재합니다.

**클라우드**

- 인터넷을 통해 불특정 다수에게 서비스를 제공하는 형태입니다.
- 서버, 네트워크장비, 데이터베이스, os 등.. 필요한 리소스들에 대해 사용한 만큼 비용을 지불하는 방식입니다.
- 서비스에 따라 IaaS, PaaS, SaaS로 나뉘며 대표적 Cloud Provider 는 Aws, MS Azure, GCP가 존재합니다.
- Serverless : 서버 작업을 서버 내부가 아닌 클라우드 서비스로 처리하는 것입니다.

**AWS 개념**

- Amazon Web Services 로 클라우드 컴퓨팅의 대표적 기업
- 컴퓨팅, 운영체제, 네트워킹, 스토리지, 응용프로그램(웹서버, DB, CRM)등을 지원합니다.

**AWS 구성**

- **Region** - 복수개의 데이터센터의 물리적 위치 ex) 서울에 존재하는 데이터 센터
- **AZ(Avaliability Zones)** - 하나의 Region내에 공간적으로 분리된 전원, 백업 역할을 하는 안전 장치
- **EC2(Elastic Compute Cloud)** - 가상 서버, 독립된 하나의 컴퓨터를 임대해주는 것, 다양한 OS를 사용 가능하며 cpu, 메모리, 네트워크에 따른 다양한 인스턴스 타입을 지원하며 다양한 과금 옵션도 제공
- **Instance** - 하나의 컴퓨터 개념, 원격으로 접속하여 제어 가능하며 웹서버 설치, DB 환경 구축 가능 (AWS에서 빌리는 컴퓨터를 Instance라고 칭함)
- **RDS(Relational Database Service)** - AWS에서 제공하는 관계형 데이터베이스 서비스. EC2로 직접 배포하고 관리할 수 있지만, RDS를 사용하면 자동 유지보수 및 관리가 가능 (모니터링, 주기적 백업을 대신 해줌)
- **S3(Simple Storage Service)** - AWS의 클라우드 스토리지 서비스이고 웹에 데이터를 저장하는 저장소 (구글 드라이브, 네이버 MyBox와 같음)
- **버킷** - S3에 저장되는 파일들이 담기는 바구니 (파일을 저장하는 최상위 디렉터리), 키 - 값 형태로 데이터 저장
- **PM2** - PM2로 서버를 실행하면, 이제 터미널을 종료하더라도, node.js 애플리케이션이 프로세스로 실행. 중단 및 재시작, 또는 상태를 보기 위한 명령어는 기억해야함.
    - “pm2 start” - 프로세스 시작
    - "pm2 stop" 프로세스 중지
    - "pm2 restart" 프로세스 재시작
    - "pm2 ls" 프로세스 목록 보기
    - "pm2 log" 프로세스 로그 보기

# 트러블슈팅

### 이슈

### war 파일 톰캣에서 실행 후 CSS 파일 미적용 및 경로로 인한 오류 발생

- 운영서버에 추가한 war명 (jcticket)이 url에 들어가며 발생
- (jcticket) was 파일명이 왜 들어가는지, url에 들어간 걸 빼는 방법을 구글링했으나 못찾음
- 기존 /resources/js/admin/admin.js 와 같은 파일들에 동적 경로를 붙이기로 함.

### 방법

### jsp 파일내에 동적 경로 설정 추가

```html
<link rel="stylesheet" href="${pageContext.request.contextPath}/resources/css/admin/admin.css">
<script src="${pageContext.request.contextPath}/resources/js/admin/admin.js"></script>

<form id="userSearch" action="${pageContext.request.contextPath}/admin/user" method="get">
```

- was 파일명이 들어가는 방법은 해결하지 못했으나 jsp 파일 경로내에 동적 경로를 추가함으로써 운영에도 정상적으로 반영되는 것