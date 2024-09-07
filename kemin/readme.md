### Lending - Upside Academy audit

*kemin_Lending에 대한 감사 보고서*

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
    - https://github.com/gdh8230/Lending_solidity/blob/main/src/Lending.sol / https://github.com/gdh8230/Lending_solidity/commit/a699951e7bb896459d14983a6f82268f30b7d1dc
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

### **취약점 #1: `liquidate` 함수의 토큰 수령 누락**

- **심각도 (Severity)**: **치명적 (Critical)**
- **라인 (Line)**: src/Dex.sol : 60
- **설명 (Description)**
    - 청산 로직이 실행 될 때 청산을 실행하는 사람으로부터 `usdc`를 받아않고 그냥 청산을 완료시킨다.
- **영향 (Impact)**
    - 공격자는 본인이 예치를 하고 최대로 빌린다음 전혀 갚지 않고 본인을 본인이 청산하게 된다면, 해당 프로토콜의 모든 금액을 가져 올 수 있다.
- **추천 사항 (Recommendation)**
    - 청산을 할 때 청산을 행하는 사람으로부터 청산시키는 금액만큼을 `transferfrom`을 통해 받아온다.