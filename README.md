# docker-bitcore
create a bitcoin node real quick-like
inspired by [this](https://hub.docker.com/r/sena/bitcore/)

## quick-start
First, create a volume in which the persistent data may be stored. This is the blockchain, and the node configuration json file `bitcoin-node.json`
```
docker volume create --name bitcore_data
```

Add your desired `bitcoin-node.json` file into the volume. [Service options list](https://github.com/bitpay/bitcore-node/blob/master/bitcore-node.json.sample).
Example:
```
{
  "network": "livenet",
  "port": 3001,
  "services": [
    "bitcoind",
    "web"
  ]
}
```

Now, run the image with flags to punch out ports for various services you are intending to enable and designate in your `bitcoin-node.json` file.
```
docker run -d --restart=always --name bitcore \
   -p 3001:3001 -p 8333:8333 \
   -v bitcore_data:/root/.bitcore \
   nthieling/bitcore
```
