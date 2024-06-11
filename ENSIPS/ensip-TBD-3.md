---
ensip: TBD
title: ENS Profile
status: Idea
type: ENSRC
author: raffy.eth <raffy@unruggable.com>
created: 2024-6-10
---

Use `addr(<exotic coinType>)` to store a light-weight description of additional ENS records (text, addr, contenthash, ...) that a name may have.

ENS Graph indexeding can only identify on-chain L1 records.  This ENSIP would allow CCIP-Read servers (offchain and L2-via-EVMGateway) to display/advertise additional records.

Community members can share the same profile contract, which exposes a common set of records.

* Define ENS Standard Profile
	* Version 1
		* [Texts](https://github.com/ensdomains/ens-app-v3/blob/main/src/constants/textRecords.ts): `name email url avatar location description notice keywords com.discord com.github com.reddit com.twitter org.telegram`
		* [Addrs](https://github.com/ensdomains/ens-app-v3/blob/main/src/constants/supportedAddresses.ts): `eth btc bnb doge ltc dot sol`
		* Contenthash, Pubkey, ABI?

* Forum Posts:
	1. https://discuss.ens.domains/t/temp-check-standardize-education-text-record/18950/2?u=raffy
	1. https://discuss.ens.domains/t/eth-cd-a-social-hub-for-ens-domains/18119/13

* Experimental Implementations:
	* Solidity: https://github.com/adraffy/tkn-gateway/blob/main/TNS/TNS8.sol	
		* `addFields()`, `removeFieldAt()`, `makeCalls()`
	* Javascript: https://github.com/resolverworks/enson.js/blob/main/src/Record.js#L256
		* `makeCalls()`

* Usage Example:  
	```js
	// TODO fix this
	// get resolver (ENSIP-10)
	resolver = findResolve(name)
	// get normal records + profile
	data = multicall([...$RECORDS, addr(PROFILE_COINTYPE)])
	// decode profile
	profile = decodeProfile(data[-1]);
	if (profile) { // get additional records
		data += multicall([...profile])
	}
	```

* Formats:
	* Field List Encoding (FLE)
		* eg. `[addr(60), addr(123), text("chonk"), ...]`
	* Contract Encoding
		* eg. `abi.encodePacked(address(C))`
		* where `C` = contract with `profile(name) returns FLE`
	* TBD
