# 2장 운영체제 개요

## 1. 운영체제의 목적

운영체제?

- 응용 프로그램의 실행 제어하는 프로그램

운영체제의 목적

- 편리성 : 컴퓨터 편리하게 사용
- 효율성 : 컴퓨터 시스템 자원 효율적인 방법으로 사용
- 발전성 : 새로운 시스템 기능 도입으로 계속 발전해 나가야..

운영체제의 기능

- 컴퓨터 사용자와 하드웨어 사이 중재자 역할
- 사용자 관점 : 사용자/컴퓨터 인터페이스로서 운영체제
    - 사용자가 컴퓨터를 손쉽게 사용할 수 있게 해줌
    - 컴퓨팅 환경 제공
- 시스템 관점 : 자원관리자로서 운영체제
    - 일반적인 컴퓨터 소프트웨어와 동일하게 기능 (운영체제도 SW다)
    - 수시로 응용에 제어 양도해가며 실행, 스케줄링 기능

커널

- 주 메모리에 상주하는 운영체제 핵심
- 자주 사용되는 운영체제의 영역

운영체제 발전의 용이성

- 운영체제가 계속해서 버전 업그레이드 하는 이유
    - 하드웨어 업그레이드
    - 새로운 유형의 하드웨어 지원, 서비스 도입
    - 버그 수정

## 2. 운영체제의 발전

순차처리 → 단순일괄 처리 시스템 → 멀티프로그래밍 일괄처리 시스템 → 시분할 시스템

### 순차처리

- 운영체제 없음
- **콘솔**을 통해 운영
- 종이로 CPU 사용 신청하는 CPU 스케줄링 시간낭비 문제

### 단순 일괄 처리 시스템

**모니터**로 일괄처리 작업

- 제어 → 모니터 → 다음 작업 읽음

JCL(Job Control Language) : 모니터가 이해할 수 있는 명령

- 사용하는 컴파일러, 데이터가 무엇인지 제공

모니터가 필요로 하는 하드웨어 기능

- 메모리 보호
- 타이머 : 단일작업이 시스템 독점하지 못하도록
- 특권 명령어 : 모니터만 수행할 수 있음
- 인터럽트 : 제어를 운영체제와 사용자 프로그램 사이에서 전달

비효율성

- 처리기 진행 전 IO 명령어 대기해야 함
- A : 수행 - 대기 - 수행 - 대기

### 멀티프로그래밍 일괄처리 시스템

- **여러개의 프로그램**이 메모리에 올라와 CPU를 번갈아가며 사용
- 운영체제 기능
    - 운영체제에 의해 IO 작업 수행
    - 메모리 관리 → 여러개의 job에 메모리 나눠 할당
    - CPU 스케줄링(=interupt, 문맥교환) : 준비 상태의 작업중 하나 선택해 CPU 할당
- 멀티프로그래밍 목적
    - CPU 사용률 극대화
- 단점
    - 수행중인 작업과 상호작용 안됨

### 시분할 시스템 (Time Sharing)

- 교행 수행 시켜줌
- 비자발적으로 CPU 놓을 수 있음
    - = 운영체제가 강제로 끊음
- 처리기 시간을 여러 사용자가 공유 (번갈아 사용)
- 다수 사용자는 터미널 통해 동시에 시스템 접근
    - OS : CPU 시간 쪼개서 각 사용자 프로그램 실행

|  | 일괄처리 다중프로그래밍 | 시분활 |
| --- | --- | --- |
| 주요 목적 | 처리기 이용률 최대화 | 응답시간 최소화 |
| 운영체제에 대한 명령어 소스 | 작업과 함께 제어 언어 명령어 제공 | 터미널에서 입력되는 명령어 |
|  | 자발적으로 CPU 놓음 | 비자발적으로 CPU 놓을수 있음 |

## 3. 주요 성과

### 프로세스 관리

- 프로세스란
    - 운영체제 내부구조 중 가장 기초
    - 실행중 프로그램<인스턴스<개체<활동 단위
- 프로세스 관리
    - 멀티 프로그래밍 일괄처리 동작 : 처리기가 주 메모리의 여러 프로그램을 돌아가며 실행
    - 시분할 : 개별사용자에 빨리 응답 & 동시에 여러 사용자들 지원 (타이밍, 동기화)
    - 실시간 트랜잭션 시스템 : 한 DB에 대해 동시에 질의와 갱신
- 운영체제 오류의 주요 원인
    - 부적절한 동기화 : 서로 공유 자원 사용하려 할때
    - 비결정적 프로그램 실행 : 스케줄링 순서에 따라 실행결과 달라짐
    - 상호배제 실패 : 동시에 공유자원 사용 시도한 경우
    - 교착상태 (deadlock) : 서로 상대방 실행 기다리며 무한 대기
- 프로세스 구성요소
    - 코드 : 실행 가능한 프로그램
    - 데이터 : 프로그램 수행에 필요한 데이터 (ex. 변수, 작업공간, 버퍼..)
    - 실행 문맥(= 프로세스 상태)
        - OS가 실행문맥 통해 프로세스 감시, 제어

실행 중인 프로세스의 모든 상태 → 프로세스 문맥에 저장

### 메모리 관리

메모리 관리를 위해 OS가 지원할 핵심 기능들

- 프로세스 분리
- 자동할당 및 관리
- 모듈식 프로그래밍 지원
- 보호 및 접근 제어
- 영구적 저장 지원

### 가상 메모리

- 논리적 관점에서 메모리 주소 지정할 수 있게 함
- 프로그램들이 통일된 주소 지정 방식 사용하게 함

### 페이징

- 프로세스 메모리 → **페이지**라는 **고정 크기 블록** 단위로 잘라 관리
- 프로그램이 가상주소를 통해 원하는 워드에 접근
    - 가상 주소 : 가상페이지 번호 + 페이지 내 옵셋
- 프로그램에서 사용한 가상 주소 → 주메모리의 물리 주소로 동적으로 변경
    - OS가 CPU의 MMU에 매핑 정보 제공

### 정보 보호와 보안

- 가용성
- 인증
- 데이터 무결성
- 기밀성

### 스케줄링과 자원관리

- OS의 핵심기능 : 자원관리
- 효율성, 공정성, 반응시간 차등화

## 4. 최근 운영체제로의 발전

- 필요에 따라 OS 구조 바꾸는 방법으로 새 기능 지원
    - 마이크로커널 구조
    - 멀티쓰레딩
    - 대칭적 멀티프로세싱
    - 분산 운영체제
    - 객체지행 설계

### 마이크로커널 구조

- 핵심 기능만 커널에 포함시킴
    - 주소 공간관리
    - 메모리 프로세스간의 통신
    - 운체 기능등이 밖에 나와있음
- 구현 단순화
- 유연성 제공
- 분산환경에 적합한 커널 구조

### 멀티 쓰레딩

- 한프로세스를 여러개의 스레드로 나누어 병행적 실행
- 쓰레드
    - CPU에 작업 할당하는 단위
    - 순차적으로 실행, 인터럽트 가능
- 프로세스
    - 시스템 자원들의 컨테이너 역할
    - 응용의 모듈화 수준과 관련된 사건들의 타이밍 조절 가능

### 대칭형 멀티프로세싱

여러 프로세스들이 동시에 실행될 수 있는 구조

- OS가 스레드나 프로세스들 각 처리기로 스케줄링
- 처리기간 동기화도 책임짐

장점

- 성능 : 서로 다른 처리기상 여러 프로세스 동시 실행 가능
- 가용성 : 처리기 하나 고장나도 전체는 돌아감
- Incremental Growth : 처리기 추가한 만큼 전체 성능 높아짐
- 확장성 : 처리기 개수 조절하여 다양한 제품 출시 가능

## 5. 결함허용

- hw, sw 고장에도 sw가 정상작동할 수 있는 능력
- 대개 어느정도의 복사본 (여분 설비) 동반됨
- 시스템 신뢰성 높이기 위해 고안됨

### 결함 허용의 기본 개념

- 결함 허용 수준 측정하는 단위
    - 신뢰성 : t=0 시간에 정상 작동하던 시스템이 임의시간까지 계속 정상적으로 작동할 확률
    - Mean Time To Failure (MTTF): 결함 발생하기까지의 평균시간
    - Mean Time To Repair (MTTR): 결함이 발생한 것을 수리완료하기까지 걸리는 평균시간
    - Availability(A) : 총 시간 중 사용자의 요청을 서비스 할 수 있던 시간이 얼마나 되는지의 비율

### 결함 유형 및 여분 설비 유형

- 영구적
    - 한번 발생하면 영구적으로 존재
    - 새것으로 교체되거나 수리될때까지
- 일시적
    - 모든 동작환경에서 항시 나타나지 않음
    - 단발적 : 한번 발생하고 마는 유형
    - 간헐적 : 예상할 수 없는 시점에 수차례 발생

### 운영체제의 결함허용 기법

- 프로세스 분리 : 오류가 난 프로세스에 영향주지 않게
- 병행성 제어 : 공유 디스크 혼자 쓰기 못하게
- 가상기계 : 어떤 CPU를 특정 응용만 쓰게
- 체크 포인트와 롤백 : 그 시점까지 저장. 오류 커지면 롤백

## 6. 멀티프로세서와 멀티코어를 위한 운영체제 설계사항

- SMP를 위한 고려사항
    - 동시 병행 프로세스 or 스레드
    - 스케줄링
    - 동기화
    - 메모리 관리
    - 신뢰성과 결함 허용
