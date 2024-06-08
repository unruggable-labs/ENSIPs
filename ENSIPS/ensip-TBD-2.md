---
ensip: TBD
title: DataURI and URL Contenthash
status: Idea
type: ENSRC
author: Prem Makeig (premm.eth) <premm@unruggable.com>, raffy.eth <raffy@unruggable.com>
created: 2024-6-7
---

* Objective: put web content directly into ENS contenthash.  When combined with offchain servers, provides alternative hosting solution.  When combined with EVMGateway, provides a decentralized solution using affordable? L2 storage.

* Two new formats
	1. URL
		* Format: `uvarint(codec1) + <URL as utf8 bytes>`
	1. DataURI
		* Format: `uvarint(codec2) + byte(length(MIME)) + <MIME bytes as ascii> + <DATA as bytes>`
		* `mime` cannot exceed 255 bytes (or could be another uvarint)

* Multicodec: need to figure out `codec1` and `codec2` values
	* [I think with a large enough value we can just pick one?](https://github.com/multiformats/multicodec/tree/master?tab=readme-ov-file#adding-new-multicodecs-to-the-table)

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
