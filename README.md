# palmon-assets

Versioned game-asset database for *Palmon: Survival*, published by
[`palmon-extractor`](https://github.com/deadcodes/palmon-extractor)'s
`scripts/game/publish_asset_repo.py`.

**This repository is generated. Do not hand-edit it.** Every file here -- assets and
the `index/` database alike -- is written by that publish step; fix the source
recovery or the publisher instead of editing a checkout of this repo directly.

## Versioning

One commit and one tag per published game version, tagged `rvNNN` (the game's CDN
`ResourceVersion`). A published tag is immutable and is never rewritten -- assets live
at their original recovery paths, so an unchanged file across two versions costs
nothing in the git history.

## Fetching a version's assets

Any path at any published version is served directly off jsDelivr's GitHub CDN, no
server required:

    https://cdn.jsdelivr.net/gh/deadcodes/palmon-assets@<tag>/<path>

for example:

    https://cdn.jsdelivr.net/gh/deadcodes/palmon-assets@rv432/uiv3/texture/bg/goldrobberbg.png

## The `index/` directory

`index/` describes the database itself, not game content:

- `index/versions.json` -- every published version, in order.
- `index/assets/<00-0f>.json` -- 16 content-sharded files covering every known asset
  record and its full history (added/modified/removed/renamed, per version).
- `index/summary.json` -- a derived, human-readable report (totals, categories,
  shard sizes) rebuilt on every publish.
- `index/lookup.json` -- (when present) a game entity id -> art lookup.

`index/versions.json` is the one file consumers should treat as a mutable pointer --
its jsDelivr cache is purged after every push.
