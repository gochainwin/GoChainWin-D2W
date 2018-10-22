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
| - | --------------- | ------- |:----- |
| 0 | betMask         | uint256 | 1
| 1 | modulo          | uint256 | 2
| 2 | commitLastBlock | uint256 | 6552635
| 3 | commit          | uint256 | 105924773861004735583835816423796625830841821263867874621173584848383761270567
| 4 | r               | bytes32 | fe92e2efd9eba629eff34aef11e6fd5e77c15448e6778d20a47aa2da32f9a583
| 5 | s               | bytes32 | 62eb096928992f511faecb354ba24249b0a746d80f0cabf80022b3ec2529291c

## Constants
**HOUSE_EDGE_PERCENT 
HOUSE_EDGE_MINIMUM_AMOUNT** 
Each bet is deducted 2% in favour of the house, but no less than some minimum. The lower bound is dictated by gas costs of the settleBet transaction, providing headroom for up to 10 Gwei prices.

**MIN_JACKPOT_BET** 
Bets lower than this amount do not participate in jackpot rolls (and are not deducted **JACKPOT_FEE**).

**JACKPOT_MODULO 
JACKPOT_FEE** 
Chance to win jackpot (default 0.1%) and fee deducted into jackpot fund.

**MIN_BET 
MAX_AMOUNT** 
There is minimum and maximum bets. We'll probably want to adjust the min downward once we have the system in production, since the mins were based on the minimum amount you can effectively transfer with fees on the ETH network.

**MAX_MODULO** 
Modulo is a number of equiprobable outcomes in a game: 
  - 2 for coin flip 
  - 6 for dice 
  - 6 * 6 = 36 for double dice 
  - 100 for goroll 
  - 37 for roulette 
  etc. 
  
 It's called so because 256-bit entropy is treated like a huge integer and the remainder of its division by modulo is considered bet outcome. 

**MAX_MASK_MODULO** 
For modulos below this threshold rolls are checked against a bit mask, thus allowing betting on any combination of outcomes. For example, given modulo 6 for dice, 101000 mask (base-2, big endian) means betting on 4 and 6; for games with modulos higher than threshold (gooll), a simple limit is used, allowing betting on any outcome in (0, N) range. 
 
The specific value is dictated by the fact that 256-bit intermediate multiplication result allows implementing population count efficiently for numbers that are up to 42 bits, and 40 is the highest multiple of eight below 42. 
