### MEV-Geth WS demo


`mev_geth/` is a fork with a websocket branch, [diff](https://github.com/flashbots/mev-geth/compare/master...taarushv:websockets) (WIP)

`index.js` is a example relay ws server that submits bundles

Instructions
* Install server dependencies with `yarn install`
* Setup private chain datadir and genesis with `rm -rf datadir/ && make geth && ./build/bin/geth init --datadir datadir genesis.json` (in mev-geth folder)
* Run WS server first with `yarn start` (in root folder, same for below)
* Run MEV-Geth: `../mev-geth/build/bin/geth --datadir ../mev-geth/datadir --rpc --rpcapi debug,personal,eth,net,web3,txpool,admin,miner --miner.etherbase=0xd912aecb07e9f4e1ea8e6b4779e7fb6aa1c3e4d8 --miner.gasprice 0 --mine --miner.threads=8`

Output

* WS Server 
```
yarn run v1.22.10
$ node index.js
Funding account.....
Balance: 1000000000000000000
Submitting bundle
Miner before 1029000000000000000000
Miner after 1031020000000000000000
Profit (ETH) 0.02
Profit equals bribe? true
```
* MEV-Geth
```
INFO [04-20|09:22:37.879] Flashbots bundle                         ethToCoinbase=20000000000000000 gasUsed=42000 bundlePrice=476190476190 bundleLength=2
INFO [04-20|09:22:37.889] Commit new mining work                   number=16 sealhash="2d6cec…8c8368" uncles=0 txs=0 gas=0     fees=0 elapsed=7.682ms     isFlashbots=false
INFO [04-20|09:22:37.889] Proposed miner block                     blockNumber=16 profit=0 isFlashbots=false sealhash="2d6cec…8c8368" parentHash="4f2e21…cff0bc"
INFO [04-20|09:22:37.893] Commit new mining work                   number=16 sealhash="42af94…09c27f" uncles=0 txs=2 gas=42000 fees=0 elapsed=24.225ms    isFlashbots=true
INFO [04-20|09:22:37.894] Proposed miner block                     blockNumber=16 profit=20000000000000000 isFlashbots=true  sealhash="42af94…09c27f" parentHash="4f2e21…cff0bc"
INFO [04-20|09:22:38.577] Generating DAG in progress               epoch=1 percentage=7 elapsed=7.871s
INFO [04-20|09:22:38.587] Successfully sealed new block            number=16 sealhash="42af94…09c27f" hash="1bba33…d5362e" elapsed=693.521ms
INFO [04-20|09:22:38.587] 🔗 block reached canonical chain          number=9  hash="14b5ff…aac587"
```