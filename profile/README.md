# Solra 🌞🚀

## 1. 🧭 프로젝트 소개

**SOLRA**는 *Solar + Infra*의 합성어로,  
어디서든 항상 떠 있는 태양처럼 안정적이고 지속 가능한 인프라를 제공하겠다는 의지를 담은  
Kubernetes 통합 관리 플랫폼입니다.

> **Secure On-premise Lightweight Resource Automation**  
> → 기업 내부망에서 Kubernetes 클러스터와 리소스를 안전하게 자동화하고 제어하는 B2B 전용 SaaS 솔루션

---

### 🔎 배경 및 문제 정의

기존 Kubernetes 운영 환경에서의 문제점:

- 다수의 클러스터 관리 포인트 분산 → 통합 관리 어려움
- 사용자/부서별 접근 권한 미흡 → 보안 취약성
- GitOps, 모니터링, 테스트 자동화 → 조직마다 개별 운영
- UI 기반 관리 부재 → DevOps 학습 비용 상승

**SOLRA는 이러한 문제를 해결하고자**  
기업이 자체 구축한 Kubernetes 클러스터를 중앙에서 통합 관리하며,  
보안과 자동화를 동시에 강화하는 플랫폼으로 설계되었습니다.

---

## 2. 🌟 주요 특징 및 핵심 기능

| 범주                  | 설명                                                                |
| --------------------- | ------------------------------------------------------------------- |
| 🧑‍💼 사용자/조직 관리   | ROOT, ORG_ADMIN, DEPT_ADMIN 권한 분리 및 부서별 리소스 제어         |
| 📦 K8s 클러스터 관리  | 온프레미스 & 퍼블릭 클라우드(AWS, GCP, Azure) 클러스터 등록 및 조회 |
| 🚀 리소스 배포 자동화 | Argo CD + GitOps 기반 선언적 배포 및 자동 복구                      |
| 🔐 RBAC + PBAC 권한   | 역할(Role) + 권한(Permission) 기반 세분화된 접근 제어               |
| 📊 모니터링 대시보드  | Prometheus + Grafana로 실시간 메트릭, Alertmanager로 알림 설정      |
| 💥 Chaos Engineering  | Kube-monkey를 통한 무작위 Pod 종료/복구로 인프라 탄력성 검증        |

---

## 3. 🏢 활용 대상

- 사내 Kubernetes 인프라를 보유한 기업
- 팀/부서별 쿠버네티스 리소스 접근 제어가 필요한 DevOps 팀
- GitOps, 모니터링, Chaos Engineering을 일원화하려는 인프라 운영팀

---

## 4. 👨‍💻 주요 화면 (예정)

> 📸 주요 화면 스크린샷 및 GIF는 추가 예정입니다.

---

## 5. 👥 팀원 소개

| <img src="https://avatars.githubusercontent.com/u/107902336?v=4" width="220" /> | <img src="https://avatars.githubusercontent.com/u/193316939?v=4" width="220" /> | <img src="https://github.com/EOTAEGYU.png" width="220" /> |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | --------------------------------------------------------- |
| 김대연<br/>[@dyoun12](https://github.com/dyoun12)                               | 박재희<br/>[@JaeHee-devSpace](https://github.com/JaeHee-devSpace)               | 어태규<br/>[@EOTAEGYU](https://github.com/EOTAEGYU)       |

---

## 6. 🛠️ 기술 스택

<image src = "https://github.com/solra-org/.github/blob/main/images/Solra%20%EA%B8%B0%EC%88%A0%20%EC%8A%A4%ED%83%9D.png?raw=true">

### 📌 백엔드 & 데이터 처리

- **Spring Boot**: 백엔드 API 서버
- **Fabric8 Kubernetes Client**: 클러스터 연동
- **MySQL**: 사용자, 조직, 클러스터 메타데이터 저장
- **Redis**: JWT 및 세션 관리
- **Terraform, Ansible**: 인프라 자동화

### 📊 모니터링 & Chaos Engineering

- **Prometheus, Grafana**: 메트릭 수집 및 시각화
- **Alertmanager**: 알림 시스템
- **Kube-monkey**: Chaos Engineering 테스트

### ⚙️ 인프라 & DevOps

- **Kubernetes (K8s)**: 컨테이너 오케스트레이션
- **Argo CD**: GitOps 기반 배포
- **NGINX**: 리버스 프록시, 트래픽 라우팅
- **Git**: 형상 관리

### 🌐 프론트엔드

- **React**: Web UI

---

## 7. 🏗️ 아키텍처

### VMware 기반 시스템 아키텍처

<image src = "https://github.com/solra-org/.github/blob/main/images/%EC%8B%9C%EC%8A%A4%ED%85%9C%20%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98.png?raw=true" width = 500>

### 📦 **VMware 구성 요약**

- **VMware ESXi**
  - 물리 서버에서 직접 실행되는 하이퍼바이저
  - VM(가상머신)들을 호스팅
- **VMware vCenter Server**
  - 여러 ESXi 서버와 VM을 중앙 관리
  - VM 배포, 리소스 할당, 모니터링, 마이그레이션 등을 관리
- **VMware vSphere Client**
  - 관리자/운영자가 접속해 VM과 vCenter 관리

---

### 🗄️ **VM 설계표**

| 역할                             | 구성 내용                                               |
| -------------------------------- | ------------------------------------------------------- |
| **HAProxy** (lb-node)            | 2vCPU, 2GB RAM, 100GB Disk, IP 10.5.100.10              |
| **Control Plane** (master-1/2/3) | 각 2vCPU, 4GB RAM, 100GB Disk, IP 10.5.100.11~13        |
| **Worker Node** (worker-1/2/3)   | 각 4vCPU, 8GB RAM, 100GB Disk, IP 10.5.100.21~23        |
| **Gitlab**                       | 4vCPU, 8GB RAM, 100GB Disk, IP 10.5.100.30              |
| **Database Master/Slave**        | 각 4vCPU, 8GB RAM, 200GB Disk, IP 10.5.100.41/42        |
| **NAT Server**                   | 2vCPU, 4GB RAM, 50GB Disk, IP 10.0.100.14, 192.168.0.24 |
| **DNS Server**                   | 2vCPU, 4GB RAM, 30GB Disk, IP 10.0.100.11               |

### 서비스 아키텍처

<image src = "https://github.com/solra-org/.github/blob/main/images/%EC%84%9C%EB%B9%84%EC%8A%A4%20%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98.png?raw=true">

🧑‍💻 **Developer (개발자)**

- GitLab Server에 git commit & push로 코드 푸시
- GitLab에서 CI/CD 파이프라인(Webhook) 자동 트리거

🛠 **GitLab Server**

- CI/CD 파이프라인: Jenkins Master + Agents로 빌드/배포
- Manifest 관리: Kubernetes 리소스 매니페스트 업데이트 및 GitOps 리포로 커밋

⚙️ **CI/CD (Jenkins)**

- Master → Agents에게 작업 분배
- 최종적으로 Docker 이미지 빌드 후 harbor로 Push

📦 **Solra-harbor (Harbor)**

- GitLab CI/CD에서 빌드한 Docker 이미지 저장소
- Argo CD가 Pull하여 Kubernetes에 배포

🚀 **Argo CD**

- GitOps 방식으로 manifest, 이미지 pull
- Kubernetes 클러스터 내 애플리케이션 자동 배포 및 동기화 관리

🌐 **Ingress Controller**

- 외부에서 들어오는 트래픽을 서비스별로 라우팅 (예: NGINX Ingress)

💥 **Kube-monkey**

- Chaos Engineering 툴
- → 무작위로 Pod를 종료하여 클러스터의 복원력 테스트

📊 **Monitoring Stack**

- Grafana: 시각화 대시보드
- Prometheus: 메트릭 수집
- Alertmanager: 경보/알림
- Loki: 로그 수집/검색

🧩 **Solra 플랫폼 구성**

- Vite: 프론트엔드 빌드 툴 (React/JS 등)
- Spring Boot: 백엔드 API 서버
- Redis: 캐시/세션 관리 (master-slave 구성)

💾 **RDBMS**

- MySQL master-slave 구조로 데이터 저장

🛡 **WireGuard VPN Server**

- 사내/외부 접속 시 안전한 VPN 터널 제공

🖥️ **Lb Server (HAProxy)**

- 로드 밸런싱, L7 트래픽 관리

---

## 8. 📁 프로젝트 구성

```
/backend # Spring Boot API 서버
/frontend # React 기반 Web UI
/infra # Terraform, Ansible 스크립트
/monitoring # Prometheus, Grafana, Alertmanager 설정
/chaos-engineering # Kube-monkey 설정
/docs # 설계 및 문서 자료
```

---

## 9. 💭 기술적 고민

- RBAC & PBAC 설계: 단순 역할 분리 → 다계층 권한 설계로 확장
- 퍼블릭 클라우드 & 온프레미스 동시 지원 아키텍처
- GitOps 자동화 vs 수동 배포 공존 방안
- Chaos Engineering 도입의 안전성 및 범위

---

## 10. 🔧 향후 개선 방향

- 🔒 OIDC 연동으로 외부 인증 지원
- 🌍 다국어 Web UI 제공
- 🛡️ 롤백 및 장애 대응 로직 고도화
- ☁️ Oracle, IBM Cloud 등 클라우드 플랫폼 확장

---
