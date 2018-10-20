# GoChainWin-D2W
GoChainWin SmartContract


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
