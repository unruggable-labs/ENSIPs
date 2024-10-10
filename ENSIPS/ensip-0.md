---
ensip: 0
title: ENSIP Purpose and Guidelines
status: Living
type: Meta
author: Prem Makeig | premm.eth (@nxt3d) <premm@unruggable.com>
created: 2024-4-26
---

## What is an ENSIP?

ENSIP stands for Ethereum Name Service Improvement Proposal. An ENSIP is a design document providing information to the ENS and the broader Ethereum and blockchain community, describing a new feature or a change to the ENS protocol or a new standard to be used by the ENS community. The ENSIP should provide a concise technical specification of the feature, change, or standard and a rationale for the said feature, change, or standard. The ENSIP author is responsible for building consensus within the community and documenting dissenting opinions.

## ENSIP Rationale

This ENSIP aims to establish a system similar to that of EIPs, including various stages for ENSIPs such as draft, review, last call, and final. It will allow for proposing new features, changes, and standards, gathering community technical input on issues, and documenting the design decisions involved. Maintained as text files in a versioned repository, the revision history of ENSIPs will serve as the historical record of each proposal.

For ENS implementers, ENSIPs provide a convenient way to track the progress of their implementations. Ideally, each implementation maintainer would list the ENSIPs they have implemented, offering end users a convenient method to check the current status of a given implementation or library.

## ENSIP Types

There are three types of ENSIPs:

- A **Standards Track ENSIP** describes any change that affects most or all ENS implementations, such as changes to the ENS protocol, including the way an ENS name is resolved, proposed application standards/conventions, or any change or addition that affects the interoperability of applications using ENS. Standards Track ENSIPs consist of three parts—a design document, an implementation, and (if warranted) an update to the formal protocol specification. Furthermore, Standards Track ENSIPs can be broken down into the following categories:

  - **Core**: improvements requiring a change to the way that ENS names are resolved by clients, standards that affect the validity of ENS name character combinations, or any standard that would reasonably affect the everyday use of ENS names by users and clients.
  - **ENSRC**: application-level standards and conventions, including contract standards such as resolver standards, name registries, URI schemes, library/package formats, and wallet integrations.

- A **Meta ENSIP** describes a process surrounding ENS or proposes a change to (or an event in) a process. Process ENSIPs are like Standards Track ENSIPs but apply to areas other than the ENS protocol itself. They may propose an implementation, but not anything that changes the way ENS names are resolved, for example; they often require community consensus; unlike Informational ENSIPs, they are more than recommendations, and users are typically not free to ignore them. Examples include procedures, guidelines, changes to the decision-making process, and changes to the tools or environment used in ENS development. Any meta-ENSIP is also considered a Process ENSIP.

- An **Informational ENSIP** describes an ENS protocol design issue, or provides general guidelines or information to the ENS community, but does not propose a new feature or a change to the protocol. Informational ENSIPs do not necessarily represent ENS community consensus or a recommendation, so users and implementers are free to ignore Informational ENSIPs or follow their advice.

It is highly recommended that a single ENSIP contain a single key proposal or new idea. The more focused the ENSIP is, the more successful it tends to be. A change to one application or client doesn't require an ENSIP; a change that affects multiple clients, such as wallets or libraries, or defines a standard for multiple apps to use, does.

An ENSIP must meet certain minimum criteria. It must provide a clear and complete description of the proposed enhancement. The enhancement must represent a net improvement. The proposed implementation, if applicable, must be solid and must not complicate the protocol unduly.

### Special requirements for Core ENSIPs

If a **Core ENSIP** mentions or proposes changes to the ENS protocol, it should cite a previous ENSIP whenever possible, in order to root the proposal in an existing aspect of the protocol.

## ENSIP Work Flow

### Shepherding an ENSIP

Parties involved in the process are you, the champion or ENSIP author, the ENSIP editors, and the ENS DAO.

Before writing a formal ENSIP, you should first vet your idea by discussing it with the ENS community to ensure originality and avoid rejection due to prior research. Opening a thread on the ENS DAO forum is recommended. Once vetted, your responsibility is to present the idea in an ENSIP Draft, inviting feedback from editors, developers, and the community. It's important to gauge interest in the ENSIP relative to the effort involved in implementing it and how many parties will need to adopt it. Negative feedback could prevent the ENSIP from advancing beyond the Draft stage.

### Core ENSIPs

For Core ENSIPs, given that they may require upgrades to smart contracts, gateways, and client implementations to be considered Final (see "ENSIPs Process" below), you will need to either provide an implementation for clients or convince clients to implement your ENSIP.

The best way to get feedback from ENS developers is to present the ENSIP at the ENS Ecosystem call. The ENS Ecosystem call serves as a way for developers in the ENS community to get feedback on their projects, as well as discuss improvements to ENS, including the core ENS protocol.

These calls may result in a "rough consensus" around the merits of an ENSIP, and may serve to direct authors of ENSIPs to further consult relevant parties who may be impacted, for example, wallets, or well-known dapps that implement the ENS protocol.

*In short, your role as the champion is to write the ENSIP using the style and format described below, shepherd the discussions in the appropriate forums, and build community consensus around the idea.*

### ENSIP Process

The following is the standardization process for all ENSIPs in all tracks:

![ENSIP Status Diagram](../assets/ENSIP-0/EIP-process-update.jpg)

**Idea** - An idea that is pre-draft. This is not tracked within the ENSIP Repository.

**Draft** - The first formally tracked stage of an ENSIP in development. An ENSIP is merged by an ENSIP Editor into the ENSIP repository when properly formatted.

**Review** - An ENSIP Author marks an ENSIP as ready for and requesting Peer Review.

**Last Call** - This is the final review window for an ENSIP before moving to `Final`. An ENSIP editor will assign `Last Call` status and set a review end date (`last-call-deadline`), typically 14 days later.

If this period results in necessary normative changes, it will revert the ENSIP to `Review`.

**Final** - This ENSIP represents the final standard. A Final ENSIP exists in a state of finality and should only be updated to correct errata and add non-normative clarifications.

A PR moving an ENSIP from Last Call to Final SHOULD contain no changes other than the status update. Any content or editorial proposed change SHOULD be separate from this status-updating PR and committed prior to it.

**Stagnant** - Stagnant - Any ENSIP in `Draft`, `Review`, or `Last Call` if inactive for a period of 6 months or greater is moved to `Stagnant`. An ENSIP may be resurrected from this state by Authors or ENSIP Editors through moving it back to `Draft` or its earlier status. If not resurrected, a proposal may stay forever in this status.

> *ENSIP Authors are notified of any algorithmic change to the status of their ENSIP*

**Withdrawn** - The ENSIP Author(s) have withdrawn the proposed ENSIP. This state has finality and can no longer be resurrected using this ENSIP number. If the idea is pursued at a later date, it is considered a new proposal.

**Living** - A special status for ENSIPs that are designed to be continually updated and not reach a state of finality. This includes most notably ENSIP-0.

## What belongs in a successful ENSIP?

Each ENSIP should have the following parts:

- Preamble - RFC 822 style headers containing metadata about the ENSIP, including the ENSIP number, a short descriptive title (limited to a maximum of 44 characters), a description (limited to a maximum of 140 characters), and the author details. Irrespective of the category, the title and description should not include the ENSIP number. See [below](./ensip-0.md#eip-header-preamble) for details.
- Abstract - The abstract is a multi-sentence (short paragraph) technical summary. This should be a very terse and human-readable version of the specification section. Someone should be able to read only the abstract to get the gist of what this specification does.
- Motivation *(optional)* - A motivation section is critical for ENSIPs that want to change the Ethereum protocol. It should clearly explain why the existing protocol specification is inadequate to address the problem that the ENSIP solves. This section may be omitted if the motivation is evident.
- Specification - The technical specification should describe the syntax and semantics of any new feature. The specification should be detailed enough to allow competing, interoperable implementations including wallets and libraries.
- Rationale - The rationale fleshes out the specification by describing what motivated the design and why particular design decisions were made. It should describe alternate designs that were considered and related work, e.g., how the feature is supported in other languages. The rationale should discuss important objections or concerns raised during the discussion around the ENSIP.
- Backwards Compatibility *(optional)* - All ENSIPs that introduce backwards incompatibilities must include a section describing these incompatibilities and their consequences. The ENSIP must explain how the author proposes to deal with these incompatibilities. This section may be omitted if the proposal does not introduce any backwards incompatibilities, but this section must be included if backward incompatibilities exist.
- Test Cases *(optional)* - Test cases for an implementation are mandatory for ENSIPs that are affecting consensus changes. Tests should either be inlined in the ENSIP as data (such as input/expected output pairs) or included in `../assets/ensip-###/<filename>`. This section may be omitted for non-Core proposals.
- Reference Implementation *(optional)* - An optional section that contains a reference/example implementation that people can use to assist in understanding or implementing this specification. This section may be omitted for all ENSIPs.
- Security Considerations - All ENSIPs must contain a section that discusses the security implications/considerations relevant to the proposed change. Include information that might be important for security discussions, surfaces risks and can be used throughout the lifecycle of the proposal. E.g., include security-relevant design decisions, concerns, important discussions, implementation-specific guidance and pitfalls, an outline of threats and risks and how they are being addressed. ENSIP submissions missing the "Security Considerations" section will be rejected. An ENSIP cannot proceed to status "Final" without a Security Considerations discussion deemed sufficient by the reviewers.
- Copyright Waiver - All ENSIPs must be in the public domain. The copyright waiver MUST link to the license file and use the following wording: `Copyright and related rights waived via [CC0](../LICENSE.md).`

## ENSIP Formats and Templates

ENSIPs should be written in [markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) format. There is a [template](../ensip-template.md) to follow.

## ENSIP Header Preamble

Each ENSIP must begin with an [RFC 822](https://www.ietf.org/rfc/rfc822.txt) style header preamble, preceded and followed by three hyphens (`---`). This header is also termed ["front matter" by Jekyll](https://jekyllrb.com/docs/front-matter/). The headers must appear in the following order:

`ENSIP`: *ENSIP number*

`title`: *The ENSIP title is a few words, not a complete sentence*

`description`: *Description is one full (short) sentence*

`author`: *The list of the author's or authors' name(s), ENS name(s), username(s), and email(s). Details are below.*

`discussions-to`: *The URL pointing to the official discussion thread*

`status`: *Draft, Review, Last Call, Final, Stagnant, Withdrawn, Living*

`last-call-deadline`: \*The date last call period ends on (Optional field, only needed when status is Last Call)

`type`: *One of `Standards Track`, `Meta`, or `Informational`*

`category`: *One of `Core` or `ERC`* (Optional field, only needed for `Standards Track` ENSIPs)

`created`: *Date the ENSIP was created on*

`requires`: *ENSIP number(s)* (Optional field)

`withdrawal-reason`: *A sentence explaining why the ENSIP was withdrawn.* (Optional field, only needed when status is `Withdrawn`)

Headers that permit lists must separate elements with commas.

Headers requiring dates will always do so in the format of ISO 8601 (yyyy-mm-dd).

### `author` header

The `author` header lists the names, ENS names, email addresses or usernames of the authors/owners of the ENSIP. Those who prefer anonymity may use a ENS name and username only, or a first name, ENS name, and a username. The format of the `author` header value must be:

> Random J. User | randomu.eth &lt;address@dom.ain&gt;

or

> Random J. User | randomu.eth (@username)

or

> Random J. User | randomu.eth (@username) &lt;address@dom.ain&gt;

if the email address and/or GitHub username is included, and

> Random J. User | randomu.eth

if neither the email address nor the GitHub username are given.

At least one author must use a GitHub username, in order to get notified on change requests and have the capability to approve or reject them. All authors must have an ENS name.

### `discussions-to` header

While an ENSIP is a draft, a `discussions-to` header will indicate the URL where the ENSIP is being discussed.

The preferred discussion URL is a topic on [ENS Forum](http://discuss.ens.domains). The URL cannot point to GitHub pull requests, any URL which is ephemeral, or any URL which can get locked over time (e.g., Reddit topics).

### `type` header

The `type` header specifies the type of ENSIP: Standards Track, Meta, or Informational. If the track is Standards, please include the subcategory (core or ERC).

### `category` header

The `category` header specifies the ENSIP's category. This is required for standards-track ENSIPs only.

### `created` header

The `created` header records the date that the ENSIP was assigned a number. The date should be in the yyyy-mm-dd format, e.g., 2001-08-14.

### `requires` header

ENSIPs may have a `requires` header, indicating the ENSIP numbers that this ENSIP depends on. If such a dependency exists, this field is required.

A `requires` dependency is created when the current ENSIP cannot be understood or implemented without a concept or technical element from another ENSIP. Merely mentioning another ENSIP does not necessarily create such a dependency.

## Linking to External Resources

With EIPs (Ethereum Improvement Proposal), external links are disallowed except for a predefined set which are specified, including their format in EIP-1. For ENSIPs, external links are allowed; however, external links **MUST** conform to the formats if specified in this document. Because links may become broken if the URL destinations change or disappear, extra care should be taken when including external links. For example, a link to a GitHub document should include a commit, e.g., "/blob/23234...23a74/". It is within the discretion of ENSIP editors whether to allow external links on a case-by-case basis.

### Execution Client Specifications

Links to the Ethereum Execution Client Specifications may be included using normal markdown syntax, such as:

```markdown
[Ethereum Execution Client Specifications](https://github.com/ethereum/execution-specs/blob/9a1f22311f517401fed6c939a159b55600c454af/README.md)
```

Which renders to:

[Ethereum Execution Client Specifications](https://github.com/ethereum/execution-specs/blob/9a1f22311f517401fed6c939a159b55600c454af/README.md)

Permitted Execution Client Specifications URLs must anchor to a specific commit, and so must match this regular expression:

```regex
^(https://github.com/ethereum/execution-specs/(blob|commit)/[0-9a-f]{40}/.*|https://github.com/ethereum/execution-specs/tree/[0-9a-f]{40}/.*)$
```

### Consensus Layer Specifications

Links to specific commits of files within the Ethereum Consensus Layer Specifications may be included using normal markdown syntax, such as:

```markdown
[Beacon Chain](https://github.com/ethereum/consensus-specs/blob/26695a9fdb747ecbe4f0bb9812fedbc402e5e18c/specs/sharding/beacon-chain.md)
```

Which renders to:

[Beacon Chain](https://github.com/ethereum/consensus-specs/blob/26695a9fdb747ecbe4f0bb9812fedbc402e5e18c/specs/sharding/beacon-chain.md)

Permitted Consensus Layer Specifications URLs must anchor to a specific commit, and so must match this regular expression:

```regex
^https://github.com/ethereum/consensus-specs/(blob|commit)/[0-9a-f]{40}/.*$
```

### Networking Specifications

Links to specific commits of files within the Ethereum Networking Specifications may be included using normal markdown syntax, such as:

```markdown
[Ethereum Wire Protocol](https://github.com/ethereum/devp2p/blob/40ab248bf7e017e83cc9812a4e048446709623e8/caps/eth.md)
```

Which renders as:

[Ethereum Wire Protocol](https://github.com/ethereum/devp2p/blob/40ab248bf7e017e83cc9812a4e048446709623e8/caps/eth.md)

Permitted Networking Specifications URLs must anchor to a specific commit, and so must match this regular expression:

```regex
^https://github.com/ethereum/devp2p/(blob|commit)/[0-9a-f]{40}/.*$
```

### World Wide Web Consortium (W3C)

Links to a W3C "Recommendation" status specification may be included using normal markdown syntax. For example, the following link would be allowed:

```markdown
[Secure Contexts](https://www.w3.org/TR/2021/CRD-secure-contexts-20210918/)
```

Which renders as:

[Secure Contexts](https://www.w3.org/TR/2021/CRD-secure-contexts-20210918/)

Permitted W3C recommendation URLs MUST anchor to a specification in the technical reports namespace with a date, and so MUST match this regular expression:

```regex
^https://www\.w3\.org/TR/[0-9][0-9][0-9][0-9]/.*$
```

### Web Hypertext Application Technology Working Group (WHATWG)

Links to WHATWG specifications may be included using normal markdown syntax, such as:

```markdown
[HTML](https://html.spec.whatwg.org/commit-snapshots/578def68a9735a1e36610a6789245ddfc13d24e0/)
```

Which renders as:

[HTML](https://html.spec.whatwg.org/commit-snapshots/578def68a9735a1e36610a6789245ddfc13d24e0/)

Permitted WHATWG specification URLs must anchor to a specification defined in the `spec` subdomain (idea specifications are not allowed) and to a commit snapshot, and so must match this regular expression:

```regex
^https:\/\/[a-z]*\.spec\.whatwg\.org/commit-snapshots/[0-9a-f]{40}/$
```

Although not recommended by WHATWG, ENSIPs must anchor to a particular commit so that future readers can refer to the exact version of the living standard that existed at the time the ENSIP was finalized. This gives readers sufficient information to maintain compatibility, if they so choose, with the version referenced by the ENSIP and the current living standard.

### Internet Engineering Task Force (IETF)

Links to an IETF Request For Comment (RFC) specification may be included using normal markdown syntax, such as:

```markdown
[RFC 8446](https://www.rfc-editor.org/rfc/rfc8446)
```

Which renders as:

[RFC 8446](https://www.rfc-editor.org/rfc/rfc8446)

Permitted IETF specification URLs MUST anchor to a specification with an assigned RFC number (meaning cannot reference internet drafts), and so MUST match this regular expression:

```regex
^https:\/\/www.rfc-editor.org\/rfc\/.*$
```

### Bitcoin Improvement Proposal

Links to Bitcoin Improvement Proposals may be included using normal markdown syntax, such as:

```markdown
[BIP 38](https://github.com/bitcoin/bips/blob/3db736243cd01389a4dfd98738204df1856dc5b9/bip-0038.mediawiki)
```

Which renders to:

[BIP 38](https://github.com/bitcoin/bips/blob/3db736243cd01389a4dfd98738204df1856dc5b9/bip-0038.mediawiki)

Permitted Bitcoin Improvement Proposal URLs must anchor to a specific commit, and so must match this regular expression:

```regex
^(https://github.com/bitcoin/bips/blob/[0-9a-f]{40}/bip-[0-9]+\.mediawiki)$
```

### National Vulnerability Database (NVD)

Links to the Common Vulnerabilities and Exposures (CVE) system as published by the National Institute of Standards and Technology (NIST) may be included, provided they are qualified by the date of the most recent change, using the following syntax:

```markdown
[CVE-2023-29638 (2023-10-17T10:14:15)](https://nvd.nist.gov/vuln/detail/CVE-2023-29638)
```

Which renders to:

[CVE-2023-29638 (2023-10-17T10:14:15)](https://nvd.nist.gov/vuln/detail/CVE-2023-29638)

### Ethereum Yellow Paper

Links to the Ethereum Yellow Paper may be included using normal markdown syntax, such as:

```markdown
[Ethereum Yellow Paper](https://github.com/ethereum/yellowpaper/blob/9c601d6a58c44928d4f2b837c0350cec9d9259ed/paper.pdf)
```

Which renders to:

[Ethereum Yellow Paper](https://github.com/ethereum/yellowpaper/blob/9c601d6a58c44928d4f2b837c0350cec9d9259ed/paper.pdf)

Permitted Yellow Paper URLs must anchor to a specific commit, and so must match this regular expression:

```regex
^(https://github\.com/ethereum/yellowpaper/blob/[0-9a-f]{40}/paper\.pdf)$
```

### Execution Client Specification Tests

Links to the Ethereum Execution Client Specification Tests may be included using normal markdown syntax, such as:

```markdown
[Ethereum Execution Client Specification Tests](https://github.com/ethereum/execution-spec-tests/blob/d5a3188f122912e137aa2e21ed2a1403e806e424/README.md)
```

Which renders to:

[Ethereum Execution Client Specification Tests](https://github.com/ethereum/execution-spec-tests/blob/d5a3188f122912e137aa2e21ed2a1403e806e424/README.md)

Permitted Execution Client Specification Tests URLs must anchor to a specific commit, and so must match this regular expression:

```regex
^(https://github.com/ethereum/execution-spec-tests/(blob|commit)/[0-9a-f]{40}/.*|https://github.com/ethereum/execution-spec-tests/tree/[0-9a-f]{40}/.*)$
```

### Digital Object Identifier System

Links qualified with a Digital Object Identifier (DOI) may be included using the following syntax:

````markdown
This is a sentence with a footnote.[^1]

[^1]:
    ```csl-json
    {
      "type": "article",
      "id": 1,
      "author": [
        {
          "family": "Jameson",
          "given": "Hudson"
        }
      ],
      "DOI": "00.0000/a00000-000-0000-y",
      "title": "An Interesting Article",
      "original-date": {
        "date-parts": [
          [2022, 12, 31]
        ]
      },
      "URL": "https://sly-hub.invalid/00.0000/a00000-000-0000-y",
      "custom": {
        "additional-urls": [
          "https://example.com/an-interesting-article.pdf"
        ]
      }
    }
    ```
````

Which renders to:

<!-- markdownlint-capture -->
<!-- markdownlint-disable code-block-style -->

This is a sentence with a footnote.[^1]

[^1]:
    ```csl-json
    {
      "type": "article",
      "id": 1,
      "author": [
        {
          "family": "Jameson",
          "given": "Hudson"
        }
      ],
      "DOI": "00.0000/a00000-000-0000-y",
      "title": "An Interesting Article",
      "original-date": {
        "date-parts": [
          [2022, 12, 31]
        ]
      },
      "URL": "https://sly-hub.invalid/00.0000/a00000-000-0000-y",
      "custom": {
        "additional-urls": [
          "https://example.com/an-interesting-article.pdf"
        ]
      }
    }
    ```

<!-- markdownlint-restore -->

See the [Citation Style Language Schema](https://resource.citationstyles.org/schema/v1.0/input/json/csl-data.json) for the supported fields. In addition to passing validation against that schema, references must include a DOI and at least one URL.

The top-level URL field must resolve to a copy of the referenced document which can be viewed at zero cost. Values under `additional-urls` must also resolve to a copy of the referenced document, but may charge a fee.

## Linking to other ENSIPs

References to other ENSIPs should follow the format `ENSIP-N` where `N` is the ENSIP number you are referring to. Each ENSIP that is referenced in an ENSIP **MUST** be accompanied by a relative markdown link the first time it is referenced, and **MAY** be accompanied by a link on subsequent references. The link **MUST** always be done via relative paths so that the links work in this GitHub repository, forks of this repository, the main ENSIPs site, mirrors of the main ENSIP site, etc. For example, you would link to this ENSIP as `./ensip-0.md`.

## Linking to EIPs (Ethereum Improvement Proposals)

References to EIPs should follow the format `ENSIP-N` where `N` is the EIP number you are referring to. Each EIP that is referenced in an ENSIP **MUST** be accompanied by a markdown link the first time it is referenced, and **MAY** be accompanied by a link on subsequent references.

```markdown
[EIP-1](https://github.com/ethereum/EIPs/blob/1127009641b872ed180a33d618d1a5f8efbe0583/EIPS/eip-1.md)
```

Which renders to:

[EIP-1](https://github.com/ethereum/EIPs/blob/1127009641b872ed180a33d618d1a5f8efbe0583/EIPS/eip-1.md)

Permitted Ethereum Improvement Proposal URLs must anchor to a specific commit, and so must match this regular expression:

```regex
https://github.com/ethereum/EIPs/blob/1127009641b872ed180a33d618d1a5f8efbe0583/EIPS/eip-1.md
^(https://github.com/ethereum/EIPS/blob/[0-9a-f]{40}/eip-[0-9]+\.md)$
```

## Auxiliary Files

Images, diagrams, and auxiliary files should be included in a subdirectory of the `assets` folder for that ENSIP as follows: `assets/ENSIP-N` (where **N** is to be replaced with the ENSIP number). When linking to an image in the ENSIP, use relative links such as `../assets/ensip-1/image.png`.

## Transferring ENSIP Ownership

It occasionally becomes necessary to transfer ownership of ENSIPs to a new champion. In general, we'd like to retain the original author as a co-author of the transferred ENSIP, but that's really up to the original author. A good reason to transfer ownership is because the original author no longer has the time or interest in updating it or following through with the ENSIP process, or has fallen off the face of the 'net (i.e., is unreachable or isn't responding to email). A bad reason to transfer ownership is because you don't agree with the direction of the ENSIP. We try to build consensus around an ENSIP, but if that's not possible, you can always submit a competing ENSIP.

If you are interested in assuming ownership of an ENSIP, send a message asking to take over, addressed to both the original author and the ENSIP editor. If the original author doesn't respond to the email in a timely manner, the ENSIP editor will make a unilateral decision (it's not like such decisions can't be reversed :)).

## ENSIP Editors

The current ENSIP editors are

- Nick Johnson (@Arachnid)
- Prem Makeig (@nxt3d)
- Steve Katzman (@stevieraykatz)

If you would like to become an ENSIP editors, please contact a current editor.

Generally, ENSIP editors will be responsible for choosing new ENSIP editors.

## ENSIP Editor Responsibilities

For each new ENSIP that comes in, an editor does the following:

- Read the ENSIP to check if it is ready: sound and complete.
- The title should accurately describe the content.
- Check the ENSIP for language (spelling, grammar, sentence structure, etc.), markup (GitHub-flavored Markdown), code style

If the ENSIP isn't ready, the editor will send it back to the author for revision with specific instructions. For EIPs, generally, a new EIP will not be sent back to the author solely based on merit. However, for ENSIPs, editors can refuse to merge an ENSIP to protect against low-effort or AI-created applications, ensuring the quality and integrity of proposals.

Once the ENSIP is ready for the repository, the ENSIP editor will:

- Assign an ENSIP number (generally incremental; editors can reassign if number sniping is suspected).
- Merge the corresponding [pull request](link?)
- Send a message back to the ENSIP author with the next step.

Many ENSIPs are written and maintained by developers with write access to the ENS Labs codebase. The ENSIP editors monitor ENSIP changes, and correct any structure, grammar, spelling, or markup mistakes we see.

The editors don't pass judgment on ENSIPs. We merely do the administrative & editorial part.

Unlike EIPs, however, currently ENS Labs has oversight authority over ENSIPs, and even if an ENSIP meets all the guidelines, it is not guaranteed that the ENSIP will be made final.

## Style Guide

### Titles

The `title` field in the preamble:

- Should not include the word "standard" or any variation thereof; and
- Should not include the ENSIP's number.

### Descriptions

The `description` field in the preamble:

- Should not include the word "standard" or any variation thereof; and
- Should not include the ENSIP's number.

### ENSIP numbers

When referring to an ENSIP with a `category` of `ENSRC`, it must be written in the hyphenated form `ENSRC-X`, where `X` is that ENSIP's assigned number. When referring to ENSIPs with any other `category`, it must be written in the hyphenated form `ENSIP-X`, where `X` is that ENSIP's assigned number.

### RFC 2119 and RFC 8174

ENSIPs are encouraged to follow [RFC 2119](https://www.ietf.org/rfc/rfc2119.html) and [RFC 8174](https://www.ietf.org/rfc/rfc8174.html) for terminology and to insert the following at the beginning of the Specification section:

> The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119 and RFC 8174.

## History

This document was derived heavily from [EIP-1](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1.md), authored by Martin Becze <mb@ethereum.org> and Hudson Jameson <hudson@ethereum.org>. They are not responsible for its use in the Ethereum Name Service Improvement Process, and should not be bothered with technical questions specific to ENS or the ENSIP. Please direct all comments to the ENSIP editors.

## Copyright

Copyright and related rights waived via [CC0](../LICENSE.md).
