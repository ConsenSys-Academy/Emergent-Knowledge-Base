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
