# Task Pay (A protocol that gives you a proof of being paid if you accomplish the task)

## ___Task based payment escrow for everyday people.___

## Roadmap
- ### Phase 1 (Make it work)
  - Write spaghetti solidity contracts to accomplish the goal.
  - Write a simple react frontend to talk to the smart contract.

- ### Phase 2 (Can't be evil)
  - Look for code vulnerability and solve them.


- ### Phase 3 (Make it clean)
  - Update solidity code to follow industry standard. 
  - Detatch logic and state so that we can have upgradable contracts using proxy and fallbacks.


- ### Phase 4 (Build on the footstep of giants)
  - Use standard libraries if they are needed to make code better.


- ### Phase 5 (Make it effecient)
  - Optimise for user experience.
  - Optimise for gas.





## Contracts Needed: 

 > ### I will try to describe few functionalities I want out of the contracts. It is not well thought through but we will add and remove what makes sense along the way.

- Task.sol
  > This is a parent contract that will speak to Escrow, ConflictResolver and TrustProtocol.
  
  - createTask - a payable function which takes in task url of IPFS metadata and other necessary details
  - commitTask - A person who is skilled enough to do the task can commit to the task with commit thresold for escrow.
  - claimIncentive - Once the task is flagged as completed by creator the committer can claim the incentive along with his commit thresold amount.

- Escrow.sol
  
  - Will be a modified version of BOA(Burnable Open Payments)
  - ### Methods:
    - burn - allows you to create task with trustScore, amount depositAmount and description bytes32 reference to IPFS and task deadline should emit TaskCreated event with details
    - release(taskId, trustScore) - allows you to join to solve specific task if you deposit fund and have enough trust score
	- commit - will allow you to claim incentive for the task you completed

- Conflict.sol

  - ### Methods:
    - raiseConflict -Allows you to raise conflict
	- silentlyResolve - If both parties agree to dissolve escrow they are able to do so without loosing their trust score
	- resolveConflict - burn the tokens and deduct trust score of the parties relative to their burn weight. If trust score is low for both of the parties nobody will want to work with them


- Trust.sol 

  - ` is optional will be implemented only if we get escrow and conflict part done.`

  > This contract will increment or decrement your trust score on result of the task. If the task is completed without any conflicts your trust score will be incremented. Let's not go deep on how to calculate trust score here. Let's say anyone who joins the task will get a normal trust score of 5. Depending on his dealings wallet address trust score will be recalculated. We will create a simple formula for re calculating trust score. 





