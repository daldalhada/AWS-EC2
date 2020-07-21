# 클라우드 서비스란?

##### 그전에, 서버를 구축하는 방법에는 어떤 것들이 있을까
#####  &nbsp; &nbsp; &nbsp; 1. 집에다가 장비를 직접 구축하는 것

##### &nbsp; &nbsp; &nbsp; 2. AWS 같은 클라우드 서비스에서 물리적 자원을 대여받는 것

<br>

##### 그렇다면, 직접 구축하는 것에 비해 어떤 장점이 있을까?
#####  &nbsp; &nbsp; &nbsp; 1. 장비가 필요 없음(구매할, 관리할 필요가 없다.)

##### &nbsp; &nbsp; &nbsp; 2. 자원의 확장 및 축소가 쉬워짐
##### &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; 장비를 사용하는 서버에 갑자기 사용량이 증가했다고 가정했을 때, <br> &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; 이 때 서버 자원을 추가하려면 장비를 따로 추가로 구매해야 함 <br> &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; (번거롭고 대응도 느리다.)

<br>

### 결국,  클라우드 서비스란 물리적 자원 혹은 논리적 자원을 대여하는 것

<br>

# AWS EC2

**EC2**는 Elastic Computer Cloud의 약자이다.  즉, 물리적인 자원을 대여해주는 클라우스 서비스이다. 

##### 특징
#####  &nbsp; &nbsp; &nbsp;  1. 원하는 만큼 CPU, 메모리, 디스크 등 자원의 크기를 선택하고 생성할 수 있음 <br>&nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;(필요한 만큼 자원을 대여해서 사용)
#####  &nbsp; &nbsp; &nbsp;  2. 운영체제도 선택 가능하다. (우분투 등을 선택하고 EC2를 생성해야 한다.)

#####  단계
#####  &nbsp; &nbsp; &nbsp;  1. Amazon Machine Image(AMI) 선택
#####  &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; - 인스턴스를 시작하는데 필요한 소프트웨어 구성(OS, 애플리케이션 서버, 애플리케이션)이 포함된 <br> &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp; &nbsp; 템플릿
#####  &nbsp; &nbsp; &nbsp;  2. 인스턴스 유형 선택 (우분투 등을 선택하고 EC2를 생성해야 한다.)
#####  &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; - 인스턴스는 애플리케이션을 실행할 수 있는 가상 서버이다. CPU, 메모리, 스토리지 및 네트워크 <br> &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp; &nbsp; 용량의 다양한 조합이 있으며, 애플리케이션에 사용할 적절한 리소스 조합을 유연하게 선택할 수 <br> &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp; &nbsp;  있다. 

#####  &nbsp; &nbsp; &nbsp;  3. 인스턴스 세부 정보 구성
#####  &nbsp; &nbsp; &nbsp;  4. 스토리지 추가(디스크)
#####  &nbsp; &nbsp; &nbsp;  5. 태그 추가
#####  &nbsp; &nbsp; &nbsp;  6. 보안 그룹 구성
#####  &nbsp; &nbsp; &nbsp;  7. 인스턴스 시작 검토
#####  &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; - 기존 키 페어 선택 또는 새 키 페어 생성


<br> 


## keyPair 인증

#####  &nbsp; &nbsp; &nbsp;  1. chmod 400 keyPair이름(MAC, 윈도우는 건너띔)
#####  &nbsp; &nbsp; &nbsp;  2. keyPair가 있는 경로로 가서 ssh -i keyPair이름 사용자정보@퍼블릭 아이피 주소
#####  &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; - 사용자정보 : Amazon Linux는 ec2-user / Ubuntu는 ubuntu


#### 쉘 명령어

	1. whoami

		- 사용자 정보 출력

	2. pwd

		- 현재 디렉토리


<br>


##  Node.js 애플리케이션을 배포해보기

#####  &nbsp; &nbsp; &nbsp;  1. NVM(Node Version Manager) 사용
#####  &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; - Node.js 같은 경우 버전이 많다 보니깐 굉장히 버전에 민감함
#####  &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; - 이것들을 사용 요건에 맞추어 버전 상관없이 깔다보면 많이 더러워짐
#####  &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; - 이런 현상의 파편화된 것을 최소하 하고자 버전을 관리해주는 것을 사용

<br>

#####  &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; - 설치 &nbsp; &nbsp; https://github.com/nvm-sh/nvm/blob/master/README.md
#####  &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; - node의 어떤 버전을 사용할지 알려줘야 함 (nvm install --버전 명)
#####  &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; 예) nvm install --lts ==> 안정적인 릴리즈 버전
#####  &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; - 설치는 했지만 사용한다고 안했기 때문에 알려줘야 함 (nvm use --버전명)
#####  &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; 예) nvm use --lts
#####  &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; - 버전 확인 node -v, npm -v

<br>

#####  &nbsp; &nbsp; &nbsp;  2. 애플리케이션 만들기
#####  &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; - 폴더 만들기 mkdir 폴더명
#####  &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; - 폴더 들어가기 cd 폴더명
#####  &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; - express 설치 npm i -S express

<br>

#####  &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; - 터미널 하나 더 열어서 pem으로 인스턴스 접속 후 localhost으로 접근
#####  &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; - 퍼블릭 도메인으로 접근
#####  &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; <em>이 때 애플리케이션에 해당하는 포트번호를 AWS EC2 보안 그룹에서 설정해줘야 함 </em> <br>&nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp;  <em> ⇒ 설명란 보안그룹에서 보안그룹을 선택 후 인바운드 규칙을 편집을 누르고 포트를 추가</em>



## EC2 자원 삭제하기

#####  &nbsp; &nbsp; &nbsp;  1. pem 파일 삭제
#####  &nbsp; &nbsp; &nbsp;  2. 아마존 콘솔에 가서 작업탭에 인스턴스 상태 ==> 종료를 클릭
#####  &nbsp; &nbsp; &nbsp;  3. 네트워크 및 보안 탭에 가서 보안 그룹을 삭제
#####  &nbsp; &nbsp; &nbsp;  4. EC2 대시보드 탭에 가서 리소스 란의 키 페어를 누르고 키 페어를 삭제
