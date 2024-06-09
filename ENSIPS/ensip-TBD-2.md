---
ensip: TBD
title: DataURI and URL Contenthash
status: Idea
type: ENSRC
author: Prem Makeig (premm.eth) <premm@unruggable.com>, raffy.eth <raffy@unruggable.com>
created: 2024-6-7
---

# Abstract 

This ENSIP extends the `contenthash` field to support two additional content types: Data URIs and URLs.

# Motivation

The `contenthash` field has become the standard for using ENS names for decentralized websites and dapps. With ENSIP-10 and CCIP-Read (EIP-3668), resolving ENS records from L2s and offchain is now possible, reducing the cost of using the `contenthash` field. This makes adopting the DataURI standard feasible, allowing content like webapps, images, and videos to be stored either onchain or offchain. While ENS names are traditionally linked with decentralization, CCIP-Read has increased their flexibility, enabling use cases like centralized offchain names. However, the `contenthash` field still supports only decentralized storage. This ENSIP also introduces a new URL content type for the `contenthash` field, allowing browsers to redirect to a standard URL when loading an ENS name.

# Specification

ENSIP-7 introduced the `contenthash` field for resolving ENS names to content hosted on distributed systems such as IPFS and Swarm. The value returned by `contenthash` is represented as a machine-readable multicodec, which permits a wide range of protocols to be supported by ENS names. The format is specified as follows:

```
<protoCode uvarint><value []byte>
```

protoCodes and their meanings are specified in the multiformats/multicodec repository.

This intruduces two new types of new multicodecs, URI and Data URI.  

We have proposed to multiformats the [protoCodes](https://github.com/multiformats/multicodec/tree/master?tab=readme-ov-file#adding-new-multicodecs-to-the-table):

[!WARNING] 
These protoCodes are not approved yet! Use ENS specific codes instead until they become approved.

URI: 0xf2 
Data URI: 0xf3

However, we have no control over whether these protoCodes will be approved. It is however possible to have ENS specific protoCodes using a pre-reserved range of protoCodes, 0x300000 to 0x3FFFFF, set aside for application speciific use cases. 

ENS specific protoCodes:

URI: 0x38d195
Data URI: 0x38d196


## Two new formats ?? Do thise need to be multihashes becasue of ENSIP-7
	1. URL
		* Format: `uvarint(codec1) + <URL as utf8 bytes>`

	1. DataURI
		* Format: `uvarint(codec2) + byte(length(MIME)) + <MIME bytes as ascii> + <DATA as bytes>`
		* `mime` cannot exceed 255 bytes (or could be another uvarint)

* Render as Human-readable URL
	1. URL: `$URL` (literal)
	1. DataURI: `data:$MIME;base64,${btoa($DATA)}`

* Render via Gateway (eg. `.limo`)
	1. URL: `HTTP 307`
		* `Location: $URL$PATH`
		* eg. `https://nick.eth.limo/a/b.c?d=e` has path `/a/b.c?d=e`
	1. DataURI: `HTTP 200`
		* `Content-type: $MIME`
		* For servable content, like: `text/*`, serve the same content regardless of path.
			* eg. `https://premm.eth.limo` === `https://premm.eth.limo/a/b/c`
			* Use HTML+JS to dynamically handle the path/querystring
			* See web archive ideas (below)
		* Otherwise:
			* `Content-Transfer-Encoding: binary` (or mime is sufficient?)
		
* Note: you can stick a `data:...` in URL but 4/3 data overhead and it will redirect instead of serve under your domain name

* Note: although storage costs likely curtail sizes, we should probably defines limits:
	* URL: [2000? bytes](https://stackoverflow.com/questions/417142/what-is-the-maximum-length-of-a-url-in-different-browsers)
	* DataURI: 1MB?

* Web Archive:
	* IPFS allows hash/path to index into a pinned directory
	* DataURI with text/html would allow text content, but no relative assets (like images)
	* Either utilize an existing .webarchive format, like a special mime that is actually a zip archive of a web directory
	* Users could also create a single HTML file using a bundler that embeds all of the content inline or compressed using JS

* Issues: malicious files, rick rolls, zip bombs, etc.
