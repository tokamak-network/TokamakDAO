# 안건 제출
> 다오 안건 제출시에는 수수료(톤)를 지불해야 합니다. 따라서 TON approveAndCall 함수를 이용하여, 정해진 톤을 수수료로 지불하면서, 안건을 제출할 수 있습니다.

---

## 사전 준비사항
1. **지갑 준비**
   - 지갑(메타마스크 등)과 TON 토큰을 준비합니다.
   - 컨트랙트 주소 등은 [contract addresses.md](./contract%20addresses.md) 문서를 참고하세요.

2. **아젠다 수수료 준비**
   - [DAOAgendaManager.createAgendaFees()](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F4) 조회를 통해 아젠다 수수료 톤을 확인해주세요.
   - 준비된 지갑의 톤 보유량이 수수료(톤) 보다 많아야 합니다. 이 금액은 아젠다 제출 수수료로 지불됩니다.
   - 현재 아젠다 제출 수수료 (톤) : 10000000000000000000 (10 TON)


## 아젠다 제출 파라미터

### 실행 함수
TON approveAndCall 을 이용해서, 트랜잭션을 보낼때는 실행되는 트랜잭션을 인코딩해서 파리미터로 전송해야 합니다.
  - [TON.approveAndCall(address,uint256,bytes)](https://etherscan.io/address/0x2be5e8c109e2197D077D13A82dAead6a9b3433C5#writeContract#F3)

  - Function: approveAndCall(address spender,uint256 amount,bytes data)
  - Parameters:
    - address spender    : 위원회 컨트랙트 주소  0xDD9f0cCc044B0781289Ee318e5971b0139602C26
    - uint256 amount     : 승인할 TON 금액  10000000000000000000
    - bytes **agenda_data**  : 아젠다 생성 데이터 (동적 크기)



### agenda_data 생성하기 (동적 크기)

- 공지기간과 투표기간은 정해진 최소시간보다 같거나 커야한다.
  - [DAOAgendaManager.minimumNoticePeriodSeconds()](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F20) : 1382400 (16일)
  - [DAOAgendaManager.minimumVotingPeriodSeconds()](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F21) : 172800  (2일)

#### 아젠다 트랜잭션으로 데이타 생성하기 : 레거시 버전 (5개 파라미터)
 - 아래의 형태로 데이타 인코딩하여 agenda_data를 생성한다.
    - (address[] targets, uint128 noticePeriodSeconds, uint128 votingPeriodSeconds, bool atomicExecute, bytes[] calldatas)
 - **데이타 인코딩을 수작업으로 하기는 어려움이 있으므로, [다오 커뮤니티 버전의 sample-1](https://github.com/tokamak-network/dao-community-version/blob/main/sample-1/README_KR.md#%EC%8B%A4%ED%96%89-%EB%B0%A9%EB%B2%95) 의 배포된 앱을 이용하여 아젠다 생성을 권장한다.**

```
  address[] targets,              // 실행할 컨트랙트 주소 배열
  uint256 noticePeriodSeconds,    // 공지기간(초)
  uint256 votingPeriodSeconds,    // 투표기간(초)
  bool atomicExecute,             // true
  bytes[] calldata                // 실행할 함수 calldata 배열
```

#### Example
- 아래 두개의 트랜잭션을 순차적으로 실행하는 안건인 경우,
  - (1) The 1st transaction : SeigManager.updateSeigniorageLayer(address tokamak1)
  - (2) The 2nd transaction : TON.setCreateAgendaFees(uint256 amount)
    - ->  예: 1 TON 설정 시 amount = 10^18 = 0x0de0b6b3a7640000
  - 제안 파라미터 예시값
  ```
    - targets: [0x0b55a0f463b6defb81c6063973763951712d0e5f,0xcD4421d082752f363E1687544a09d5112cD4f484]
    - noticePeriodSeconds: (예) 1382400 (16일) =
    0x0000000000000000000000000000000000000000000000000000000000151800
    - votingPeriodSeconds: (예) 172800 (2일) =
    0x000000000000000000000000000000000000000000000000000000000002A300
    - atomicExecute: true
    - calldatas:
      - calldatas[0] =  updateSeigniorageLayer(layer2: address)
        - TOKAMAK1_ADDRESS: 0xf3b17fdb808c7d0df9acd24da34700ce069007df
        - 바이트: 0x{sel_updateSeigniorageLayer} + 000000000000000000000000{TOKAMAK1_ADDRESS}
          - 주의: {sel_updateSeigniorageLayer} = keccak256("updateSeigniorageLayer(address)")의 앞 4바이트
          - 0x1e1f0b60000000000000000000000000f3b17fdb808c7d0df9acd24da34700ce069007df

      - calldatas[1] = setCreateAgendaFees(uint256)
        - 바이트: 0x{sel_setCreateAgendaFees} + 0000000000000000000000000000000000000000000000000000000000000000de0b6b3a7640000
        - 주의: {sel_setCreateAgendaFees} = keccak256("setCreateAgendaFees(uint256)")의 앞 4바이트
        - 0xb4f69b6a0000000000000000000000000000000000000000000000000de0b6b3a7640000
  ```

  - **최종 생성된 Example의 agenda_data**
  ```
  0x00000000000000000000000000000000000000000000000000000000000000a00000000000000000000000000000000000000000000000000000000000151800000000000000000000000000000000000000000000000000000000000002a3000000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000020000000000000000000000000b55a0f463b6defb81c6063973763951712d0e5f000000000000000000000000cd4421d082752f363e1687544a09d5112cd4f4840000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000000000241e1f0b60000000000000000000000000f3b17fdb808c7d0df9acd24da34700ce069007df000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000024b4f69b6a0000000000000000000000000000000000000000000000000de0b6b3a764000000000000000000000000000000000000000000000000000000000000
  ```


