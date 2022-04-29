# Centrifuge Development

[![Docker](https://img.shields.io/static/v1?label=shipped+with&message=Docker&color=287cf9)](https://www.docker.com/)
[![embrio.tech](https://img.shields.io/static/v1?label=by&message=EMBRIO.tech&color=24ae5f)](https://embrio.tech)
[![Centrifuge](https://img.shields.io/static/v1?label=for&message=Centrifuge&color=2762ff)](https://centrifuge.io/)

A development repository to combine and manage all necessary services to easily develop the centrifuge insights dashdoard.

![centrifuge-architecture](https://user-images.githubusercontent.com/16650977/162206089-a1fac1d5-948f-41aa-badc-6e36ae08482b.png)
_Figure: Architectural diagram of the development environment._

## Getting Started

### Prerequisites

- git
- docker
- docker-compose

### Initialize

    $ git clone --recurse-submodules git@github.com:embrio-tech/centrifuge-development.git
    $ cd centrifuge-development
    $ cp .env.sample .env

### Start

    $ docker-compose up --build

If you run this for the first time, it might take a while. :hourglass_flowing_sand: Get a coffee, sit back, and relax! :coffee: :palm_tree:

### Access

#### Centrifuge insights

The frontend can be accessed under the following link: [http://localhost:8010](http://localhost:8010/)

#### Centrifuge subql

The subql query playground is available here: [http://localhost:3000](http://localhost:3000/)

### Scrap

    $ docker-compose down -v

## Data Model

```mermaid
erDiagram
    Timekeeper {
        string id PK
        date lastPeriod
    }

    Pool ||--|| PoolState: ""
    Pool {
        String id PK
        String type "idx"

        Date createdAtTimestamp
        Int createdAtHeight

        String currency
        String metadata

        Int minEpochTime
        Int challengeTime
        Int maxNavAge

        Int currentEpoch
        Int lastEpochClosed
        Int lastEpochExecuted

        String stateId FK
    }

    PoolState ||..|| PoolSnapshot: "onNewPeriod"
    PoolState{
        String id PK

        BigInt netAssetValue
        BigInt totalReserve
        BigInt availableReserve
        BigInt maxReserve
        BigInt totalDebt
    }

    PoolSnapshot }o--|| Pool: ""
    PoolSnapshot {
        String id PK
        String poolId FK

        Date timestamp
        Int blockHeight

        BigInt netAssetValue
        BigInt totalReserve
        BigInt availableReserve
        BigInt maxReserve
        BigInt totalDebt

        BigInt totalBorrowed
        BigInt totalRepaid
        BigInt totalInvested
        BigInt totalRedeemed
    }

    Tranche }o--|| Pool: ""
    Tranche ||--|| TrancheState: ""
    Tranche {
        String id PK
        String type "idx"
        String poolId FK
        Int trancheId

        Bool isResidual
        Int seniority
        BigInt interestRatePerSec
        BigInt minRiskBuffer

        String state FK
    }

    TrancheState ||..|| TrancheSnapshot: "onNewPeriod"
    TrancheState {
        String id PK

        BigInt supply
        Float price

        BigInt outstandingInvestOrders
        BigInt outstandingRedeemOrders

        BigInt yield30Days
        BigInt yield90Days
        BigInt yieldSinceInception
    }

    TrancheSnapshot }o--|| Tranche: ""
    TrancheSnapshot {
        String id PK
        String trancheId FK

        Date timestamp
        Int blockHeight

        BigInt supply
        Float price

        BigInt outstandingInvestOrders
        BigInt outstandingRedeemOrders

        BigInt yield30Days
        BigInt yield90Days
        BigInt yieldSinceInception
    }

    Epoch }|--|| Pool: ""

 %% InvestorTransaction
 %% BorrowerTransaction
 %% Account
 %% AccountBalance
 %% Loan
```

## Contact

[EMBRIO.tech](https://embrio.tech)  
[hello@embrio.tech](mailto:hello@embrio.tech)  
+41 44 552 00 75

## License

The code is licensed under the [GNU Lesser General Public License v2.1](https://github.com/embrio-tech/centrifuge-insights/blob/main/LICENSE)
