---
ensip: TBD
title: Hashed Bytes Storage
status: Idea
type: ENSRC
author: raffy.eth <raffy@unruggable.com>
created: 2024-18-7
---

# Abstract 

This ENSIP describes how to store an *optional* keccak256 hash (`bytes32`) for any Solidity storage value to reduce `eth_getProof` requirements: O(N) &rarr; O(1).

# Sketch

Note: This should work for any storage but is easiest to explain for `bytes`.

When EVMGateway read a `bytes` at `$SLOT` that spans more than `$SLOTS_THRESHOLD` slots, the EVMGateway can optimistically read `HASH_SLOT($SLOT)` and then compare if it matches `keccak256()` of 32-byte aligned bytes (0-padded).  If so, instead of proving every slot, only the slot of the hash needs proven and the slot data can be supplied unverified.  This massively reduces `eth_getProof` overhead for large storage values.

### Potential Encoding Functions
```
// requirement: an unlikely computed slot, parameterized by slot

bytes32 constant C = keccak256("ensip.hashslot") - 1;
function HASH_SLOT(uint256 slot) {
	// some unlikely mapped position
	return keccak256(abi.encode(slot, C)) - 1;
}

function HASH_SLOT(uint256 slot) {
	// hash of bit rotate
	return keccak256(abi.encode((slot << 128) | (slot >> 128))) - 1;
}

uint256 constant SLOTS_THRESHOLD = 10;
uint256 constant BYTES_THRESHOLD = SLOTS_THRESHOLD > 0 ? ((SLOTS_THRESHOLD-1) << 5) + 1 : 0;
```

### Example Usage

```solidity
contract Test {
	bytes value; // slot #0
	function setValue(bytes memory v) external {
		// update value
		value = v;
		// update HASH_SLOT() of value
		if (v.length >= BYTES_THRESHOLD) { // optional conditional
			bytes32 slot = HASH_SLOT(value.slot);
			bytes padded = abi.encode(v);
			assembly {
				sstore(slot, keccak256(padded, mload(padded)))
			}
		}
	}
}
```

### Related

* [LeadingHashStorage](https://github.com/3dns-xyz/contracts/blob/master/src/utils/storage/LeadingHashStorage.sol) from 3DNS
