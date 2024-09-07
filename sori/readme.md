### Lending - Upside Academy audit

 *sori_Lending에 대한 감사 보고서*

---

### **1. 요약 (Executive Summary)**

감사 프로세스에 대한 간략한 개요를 제공하며, 목표, 범위 및 주요 발견 사항에 대한 요약을 포함합니다.

- **감사 시작일**: 2024.09.07
- **감사 종료일**: 2024.09.07
- **감사자**: bob
- **주요 발견 사항**:
    - 1 개의 치명적 이슈 (Critical Issues)
    - 2 개의 높은 위험도 이슈 (High Issues)
    - 1 개의 중간 위험도 이슈 (Medium Issues)

---

### **2. 감사 개요 (Audit Overview)**

- **감사 이름**: Lending_Audit
- **대상 버전 / 커밋 ID**:
    - https://github.com/ExploitSori/Lending_solidity/blob/main/src/DreamAcademyLending.sol / https://github.com/ExploitSori/Lending_solidity/commit/1f39399d0abc00aa65f00de99926c9e172513405
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

### **취약점 #1: `deposit` 함수의 연산자 오류**

- **심각도 (Severity)**: **높음 (High)**
- **라인 (Line)**: src/Dex.sol : 61 - 69
- **설명 (Description)**
    - `deposit`을 할 때 기존 금액에 더하는 것이 아닌 덮어 쓰는 형식으로 구현되어 있음
- **영향 (Impact)**
    - 유저가 아무리 예치를 해도 마지막에 예치한 금액만 인정이 되어 이전에 예치한 금액에 대한 권리를 잃어버리게 됨.
- **추천 사항 (Recommendation)**
    - =를 += 으로 수정 요망.

### **취약점 #2: `borrow` 함수의 전송 오류**

- **심각도 (Severity)**: **높음 (High)**
- **라인 (Line)**: src/Dex.sol : 102
- **설명 (Description)**
    - 이더를 빌리는 로직으로 보여지지만 실제로는 `msg.sender`의 `usdc`를 가져오고 있음.
- **영향 (Impact)**
    - 유저는 `eth`를 빌릴 목적으로 함수를 실행하면 가지고 있는 `usdc`를 컨트랙에 뺏기게 됨.
- **추천 사항 (Recommendation)**
    - `eth`를 전송해주는 로직으로 수정을 요함.

### **취약점 #3: `repay` 함수의 검증 오류**

- **심각도 (Severity)**: **중간 (Medium)**
- **라인 (Line)**: src/Dex.sol : 147
- **설명 (Description)**
    - `usdc`를 통해 `eth`를 빌리고 상환을 하려는 상황에서 상환을 하려면 `eth`를 예치한 상태여야 함.
- **영향 (Impact)**
    - 유저가 `ETH`의 대출을 실행하고 갚으려고 하면 `ETH`를 상환하려는 만큼 예치를 해야하는 아이러니한 상황이 생긴다.
- **추천 사항 (Recommendation)**
    - 해당 부분을 삭제한다.

### **취약점 #4: `withdraw` 함수의 검증 부족**

- **심각도 (Severity)**: **치명적 (Critical)**
- **라인 (Line)**: src/Dex.sol : 206 - 240
- **설명 (Description)**
    - 인출하는데 있어 조건 검사 없이 인출이 실행된다.
- **영향 (Impact)**
    - 공격자가 돈을 예치한 다음 해당하는 최대한 많은 양을 `borrow`한 다음 본인의 예치한 금액을 인출하는 방법으로 여러 주소로 실행한다면 프로토콜의 모든 금액을 빼갈 수 있다.
- **추천 사항 (Recommendation)**
    - `withdraw`함수에 빌린금액에 비례하여 `LTV` 조건 검사를 필요로 한다.