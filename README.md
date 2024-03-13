## 🚨 어플리케이션 플랫폼 기술지원 종료 
#### 어플리케이션 플랫폼 기술지원 종료 일정 : 2025년 1월 31일  
지원 종료일 전까지 기 보급된 어플리케이션 플랫폼 유지보수를 위한 업그레이드 버전 및 보안 패치 제공  
지원 종료 이후 보안문제가 발생하여도 기술지원이 불가  

## ap-portal-api-release
<!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->
[![All Contributors](https://img.shields.io/badge/all_contributors-2-orange.svg?style=flat-square)](#contributors-)
<!-- ALL-CONTRIBUTORS-BADGE:END -->

### Portal 배포 방식에 따른 branch 분리
  - Bosh를 이용한 VM 배포
    - branch : "master" branch 사용
    - version 표기 방식 : e.g.) v2.1.0, v2.2.0 ...

  - CF CLI를 이용한 cloudfoundry container 배포
    - branch : "portal-container-infra" branch 사용 (Portal 운영에 필요한 infra환경 구성)
    - version 표기 방식 [version + "-ctn"] : e.g.) v2.2.0-ctn ...

### Application Platform Portal API Release Configuration
  - Bosh를 이용한 VM 배포
    - binary_storage : 1 machine
    - haproxy : 1 machine
    - mariadb : 1 machine
    - ap-portal-registration : 1 machine
    - ap-portal-gateway : 1 machine
    - ap-portal-api : 1 machine
    - ap-portal-common-api : 1 machine
    - ap-portal-log-api : 1 machine
    - ap-portal-storage-api : 1 machine

  - CF CLI를 이용한 cloudfoundry container 배포
    - binary_storage & mariadb : 1 machine

### Create Application Platform Portal API Release
  - Download the latest Application Platform Portal API Release
    ```
    ### Bosh를 이용한 VM 배포
    $ git clone https://github.com/K-PaaS/ap-portal-api-release.git
    $ cd ap-portal-api-release

    ### CF CLI를 이용한 cloudfoundry container 배포
    $ git clone -b portal-container-infra https://github.com/K-PaaS/ap-portal-api-release.git
    $ cd ap-portal-api-release
    ```

  - Download & Copy "source files" into the src directory
    ```
    ## download source files
    $ wget -O src.zip https://nextcloud.k-paas.org/index.php/s/EzLBCjL8L6SjBTp/download

    ## unzip download source files
    $ unzip src.zip

    ## final src directory
    src
      ├── haproxy
      │   └── haproxy-1.6.5.tar.gz
      ├── java
      │   └── server-jre-8u121-linux-x64.tar.gz
      ├── mariadb
      │   └── mariadb-10.5.17-linux-x86_64.tar.gz
      ├── ap-portal-api
      │   └── ap-portal-api.jar
      ├── ap-portal-common-api
      │   └── ap-portal-common-api.jar
      ├── ap-portal-gateway
      │   └── ap-portal-gateway.jar
      ├── ap-portal-log-api
      │   └── ap-portal-log-api.jar
      ├── ap-portal-registration
      │   └── ap-portal-registration.jar
      ├── ap-portal-storage-api
      │   └── ap-portal-storage-api.jar
      ├── python
      │   └── Python-3.6.9.tgz
      └── swift-all-in-one
          └── README.txt ( dependencies : apache2 2.4.58 )
          └── swift-2.31.1.tar.gz

     ----------------------------------------------------------------------------------------------------
     ### CF CLI를 이용한 cloudfoundry container 배포시, 사용하지 않는 source files을 지우고 release를 생성할 수 있다.(Option)
     $ rm -rf src/ap-portal-* src/haproxy src/java

     ### final src directory
     src
       ├── mariadb
       │   └── mariadb-10.5.17-linux-x86_64.tar.gz
       ├── python
       │   └── Python-3.6.9.tgz
       └── swift-all-in-one
           └── swift-2.31.1.tar.gz
     ----------------------------------------------------------------------------------------------------
    ```
  - Create Application Platform Portal API Release
    ```
    ## <VERSION> :: release version (e.g. 2.5.1 or 2.5.1-ctn)
    ## <RELEASE_TARBALL_PATH> :: release file path (e.g. /home/ubuntu/workspace/ap-portal-api-release-<VERSION>.tgz)
    $ bosh -e <bosh_name> create-release --name=ap-portal-api --sha2 --version=<VERSION> --tarball=<RELEASE_TARBALL_PATH> --force
    ```
### Deployment
- https://github.com/K-PaaS/portal-deployment

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://github.com/jinhyojin"><img src="https://avatars.githubusercontent.com/u/76993633?v=4?s=100" width="100px;" alt=""/><br /><sub><b>jinhyojin</b></sub></a><br /><a href="https://github.com/K-PaaS/ap-portal-api-release/issues?q=author%3Ajinhyojin" title="Bug reports">🐛</a> <a href="https://github.com/K-PaaS/ap-portal-api-release/commits?author=jinhyojin" title="Tests">⚠️</a> <a href="https://github.com/K-PaaS/ap-portal-api-release/commits?author=jinhyojin" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/okpc579"><img src="https://avatars.githubusercontent.com/u/55691511?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Ruby</b></sub></a><br /><a href="#infra-okpc579" title="Infrastructure (Hosting, Build-Tools, etc)">🚇</a> <a href="https://github.com/K-PaaS/ap-portal-api-release/commits?author=okpc579" title="Tests">⚠️</a> <a href="https://github.com/K-PaaS/ap-portal-api-release/commits?author=okpc579" title="Code">💻</a></td>
  </tr>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!
