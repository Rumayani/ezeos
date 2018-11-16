# EZEOS

[![standard-readme compliant](https://img.shields.io/badge/standard--readme-OK-green.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)
[![Open Source Love](https://badges.frapsoft.com/os/v1/open-source.png?v=103)](https://github.com/ellerbrock/open-source-badges/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
[![MIT Licence](https://badges.frapsoft.com/os/mit/mit.png?v=103)](https://opensource.org/licenses/mit-license.php)

#### _A simple testing/learning tool for EOS._

## Table of Contents

- [Background](#background)
- [Install](#install)
- [Usage](#usage)
- [Maintainers](#maintainers)
- [Contribute](#contribute)
- [License](#license)

## Background

The tool was created as a means to quickly and easily experiment with EOSIO on mac or linux on the main or test net.
This version does not create a local node for you, but you can connect to it if you run it separately.
You can explore the EOSIO blockchain, create wallets and import keys, create accounts, view account balance,
get tables and use a contract to transfer funds to a ledger.

## Install

For working with EOSIO and ezeos you need to install:
1. EOSIO
2. EOSIO.CDT
3. Required python modules.

### 1. EOSIO
#### Standalone EOSIO (recommended)

Install [EOSIO](https://github.com/EOSIO/eos) (v1.4.1) in the `~/eos` directory by following the official repository instruction.

#### Docker EOSIO
For using docker container with EOSIO you have to have docker installed.

0. If you don't already have docker, you can download it [here](https://www.docker.com/community-edition).

1. Setup a development diretory.

You're going to need to pick a directory to work from, it's suggested to create a contracts directory somewhere on your local drive.
```
mkdir /home/username/contracts
cd /home/username/contracts
```

2. Get the latest or specific version docker image. The versions you can find [here](https://hub.docker.com/r/eosio/eos/tags/)

```
# To get the latest version
docker pull eosio/eos

# To get the concrete version
docker pull eosio/eos:v1.4.2
```

3. Boot container (The following command you are doing only once)
```
# Boot latest version container
docker run --name eos \
  --publish 127.0.0.1:5555:5555 \
  --volume /home/username/contracts:/home/username/contracts \
  --detach \
  eosio/eos \
  /bin/bash -c "keosd --http-server-address=0.0.0.0:5555"

# Boot concrete version container
docker run --name eos \
  --publish 127.0.0.1:5555:5555 \
  --volume /home/username/contracts:/home/username/contracts \
  --detach \
  eosio/eos:v1.4.2 \
  /bin/bash -c "keosd --http-server-address=0.0.0.0:5555"
```
> eos - The **required** name of the container.

> --volume - Alias a work volume on your local drive to the docker container.

4. Check the container

```
docker logs --tail 10 eos
```
You should see some output in the console that looks like this:
```
info 2018-11-16T18:20:00.189 thread-0  http_plugin.cpp:554  add_handler  ] add api url: /v1/wallet/list_keys
info 2018-11-16T18:20:00.189 thread-0  http_plugin.cpp:554  add_handler  ] add api url: /v1/wallet/list_wallets
info 2018-11-16T18:20:00.189 thread-0  http_plugin.cpp:554  add_handler  ] add api url: /v1/wallet/lock
info 2018-11-16T18:20:00.189 thread-0  http_plugin.cpp:554  add_handler  ] add api url: /v1/wallet/lock_all
info 2018-11-16T18:20:00.189 thread-0  http_plugin.cpp:554  add_handler  ] add api url: /v1/wallet/open
info 2018-11-16T18:20:00.189 thread-0  http_plugin.cpp:554  add_handler  ] add api url: /v1/wallet/remove_key
info 2018-11-16T18:20:00.189 thread-0  http_plugin.cpp:554  add_handler  ] add api url: /v1/wallet/set_timeout
info 2018-11-16T18:20:00.189 thread-0  http_plugin.cpp:554  add_handler  ] add api url: /v1/wallet/sign_digest
info 2018-11-16T18:20:00.189 thread-0  http_plugin.cpp:554  add_handler  ] add api url: /v1/wallet/sign_transaction
info 2018-11-16T18:20:00.189 thread-0  http_plugin.cpp:554  add_handler  ] add api url: /v1/wallet/unlock

```
5. Start/Stop your container
```
docker start eos
docker stop eos
```

6. Open the container shell
```
docker exec -it eos bash
```

To exit cast `exit`

6. Aliases

You don't want to enter into the Docker container's bash every time you need to interact with Cleos, Nodeos or Keosd. A solution to this is to create an aliases.

Add the following lines to your `.bashrc` or `.zshrc` or `.profile`
```
alias cleos='docker exec -it eos /opt/eosio/bin/cleos
alias nodeos='docker exec -it eos /opt/eosio/bin/nodeos
alias keosd='docker exec -it eos /opt/eosio/bin/keosd
```

### 2. EOSIO.CDT
For working with contracts you need to install Contract Development Toolkit. Currently our contracts are supporting the version **v1.2.1**. For the new contracts you can install the latest version of CDT. Follow the official installation guide for [EOSIO.CDT](https://github.com/EOSIO/eosio.cdt)

### 3. Required python modules
For using ezeos you nneed to install:
1. Python 3
2. PyQt5
3. pip3 install pexpect
4. pip3 install requests
5. pip3 install pyte
6. pip3 install psutil
7. pip3 install socketIO_client
8. pip3 install moneywagon

## Usage

At the root of this project:

```
cd src
```

Run:
```
python3 ezeos.py
```

Happy hacking!

## Maintainers

[@sylvaincormier](https://github.com/sylvaincormier)

## Contribute

If you are interested in contributing, please read [the code of conduct file](code-of-conduct.md).

PRs are accepted, but be aware that the tool currently meets our very limited needs and so our time to review is limited. We decided to share it with the open source community in the hopes that it would be as useful for others as it has been for us. You are encouraged to fork it and make a go of it on your own. Having said that, we would love to hear from you about your efforts! If we can help we will!

Small note: If editing the README, please conform to the [standard-readme](https://github.com/RichardLitt/standard-readme) specification.

## License

MIT © 2018 VolentixLabs
