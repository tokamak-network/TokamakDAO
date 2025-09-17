# Proposal Details
> Functions to view detailed information of an agenda.
## DAOAgendaManager: [etherscan link](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484)
---


### [agendas(uint256 index)](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F1)

Get agenda information by index

- Parameters
  - uint256 index: Agenda index to query (starts from 0)
- Returns
  - LibAgenda.Agenda memory: The Agenda struct for the specified agenda
```
    struct Agenda {
        uint256 createdTimestamp;               /// agenda creation time (sec)
        uint256 noticeEndTimestamp;             /// notice end time (sec)
        uint256 votingPeriodInSeconds;          /// voting period (sec)
        uint256 votingStartedTimestamp;         /// voting start time (sec)
        uint256 votingEndTimestamp;             /// voting end time (sec)
        uint256 executableLimitTimestamp;       /// execute limit time (sec)
        uint256 executedTimestamp;              /// agenda executed time (sec)
        uint256 countingYes;                    /// yes votes
        uint256 countingNo;                     /// no votes
        uint256 countingAbstain;                /// abstain votes
        AgendaStatus status;                    /// agenda status
        AgendaResult result;                    /// agenda result
        address[] voters;                       /// voters addresses
        bool executed;                          /// executed flag
    }

    /// status
    enum AgendaStatus { NONE, NOTICE, VOTING, WAITING_EXEC, EXECUTED, ENDED }

    /// result
    enum AgendaResult { PENDING, ACCEPT, REJECT, DISMISS }

```
*********


### [numAgendas()](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F22)

Total number of agendas

- Parameters
  - None
- Returns
  - uint256: total count of agendas

*********


### [isVotableStatus(uint256 _agendaID)](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F18)

Whether the agenda is in a votable status

- Parameters
  - uint256 _agendaID: Agenda index to check
- Returns
  - bool: true if votable, false otherwise

*********


### [canExecuteAgenda(uint256 _agendaID)](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F2)

Whether the agenda is executable

- Parameters
  - uint256 _agendaID: Agenda index to check
- Returns
  - bool: true if executable, false otherwise

*********

### [hasVoted(uint256 _agendaID, address _user)](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F17)

Whether a user has voted on a specific agenda

- Parameters
  - uint256 _agendaID: Agenda index to check
  - address _user: Account address to check
- Returns
  - bool: true if voted, false if not

*********

### [isVoter(uint256 _agendaID, address _user)](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F19)

Whether a user is a voter for a specific agenda

- Parameters
  - uint256 _agendaID: Agenda index to check
  - address _user: Account address to check
- Returns
  - bool: true if voter, false otherwise

*********


