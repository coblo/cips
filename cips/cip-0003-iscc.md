# ISCC Registration

| CIP:     | 0003                                                       |
| -------- | ---------------------------------------------------------- |
| Title:   | ISCC Registration                                   |
| Authos:  | TP                                                         |
| Status:  | ![Draft](http://rfc.unprotocols.org/spec:2/COSS/draft.svg) |
| Created: | 2018-01-13                                                |
| License: | BSD-2-Clause                                               |

## Purpose

An open an public registry for [ISCC](http://iscc.codes/) content identifiers. 
This documents specifies an open stream named `iscc` that can be used to 
register ISCC content codes and optionally associated metadata.

## Schema

The ISCC-stream is named `iscc` and is readable and writable by every 
blockchain participant. The stream uses multiple keys for each stream-item 
where each key represents one of the 4 ISCC components:
`Meta-ID`, `Content-ID`, `Data-ID`, `Instance-ID`.

The stream-item value must be a JSON object that supports a set of defined 
top-level fields which are specified below. Applications **may** add custom 
fields at the top level but **must** prefix those fields with an underscore to 
avoid collisions with future extensions of the 
[ISCC Metadata specification](http://iscc.codes/specification/#iscc-metadata). 

### Top-Level Fields

#### version (optional)

Version of ISCC registry schema. Assumed to be 1.0 if omitted.

#### title (required)

Title of an intangible creation.

The UTF-8 encoded value of the `title`-field must not exceed 128 bytes. For a 
valid **ISCC** entry the value of this field together with the optional 
`extra`-field must encode to the MetaID that was given as the first key of the 
stream-item.

#### extra (optional)

A short statement that distinguishes this intangible creation from another one. 

The UTF-8 encoded value of the `extra`-field must not exceed 128 bytes.

#### hash (optional)

The full 64 character hex-encoded top-hash (merkle root) retuned by the 
instance_id function.

#### meta (optional)

A list of one or more metadata entries. Must include at least one entry if 
specified. 

A metadata entry allows for a flexible and extendable way to supply additional 
industry specific metadata about the identified content. It is a JSON object 
with the fields `schema`, `mediatype`, `data`, `url`. The `schema`-field may 
indicate a well known metadata schema (such as Dublin Core, IPTC, ID3v2, ONIX) 
that is used. The `mediatype`-field specifies an 
[IANA Media Type](https://www.iana.org/assignments/media-types/media-types.xhtml). 
The `data`-field is only required if the`url` field is omitted. It holds the 
metadata conforming to the indicated `schema` and `mediatype.` The `url`-field 
is only required if the `data`-field is omitted. The `url` is an external link 
that is expected to host the metadata with the indicated `schema` and 
`mediatype`.  

## Examples

Minimal **ISCC** registry entry value:

```json
{
  "title": "The Neverending Story"
}
```

With extra field:

```json
{
  "title": "The Neverending Story",
  "extra": "1984 fantasy film based on novel"
}
```

With **ISCC** data integrity hash:

```json
{
  "title": "The Neverending Story",
  "hash": "40aeb0ef856a8dbfa4e9897de98b1a1eef7e24f8744e65cd33118b40d9741147"
}
```
With linked Metadata:

```json
{
  "title": "Ubu: A face-to-face connector app for Hubud members",
  "meta": 
  [
    {
      "schema": "xmp",
      "mediatype": "application/rdf+xml",
      "url": "http://camwebb.info/blog/2014-11-19/ubu.xmp"
    }
  ]
}
```

With custom inline Metadata:

```json
{
  "title": "The Neverending Story",
  "meta": 
  [{
    "schema": "schema.org",
    "mediatype": "application/ld+json",
    "data": 
      {
        "@context": "http://schema.org",
        "@type": "Movie",
        "name": "The Neverending Story",
        "dateCreated": "6 April, 1984",
        "director": "Wolfgang Petersen",
        "actors": ["Noah Hathaway", "Barret Oliver", "Tami Stronach"],
        "duration": "1:42:00"
      }
  }]
}
```

With application specific custom field:

```json
{
  "title": "The Neverending Story",
  "_productionCompany": "Bavaria Studios"
}
```
