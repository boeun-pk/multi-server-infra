# 리눅스 기반 다중 서버 인프라 구축

Ubuntu 기반 가상 머신 4대로 로드밸런서·웹서버·DB서버를 분리 구성하고,
Prometheus, Grafana 모니터링 대시보드로 리소스를 실시간 감시할 수 있는 프로젝트입니다.

> 진행 기간: 2026.04 ~ 2026.05



## 아키텍처

![architecture](./images/architecture.png)

- 0호기(LB) → 1호기/3호기(Web) → 2호기(DB)
- 1호기 장애 시 3호기로 자동 전환


## 기술 스택

![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=flat&logo=ubuntu&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=flat&logo=nginx&logoColor=white)
![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=flat&logo=mariadb&logoColor=white)

![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=flat&logo=nginx&logoColor=white)
![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=flat&logo=mariadb&logoColor=white)
![Ansible](https://img.shields.io/badge/Ansible-EE0000?style=flat&logo=ansible&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat&logo=grafana&logoColor=white)



## 디렉토리 구조

multi-server-infra/
│
├── site.yml                    # 마스터 플레이북 - 전체 인프라 자동 구축
├── hosts.yml                   # 인벤토리 - 서버 목록 및 vault 변수 연결
├── hosts.ini                   # 인벤토리 참고용 (비밀번호 없는 버전)
├── .gitignore                  # vault.yml 깃허브 업로드 제외
├── README.md                   # 프로젝트 설명
│
├── mariadb_setup.yml           # DB 서버 구축 자동화
├── web_setup.yml               # Web 서버 구축 및 PHP 배포 자동화
├── lb_setup.yml                # 로드밸런서 구축 자동화
├── node_exporter_setup.yml     # 전체 서버 모니터링 에이전트 설치 자동화
├── prometheus_setup.yml        # Prometheus + Grafana 설치 자동화
│
├── group_vars/
│   └── all/
│       └── vault.yml           # ansible vault로 암호화된 서버 비밀번호 (gitignore 처리)
│
└── templates/
    ├── index.php.j2            # PHP 웹 페이지 템플릿 (DB 연결 및 접속 로그)
    ├── lb_default.conf.j2      # Nginx 로드밸런서 설정 템플릿
    └── nginx_web.conf.j2       # Nginx + PHP-FPM 연동 설정 템플릿



## 주요 기능 
- 다중 서버 구축, 자동화, 로드밸런싱, 모니터링


## 트러블슈팅

### CPU 모니터링 스크립트 오류 및 측정 방식 개선

| 구분 | 내용 |
|---|---|
| 문제 상황 | CPU 사용량이 100%로 잘못 표시됨 |
| 원인 파악 | awk 계산 방식이 서버 출력 포맷과 불일치 |
| 해결 방법 | mpstat으로 측정 방식 변경 |
| 결과 | 실제 부하가 정상적으로 반영됨 |


| 구분 | 내용 |
|---|---|
| 문제 상황 | CPU 사용량이 100%로 잘못 표시됨 |
| 원인 파악 | awk 계산 방식이 서버 출력 포맷과 불일치 |
| 해결 방법 | mpstat으로 측정 방식 변경 |
| 결과 | 실제 부하가 정상적으로 반영됨 |




## 실행 방법
git clone부터 site.yml 실행까지 순서



## 회고 및 개선할 점
이걸 aws 에 올려서 서버 만들고 바로 자동화 툴로 서버 세팅하는 것도 하려고 계획함. 

실제 가동되는 서비스를 올려보지 못한 것이 아쉬움 




