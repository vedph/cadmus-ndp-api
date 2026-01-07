## Change Log

- 2026-01-07:
  - added thesaurus for comment keyword languages.
  - fixed thesaurus of Commedia contexts.
  - added 3 new note parts to iconography item to preserve legacy data from IDP `immagini`, with roles `isd` (=subject details, corresponding to IDP rapporti con la tradizione dantesca), `ift` (=figurative theme, corresponding to IDP rapporti extradanteschi), and `msc` (=miscellaneous, corresponding to IDP note).

### 2.0.4

- 2025-12-29: updated packages.
- 2025-12-28: thesauri.
- 2025-12-19:
  - updated thesauri.
  - added 2 note parts to iconography item with roles `exe` and `ptx`.
  - replaced the categories part with role `ico` in iconography with 2 categories with roles `ict` and `ics`.
- 2025-12-17:
  - added thesaurus `it.vedph.flags_dri`.
  - changes to some entries of existing thesauri.
  - moved the `flags` part from drawings projects to drawing items. Items require this detail, while for projects they can be collected from their items.

### 2.0.3

- 2025-12-12: updated decorations thesauri (`cod-decoration-element-gildings@en`, `cod-decoration-element-techniques@en`, `cod-decoration-element-tools@en`, `cod-decoration-element-types@en`, `cod-decoration-element-typologies@en`, `cod-decoration-flags@en`, `cod-decoration-type-hidden@en`).
- 2025-12-09: updated thesauri.

### 2.0.2

- 2025-12-04:
  - updated packages and refactored MOL configuration to use PostgreSQL instead of LiteDB.
  - added `- CONNECTIONSTRINGS__MOL=Server=cadmus-ndp-pgsql;port=5432;Database=mol;User Id=postgres;Password=postgres;Include Error Detail=True` to Docker compose script.

### 2.0.1

- 2025-11-28: updated packages.
- 2025-11-27: added MOL lookup support.
- 2025-11-26: changed/added thesauri:
  - `categories_bio`
  - `categories_ctx`
  - `cod-shelfmark-libraries`
  - `physical-state-features`

### 2.0.0

- 2025-11-26: Docker.
- 2025-11-24:
  - ⚠️ upgraded to NET 10.
  - enabled graph in settings.

### 1.0.8

- 2025-11-22:
  - updated packages, still on .NET 9 until NpgSql components for .NET 10 are ready.
  - added options to codicology seeder profiles.

### 1.0.7

- 2025-11-10: updated thesauri.
- 2025-11-09:
  - updated packages.
  - added settings for shelfmarks part.
  - added to thesauri a list of libraries from a sample Excel document where A=cityand B=library, adapting it as follows:
  - save as CSV.
  - apply this replacement: find `^([^;]+);([^\n\r]+)([\n\r])` and replace with `$2 ($1)$3` (=move city after library name in parentheses).
  - added a new thesaurus entry `cod-shelfmark-libraries@en` and used this prompt to convert the result into thesauri entries: `Convert the following list of strings into JSON entries for the newly added cod-shelfmark-libraries@en object. Each line must become an entry in entries, having value=string, and id=identifier built from value by lowercasing it, removing the final city in (), removing all non-letter characters, trim, replace inner spaces with dashes, and remove diacritics from letters. If this ID happens to be equal to any of the others, append to it the city name after a dash. Here is the list: ...`.
- 2025-10-31: updated packages and thesauri.
- 2025-10-28:
  - updated packages.
  - added NDP-specific parts.

### 1.0.6

- 2025-10-14:
  - removed `categories:edits` from iconography in profile.
  - updated packages.
- 2025-10-08: updated packages.
- 2025-10-06: updated packages.

### 1.0.5

- 2025-10-03: updated packages and generated Docker image.
- 2025-09-27: added iconography parts.
- 2025-09-26:
  - replaced bibliography with references (will be used via Zotero).
  - added preservation state to manuscripts.

### 1.0.4

- 2025-09-24:
  - refactored profile.
  - added drawing packages.

### 1.0.3

- 2025-09-19:
  - updated packages.
  - added drawings, iconographies, persons to profile except for those parts which are still missing.
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
