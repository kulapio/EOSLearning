# EOSLearning
EOS Learning WIKI

## 1. Start Private Blockchain
```shell
#!/bin/sh
docker volume create eosio-work
docker volume create eosio-data

docker run --rm --name eosio \
    -d -p 8888:8888 \
    -p 9876:9876 \
    --mount source=eosio-work,target=/work \
    --mount source=eosio-data,target=/mnt/dev/data \
    eosio/eos-dev \
    /bin/bash -c "nodeos -e -p eosio --plugin eosio::wallet_api_plugin --plugin eosio::wallet_plugin --plugin eosio::producer_plugin --plugin eosio::history_plugin --plugin eosio::chain_api_plugin --plugin eosio::history_api_plugin --plugin eosio::http_plugin -d /mnt/dev/data --http-server-address=0.0.0.0:8888 --access-control-allow-origin=* --contracts-console"

docker exec -t eosio \
/bin/bash -c "echo \"PATH=$PATH:/opt/eosio/bin\" >> /root/.bashrc"
```

## 2. Make alias command for convenient usage
```shell
alias cleos='docker exec eosio /opt/eosio/bin/cleos --wallet-url http://localhost:8888'
````

## 3. Create wallet
```shell
cleos wallet create
```

## 4. Unlock wallet
```shell
$ cleos wallet unlock --password [Your password on step 3)]
```
