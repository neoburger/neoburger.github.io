# Home

*bNEO* is a standard [NEP-17](https://docs.neo.org/docs/en-us/develop/write/nep17.html) token with decimals `8` and it can be minted from *NEO* and redeemed to *NEO* 1:1.

*bNEO* holders enjoy optimized *GAS* reward in Neo governance and it's easy and free to transfer *bNEO* to anyone else. Once *bNEO* is transfered, *GAS* reward after the transaction will be distributed to the receiver.

## Use *bNEO*

The smart contract of NeoBurger is well designed to make it easy to use on all kinds of wallets.

> *bNEO* is awailable on mainnnet and testnet with same script hash and contract address

- *bNEO* script hash: `0x48c40d4666f93408be1bef038b6722404d9a4c2a`
- *bNEO* contract address: `NPmdLGJN47EddqYcxixdGMhtkr7Z5w4Aos`

| operation | description |
| --- | --- |
| **mint** *bNEO* | send *NEO* to `NPmdLGJN47EddqYcxixdGMhtkr7Z5w4Aos` and you will receive the same amount of *bNEO* instantly in the same transaction |
| **redeem** *bNEO* | send withdraw fee (*GAS*) to `NPmdLGJN47EddqYcxixdGMhtkr7Z5w4Aos` and you will redeem *bNEO* to *NEO* instantly in the same transaction (the withdraw fee is `0.01` *GAS* per *NEO*) (it is better to send integer multiples of `0.01` *GAS* because *NEO* is indivisible) |
| **claim** *GAS* | send any amount of *bNEO* to `NPmdLGJN47EddqYcxixdGMhtkr7Z5w4Aos` and you will claim your *GAS* reward (it's better to send `0` *bNEO* if your wallet supports sending `0` amount) |

## Applications

The following tools are supportted for better usage.

- dashboard (comming soon)
- web gui (comming soon)
- ...

## How it works

```
+--------------+      NEO       +--------------+      NEO       +--------------+
|              ├--------------->|              |................|              |
|              |                |              |                |              |
|              |      bNEO      |              |                |              |
|     USER     |<---------------┤  NEO BURGER  |                |NEO GOVERNANCE|
|              |                |              |                |              |
|              |      GAS       |              |      GAS       |              |
|              |<---------------┤              |<---------------┤              |
+--------------+                +--------------+                +--------------+
```

> NEO token holders decide who is in charge of maintaining the Neo network through the election of a Neo Council. GAS token rewards are distributed to voters and council members alike.

See more on [Governance - Neo Smart Economy](https://neo.org/gov)

By Collecting *NEO*, NeoBurger can be more efficient on earning rewards in Neo governance. Using NeoBurger is always better than do it by yourself.

## Fee

- performance fee: `1%` (will be sent to the treasury)
- withdraw fee: `0.01` *GAS* per *NEO* (`99%` will be distributed to *bNEO* holders and `1%` to the treasury)

## Strategy

We have enough confidence in providing optimized strategy to earn more *GAS*.

The permission of strategist is restricted by the candidate whitelist in order to protect the dbft assumptions since it's our responsibility to keep the network safu.

## Governance

The governance modulo is under developing and it is expected to have a good DAO application on Neo.

Eventually NeoBurger is a DAO based project and the DAO will be the owner of entire project.

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
