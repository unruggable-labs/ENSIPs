---
ensip: TBD
title: Verified Web Archive (VWA) Contenthash
status: Idea
type: ENSRC
author: Prem Makeig (premm.eth) <premm@unruggable.com>, raffy.eth <raffy@unruggable.com>
created: 2024-12-6
---

# Abstract 

This ENSIP extends the `contenthash` field to support the additional content types, data URL and URI, as well as a newly introduced Verfied Web Archive (VWA) content type. 

# Motivation

The `contenthash` field has become the standard for using ENS names for decentralized websites and dapps. With ENSIP-10 and CCIP-Read (EIP-3668), resolving ENS records from L2s and offchain is now possible, reducing the cost of using the `contenthash` field. This makes adopting the [data URL](https://datatracker.ietf.org/doc/html/rfc2397) standard feasible, allowing content like webapps, images, and videos to be stored onchain or offchain. While ENS names are traditionally linked with decentralization, CCIP-Read has increased their flexibility, enabling use cases like centralized offchain names. However, the `contenthash` field still supports only decentralized storage. Data URLs are useful for resolving static content, however, it is not possible to use data URLs for resolving multipage applications. This ENSIP introduces a new primitive web format, Verified Web Archive (VWA), specicaly design to allow for multipage web applications to stored onchain and resolved using a ENS name.  

# Specification

ENSIP-7 introduced the `contenthash` field for resolving ENS names to content hosted on distributed systems such as IPFS and Swarm. The value returned by `contenthash` is represented as a machine-readable multicodec, which permits a wide range of protocols to be supported by ENS names. The format is specified as follows:

```
<protoCode uvarint><value []byte>
```

protoCodes and their meanings are specified in the [multiformats/multicodec](https://github.com/multiformats/multicodec) repository.

This ENSIP intruduces the new types of new multicodecs, uri, data-url, and vwa.  

>[!WARNING] 
>This protoCodes is not approved yet!.

vwa: 0xf4

## Verified Web Archive (VWA)

Recently with the development of low cost L2 blockchains for Etherem and data availabilty, i.e. blobs, it is now possible to post larger amounts of data onchain at a lower cost. It is therefore feasible to post complete multipage websites, such as Vitalik.eth onchain, there is however, no existing `contenthash` format that is well suited for this application. We introduce the VWA standard which is a composable multipart standard, that allows for individual components of for example Vitalik's blog, to be stored onchain, individually, for example images, HTML pages, CSS files, and JavaScript files. These files can be saved on any supported blockchain as inscriptions, or for example as blobs on L1 Ethereum. In the case of blobs, only the hash of the data in the form of the transaction id, is saved permanently on the blockchain. In this case it will be necessary for the resolving gateway to have access to a index of all blobs data saved to L1 Ethereum. While the data is is not stored onchian, using blobs, allows for data hashes to be used to verify data, as well as publish data to the entire Ethereum community. 

Format: `uvarint(??) + byte(length(MIME)) + <MIME bytes as ascii> + <DATA as bytes>`

The VWA format is the same as the data URL format, however a new metadata JSON standard is introduced, that allows for creating a web archive. 

If the mime type is `application/json`, then the json, the JSON data must be in the following format:

There MUST be one `vwa_v1` outermost object, which identifies the metadata as a VWA metadata file, with a version number. 

There MAY be as many `pages` objects, which MUST have one and only one `path` parameters, and MUST contain either a `id` parameter, or a `data` parameter. The `id` parameter is used for incriptions and blobs transactions, and MUST include a `thash` parameter, as well as a `ensip11_id`.

For `data` paramaters the format is the same as dara-url, `uvarint(f3) + byte(length(MIME)) + <MIME bytes as ascii> + <DATA as bytes>`.

Because VWA metadata files can contain other VWA metadata files, it is therefore possible for whole subdirectores to be stored in separate blockchain transactions. For example if the path of a given URL request is `/blog/march/1`, and the `contenthash` of the ENS name points to a VWA metadata file, the the gateway will first look for a path that matches `/blog/march/1`, if that can't be found, then it will look for a path that matches `/blog/march/`. If that patch exists, and contains an `id` that points to a valid VMA metadata file, then start the process over again, looking for the `/blog/march/1` path. If the exact path can be found then, access the `id` of the path and return the data-url content. This process can be reapeated as many times as necessary to find the correct path and data to resolve. 

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


