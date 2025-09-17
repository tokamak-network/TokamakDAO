# Executing a Proposal
> Functions for executing an agenda.
> Anyone can execute an agenda that has passed by vote.


## DAOAgendaManager: [etherscan link](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#code)

---

### [canExecuteAgenda(uint256 _agendaID)](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F2)

Whether the agenda is executable

- Parameters
  - uint256 _agendaID: Agenda index to query
- Returns
  - bool: true if executable, false otherwise

*********


## DAOCommitteeProxy: [etherscan link](https://etherscan.io/address/0xDD9f0cCc044B0781289Ee318e5971b0139602C26#writeProxyContract)
---


### executeAgenda(uint256 _agendaID)

Function to execute an agenda.
DAO committee logic consists of multiple parts. This function's logic may not be displayed on Etherscan, so you must call the contract function directly using ABI on a tool like [MyEtherWallet](https://www.myetherwallet.com/wallet/interact).


- Parameters
    - Contract address : 0xDD9f0cCc044B0781289Ee318e5971b0139602C26
    - ABI
    ```
    [{
      "inputs": [
        {
          "internalType": "uint256",
          "name": "_agendaID",
          "type": "uint256"
        }
      ],
      "name": "executeAgenda",
      "outputs": [],
      "stateMutability": "nonpayable",
      "type": "function"
    }]
    ```
    - _agendaID : Index of the agenda to execute

- Execute : Click Write

![Input1 View](../img/execute_0.png)
![Input2 View](../img/execute_1.png)

*********


