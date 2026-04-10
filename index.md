# Home

> **⚠️ Important: NeoBurger service is ending. Withdraw your funds now**

*bNEO* is a standard [NEP-17](https://docs.neo.org/docs/en-us/develop/write/nep17.html) token with decimals `8` and it can be minted from *NEO* and redeemed to *NEO* 1:1. *bNEO* holders receive the optimized *GAS* reward in [NEO GOVERNANCE](https://neo.org/gov).

---

## Important Announcement: NeoBurger Service Discontinuation Due to Neo Protocol Changes

Dear NeoBurger Community and bNEO/NB Holders,

We are writing to inform you of upcoming changes that will affect NeoBurger operations.

### Neo Protocol Update

The Neo blockchain is implementing a fundamental change to its voting and reward distribution mechanism (see [PR #4453](https://github.com/neo-project/neo/pull/4453)). The upcoming update will remove the additional rewards previously given to voters and distribute all rewards equally among NEO holders, regardless of voting participation.

**We strongly support this change and believe it represents an important evolution for the Neo ecosystem.** This update is more practical and reasonable for the protocol's long-term sustainability. We fully endorse the Neo core team's decision and are highly optimistic about the positive impact this will have on the ecosystem's health, stability, and future growth.

### Impact on NeoBurger

NeoBurger was designed and built on the existing reward distribution rules, where voting participation generated additional yields. With the removal of this mechanism, **the underlying conditions that NeoBurger relies on will no longer exist**. There is simply no reason for NeoBurger to continue operating under the new protocol rules.

### Service Timeline

* **Before 2026-05-01 00:00:00 UTC**: NeoBurger will operate normally. bNEO minting, redemption, and GAS distribution will function as usual. **We strongly encourage all users to withdraw their funds during this period.**
* **2026-05-01 00:00:00 UTC to 2026-08-01 00:00:00 UTC**: GAS reward distribution will cease. However, minting and redemption functions will remain operational. **Users must withdraw all assets before this period ends.**
* **After 2026-08-01 00:00:00 UTC**: All NeoBurger services will be shut down. For users who have not yet withdrawn their funds, please email [neoburger666@gmail.com](mailto:neoburger666@gmail.com) for further technical support.

**We strongly recommend that all users redeem your bNEO back to NEO at your earliest convenience.**

Thank you for being part of the NeoBurger journey.

---

## Applications

* [dashboard](dashboard)
* [web gui](https://neoburger.io)

## Use *bNEO*

The smart contract of NeoBurger is well designed to support all kinds of wallets.

| operation | description |
| --- | --- |
| **mint** *bNEO* | send *NEO* to `NPmdLGJN47EddqYcxixdGMhtkr7Z5w4Aos` and you will receive the same amount of *bNEO* instantly in the same transaction |
| **redeem** *bNEO* | send withdraw fee (*GAS*) to `NPmdLGJN47EddqYcxixdGMhtkr7Z5w4Aos` and you will redeem *bNEO* to *NEO* instantly in the same transaction (the withdraw fee is `0.001` *GAS* per *NEO*) (it is better to send integer multiples of `0.001` *GAS* because *NEO* is indivisible) (the argument `data` of `transfer` invocation must be `null` which is default for most wallets) |
| **claim** *GAS* | send any amount of *bNEO* to `NPmdLGJN47EddqYcxixdGMhtkr7Z5w4Aos` and you will claim your *GAS* reward (it's better to send `0` *bNEO* if your wallet supports sending `0` amount) |

* *bNEO* script hash: `0x48c40d4666f93408be1bef038b6722404d9a4c2a`
* *bNEO* contract address: `NPmdLGJN47EddqYcxixdGMhtkr7Z5w4Aos`

> Once *bNEO* is transfered, *GAS* reward afterwards will be distributed to the receiver.
>
> Holding *bNEO* implies vote delegation in [NEO GOVERNANCE](https://neo.org/gov).

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

Neoburger is 7x24 maintained by automated systems and optimized strategies. Neoburger always tries to maximize the *GAS* reward by adjusting the voting targets and voting positions of Neoburger agents since the marginal revenues of each candidate are different and changing all the time.

The permission of the strategist is restricted by the candidate whitelist in order to protect the dbft assumptions since it's our responsibility to keep the network safu.

For more about NeoBurger strategies, see [here](strategy).

## Fee

### Performance Fee

`1%` (will be sent to the treasury)

> Performance fee is necessary for this project to survive and it is just `1%` of the *GAS* profit.

### Withdraw Fee

`0.001` *GAS* per *NEO* (`99%` will be distributed to *bNEO* holders and `1%` to the treasury)

> Withdraw fee is necessary to ensure the profit safety of exsiting *bNEO* holders.
>
> * Every withdraw will affect other bNEO holders' profit because it breaks the current *NEO* distribution on each agent contract and *GAS* reward is not optimal until the strategist re-adjust the *NEO* distribution again.
> * the *GAS* reward will be distributed to all *bNEO* holders when the harvest operation is called and the harvest operaiton is triggered every serval hours. Imaging a hacker deposits a huge amount of *NEO* 1 second before the harvest operation and then withdraw its *NEO* 1 second after the harvest, then the hacker will get most of the *GAS* reward of this harvest (because *GAS* is distributed based on the *bNEO* balance and the hacker has a huge amount of *bNEO* at that time). Actually the hacker contributes almost nothing but steals *GAS* reward from existing *bNEO* holders. To avoid this kind of risks, withdraw fee is used.
>
>   The profit of the hacker can be calculated by the following expression
>
>   ```
>   P = G * X / (X + T) - X * F * T / (X + T)
>   ```
>
>   where
>
>   + `P`: profit of the hacker
>   + `G`: *GAS* reward to be harvested
>   + `F`: withdraw fee factor
>   + `T`: *NEO* deposited by other users
>   + `X`: *NEO* deposited by the hacker
>
>   thus
>
>   ```
>   P < 0 -> G < F * T
>   ```
>
>   That's how the withdraw fee it decided.
