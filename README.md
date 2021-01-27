# lien-zinc-RD
Testing Lien's basic LBT vs SBT DEX PoC
[WARNING] a new set of address and private key is required

(1)

have the faucet of rinkeby testnet
Rinkeby Fauset https://faucet.rinkeby.io/

have some transactions here to get registered
Zksync https://wallet.zksync.io/account 

reference: 
https://zinc.zksync.io/07-smart-contracts/04-troubleshooting.html?highlight=account#unlocking-a-zksync-account

(2)

install and enable zinc command and zargo command

https://github.com/matter-labs/zinc/releases

linux:
zinc-0.2.1-linux.tar.gz

mac:
zinc-0.2.1-macos.zip

make sure $PATH includes their path. 

(3)

`$ git clone https://github.com/LienFinance/lien-zinc-RD.git`
`$ zargo publish --instance default --network rinkeby`

get the contract address and export it

`$ export CA=[your contract address]`

then mint LBT/SBT from your ether
`$ zargo call --method mint  --address $CA  --network rinkeby`

(4) 

query command can get the storage of contract
check the balance of LBT/SBT
`$ zargo query  --address $CA  --network rinkeby`

(5)

you can order the 
`"orderDOTC":{"_amount":"50","flag":false},`

`$ zargo call --method orderDOTC  --address $CA  --network rinkeby`

swap with this command 
`$ zargo call --method lbtPerSbt  --address $CA  --network rinkeby`

(6) 

you can redeem your lbt with this command.
`$ zargo call --method exchangeLBT2Ether  --address $CA  --network rinkeby`
