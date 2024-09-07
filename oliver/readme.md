### Lending - Upside Academy audit

Oliver_*Lending에 대한 감사 보고서*

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
    - https://github.com/oliverslife/Lending_solidity/blob/master/src/DreamAcademyLending.sol / https://github.com/oliverslife/Lending_solidity/commit/a88436873ff204bcc0cc337eddefe94782384ef3
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

## **취약점 #1: `repay` 함수의 반환처리 누락**

- **심각도 (Severity)**: **치명적 (Critical)**
- **라인 (Line)**: src/Dex.sol : 60
- **설명 (Description)**
    - `repay`를 할 때 프로토콜에서의 값만 업데이트를 하고 실제로 반환받지 않고있다.
- **영향 (Impact)**
    - 공격자가 실제 금액은 반환하지 않으면서 반환이 완료된 것으로 인정되기 때문에 프로토콜의 모든 `usdc`를 훔쳐 갈 수 있다.
- **추천 사항 (Recommendation)**
    - 유저의 금액을 `transferfrom`을 통해 반환 받는 로직이 필요로하다.