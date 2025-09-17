# Submitting a Proposal
> When submitting a DAO agenda, you need to pay a fee in TON. Use TON's approveAndCall function to pay the designated TON fee while submitting the agenda.
## TON: [etherscan link](https://etherscan.io/address/0x2be5e8c109e2197D077D13A82dAead6a9b3433C5)
---

## Prerequisites
1. **Wallet preparation**
   - Prepare a wallet (e.g., MetaMask) and TON tokens.
   - For contract addresses, see [contract addresses.md](./contract%20addresses.md).

2. **Prepare agenda fee**
   - Check the required TON fee via [DAOAgendaManager.createAgendaFees()](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F4).
   - Ensure your wallet balance in TON is greater than the fee. This amount will be paid as the agenda submission fee.
   - Current agenda creation fee (TON): 10000000000000000000 (10 TON)


## Proposal parameters

### Function to execute
When sending the transaction via TON approveAndCall, you must encode the transaction data to be executed and pass it as a parameter.
  - [TON.approveAndCall(address,uint256,bytes)](https://etherscan.io/address/0x2be5e8c109e2197D077D13A82dAead6a9b3433C5#writeContract#F3)

  - Function: approveAndCall(address spender,uint256 amount,bytes data)
  - Parameters:
    - address spender    : Committee contract address  0xDD9f0cCc044B0781289Ee318e5971b0139602C26
    - uint256 amount     : TON amount to approve  10000000000000000000
    - bytes **agenda_data**  : Agenda creation data (dynamic size)



### Creating agenda_data (dynamic size)

- Notice period and voting period must be greater than or equal to the minimum.
  - [DAOAgendaManager.minimumNoticePeriodSeconds()](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F20) : 1382400 (16 days)
  - [DAOAgendaManager.minimumVotingPeriodSeconds()](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F21) : 172800  (2 days)

#### Creating agenda transaction data: Legacy version (5 parameters)
 - Encode data in the following form to create agenda_data.
    - (address[] targets, uint128 noticePeriodSeconds, uint128 votingPeriodSeconds, bool atomicExecute, bytes[] calldatas)
 - Because manual data encoding is difficult, it is recommended to use the deployed app of [dao-community-version sample-1](https://github.com/tokamak-network/dao-community-version/blob/main/sample-1/README_KR.md#%EC%8B%A4%ED%96%89-%EB%B0%A9%EB%B2%95) to create the agenda.

```
  address[] targets,              // Contract addresses to call
  uint256 noticePeriodSeconds,    // Notice period (seconds)
  uint256 votingPeriodSeconds,    // Voting period (seconds)
  bool atomicExecute,             // true
  bytes[] calldata                // Calldata array for functions to call
```

#### Example
- For an agenda that sequentially executes two transactions:
  - (1) The 1st transaction: SeigManager.updateSeigniorageLayer(address tokamak1)
  - (2) The 2nd transaction: TON.setCreateAgendaFees(uint256 amount)
    - -> Example: For 1 TON, amount = 10^18 = 0x0de0b6b3a7640000
  - Example proposal parameters
  ```
    - targets: [0x0b55a0f463b6defb81c6063973763951712d0e5f,0xcD4421d082752f363E1687544a09d5112cD4f484]
    - noticePeriodSeconds: (ex) 1382400 (16 days) =
    0x0000000000000000000000000000000000000000000000000000000000151800
    - votingPeriodSeconds: (ex) 172800 (2 days) =
    0x000000000000000000000000000000000000000000000000000000000002A300
    - atomicExecute: true
    - calldatas:
      - calldatas[0] =  updateSeigniorageLayer(layer2: address)
        - TOKAMAK1_ADDRESS: 0xf3b17fdb808c7d0df9acd24da34700ce069007df
        - bytes: 0x{sel_updateSeigniorageLayer} + 000000000000000000000000{TOKAMAK1_ADDRESS}
          - Note: {sel_updateSeigniorageLayer} is the first 4 bytes of keccak256("updateSeigniorageLayer(address)")
          - 0x1e1f0b60000000000000000000000000f3b17fdb808c7d0df9acd24da34700ce069007df

      - calldatas[1] = setCreateAgendaFees(uint256)
        - bytes: 0x{sel_setCreateAgendaFees} + 0000000000000000000000000000000000000000000000000000000000000000de0b6b3a7640000
        - Note: {sel_setCreateAgendaFees} is the first 4 bytes of keccak256("setCreateAgendaFees(uint256)")
        - 0xb4f69b6a0000000000000000000000000000000000000000000000000de0b6b3a7640000
  ```

  - **Final example of generated agenda_data**
  ```
  0x00000000000000000000000000000000000000000000000000000000000000a00000000000000000000000000000000000000000000000000000000000151800000000000000000000000000000000000000000000000000000000000002a3000000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000020000000000000000000000000b55a0f463b6defb81c6063973763951712d0e5f000000000000000000000000cd4421d082752f363e1687544a09d5112cd4f4840000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000000000241e1f0b60000000000000000000000000f3b17fdb808c7d0df9acd24da34700ce069007df000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000024b4f69b6a0000000000000000000000000000000000000000000000000de0b6b3a764000000000000000000000000000000000000000000000000000000000000
  ```


