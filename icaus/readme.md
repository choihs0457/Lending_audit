### Lending - Upside Academy audit

*icarus_Lending에 대한 감사 보고서*

---

### **1. 요약 (Executive Summary)**

감사 프로세스에 대한 간략한 개요를 제공하며, 목표, 범위 및 주요 발견 사항에 대한 요약을 포함합니다.

- **감사 시작일**: 2024.09.07
- **감사 종료일**: 2024.09.07
- **감사자**: bob
- **주요 발견 사항**:
    - 1 개의 치명적 이슈 (Critical Issues)

---

### **2. 감사 개요 (Audit Overview)**

- **감사 이름**: Lending_Audit
- **대상 버전 / 커밋 ID**:
    - https://github.com/pluto1011/-Lending-DEX-_solidity/blob/main/src/DreamAcademyLending.sol / https://github.com/pluto1011/-Lending-DEX-_solidity/commit/d22ce57192079037f493b5eee3cad624fdfc2617
- **적용 기술**: Smart contracts
- **기술 스택**: Smart contracts [Solidity]

---

### **3. 심각도 범주 (Severity Categories)**

- **치명적 (Critical)**: 공격 비용이 낮고, 서비스의 가용성에 영향을 주거나 금전적 이득을 취할 수 있는 취약점.
- **높음 (High)**: 서비스 운영에 명확한 문제를 초래할 수 있는 취약점. 공격 비용이 높더라도 영향이 큰 경우 포함.
- **중간 (Medium)**: 특정 조건 하에서 서비스에 예기치 않은 영향을 줄 수 있는 취약점.
- **낮음 (Low)**: 서비스에 경미한 영향을 줄 수 있는 취약점. 성공률이 낮거나 영향이 적음.
- **정보성 (Informational)**: 사용자나 프로토콜에 직접적인 영향을 미치지 않는 정보성 발견 사항.

---

### **4. 상세 취약점 (Detailed Findings)**

## **취약점 #1: 코드 전반에 걸친 조건 검증 문제**

- **심각도 (Severity)**: **치명적 (Critical)**
- **라인 (Line)**: src/Dex.sol : all
- **설명 (Description)**
    - 함수들 곳곳에 특정 상황에 대해서 특정 반환 값을 선언해서 사용중이다.
- **영향 (Impact)**
    - 시스템이 정상적으로 동작하지 않게되고, 특정 상황들만을 가정해서 동작하기 때문에 사실상 모든 부분이 취약하다. 단순한 예시로 `getAccruedSupplyAmount`에서는 `if`문에 걸리지 않으면 리턴값이 없다.
- **추천 사항 (Recommendation)**
    - 코드를 전체적으로 다시 작성해야한다.