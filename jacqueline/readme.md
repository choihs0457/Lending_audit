### Lending - Upside Academy audit

jacqueline*_Lending에 대한 감사 보고서*

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
    - https://github.com/je1att0/Lending_solidity/blob/main/src/UpsideAcademyLending.sol [/](https://github.com/je1att0/Lending_solidity/blob/main/src/UpsideAcademyLending.sol) https://github.com/je1att0/Lending_solidity/commit/7bb6357b7e5742133581be4acafe811bbbe3ee77
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

### **취약점 #1: `withdraw` 함수의 `usdc` 검증 오류**

- **심각도 (Severity)**: **치명적 (Critical)**
- **라인 (Line)**: src/Dex.sol : 60
- **설명 (Description)**
    - `usdc`에 대한 인출에서 아무런 검증없이 돌려주고있다.
- **영향 (Impact)**
    - 공격자가 예치를 하고 최대한으로 빌린 뒤 돈을 빼가는 방식으로 모든 `usdc`를 빼 갈 수 있다.(그냥 아무 유저나 해당 함수를 실행하면 모든 돈을 그냥 준다.)
- **추천 사항 (Recommendation)**
    - 빌린 금액에 대해 담보가치와의 `LTV`를 계산해서 인출에 제한을 두도록 한다.