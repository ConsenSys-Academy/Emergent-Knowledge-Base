### Question
Can anyone give any more information about the use of events as cheap storage in smart contracts? As far as I can see, it is just that emitted information can be retrieved by scraping logs rather than querying on-chain data - is that it?
### Answer
Yes and querying on-chain data will only give you the latest state. Event logs can give you a clean history of every time that function was called (who it was called by, resulting state change, etc.) and you can filter event logs using queries (e.g. every time address xyz has voted on a proposal). So when you're defining a new event, consider what parameters might be useful in the context of the dapp, so that people can query for it.  Some additional reading on the topic:  https://link.medium.com/LsHdBBXEmjb



