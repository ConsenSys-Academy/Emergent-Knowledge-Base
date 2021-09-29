### Question
Can anyone give any more information about the use of events as cheap storage in smart contracts? As far as I can see, it is just that emitted information can be retrieved by scraping logs rather than querying on-chain data - is that it?
### Answer
Yes and querying on-chain data will only give you the latest state. Event logs can give you a clean history of every time that function was called (who it was called by, resulting state change, etc.) and you can filter event logs using queries (e.g. every time address xyz has voted on a proposal). So when you're defining a new event, consider what parameters might be useful in the context of the dapp, so that people can query for it.  Some additional reading on the topic:  https://link.medium.com/LsHdBBXEmjb

### Question
Is it possible to revert bytecode to a higher lvl language? Or do you know of any good decompiler?
### Answer
This is this is a popular disassembler (listed in the course): https://github.com/crytic/ethersplay.  You can also use tools like https://www.curvegrid.com/blog/day-1-evmdis-a-solidity-disassembler or https://eveem.org/ or https://ethervm.io/ to decompile.

### Question
Can somebody explain a certain row in the Multi-Sig Tutorial? In the method 'executeTransaction' we call another contract with the destination address then use this:
```
(bool success, bytes memory returnedData) = t
                .destination
                .call
                .value(t.value)(t.data);
```
to update a variable in another contract.
I cannot understand how the 'storedData' in SimpleStorage.sol gets updated without calling the set(uint x) method? How does this work?
### Answer
If you encode the signature set(uint) of the setint function with the value of 5 as the parameter, the data for it ends up like so (taken from tutorial)
```
var  encoded = '0x60fe47b1000000000000000000000000000000000000000000000000000000000005
```
This encoded data is then submitted by doing
```
ms.submitTransaction(ss.address, 0, encoded, {from: accounts[0]})
```
When you now use the destination.call.value(t.value)(t.data) it is effectively going to the SimpleStorage contract, decoding the data, finding set, passes it the value of 5 and changes the value by executing set.  So it is actually calling set. The multisig wallet stores encoded function executions (by means of encoded function signatures and the parameter data) that only once confirmed execute. See https://abi.hashex.org/
### Question
When should I use delegateCall()? Also I don't understand why the state of the caller contract changes. Seems very risky to use delegateCall() as one has to be sure about the effects.
### Answers
#### Answer 1
Check this out: https://www.youtube.com/watch?v=oinniLm5gAM. The order of your variables in the contract have to be exact. I can't really see where you would want to have this kind of thing where you call a function in another contract and then use your own variables to store that state. That's like something you would do in C by accident.
Kind of makes the whole safe and immutable contract code super unsafe. You would be better having a library of pure functions with no state changes. Call them and return the values.
#### Answer 2
There are definitely risks involved for sure. What it does give you, is the ability to abstract logic into  another contract (specifically for writing to storage and doing validation logic).
If lets say you were constructing new ERC721 (NFT) or some other contract, the caller would be paying hefty gas fees for the construction. The delegatecall usage would save gas, and allow you to reuse that code.
That said, be vigilant on usage as per the link above.
The size of the contract using delegate calls would be a lot smaller than the called contract.
#### Answer 3
Delegate calls are a key part of proxy contracts - which allow smart contracts to be 'upgraded'. Lot of proxy contracts lying around in DeFi: https://blog.openzeppelin.com/proxy-patterns/
### Question
If a contract has a Private variable, and there is no public view function or method to call it, is the variable value 100% hidden from users or other smart contracts?
### Answer
Nope, it is more a case of contract/code access to set/read vs. humans or bots scanning contract storage or opcode executions: https://hackernoon.com/your-private-solidity-variable-is-not-private-save-it-before-it-becomes-public-52a723f29f5e 
