# 안건 투표하기
> 안건에 투표하기 위한 함수를 안내합니다.
> 다오 멤버만 안건에 투표를 할 수 있습니다.

## DAOAgendaManager: [etherscan link](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484)

---

### [isVotableStatus(uint256 _agendaID)](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F18)

안건 투표 가능한 상태인지 여부

- 파라미터
  - uint256 _agendaID: 조회할 안건 인덱스
- 결과
  - bool: true 이면 투표 가능한 상태, false 이면 투표 불가능한 상태

*********


### [hasVoted(uint256 _agendaID, address _user)](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F17)

_user가 특정 안건에 투표했는지 여부

- 파라미터
  - uint256 _agendaID: 확인할 안건 인덱스
  - address _user: 확인할 계정 주소
- 결과
  - bool: true 이면 투표했음, false 이면 투표안했음.

*********

### [isVoter(uint256 _agendaID, address _user)](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F19)

_user가 특정 안건의 투표자인지 여부

- 파라미터
  - uint256 _agendaID: 확인할 안건 인덱스
  - address _user: 확인할 계정 주소
- 결과
  - bool: true 이면 투표자임, false 이면 투표자가 아님.

*********


## Candidate / CandidateAddOnProxy  (다오 멤버마다 Candidate주소가 다름)

*********

### candidate()
Candidate 컨트랙의 실제 운영자 주소를 확인할 수 있습니다.

- 파라미터
  - 없음
- 결과
  - candidate 계정 주소

*********


### castVote(uint256 _agendaID, uint256 _vote, string calldata _comment)

candidate() 계정만 이 함수를 실행하여 투표를 할 수 있습니다.

- 파라미터
  - uint256 _agendaID: 조회할 안건 인덱스 (0부터 시작)
  - uint256 _vote: 0:기권, 1:찬성, 2:반대
  - string _comment: 투표시 의견을 기록할 수 있습니다.
- 결과
  - 없음

*********

