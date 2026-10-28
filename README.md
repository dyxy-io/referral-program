<p align="center">
  <img src="https://docs.dyxy.io/logo/dark.svg" alt="DYXY" height="48">
</p>

# DYXY Referral program

How the DYXY referral program works: a 10% trading fee discount for invited traders, and 30% to 50% of their trading fees for referrers, with tiers set by monthly network volume.

> This repository describes how the program works. It does not contain DYXY source code. User guide: [docs.dyxy.io/referrals](https://docs.dyxy.io/referrals/overview).

## Overview

```mermaid
flowchart LR
    R["Referrer"] -- shares code --> T1["Trader A"]
    R -- shares code --> T2["Trader B"]
    T1 -- trades, 10% off fees --> F[("Trading fees")]
    T2 -- trades, 10% off fees --> F
    F -- 30% / 40% / 50% by tier --> R
```

| | Referred trader | Referrer |
| --- | --- | --- |
| Benefit | 10% off all trading fees | 30%–50% of referred traders' fees |
| Applies to | Swaps, perps (incl. Degen mode), stocks, bots | All trades of the referral network |
| Condition | Link wallet to a code | Share a code |

Pools, staking and lending carry no DYXY fee, so they generate no referral rewards.

## Tiers

| Tier | Network volume in a calendar month | Referrer share |
| --- | --- | --- |
| 1 | $0 – $1M | **30%** |
| 2 | $1M – $10M | **40%** |
| 3 | Above $10M | **50%** |

## Monthly recalculation

```mermaid
sequenceDiagram
    participant N as Referral network
    participant P as Program
    participant R as Referrer
    Note over R: New referrer starts in Tier 1 (30%)
    N->>P: Month M trading volume
    P->>P: Month ends → assign tier from month M volume
    P->>R: Tier applies during month M + 1
    N->>P: Fees paid in month M + 1
    P->>R: Rewards = fees × tier share
```

- Volume counts every trade by every wallet linked to the code.
- The tier for each month is set by the previous month's volume.
- Tiers move up and down with volume.

## Formulas

```
trader fee paid   = standard fee × (1 − 10%)
referrer reward   = Σ trader fees paid × tier share
tier(month M+1)   = f(network volume in month M)
```

## Worked example

| Month | Network volume | Tier in force | Fees paid by network | Referrer earns |
| --- | --- | --- | --- | --- |
| May | $800K | 1 (30%) | — | — |
| June | $3M | 1 (30%), from May | $1,800 | $540 |
| July | $12M | 2 (40%), from June | $2,500 | $1,000 |
| August | — | 3 (50%), from July | — | — |

## Rules

| Rule | |
| --- | --- |
| Codes per wallet | One. The link is permanent |
| Self-referral | Not allowed |
| Both roles | A referred trader can also refer others |
| Claiming | Rewards accrue continuously and are claimed on the Referrals page |

## License

Text and diagrams in this repository are licensed under [CC BY 4.0](LICENSE). The DYXY name and logo are not covered by this license.
