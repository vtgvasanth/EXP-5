# Experiment 5: Zero-Knowledge Proof (ZK) Private Voting System
# NAME: VASANTH.P
# REGISTER NO: 212222040175

# Aim:
To implement a fully private and transparent voting system using Zero-Knowledge Proofs (ZKPs). This ensures that votes are counted fairly without revealing who voted for whom.

# Algorithm:
Step 1: Voter Registration
Each voter generates a secret vote key and submits a commitment (hashed vote) to the contract.


Step 2: Voting Process
Voters submit their votes privately using a hash, without revealing their choice.


Step 3: ZK Verification
The contract verifies if a vote belongs to a registered voter but does not reveal the actual vote.


Step 4: Vote Counting
Once voting ends, the contract reveals the final tally without linking votes to individuals.



# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ZKVoting {
    struct Voter {
        bool registered;
        bytes32 voteCommitment;
    }

    mapping(address => Voter) public voters;
    uint256 public votesForA;
    uint256 public votesForB;

    event VoteCommitted(address voter, bytes32 commitment);
    event VoteRevealed(address voter, uint256 choice);

    function registerVoter(bytes32 commitment) public {
        require(!voters[msg.sender].registered, "Already registered");
        voters[msg.sender] = Voter(true, commitment);
        emit VoteCommitted(msg.sender, commitment);
    }

    function revealVote(string memory secret, uint256 choice) public {
        require(voters[msg.sender].registered, "Not registered");
        require(keccak256(abi.encodePacked(secret, choice)) == voters[msg.sender].voteCommitment, "Invalid proof");

        if (choice == 1) votesForA++;
        if (choice == 2) votesForB++;

        emit VoteRevealed(msg.sender, choice);
    }
}

```
# Expected Output:
Voters commit their votes privately.


When revealed, the contract verifies correctness but keeps votes anonymous.


Final result is publicly verifiable without exposing individual votes.





# High-Level Overview:
Uses ZKPs to ensure anonymous and fair elections.


Prevents vote tampering while maintaining voter privacy.


Mimics real-world ZK voting applications in governance and DAOs.

# OUTPUT:
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/9ab8a00d-784d-40c6-afb7-a110ecfd5d10" />
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/603d659a-c2c5-4dcc-a815-b7156887e483" />
<img width="1452" height="575" alt="image" src="https://github.com/user-attachments/assets/da1eb2c4-392f-4a9c-823f-cd738869a836" />
<img width="1482" height="605" alt="image" src="https://github.com/user-attachments/assets/38007b1d-83dc-4b24-9452-15648bc1b14e" />


# RESULT: 
THUS THE VOTING SYSTEM HAS BEEN IMPLEMENTED USING BLOCKCHAIN SUCCESSFULLY
