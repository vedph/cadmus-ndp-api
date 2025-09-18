# Cadmus NDP API

- [Cadmus NDP API](#cadmus-ndp-api)
  - [Facets](#facets)
    - [Facets Synoptic Table](#facets-synoptic-table)
  - [History](#history)
    - [1.0.1](#101)

🐋 Quick Docker image build:

```sh
docker buildx build . --platform linux/amd64,linux/arm64,windows/amd64 -t vedph2020/cadmus-ndp-api:1.0.1 -t vedph2020/cadmus-ndp-api:latest --push
```

(replace with the current version).

This is a Cadmus API layer customized for Cadmus NDP (Naples Dante Project). Most of its code is derived from [shared Cadmus libraries](https://github.com/vedph/cadmus-api).

- [Cadmus NDP Frac](https://github.com/vedph/cadmus-ndp-frac)
- [Cadmus NDP Books](https://github.com/vedph/cadmus-ndp-books)
- [Cadmus NDP Drawings](https://github.com/vedph/cadmus-ndp-drawings)

## Facets

The list of facets is given here with their conventional groupings used in the editor UI. The 3-letters abbreviation after each part type name refers to Cadmus model spaces different from the generic one. Here we have `COD`=codicology, `FRA`=fragments, `BOK`=books, `DRW`=drawings, `ICO`=iconography.

- **manuscript**
  - _identity_
    - metadata
    - shelfmarks (COD)
    - links
    - categories:txt
  - _history_
    - chronotopes
    - historical events:ms
    - note:hist (history)
  - _material_
    - bindings (COD)
    - sheet labels (COD)
    - material description (COD)
    - watermarks (COD)
  - _content_
    - contents (COD)
    - layouts (COD)
    - decorations (COD)
    - hands (COD)
    - edits (COD)
  - _editorial_
    - note
  - _references_
    - bibliography
- **fragment**
  - _identity_
    - metadata
    - shelfmarks (COD)
    - links
    - categories:txt
  - _history_
    - chronotopes
    - historical events:fr
    - note:hist (history)
  - _material_
    - support (FRA)
    - rulings (FRA)
    - labels:sig (FRA)
    - labels (FRA)
    - decorated counts
    - measurements
    - preservation states
  - _content_
    - contents (COD)
    - layout (FRA)
    - decorations (COD)
    - hands (COD)
    - edits (COD)
  - _editorial_
    - note
  - references
    - bibliography
- **print edition**
  - _identity_
    - metadata
    - links (this can include also authors and editors)
    - categories:txt
  - _history_
    - chronotopes:prn (print date/place)
    - chronotopes:pub (publication date/place)
  - _content_
    - fonts (BOK)
    - layouts (COD)
    - watermarks (COD)
    - figurative plan (BOK)
    - note:inc (incipit)
    - note:col (colophon)
  - _editorial_
    - note
  - _references_
    - bibliography
- **print instance**
  - _identity_
    - metadata
    - links
    - shelfmarks
    - categories:txt
  - _history_
    - historical events:pri
    - note:hist (history)
  - _material_
    - bindings (COD)
    - sheet labels (COD)
    - measurements
    - preservation states
  - _content_
    - layouts (COD)
    - figurative plan implementation (BOK)
    - decorations (COD)
    - categories:edits ("postille")
    - edits (COD)
  - _editorial_
    - note
  - _references_
    - bibliography

The following entities are to be completed:

- **drawing project**
  - _identity_
    - metadata
    - links (also for authors)
    - shelfmarks (COD)
    - district location
  - _history_
    - historical events:drp
    - note:hist (history)
  - _material_
    - bindings (COD)
    - preservation states
  - _content_
    - drawing set (DRW)
    - comment
  - _editorial_
    - note
  - _references_
    - bibliography
- **drawing item**
  - _identity_
    - metadata
    - links (also for authors)
    - shelfmarks (COD)
    - district location
  - _history_
    - historical events:drw
    - note:hist (history)
  - _material_
    - watermarks (COD)
    - preservation states
  - _history_
    - historical events
    - note:hist (history)
  - _content_
    - edits (COD)
    - iconography instructions (ICO)

> ??I would remove [drawing texts part](https://github.com/vedph/cadmus-ndp-drawings?tab=readme-ov-file#drawingtextspart) as it is superseded by COD edits.

- **iconography**
  - _identity_
    - metadata
    - index keywords
  - _relations_
    - links
    - references:cit (textual citations related to this iconography)
    - categories:ico (iconographic subjects tree)
    - categories:ctx (luoghi danteschi)
  - _content_
    - features (storie prime/seconde etc.)
    - note:dsc (description)
  - _editorial_
    - note
  - _references_
    - bibliography

❓ Questions:

- in the original iconography part, we included a list of transcribed texts. I wonder whether this is redundant given the list of citations.
- which entities in the above list besides drawing items should get the [iconography instructions part](https://github.com/vedph/cadmus-iconography/blob/master/docs/ico-instructions.md)?

### Facets Synoptic Table

| group/relations | part                                 | manuscript | fragment | print ed. | print inst. | drawing prj. | drawing itm. | iconography |
| --------------- | ------------------------------------ | ---------- | -------- | --------- | ----------- | ------------ | ------------ | ----------- |
| identity        | metadata                             | X          | X        | X         | X           | X            | X            | X           |
| identity        | shelfmarks (COD)                     | X          | X        |           | X           | X            | X            |             |
| identity        | links                                | X          | X        | X         | X           | X            | X            | X           |
| identity        | categories:txt                       | X          | X        | X         | X           |              |              |             |
| identity        | district location                    |            |          |           |             | X            | X            |             |
| identity        | index keywords                       |            |          |           |             |              |              | X           |
| history         | chronotopes                          | X          | X        |           |             |              |              |             |
| history         | historical events                    | X          | X        |           | X           |              | X            |             |
| history         | historical events:ms                 | X          |          |           |             |              |              |             |
| history         | historical events:fra                |            | X        |           |             |              |              |             |
| history         | historical events:pri                |            |          |           | X           |              |              |             |
| history         | historical events:drp                |            |          |           |             | X            |              |             |
| history         | historical events:drw                |            |          |           |             |              | X            |             |
| history         | note:hist                            | X          | X        |           | X           | X            | X            |             |
| history         | chronotopes:prn                      |            |          | X         |             |              |              |             |
| history         | chronotopes:pub                      |            |          | X         |             |              |              |             |
| material        | bindings (COD)                       | X          |          |           | X           | X            |              |             |
| material        | sheet labels (COD)                   | X          |          |           | X           |              |              |             |
| material        | material description (COD)           | X          |          |           |             |              |              |             |
| material        | watermarks (COD)                     | X          |          | X         |             |              | X            |             |
| material        | support (FRA)                        |            | X        |           |             |              |              |             |
| material        | rulings (FRA)                        |            | X        |           |             |              |              |             |
| material        | labels:sig (FRA)                     |            | X        |           |             |              |              |             |
| material        | labels (FRA)                         |            | X        |           |             |              |              |             |
| material        | decorated counts                     |            | X        |           |             |              |              |             |
| material        | measurements                         |            | X        |           | X           |              |              |             |
| material        | preservation states                  |            | X        |           | X           | X            | X            |             |
| content         | contents (COD)                       | X          | X        |           |             |              |              |             |
| content         | layouts (COD)                        | X          |          | X         | X           |              |              |             |
| content         | layout (FRA)                         |            | X        |           |             |              |              |             |
| content         | decorations (COD)                    | X          | X        | X         | X           |              |              |             |
| content         | hands (COD)                          | X          | X        |           | X           |              |              |             |
| content         | edits (COD)                          | X          | X        |           | X           |              | X            |             |
| content         | fonts (BOK)                          |            |          | X         |             |              |              |             |
| content         | figurative plan (BOK)                |            |          | X         |             |              |              |             |
| content         | figurative plan implementation (BOK) |            |          |           | X           |              |              |             |
| content         | note:inc                             |            |          | X         |             |              |              |             |
| content         | note:col                             |            |          | X         |             |              |              |             |
| content         | categories:edits                     |            |          |           | X           |              |              |             |
| content         | drawing set (DRW)                    |            |          |           |             | X            |              |             |
| content         | comment                              |            |          |           |             | X            |              |             |
| content         | iconography instructions (ICO)       |            |          |           |             |              | X            |             |
| content         | features                             |            |          |           |             |              |              | X           |
| content         | note:dsc                             |            |          |           |             |              |              | X           |
| relations       | references:cit                       |            |          |           |             |              |              | X           |
| relations       | categories:ico                       |            |          |           |             |              |              | X           |
| relations       | categories:ctx                       |            |          |           |             |              |              | X           |
| editorial       | note                                 | X          | X        | X         | X           | X            | X            | X           |
| references      | bibliography                         | X          | X        | X         | X           | X            | X            | X           |

💡 Notes:

- `categories:txt` can be used to include the generic text classification which cross-references all the text-carrier entities.
- `categories:edits` in print instances is a special classification for "postille". ??I don't know whether this could be included as a subtype in `categories:txt`, or extracted from the edits part if we are going to provide their detailed list (but I suppose this is not the case).
- `note:hist` is the narrative history of the entity. Usually its most relevant events are extracted and formalized into historical events.

## History

- 2025-09-18: refactored profile.
- 2025-09-16: updated packages.
- 2025-08-28: updated packages.
- 2025-08-13:
  - added facets in profile.
  - updated packages.
  - added thesaurus `cod-fr-layout-features_prn` for fragment layout features used for printed books.
  - replaced print layout part with that from FRAC in printed book facets.
- 2025-08-12: adding books modules and profile.
- 2025-08-07: updated packages.
- 2025-07-17: updated packages.

### 1.0.1

- 2025-07-16: updated packages.
