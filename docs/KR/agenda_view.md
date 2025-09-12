# 아젠다 상세보기
> 아젠다의 상세 정보를 확인할 수 있는 함수를 안내합니다.
- DAOAgendaManager: [etherscan link](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484)
---


*********

### [agendas(uint256 index)](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F1)

인덱스를 통해 등록된 아젠다 정보 조회

- 파라미터
  - uint256 index: 조회할 아젠다 인덱스 (0부터 시작)
- 결과
  - LibAgenda.Agenda memory: 해당 아젠다의 Agenda 구조체
```
    struct Agenda {
        uint256 createdTimestamp;               /// 아젠다 생성시간 (초)
        uint256 noticeEndTimestamp;             /// 공지 종료시간 (초)
        uint256 votingPeriodInSeconds;          /// 투표 기간 (초)
        uint256 votingStartedTimestamp;         /// 투표 시작시간 (초)
        uint256 votingEndTimestamp;             /// 투표 종료시간 (초)
        uint256 executableLimitTimestamp;       /// 실행 마감시간 (초)
        uint256 executedTimestamp;              /// 아젠다 실행시간 (초)
        uint256 countingYes;                    /// 아젠다 투표 - 찬성수
        uint256 countingNo;                     /// 아젠다 투표 - 반대수
        uint256 countingAbstain;                /// 아젠다 투표 - 기권수
        AgendaStatus status;                    /// 아젠다 상태
        AgendaResult result;                    /// 아젠다 결과
        address[] voters;                       /// 아젠다 투표자 주소배열
        bool executed;                          /// 아젠다 실행여부
    }

    /// status
    enum AgendaStatus { NONE, NOTICE, VOTING, WAITING_EXEC, EXECUTED, ENDED }

    /// result
    enum AgendaResult { PENDING, ACCEPT, REJECT, DISMISS }

```
*********


### [numAgendas()](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F22)

전체 아젠다 개수

- 파라미터
  - 없음
- 결과
  - uint256: 총 아젠다 개수

*********


### [isVotableStatus(uint256 _agendaID)](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F18)

아젠다 투표 가능한 상태인지 여부

- 파라미터
  - uint256 _agendaID: 조회할 아젠다 인덱스
- 결과
  - bool: true 이면 투표 가능한 상태, false 이면 투표 불가능한 상태

*********


### [canExecuteAgenda(uint256 _agendaID)](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F2)

아젠다 실행 가능한 상태인지 여부

- 파라미터
  - uint256 _agendaID: 조회할 아젠다 인덱스
- 결과
  - bool: true 이면 실행 가능한 상태, false 이면 실행 불가능한 상태

*********

### [hasVoted(uint256 _agendaID, address _user)](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F17)

_user가 특정 아젠다에 투표했는지 여부

- 파라미터
  - uint256 _agendaID: 확인할 아젠다 인덱스
  - address _user: 확인할 계정 주소
- 결과
  - bool: true 이면 투표했음, false 이면 투표안했음.

*********

### [isVoter(uint256 _agendaID, address _user)](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F19)

_user가 특정 아젠다의 투표자인지 여부

- 파라미터
  - uint256 _agendaID: 확인할 아젠다 인덱스
  - address _user: 확인할 계정 주소
- 결과
  - bool: true 이면 투표자임, false 이면 투표자가 아님.

*********
