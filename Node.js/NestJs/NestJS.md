# NestJS

## 설치(윈도우) 및 프로젝트 명령어

1. nodejs 설치
   
   - cmd에서 node -v로 버전 및 설치 확인
   
2. cmd에서 npm i -g @nestjs/cli

3. cmd에서 nest new project-name

   3-1. git clone 등 가져온 프로젝트라면 node_modules가 있는지 꼭!! 확인한다. 없으면 `npm install`을 해야한다

- 처음부터 만들기 위해 root 모듈인 app.module.ts 파일과 main.ts파일만 빼고 다 지우기
- 모듈 생성하기
  - Board 모듈 생성 명령어 : nest g module boards 
- Service 생성하기
  - board Service 생성하기 : nest g service boards --no-spec
    - --no-spec : 테스트를 위한 소스 코드 생성x
- uuid 모듈 사용하기
  - npm install uuid --save

