# What is Minergate

MinerGate is a mining pool created to mine various cryptocurrencies.

# What does this Docker image

This image includes the Minergate-cli, a console miner provided by MinerGate.  
A specialalized version, this Docker image includes GPU mining.  

# Usage

Get minergate-cli options:
```
docker run --rm merowech/docker-mining:minergate -help
```

Mine FantomCoin and Monero:
```
docker run -d merowech/docker-mining:minergate -user {email} -fcn+xmr
```

Further possible cryptocurrencies:  
 - bcn Bytecoin
 - xmr Monero
 - fcn Fantomcoin
 - dsh Dashcoin
 - qcn QuazarCoin
 - xdn DigitalNote
 - mcn MonetaVerde
 - aeon Aeon coin
 - inf8 Infinium-8

Possible combinations:
 - fcn+bcn
 - fcn+xmr
 - fcn+qcn
 - fcn+xdn
 - fcn+aeon
 - fcn+dsh
 - mcn+bcn
 - mcn+xmr
 - mcn+qcn
 - mcn+xdn
 - mcn+aeon
 - mcn+dsh
