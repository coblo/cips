# Content Blockchain Improvement Proposals

CIPs are governed by the [2/COSS](https://rfc.unprotocols.org/spec:2/COSS/) 
(COSS). Current versions are published at https://coblo.github.io/cips/.

| ID                         | Title                  | Type   | Status |
| ------------------------------ | ---------------------- | ------ | ------ |
| [CIP-0001](cips/cip-0001-alias.md)        | Wallet Address Aliases | Stream | ![Stable](http://rfc.unprotocols.org/spec:2/COSS/stable.svg) |
| [CIP-0002](cips/cip-0002-timestamp.md)    | Content Timestamping   | Stream | ![Stable](http://rfc.unprotocols.org/spec:2/COSS/stable.svg) |
| [CIP-0003](cips/cip-0003-iscc.md)         | ISCC Registration      | Stream | ![Draft](http://rfc.unprotocols.org/spec:2/COSS/draft.svg)   |
| [CIP-0004](cips/cip-0004-smartlicense.md) | Smart Licenses         | Stream | ![Raw](http://rfc.unprotocols.org/spec:2/COSS/raw.svg)       |

## Working on CIPs

All **CIPs** are written in [markdown](https://en.wikipedia.org/wiki/Markdown).
The markdown content is than  built and published with the 
[mkdocs](http://www.mkdocs.org/) documetation tool. If you have some basic 
command line skills you can build and run the 
[cips website](https://coblo.github.io/cips/) on your own computer. Make sure 
you have the [Git](https://git-scm.com/) and [Python](https://www.python.org/) 
installed on your system and  follow these steps on the command line:

```bash
git clone https://github.com/coblo/cips.git
cd cips
pip install -r requirements.txt
mkdocs serve
```

## Usage

All CIP documents can be found in the `cips` subfolder of this repository. The 
recommended editor for the markdown files is [typora](https://typora.io/). If 
you have commit rights to the [main repository](https://github.com/coblo/cips) 
you can deploy the site with a simple `mkdocs gh-deploy`.
