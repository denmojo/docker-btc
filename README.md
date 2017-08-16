denmojo/docker-btc
=============

This project builds a Docker image with latest ubuntu release of bitcoind and bitcoin-cli.

## Pre-requisites
  * Docker

## Building
  * `docker build -t bitcoin .`

## Configuration

Make a settings file bitcoin.conf.

## Running bitcoind
```  
   docker run --name bitcoind -d \
   --env 'BTC_RPCUSER=foo' \
   --env 'BTC_RPCPASSWORD=password' \
   --volume /your/custom/path:/bitcoin \
   --p 8332:8332
   --publish 8333:8333
   bitcoin
```

## Interacting with bitcoind
  * `docker exec -ti bitcoin bitcoin-cli -help`

It might be helpful to set up aliases in your .bashrc or .zshrc
```
alias bitcoind='docker run --name bitcoind -d --env 'BTC_RPCUSER=foo' --env 'BTC_RPCPASSWORD=password' -v /your/custom/path:/bitcoin -p 8332:8332 --publish 8333:8333 --rm -ti bitcoin'
alias bitcoin-cli='docker exec -ti bitcoind bitcoin-cli'
```

This allows you to just run bitcoin-cli as if it were local.

## Notes

Since the blockchain download is up to 152+ GB as of Aug 2017, it will take you a while to download and verify your copy of the blockchain. Please account for storage.

For further commands with bitcoin-cli, see [Original Bitcoin Client API Calls List][1].

[1]: https://en.bitcoin.it/wiki/Original_Bitcoin_client/API_calls_list
