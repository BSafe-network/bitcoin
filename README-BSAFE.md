Bitcoin Core with BSafe.Network Modifications
=============================================

This branch of Bitcoin core includes support for creating
[BSafe.Network](https://bsafe.network/)'s Bitcoin blockchain
network `bsafenet` for its own testing purposes. Please refer to
[BSafe.Network site](https://bsafe.network/) on the motivation and
activities on the BSafe.Network.

This patch is currently maintained by Shigeya Suzuki <<shigeya@wide.ad.jp>>


Repository Location
-------------------

Current primary repository is located at
[https://github.com/keio-bcl/bitcoin](https://github.com/keio-bcl/bitcoin).
The code deployed to the network is maintained in
[`bsafe-deploy`](https://github.com/keio-bcl/bitcoin/tree/bsafe-deploy)
branch. Please clone and check out the branch accordingly, like this:

    git clone https://github.com/keio-bcl/bitcoin
    cd bitcoin
    git checkout bsafe-deploy


Installation
------------

Please refer to [doc directory](doc) for general build
directions. While the maintainer believes it does not have any
platform dependency, we only tested on Debian 9, Ubuntu 18.04 LTS, and MacOS X Mojave.
Please read [doc/build-unix.md](doc/build-unix.md) or
[doc/build-osx.md](doc/build-osx.md) on dependencies for build. There
is no specific build requirement for BSafe.Network patch.  If you
find any problem, please report to the maintainer.

At our site, we're building with the following steps:

    bash # maybe safer to do this
    ./autogen.sh
    ./configure
    make
    make install # optional

We provide Debian 9 and Ubuntu 18.04 LTS specific build steps in the below for your convinience.


Running the daemon
------------------

To run with BSafeNetwork's network, use `-bsafenet` option to both
`bitcoind` and `bitcoin-cli` commands.


Update to the latest version
----------------------------

For updating the code, since we frequently rebase towards Bitcoin
Core's releases, we recommend the following steps:

    git checkout bsafe-deploy
    git fetch
    git reset --hard remotes/origin/bsafe-deploy
    # follow the same build steps

Building on Debian 9 and Ubuntu 18.04 LTS
=========================================

Following is an example of steps work for Debian 9 (Debian 9.9 to be specific) and Ubuntu 18.04 LTS.

Setup Debian or Ubuntu
----------------------
You can work on the build via Desktop or remote login via SSH, but for maintenance, we recommend to use remote login based maintenance. We also recommend to build the binary using regular user account.

For Debian, you need to setup `sudo` command, which default minimum installation don't install. You can install it and setup, via root login session:

    apt-get install -y sudo
    addgroup USERNAME sudo # replace USERNAME with your login name

Build Steps
-----------
Assuming you have logged in with USERNAME, run following commands in the order:

Install packages needed for the build:

    sudo apt-get install -y git ca-certificates autoconf libtool make gcc g++ pkg-config libssl-dev libboost-dev libboost-system-dev libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev libevent-dev libdb++-dev libboost-chrono-dev libboost-test-dev

Retrieve sources:

    mkdir ~/work/bsafe
    cd ~/work/bsafe
    git clone git@github.com:keio-bcl/bitcoin.git
    cd bitcoin
    git checkout bsafe-deploy

Configure, build and install:

    bash
    ./autogen.sh
    ./configure --with-gui=no --with-incompatible-bdb
    make
    sudo make install
