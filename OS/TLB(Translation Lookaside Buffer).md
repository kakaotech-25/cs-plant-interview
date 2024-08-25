# TLB(Translation Lookaside Buffer)

- 소형 하드웨어 캐쉬로 빠른 연관 메모리(associative memory)로 구성
- CPU 내부에 존재하는 고속 캐시 메모리로, 가상 메모리 시스템에서 가상 주소를 물리 주소로 변환하는 데 사용되는 페이지 테이블의 일부를 저장
- 페이지 테이블 조회 시간을 단축시켜 메모리 접근 성능을 향상시키는 데 중요한 역할을 한다.
- 주소 변환 캐시라고도 하는 TLB는 프로세서의 메모리 관리 장치(MMU)의 일부이다.
- 각 항목은 key와 value 두 부분으로 구성된다.
- 실행될때마다 새로운 페이지 테이블에 접근하는 과정을 반복하는 것은 프로세스 실행 속도 면에 있어서 큰 오버헤드이다. 이를 해결하기 위해 TLB가 사용된다.

## 작동방식
<img width="482" alt="image" src="https://github.com/user-attachments/assets/0c52cd16-e0d3-4cef-afd5-b7dff77c2d60">


- CPU에서 논리 주소를 생성하면, 해당 페이지 번호가 TLB에 전달됨
    - TLB는 `참조 지역성`이라는 개념을 기반으로 한다
        
        > CPU가 자주 액세스해야 하는 페이지의 항목만 포함한다는 의미

    - 페이지 번호(page number)가 발견되면(TLB hit), 해당 프레임을 즉시 알 수 있고, 메모리 접근에 사용한다.
    - 만약 페이지 번호가 없으면 (TLB miss), 페이지 테이블을 조회하여 물리 주소를 찾아한다. (→ CPU 종류에 따라 하드웨어적으로 이루어지거나 인터럽트를 통해 운영체제가 처리한다.) 이후 결과를 TLB에 저장하여 후에 같은 페이지에 접근할 때 사용할 수 있도록 한다.
    - TLB가 가득 차면, 기존 항목 중에서 교체될 항목을 선택한다.
        - 교체 정책은 LRU, FIFO부터 RoundRobin, Random 등 다양한 정책이 사용된다.
    - 몇몇 항목은 TLB에 고정 (wired down)한다. (ex. 중요 커널 코드)
    - 접근하려는 메모리의 페이지 번호가 TLB에서 발견되는 비율은 `적중률(hit ratio)` 이라고 한다. 이를 활용하여 실질 접근 시간(EMAT, effective memory acces time)을 계산할 수 있다.
        
        <aside>
        ➡️ (Hit ratio) * (TLB Hit시 접근시간) + (1 - Hit ratio) * (TLB Miss시 접근 시간)
        
        </aside>
        
    - 몇몇 항목에 ASID(address-space identifier)를 저장하여 어떤 프로세스에 속한 페이지인지 알려주어 프로세스의 정보를 보호하기 위해서 사용된다.
        - context switching 시에 전부 flush(플러쉬)하지 않아도 된다.
        - TLB Flush : TLB에 저장된 모든 엔트리를 무효화하는 과정
