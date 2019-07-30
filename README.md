## docker 배포 설정 파일

AWS Elastic Beanstalk로 Docker container를 배포를 하기 위해서는 기존 Dockerfile 말고도 하나가 더 필요합니다. 바로 **Dockerrun.aws.json**이라는 파일입니다. 이 파일을 통해서 EB가 EC2와 어떻게 뭘 공유하고, 어떤 container를 쓸 지 연결됩니다.

1. single container - with_build
2. single container - without_build
3. multi container - without_build


### 1. single container

single container는 `AWSEBDockerrunVersion`이 1인 상태, container 1개만 배포할 때를 말합니다. 주로 API 서버, 통합된 간단한 웹 앱을 배포할 때 씁니다.

이 종류는 다시 
- with_build : 빌드도 EB가 같이하기.
  - 제일 쉬운 형태
  - 매번 빌드를 처음부터 다시 해야하니 시간이 많이 걸림
- without_build : 빌드된 docker만 배포하기
  - 저장소의 url 명시 필요
  - 빌드하는 과정이 따로 이뤄져야함 like Jenkins

이 2가지 방식으로 나뉩니다.


### 2. multi container

multi container 방식은, 무조건 without_build 방식을 통해서만 배포가 가능합니다. 그렇기에 이 역시 build를 하는 과정이 따로 필요합니다.