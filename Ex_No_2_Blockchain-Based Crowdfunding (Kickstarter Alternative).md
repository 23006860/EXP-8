# Experiment 2: Blockchain-Based Crowdfunding (Kickstarter Alternative)
### NAME: SATHYANARAYANAN M
### REG NO:212224040300
### DEPARTMENT: CSE
## Aim:
To create a decentralized crowdfunding platform where donors contribute funds only if the campaign goal is met.

## Algorithm:
A project owner starts a campaign with a funding goal and deadline.


Contributors can send ETH to the campaign.


If the goal is met before the deadline, funds are released to the project owner.


If the goal is not met, contributors can withdraw their funds.


## Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Crowdfunding {
    struct Campaign {
        address creator;
        uint256 goal;
        uint256 deadline;
        uint256 amountRaised;
        bool goalMet;
        mapping(address => uint256) contributions;
    }

    Campaign public campaign;

    constructor(uint256 _goal, uint256 _duration) {
        campaign.creator = msg.sender;
        campaign.goal = _goal;
        campaign.deadline = block.timestamp + _duration;
    }

    function contribute() public payable {
        require(block.timestamp < campaign.deadline, "Campaign ended");
        campaign.amountRaised += msg.value;
        campaign.contributions[msg.sender] += msg.value;
    }

    function withdrawFunds() public {
        require(msg.sender == campaign.creator, "Only creator can withdraw");
        require(campaign.amountRaised >= campaign.goal, "Goal not met");
        payable(msg.sender).transfer(campaign.amountRaised);
        campaign.goalMet = true;
    }

    function refund() public {
        require(block.timestamp > campaign.deadline, "Campaign still active");
        require(campaign.amountRaised < campaign.goal, "Goal was met");
        uint256 amount = campaign.contributions[msg.sender];
        campaign.contributions[msg.sender] = 0;
        payable(msg.sender).transfer(amount);
    }
}
```
# Expected Output:
Users can contribute ETH to the campaign.
<img width="1920" height="1200" alt="Screenshot (13)" src="https://github.com/user-attachments/assets/da0ce422-a924-4d13-a962-6808e87c321b" />

If the goal is met, the creator can withdraw funds.

<img width="1920" height="1200" alt="Screenshot (14)" src="https://github.com/user-attachments/assets/c9f45c5e-d405-4801-9956-49c78589ee22" />


If the goal is not met, contributors can claim a refund.

<img width="1920" height="1200" alt="Screenshot (15)" src="https://github.com/user-attachments/assets/59383e0d-618a-487f-8602-79b154248d70" />


# High-Level Overview:
Teaches decentralized fundraising.


Avoids fraud by ensuring funds are only transferred if the goal is met.

# RESULT: 
Thus created a decentralized crowdfunding platform where donors contribute funds only if the campaign goal is met is executed successfully.

