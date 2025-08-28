# Cadmus NDP API

🐋 Quick Docker image build:

  docker buildx build . --platform linux/amd64,linux/arm64,windows/amd64 -t vedph2020/cadmus-ndp-api:1.0.1 -t vedph2020/cadmus-ndp-api:latest --push

(replace with the current version).

This is a Cadmus API layer customized for Cadmus NDP (Naples Dante Project). Most of its code is derived from [shared Cadmus libraries](https://github.com/vedph/cadmus-api).

- [Cadmus NDP Frac](https://github.com/vedph/cadmus-ndp-frac)
- [Cadmus NDP Books](https://github.com/vedph/cadmus-ndp-books)
- [Cadmus NDP Drawings](https://github.com/vedph/cadmus-ndp-drawings)

## History

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
