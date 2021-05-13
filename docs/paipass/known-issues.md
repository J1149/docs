# Known Issues with PAI Pass

## PAICoin Service
### Wallet erasure
The wallet seems to erase itself every once in a while. This can be found by inspecting the s3 resource under which it is stored; the size of the wallet will suddenly drop out when this occurs.

## Yggdrasil
### Yggdrasil Bleeding Schema Through 
Yggdrasil doesn't have a good mechanism to prevent bleeding through of schema's of other apps hosted on it.