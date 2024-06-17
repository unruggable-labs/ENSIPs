---
ensip: TBD
title: Verified Web Archive (VWA) Contenthash
status: Idea
type: ENSRC
author: Prem Makeig / premm.eth (@nxt3d) <premm@unruggable.com>, raffy.eth <raffy@unruggable.com>
created: 2024-12-6
---

# Abstract 

This ENSIP extends the `contenthash` field to support the newly introduced Verfied Web Archive (VWA) content type. 

# Motivation

The `contenthash` field has become the standard for using ENS names for decentralized websites and dapps. With ENSIP-10 and CCIP-Read (EIP-3668), resolving ENS records from L2s and offchain is now possible, reducing the cost of using the `contenthash` field. This makes adopting the [data URL](https://datatracker.ietf.org/doc/html/rfc2397) standard feasible, allowing content like webapps, images, and videos to be stored onchain or offchain. While ENS names are traditionally linked with decentralization, CCIP-Read has increased their flexibility, enabling use cases like centralized offchain names. Data URLs are useful for resolving static content; however, it is not possible to use data URLs for resolving multipage applications. This ENSIP introduces a new primitive web format, Verified Web Archive (VWA), specifically designed to allow for multipage web applications to be stored onchain and resolved using an ENS name.

# Specification

ENSIP-7 introduced the `contenthash` field for resolving ENS names to content hosted on distributed systems such as IPFS and Swarm. The value returned by `contenthash` is represented as a machine-readable multicodec, which permits a wide range of protocols to be supported by ENS names. The format is specified as follows:

```
<protoCode uvarint><value []byte>
```

protoCodes and their meanings are specified in the [multiformats/multicodec](https://github.com/multiformats/multicodec) repository.

This ENSIP introduces a new type of multicodec, VWA. 

>[!WARNING] 
>This protoCodes is not approved yet!.

vwa: 0xf4

## Verified Web Archive (VWA)

Recently, with the development of low-cost L2 blockchains for Ethereum and data availability, i.e., blobs, it is now possible to post larger amounts of data on-chain at a lower cost. It is therefore feasible to post complete multipage websites, such as Vitalik.eth, on-chain. However, there is currently no existing `contenthash` format that is well suited for this application.

We introduce the VWA standard, a composable multipart standard that allows for individual components of, for example, Vitalik's blog, to be stored onchain individually. This includes images, HTML pages, CSS files, and JavaScript files. These files can be saved on any supported blockchain as inscriptions or as blobs on L1 Ethereum. In the case of blobs, only the hash of the data, in the form of the transaction ID, is saved permanently on the blockchain. Therefore, it will be necessary for the resolving gateway to have access to an index of all blobs data saved to L1 Ethereum. While the data is not stored on-chain, using blobs allows for on-chain data hashes to be used to verify data, as well as publish data to the entire Ethereum community.

Format: `uvarint(??) + byte(length(ensip11IDs)) + <ensip11IDs uint64>[] + <DATA as bytes>`

The VWA format is designed to provide the gateway the information necessary to retrive all the metadata and data objects necessary to resolve the multipage website. An array of [ENSIP-11](https://docs.ens.domains/ensip/11) chain ids `ensip11IDs`, which are based on both chainID and coinType, are provided, so that gateways that don't have access to all of the chains, can revert without loading additonal data. 

The MIME type of `DATA` bytes data is UTF-8 `application/json`.

The JSON data MUST have an outermost object. It must contain one and only one inner VWA object named with the prefix "vwa" followed by the version number, which is prefixed with a 'v' (e.g., "vwa_v1", "vwa_v2", etc.), with the specific version of the VWA format.

The VWA object MAY contain one or more page objects, contained with one and only one `pages` array. Each page object MUST have one and only one `path` parameter, and MUST contain either an `id` object or a `data` parameter. The `id` object is used for inscriptions and blobs transactions and MUST include a `thash` parameter, as well as an id `ensip11_id` using the ENSIP-11 format. Data parameters have the format, `uvarint(f3) + byte(length(MIME)) + <MIME bytes as ASCII> + <DATA as bytes>`.

Because VWA metadata files can contain other VWA metadata files, it is therefore possible for whole subdirectories to be stored in separate blockchain transactions. For example, if the path of a given URL request is `/blog/march/1`, and the `contenthash` of the ENS name points to a VWA metadata file, the gateway will first look for a path that matches `/blog/march/1`. If that can't be found, then it will look for a path that matches `/blog/march/`. If that path exists and contains an `id` or `data` that contains to a valid VWA metadata file, then look for the `/blog/march/1` path. If the exact path can be found, then access the `id` of `data` of the path and return the content in the [ENSIP-TBD-2](./ensip-TBD-2.md) data URL format. This process can be repeated as many times as necessary to find the correct path and data to resolve.

```
{
  "vwa_v1": {
    "pages": [
      {
        "path": "/",
        "id": {
          "thash": "0x123abc...",
          "ensip11_id": 1
        }
      },
      {
        "path": "/about",
        "data": "0xf36def...",
      },
	  {
        "path": "/about",
        "id": {
          "thash": "0x123abc...",
          "ensip11_id": 1
        }
      },
      {
        "path": "/contact",
        "id": {
          "thash": "0x789ghi...",
          "ensip11_id": 2
        }
      },
      {
        "path": "/styles.css",
        "id": {
          "thash": "0xabc123...",
          "ensip11_id": 2
        }
      },
      {
        "path": "/script.js",
        "id": {
          "thash": "0xdef456...",
          "ensip11_id": 3
        }
      },
      {
        "path": "/images/image.png",
        "id": {
          "thash": "0xghi789...",
          "ensip11_id": 3
        }
      }
    ]
  }
}
```

# Copyright
Copyright and related rights waived via [CC0](../LICENSE.md).


