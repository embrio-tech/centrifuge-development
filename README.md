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

Services can be started individually. the following services are available: `subql`, `insights`, `blender`. These can be started with the following command

    $ docker-compose --profile <service> up --build

such as

    $ docker-compose --profile subql up --build

or for multiple services:

    $ docker-compose --profile subql --profile insights up --build

If you run this for the first time, it might take a while. :hourglass_flowing_sand: Get a coffee, sit back, and relax! :coffee: :palm_tree:

### Access

#### Centrifuge insights

The frontend can be accessed under the following link: [http://localhost:8010](http://localhost:8010/)

#### Centrifuge subql

The subql query playground is available here: [http://localhost:3000](http://localhost:3000/)

### Scrap

    $ docker-compose down -v

## Contact

[EMBRIO.tech](https://embrio.tech)  
[hello@embrio.tech](mailto:hello@embrio.tech)  
+41 44 552 00 75

## License

The code is licensed under the [GNU Lesser General Public License v2.1](https://github.com/embrio-tech/centrifuge-insights/blob/main/LICENSE)
