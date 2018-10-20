# GoChainWin-D2W
GoChainWin SmartContract

An attempt to port dice2.win to GoChain.

---

## Bet Structure.

**amount**  
*uint,* Amount in wei.

**modulo**  
*uint8,* Number of winning outcomes, used to compute the winning payment. (* modulo/rollUnder). Also used instead of a mask for games with a modulo greater than MAX_MASK_MODULO.  

**rollUnder**  
*uint8,* 

**placeBlockNumber**  
*uint40,* Block number of the placeBet transaction (tx).

**mask**  
*uint40,* Bit mask representing the winning bet outcomes (see MAX_MASK_MODULO comment).

**gambler**  
*address,* Address of the user/gambler. This is used to pay out the winning bets.

## Sample Bet.

| # | Name            | Type    | Data  |
| - | --------------- | ------- | -----:|
| 0 | betMask         | uint256 | 1
| 1 | modulo          | uint256 | 2
| 2 | commitLastBlock | uint256 | 6552635
| 3 | commit          | uint256 | 105924773861004735583835816423796625830841821263867874621173584848383761270567
| 4 | r               | bytes32 | fe92e2efd9eba629eff34aef11e6fd5e77c15448e6778d20a47aa2da32f9a583
| 5 | s               | bytes32 | 62eb096928992f511faecb354ba24249b0a746d80f0cabf80022b3ec2529291c
#	Name	Type	Data
0	betMask	uint256	1
1	modulo	uint256	2
2	commitLastBlock	uint256	6552635
3	commit	uint256	105924773861004735583835816423796625830841821263867874621173584848383761270567
4	r	bytes32	fe92e2efd9eba629eff34aef11e6fd5e77c15448e6778d20a47aa2da32f9a583
5	s	bytes32	62eb096928992f511faecb354ba24249b0a746d80f0cabf80022b3ec2529291c
