# PCB와 Context Switching

## PCB (Process Control Block)
- 운영체제가 각 프로세스를 관리하기 위해 사용하는 데이터 구조
- **Process Metadata**를 저장하는 공간
- 운영체제는 PCB를 통해 프로세스를 추적하고 적절한 자원 할당과 스케줄링을 수행하고 관리
- **Context Switching**을 수행할 때 필요한 정보를 제공

### Process Metadata
- 운영체제가 Process Metadata를 이용하여 프로세스 관리
- 프로세스의 특징을 가지고 있음
- **Process Metadata 구조**
  - Process ID (PID): 메모리에 있는 각 프로세스를 식별하기 위한 ID
  - Process State: 프로세스의 상태
  - Program Counter: 프로세스가 다음에 실행할 명령어의 주소 저장
  - CPU Registers: 프로세스가 실행 중에 사용하는 레지스터 값 저장
  - Memory Management Information: 프로세스의 메모리 주소 공간과 관련된 정보 저장
  - I/O Status Information: 프로세스의 입출력 장치와 관련된 상태 정보 저장
  - ...


## Context Switching
- CPU가 여러 프로세스를 관리하고 실행하는 데 필수적인 역할
- CPU가 현재 실행 중인 프로세스의 Context 저장하고, 다음에 실행할 프로세스의 상태를 로드하는 과정
- 여러 프로세스를 동시에 실행하는 것처럼 보임 -> 여러 프로세스를 번갈아가며 실행하는 멀티태스킹 환경의 핵심
- 여러 테스크(프로세스, 스레드)가 번갈아가며 실행해서 동시에 처리될 수 있도록 하는 방법
- CPU 사이클을 소비하므로 자원의 OverHead 발생

### 동작 과정
1. 인터럽트 발생: CPU에서 현재 실행 중인 프로세스의 작업 일시 중지
2. 현재 프로세스 상태 저장: 실행 중인 프로세스의 Context를 현재 프로세스의 PCB에 저장
3. 새로운 프로세스 선택 및 PCB 로드: 다음에 실행할 프로세스의 PCB에서 저장된 Context 로드
4. CPU 레지스터 복원: 새로운 프로세스의 Context를 CPU 레지스터에 복원 -> 새로운 프로세스가 이전에 중단된 시점에서부터 다시 실행

---
**참고자료**
- [What is Context Switching in Operating System?](https://afteracademy.com/blog/what-is-context-switching-in-operating-system/)
