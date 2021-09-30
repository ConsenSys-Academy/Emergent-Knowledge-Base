### Question
After reading the section on EIP-1559, I've a question about the priority fee -- i was wondering if this is still makes transactions susceptible to MEV, i.e., front-running
### Answer
It doesn't change anything MEV wise. Miners can still order the transactions as they see fit and can front-run. Their algorithms would probably determine the cost benefit of both.
If the juice is worth the squeeze, and they can squeeze, they will do it.

### Question
Hello everyone, I have a question regarding how miners mine a new block. When miners are competing to create a new block, do they pickup the same number of transactions from the mempool to mine? If no, for cases with uncle blocks, will the transactions that made it to uncle block be mined in another block?
### Answer
Miners pick up and prioritise the most profitable ones they can stick in a block within the short timeframe from the pool of transactions.
Those processed on an uncle block are not on the longest chain, so they would end up back in the tx pool to be mined elsewhere. 
Check this out: [Blockchain Transaction Visualizer](https://txstreet.com/v/eth)

### Question
Question about EIP 1559. In the Finematics video (https://youtu.be/MGemhK9t44Q?t=704), the narrator says ETH could be deflationary if "block reward + tip < base fee". Block reward is supply creation, base fee is supply destruction, but isn't the tip just a transfer from users to miners? Why is the tip part of this equation?
### Answers
#### Answer 1
I'm not 100% on this but I believe it's because the baseFee is the programmatic level of ETH being created, like a target. However, during crunch times where there are a lot of transactions, the baseFee will get so high as to destroy the overall amount of ETH (if only temporarily).
#### Answer 2
I think you have a point there.
If you work with the amount of ETH entering (block reward) being less than the amount of ETH being burnt then it is deflationary.
My understanding is like yours - the tip is non-destructive miner incentive. 
### Question
Hello, Is it necessary to install geth and setup a node?
### Answer
Not necessarily, but it is good practice. I think the purpose of that lesson is to learn how to do it rather than needing to have your own node.
