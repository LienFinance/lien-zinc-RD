# lien-zinc-RD

Testing Lien's basic LBT vs SBT DEX PoC 

[WARNING] 

 a new set of address and private key is required

## (1)
Obtain test ETH from the Rrinkeby testnet 

Rinkeby Fauset: https://faucet.rinkeby.io/

Generate a transaction using zkSync to create an account https://wallet.zksync.io/account

For more information: https://zinc.zksync.io/07-smart-contracts/04-troubleshooting.html?highlight=account#unlocking-a-zksync-account

## (2)

Install and enable zinc command and zargo command

https://github.com/matter-labs/zinc/releases

linux: zinc-0.2.1-linux.tar.gz

mac: zinc-0.2.1-macos.zip

Make sure that $PATH includes the path to where the files were extracted.

### [IMPORTANT]
When you use "zargo call" method, make sure you input the correct data to data/input. The, "msg" field and "arguments":"[method you use]" field are  required to be entered each time.

## (3)
Clone this repository,

`$ git clone https://github.com/LienFinance/lien-zinc-RD.git`

and make the contract initializing data in data/input.json 

`
"arguments": { "new": { "_deployer":"your address", "_strikePrice":"600" },
`

then deploy a contract

`
$ zargo publish --instance default --network rinkeby
`

export the contract address

`$ export CA=[your contract address]`

then mint LBT/SBT from your ether

`$ zargo call --method mint --address $CA --network rinkeby`

you can set the oracle price data with this command

`$ zargo call --method setLbtPerSbt --address $CA --network rinkeby`

with this argument at data/input.json (decimal 8) 

`
"setLbtPerSbt":{"_LbtPerSbtE8":"200000000"},
`

## (4)

Query command can get the storage of contract

Check the balance of your LBT/SBT

`$ zargo query --address $CA --network rinkeby`

## (5)

You can create a LBT sell order with flag=true, and a LBT buy order with flag=false

`
"orderDOTC":{"_amount":"50","flag":false},
`

`$ zargo call --method orderDOTC --address $CA --network rinkeby`

Swap with this command 

`$ zargo call --method lbtPerSbt --address $CA --network rinkeby`

### (6)

You can redeem your LBT with this command. Ether amount is always shown in E18.

`$ zargo call --method exchangeLBT2Ether --address $CA --network rinkeby`

### [IMPORTANT]

If you encounter these errors, the Zinc demo server is not available (offline).

503 Service Temporarily Unavailable /
502 Bad Gateway

