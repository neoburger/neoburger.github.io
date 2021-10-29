# Home

*bNEO* is a standard [NEP-17](https://docs.neo.org/docs/en-us/develop/write/nep17.html) token with decimals `8` and it can be minted from *NEO* and redeemed to *NEO* 1:1. *bNEO* holders receive optimized *GAS* reward in [NEO GOVERNANCE](https://neo.org/gov).

## Applications

- [dashboard](/dashboard/)
- [web gui](https://neoburger.io)

## Use *bNEO*

The smart contract of NeoBurger is well designed to support all kinds of wallets.

| operation | description |
| --- | --- |
| **mint** *bNEO* | send *NEO* to `NPmdLGJN47EddqYcxixdGMhtkr7Z5w4Aos` and you will receive the same amount of *bNEO* instantly in the same transaction |
| **redeem** *bNEO* | send withdraw fee (*GAS*) to `NPmdLGJN47EddqYcxixdGMhtkr7Z5w4Aos` and you will redeem *bNEO* to *NEO* instantly in the same transaction (the withdraw fee is `0.01` *GAS* per *NEO*) (it is better to send integer multiples of `0.01` *GAS* because *NEO* is indivisible) (the argument `data` of `transfer` invocation must be `null` which is default for most wallets) |
| **claim** *GAS* | send any amount of *bNEO* to `NPmdLGJN47EddqYcxixdGMhtkr7Z5w4Aos` and you will claim your *GAS* reward (it's better to send `0` *bNEO* if your wallet supports sending `0` amount) |

*bNEO* is awailable on both mainnnet and testnet with the same script hash and contract address:

- *bNEO* script hash: `0x48c40d4666f93408be1bef038b6722404d9a4c2a`
- *bNEO* contract address: `NPmdLGJN47EddqYcxixdGMhtkr7Z5w4Aos`

> Once *bNEO* is transfered, *GAS* reward afterwards will be distributed to the receiver.
> 
> Holding *bNEO* implies vote delegation in [NEO GOVERNANCE](https://neo.org/gov). BurgerDAO is provided to enhance [NEO GOVERNANCE](https://neo.org/gov) in a decentrilized way.

## How it works

```
+--------------+      NEO       +--------------+      NEO       +--------------+
|              |--------------->|              |................|              |
|              |                |              |                |              |
|              |      bNEO      |              |                |              |
|     USER     |<---------------|  NEO BURGER  |                |NEO GOVERNANCE|
|              |                |              |                |              |
|              |      GAS       |              |      GAS       |              |
|              |<---------------|              |<---------------|              |
+--------------+                +--------------+                +--------------+
```

Neoburger participates in [NEO GOVERNANCE](https://neo.org/gov) by making use of the deposited *NEO* and distributes the *GAS* reward to *bNEO* holders.

Neoburger is 7x24 maintained by automated systems and optimized strategies. Neoburger alway try to maximize the *GAS* reward by adjusting the voting targets and voting positions of Neoburger agents since marginal revenues of each candidate are different and changing all the time.

The permission of strategist is restricted by the candidate whitelist in order to protect the dbft assumptions since it's our responsibility to keep the network safu.

## Fee

- performance fee: `1%` (will be sent to the treasury)
- withdraw fee: `0.01` *GAS* per *NEO* (`99%` will be distributed to *bNEO* holders and `1%` to the treasury)

## Governance

Eventually NeoBurger is a DAO based project and BurgerDAO will be the owner of entire project.

The governance modulo is under developing and it is expected to have a good DAO application on Neo.

BurgerDAO is also a n enhancement for [NEO GOVERNANCE](https://neo.org/gov) and it solves the following dilemma:

> I want to vote for a candidate but I only want to vote for it if it is going to win. Otherwise, I'll vote in another candidate that will give me some GAS.

```
        OOOOOOOOOOOOOOOOOOOO        
      OO                    OO      
    OO                        OO    
  OO                            OO  
  OO         NEO BURGER         OO  
  OO                            OO  
OO                                OO
OOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOO
OONNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNOO
  OOOOOOOOOOOOOOOOOOOOOOOOOOOOOOOO  
OO                                OO
  OO    OO    OOOOOO    OO    OOOO  
  OOOOOO  OOOO      OOOO  OOOO  OO  
  OO                            OO  
    OOOOOOOOOOOOOOOOOOOOOOOOOOOO    
```
