### Lending - Upside Academy audit

damon*_Lending에 대한 감사 보고서*

---

### **1. 요약 (Executive Summary)**

감사 프로세스에 대한 간략한 개요를 제공하며, 목표, 범위 및 주요 발견 사항에 대한 요약을 포함합니다.

- **감사 시작일**: 2024.09.07
- **감사 종료일**: 2024.09.07
- **감사자**: bob
- **주요 발견 사항**:
    - 1 개의 정보성 이슈 (Informational Issues)

---

### **2. 감사 개요 (Audit Overview)**

- **감사 이름**: Lending_Audit
- **대상 버전 / 커밋 ID**:
    - https://github.com/gloomydumber/Lending_solidity/blob/master/src/DreamAcademyLending.sol  / https://github.com/gloomydumber/Lending_solidity/commit/2645135fd3ab081ac2a74ab2c0dcf297e28f190c
- **적용 기술**: Smart contracts
- **기술 스택**: Smart contracts [Solidity]

---

### **3. 심각도 범주 (Severity Categories)**

- **치명적 (Critical)**: 공격 비용이 낮고, 서비스의 가용성에 영향을 주거나 금전적 이득을 취할 수 있는 취약점.
- **높음 (High)**: 서비스 운영에 명확한 문제를 초래할 수 있는 취약점. 공격 비용이 높더라도 영향이 큰 경우 포함.
- **중간 (Medium)**: 특정 조건 하에서 서비스에 예기치 않은 영향을 줄 수 있는 취약점.
- **낮음 (Low)**: 서비스에 경미한 영향을 줄 수 있는 취약점. 성공률이 낮거나 영향이 적음.
- **정보성 (Informational)**: 사용자나 프로토콜에 직접적인 영향을 미치지 않는 정보성 발견 사항

---

### **4. 상세 취약점 (Detailed Findings)**

### **취약점 #1: `withdraw` 함수의 `usdc` 계산 오류**

- **심각도 (Severity)**: **정보성 (Informational)**
- **설명 (Description)**
    - `usdc`에 대한 인출에서 요청한 값이 아닌 이자를 계산해서 요청한 `amount`에 덮어 쓰고 있다.
- **영향 (Impact)**
    - 유저가 본인이 요청한 금액만큼 빠지는게 아닌 전체 금액이 빠지기 때문에 의도치 않은 동작이 발생한다.
- **추천 사항 (Recommendation)**
    - 이자 계산과 인출에 관한 로직을 분리하고 변수 관리를 좀 더 명확히 한다.