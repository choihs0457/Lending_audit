### Lending - Upside Academy audit

muang*_Lending에 대한 감사 보고서*

---

### **1. 요약 (Executive Summary)**

감사 프로세스에 대한 간략한 개요를 제공하며, 목표, 범위 및 주요 발견 사항에 대한 요약을 포함합니다.

- **감사 시작일**: 2024.09.07
- **감사 종료일**: 2024.09.07
- **감사자**: bob
- **주요 발견 사항**:
    - 1 개의 중간 위험도 이슈 (Medium Issues)

---

### **2. 감사 개요 (Audit Overview)**

- **감사 이름**: Lending_Audit
- **대상 버전 / 커밋 ID**:
    - https://github.com/GODMuang/Lending_solidity/blob/main/src/DreamAcademyLending.sol / https://github.com/GODMuang/Lending_solidity/commit/e92439b7237f1e66f68f1ef49ecfe84be21a33a4
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

### **5. 상세 취약점 (Detailed Findings)**

### **취약점 #1: `ETH` 에 대한 처리 부족**

- **심각도 (Severity)**: **중간 (Medium)**
- **라인 (Line)**: src/Dex.sol
- **설명 (Description)**
    - 현재 이더에 대한 부분이 `deposit`을 제외하면 `transfer`에서 `oog`에 걸려 아무것도 동작하지 않고있다.
- **영향 (Impact)**
    - 이더를 예금을 한 유저는 출금이 불가능 한 상태이다. repay함수의 수정 없이 로우콜로만 바꾼다면 eth를 빌린 사람은 상환 자체가 불가능한 상황이 생긴다.
- **추천 사항 (Recommendation)**
    - 로우콜로 대체를 함으로써 해결이 가능하고 추가로 `repay` 함수에서는 이더에 대한 처리가 전혀 없어서 상환이 불가능한 문제가 발생한다. 이 부분을 `ETH` 와 나눠서 처리하도록 해준다.