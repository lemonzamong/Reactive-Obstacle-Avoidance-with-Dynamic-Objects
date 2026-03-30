# Reactive Obstacle Avoidance with Dynamic Objects
**목표:** Deep RL 및 HRL을 활용하여 동적 장애물을 회피하며 미션을 수행하는 로봇 에이전트 개발

---

## 📅 프로젝트 전체 타임라인

### **Phase 1: 환경 구축 및 데이터 확보 (1~3주)**
> **Key Goal:** 시뮬레이션 환경 커스텀 및 전문가 시연 데이터셋 구축

| 주차 | 단계 | 주요 활동 (Tasks) | 산출물 (Outputs) |
| :--- | :--- | :--- | :--- |
| **1주차** | **Env Setup** | `robosuite` 설치, Panda 로봇 제어, 동적 장애물(Sphere) 삽입 코드 구현 | 커스텀 환경 코드, 장애물 구동 영상 |
| **2주차** | **Data Collection** | 전문가 시연(Teleop)을 통한 성공 데이터 수집 (50~100 세트) | `.hdf5` 전문가 데이터셋 |
| **3주차** | **Data Validation** | 데이터 Playback 검증, Observation Space(위치, 속도 등) 정합성 팩트 체크 | 데이터 구조 분석 리포트 |

---

### **Phase 2: Skill Discovery 및 하위 정책 학습 (4~6주)**
> **Key Goal:** 복잡한 동작을 의미 있는 단위 스킬(Primitives)로 분리 및 학습

| 주차 | 단계 | 주요 활동 (Tasks) | 산출물 (Outputs) |
| :--- | :--- | :--- | :--- |
| **4주차** | **Skill Definition** | '접근(Reach)', '파지(Grasp)', '회피(Avoid)' 등 하위 스킬 구간 정의 | 스킬 분류 가이드라인 |
| **5주차** | **Low-level Training** | `robomimic`을 활용한 BC-RNN 기반 하위 정책 학습 | 스킬별 로컬 체크포인트 |
| **6주차** | **Unit Testing** | 개별 스킬의 성공률 및 강인함(Robustness) 정량적 평가 | 스킬 성능 평가표 |

---

### **Phase 3: Hierarchical RL 통합 및 최적화 (7~9주)**
> **Key Goal:** 상위 정책(Manager) 학습을 통해 동적 상황 판단 지능 부여

| 주차 | 단계 | 주요 활동 (Tasks) | 산출물 (Outputs) |
| :--- | :--- | :--- | :--- |
| **7주차** | **HRL Architecture** | 상위 정책(High-level) 설계 및 Sub-goal 전달 로직 구현 | HRL 통합 코드 아키텍처 |
| **8주차** | **RL Training** | `PPO` / `SAC` 알고리즘 적용, 충돌 패널티 기반 보상 함수 최적화 | WandB 학습 로그 및 그래프 |
| **9주차** | **Curriculum RL** | 장애물 속도 및 궤적 난이도를 점진적으로 상향하며 학습 | 최적화된 하이 레벨 모델 |

---

### **Phase 4: 검증 및 최종 배포 (10~12주)**
> **Key Goal:** 일반화 성능 검증 및 차세대 시뮬레이터(Isaac Lab) 이식 테스트

| 주차 | 단계 | 주요 활동 (Tasks) | 산출물 (Outputs) |
| :--- | :--- | :--- | :--- |
| **10주차** | **Generalization** | 미학습 장애물 궤적 및 속도에 대한 성공률(Success Rate) 측정 | 최종 성능 벤치마크 결과 |
| **11주차** | **Sim-to-Sim** | `Isaac Lab` 환경 이식 및 물리 엔진 변화에 따른 성능 변화 분석 | Isaac Lab 구동 영상 |
| **12주차** | **Final Report** | 기술 문서 작성, 코드 정리, 최종 데모 및 스터디 결과 공유 | 최종 프로젝트 레포지토리 |

---

## 🛠️ 공통 기술 스택
*   **Simulator:** `robosuite` (MuJoCo 기반), `Isaac Lab` (검증용)
*   **Framework:** `robomimic`, `PyTorch`
*   **Algorithms:** BC-RNN, HBC(Hierarchical BC), PPO, SAC
*   **Logging:** `WandB` (Weights & Biases)

---

## ⚠️ 권고사항
1.  **데이터 통일:** 2주차 산출물인 `.hdf5` 파일의 Key값(`obstacle_vel` 등)이 다를 경우 이후 단계 진행이 불가하므로 엄격히 관리할 것.
2.  **로그 공유:** 모든 학습 결과는 WandB를 통해 실시간 공유하며, 피드백 세션을 가질 것.
3.  **사양 대응:** 저사양 PC 사용자는 11주차 이전에 클라우드 자원이나 고사양 팀원의 리소스를 빌려 최종 검증을 마칠 것.