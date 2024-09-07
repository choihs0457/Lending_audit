### Lending - Upside Academy audit

jeremy*_Lending에 대한 감사 보고서*

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
    - https://github.com/WOOSIK-jeremy/Lending_solidity/blob/main/src/UpsideAcademyLending.sol / https://github.com/WOOSIK-jeremy/Lending_solidity/commit/544c3aff1cac5dd1f996e451c0fcfcd93a274843
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

### **취약점 #1: `firstAccount`에 대한 관리 부족**

- **심각도 (Severity)**: **중간 (Medium)**
- **라인 (Line)**: src/Dex.sol :
- **설명 (Description)**
    - 해당 변수의 증가가 `deposit`에서 이뤄지는데 `liquidate`를 제외하면 해당 변수의 값이 컨트롤 되지 않아서 문제가 야기된다.
- **영향 (Impact)**
    - 유저가 `deposit`을 하고 `withdraw`를 반복하면 `firstAccount`값이 무한정 늘어 날 수 있는데 이렇게 되면  `borrow`함수에서 `ltvLimit`값이 계속해서 내려가고 결과적으로는 언더플로우가 나며 `borrow`가 불가능해진다.
- **추천 사항 (Recommendation)**
    - 이자에 대한 계산으로 인해서 로직이 엉킨 것으로 보인다. 이자와 별개로 LTV를 계산하고 각 변수들의 관리를 좀 더 명확히 한다.