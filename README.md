# 📘 MCPU Control Signal Design

**프로젝트 개요**  
본 프로젝트는 MU0 ISA 기반의 MCPU를 Verilog로 구현하고, 이를 위한 제어 신호(Control Signals)를 정의한 것입니다. 메모리 접근, 레지스터 조작, ALU 제어, 분기 및 점프, FSM 상태 전이 등 다양한 기능에 필요한 제어 신호의 구체적인 정의와 역할을 문서화하여 설계 및 테스트에 활용하였습니다.

---

## ✅ 핵심 제어 신호 요약

### 📂 Memory Control
- **IorD** : 0 = 명령어 접근, 1 = 데이터 접근  
- **MemRead / MemWrite** : 메모리 읽기 / 쓰기 활성화  
- **DatWidth** : 데이터 크기 선택 (단어/하프/바이트/부호 포함)  

### 🧾 Instruction & Register Control
- **IRWrite** : 명령어 레지스터(IR) 기록 허용  
- **RegDst** : 목적 레지스터 선택 (rt/rd/rs/31)  
- **RegDatSel** : 레지스터에 기록할 데이터 원천 선택 (ALU 결과, 메모리, PC 등)  
- **RegWrite** : 레지스터 파일 기록 여부  

### 🔢 Immediate 확장
- **EXTmode** : 부호 확장(1) 또는 0 확장(0)  

### 🧮 ALU Control
- **ALUsrcA / ALUsrcB** : ALU 입력 A, B 선택  
- **ALUop** : 연산 종류 정의 (AND, ADD, MUL, SRA 등)  
- **ALUctrl** : ALU 제어 보조 신호 (오퍼랜드 스왑, 시프트 위치)  

### 🔁 Branch / Jump 제어
- **Branch** : 분기 조건 (BEQ, BNE, 조건 분기 등)  
- **PCsrc** : 다음 PC 갱신 값 선택  
- **PCwrite** : PC 기록 여부  

### 🧠 FSM 상태 전이
- **StateSel** : FSM 다음 상태 제어  
  - 00: 초기화, 01: 명령어 기반, 11: 다음 상태 자동 이동  

---

## 🧑‍💻 활용 방식
이 제어 신호 정의는 PLA 기반 컨트롤러 구현이나 FSM 설계 시 각 명령어 단계별로 어떤 제어 신호가 필요한지를 명확하게 도식화하기 위한 기준 자료로 사용됩니다. 설계의 정확성과 일관성을 유지하는 데 핵심적인 역할을 합니다.
