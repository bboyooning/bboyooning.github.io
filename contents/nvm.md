---
date: '2022-08-29'
title: 'NVM'
categories: ['node.js']
summary: 'NVM 이용하여 Node.js 버전 관리하기'
thumbnail: './node.png'
---

### NVM 이란?

- Node Version Manager 의 약자로, 여러 버전의 Node.js 설치 및 버전 변경을 관리해주는 도구
- 상황에 맞게 Node.js 를 원하는 버전으로 설치하거나 변경할 수 있음
- 프로젝트 상황에 맞춰서 이미 짜여져 있는 코드를 분석하거나 리팩토링 할 때 용이

### NVM for Windows 다운로드

- 아래의 경로를 통해 Windows 용 nvm 설치 파일을 다운로드

  - nvm-setup.zip 다운로드
  - https://github.com/coreybutler/nvm-windows/releases
    ![](https://velog.velcdn.com/images/bboyooning/post/9865a90a-d276-43a9-beb1-0fac9f4e5838/image.png)

- 윈도우 터미널(cmd or powershell)에서 아래의 명령어를 입력하면 설치된 NVM 버전 확인 가능

  > `nvm version` > <br>

  ![](https://velog.velcdn.com/images/bboyooning/post/f66137f6-8529-4f3e-a24d-873812c723b8/image.png)

- 아래의 명령어를 입력하면 nvm 에 설치된 node 리스트를 확인할 수 있음

  > `nvm ls` > <br>

  ![](https://velog.velcdn.com/images/bboyooning/post/a954034b-cfd2-4471-8900-94c58c013c1f/image.png)

- 현재 설치할 수 있는 Node 버전 리스트 확인하기
  - https://nodejs.org/ko/download/releases/
- 설치하고 싶은 Node 버전을 아래의 명령어로 설치

  > `nvm install 버전` > <br>

  ![](https://velog.velcdn.com/images/bboyooning/post/629e4185-070f-4e19-aabc-fed879f19da2/image.png)

- 추가한 Node.js 로 버전을 바꾸고 싶으면 아래의 명령어를 이용하여 바꿈

  > `nvm use 버전` > <br>

  ![](https://velog.velcdn.com/images/bboyooning/post/173ee8df-709f-41b1-ac24-eab6300c6ca0/image.png)
  <br>

  > 이때 위와 같은 에러가 발생할 수 있는데, 이건 명령 프롬포트 창을 관리자 모드로 열어줘야함
  > <br>

  ![](https://velog.velcdn.com/images/bboyooning/post/a2b185ed-d2fe-47ec-97dc-9f580489b01e/image.png)

- 관리자 모드로 열어준 다음 변경하면 에러없이 Node.js 버전 변경됨
  <br>
  ![](https://velog.velcdn.com/images/bboyooning/post/1b883956-6658-47fc-b229-53ff92186611/image.png)
