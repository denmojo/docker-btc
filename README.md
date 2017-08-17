denmojo/docker-btc
=============

This project builds a docker image with latest ubuntu release of bitcoind server and bitcoin-cli client. Run your own full bitcoin node with docker!

## Pre-requisites
  * [Docker][1]

## Building
  * cd to cloned directory
  * `docker build -t bitcoin .`

## Configuration

Make a settings file `bitcoin.conf` in the data directory of your choosing.

## Running bitcoind
```  
   docker run --name bitcoind -d \
   --env 'BTC_RPCUSER=foo' \
   --env 'BTC_RPCPASSWORD=password' \
   --volume /your/datadir/path:/bitcoin \
   -p 8332:8332 \
   --publish 8333:8333 \
   bitcoin
```

## Interacting with bitcoind
  * `docker exec -ti bitcoin bitcoin-cli -help`

It might be helpful to set up aliases in your .bashrc or .zshrc
```
alias bitcoind='docker run --name bitcoind -d --env 'BTC_RPCUSER=foo' --env 'BTC_RPCPASSWORD=password' -v /your/datadir/path:/bitcoin -p 8332:8332 --publish 8333:8333 --rm -ti bitcoin'
alias bitcoin-cli='docker exec -ti bitcoind bitcoin-cli'
```

This allows you to just run bitcoin-cli as if it were local.

To see what bitcoind is up to, less the debug log:
`less /your/datadir/path/.bitcoin/debug.log`

This is useful to watch when you stop bitcoind so that you are sure it has finished shutting down and saving state.

## Stopping bitcoind
Provided that you created the aliases above, just run:
`bitcoin-cli stop`

Otherwise if you want the docker command:
`docker exec -ti bitcoind bitcoin-cli stop`

## Notes

Since the blockchain download is up to 152+ GB as of Aug 2017, it will take you a while to download and verify your copy of the blockchain. Please account for storage.

For further commands with bitcoin-cli, see [Original Bitcoin Client API Calls List][2].

[1]: https://www.docker.com/community-edition#/download
[2]: https://en.bitcoin.it/wiki/Original_Bitcoin_client/API_calls_list
