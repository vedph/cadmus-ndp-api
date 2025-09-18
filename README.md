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

- **drawings project**
  - _identity_
    - metadata
    - links (also for authors)
    - shelfmarks (COD)
  - _history_
    - chronotopes
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
  - _history_
    - chronotopes
    - historical events:dri
    - note:hist (history)
  - _material_
    - watermarks (COD)
    - preservation states
  - _content_
    - edits (COD)
    - iconography instructions (ICO)

> ??I would remove [drawing texts part](https://github.com/vedph/cadmus-ndp-drawings?tab=readme-ov-file#drawingtextspart) as it is superseded by COD edits.

- **iconography**
  - _identity_
    - metadata
  - _relations_
    - links
    - references:cit (textual citations related to this iconography)
    - categories:ico (iconographic subjects tree)
    - categories:ctx (luoghi danteschi)
  - _content_
    - features:ico (storie prime/seconde etc.)
    - comment (description)
  - _editorial_
    - note
  - _references_
    - bibliography

❓ Questions:

- should we add preservation states to manuscripts??
- in the original iconography part, we included a list of transcribed texts. I wonder whether this is redundant given the list of citations.
- which entities in the above list besides drawing items should get the [iconography instructions part](https://github.com/vedph/cadmus-iconography/blob/master/docs/ico-instructions.md)?

### Facets Synoptic Table

In this feature-matrix like table you find one column per entity. The cell at the intersection between each column and row contains `X` when the part is present, and/or one ore more role identifiers when that part is used with a specific role (indicated with a suffix after colon in the previous list).

This table clearly shows the modular modeling architecture of Cadmus: 32 parts (=reusable self-contained models with higher abstraction levels) are used more than 100 times, across 7 different items, covering very different knowledge domains and corresponding to material and immaterial entities. This modular architecture is mirrored in the editor UI, as each part has its own editor, which greatly speeds up development and training for end users (once you learn how to enter data in a part, you will find it again and again in the editor for other entities).

| part                                 | manuscript | fragment | print ed.      | print inst. | drawing prj. | drawing itm. | iconography |
| ------------------------------------ | ---------- | -------- | -------------- | ----------- | ------------ | ------------ | ----------- |
| bibliography                         | X          | X        | X              | X           | X            | X            | X           |
| bindings (COD)                       | X          |          |                | X           | X            |              |             |
| categories                           | txt        | txt      | txt            | txt edits   |              |              | ico ctx     |
| chronotopes                          | X          | X        | prn pub        |             | X            | X            |             |
| comment                              |            |          |                |             | X            |              | X           |
| contents (COD)                       | X          | X        |                |             |              |              |             |
| decorated counts                     |            | X        |                |             |              |              |             |
| decorations (COD)                    | X          | X        | X              | X           |              |              |             |
| drawing set (DRW)                    |            |          |                |             | X            |              |             |
| edits (COD)                          | X          | X        |                | X           |              | X            |             |
| features                             |            |          |                |             |              |              | ico         |
| figurative plan (BOK)                |            |          | X              |             |              |              |             |
| figurative plan implementation (BOK) |            |          |                | X           |              |              |             |
| fonts (BOK)                          |            |          | X              |             |              |              |             |
| hands (COD)                          | X          | X        |                | X           |              |              |             |
| historical events                    | ms         | fr       |                | pri         | drp          | dri          |             |
| iconography instructions (ICO)       |            |          |                |             |              | X            |             |
| labels (FRA)                         |            | X sig    |                |             |              |              |             |
| layouts (COD)                        | X          |          | X              | X           |              |              |             |
| layout (FRA)                         |            | X        |                |             |              |              |             |
| links                                | X          | X        | X              | X           | X            | X            | X           |
| material description (COD)           | X          |          |                |             |              |              |             |
| measurements                         |            | X        |                | X           |              |              |             |
| metadata                             | X          | X        | X              | X           | X            | X            | X           |
| note                                 | X hist     | X hist   | X hist inc col | X hist      | X hist       | X hist       | X dsc       |
| preservation states                  |            | X        |                | X           | X            | X            |             |
| references                           |            |          |                |             |              |              | cit         |
| rulings (FRA)                        |            | X        |                |             |              |              |             |
| shelfmarks (COD)                     | X          | X        |                | X           | X            | X            |             |
| sheet labels (COD)                   | X          |          |                | X           |              |              |             |
| support (FRA)                        |            | X        |                |             |              |              |             |
| watermarks (COD)                     | X          |          | X              |             |              | X            |             |

💡 Notes:

- `categories:txt` can be used to include the generic text classification which cross-references all the text-carrier entities.
- `categories:edits` in print instances is a special classification for "postille". Can we include it in `categories:txt`?
- `note:hist` is the narrative history of the entity. Usually its most relevant events are extracted and formalized into historical events.
- `note` is a generic note, mostly used for editorial purposes.

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
