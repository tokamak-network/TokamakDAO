# Voting on a Proposal
> Functions for voting on an agenda.
> Only DAO members can vote on agendas.

## DAOAgendaManager: [etherscan link](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484)

---

### [isVotableStatus(uint256 _agendaID)](https://etherscan.io/address/0xcD4421d082752f363E1687544a09d5112cD4f484#readContract#F18)

Whether the agenda is in a votable status

- Parameters
  - uint256 _agendaID: Agenda index to query
- Returns
  - bool: true if votable, false otherwise

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


## Candidate / CandidateAddOnProxy  (Each DAO member has a different Candidate address)

*********

### candidate()
Check the actual operator address of the Candidate contract.

- Parameters
  - None
- Returns
  - candidate account address

*********


### castVote(uint256 _agendaID, uint256 _vote, string calldata _comment)

Only the candidate() account can execute this function to cast a vote.

- Parameters
  - uint256 _agendaID: Agenda index to query (starts from 0)
  - uint256 _vote: 0: abstain, 1: yes, 2: no
  - string _comment: Optional vote comment
- Returns
  - None

*********


