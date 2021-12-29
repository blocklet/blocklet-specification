
# Blocklet Bundle Format

Blocklet bundles can be published to a blocklet registry, or deployed directly to a running Blocklet Server instance.

A blocklet bundle is a tarball consists of following files:

- `blocklet.yml`: the blocklet meta file
- `logo.jpg|png|svg`: should be exactly the same file of `logo` field from blocklet meta
- `blocklet.js`: if the blocklet is bundled in `webpack` mode, this file is the webpack output file
- `blocklet.zip`: if the blocklet is bundled in `zip` mode, this file must exist, the the `main` field of blocklet meta should point to this file
- `blocklet.md`: blocklet documentation, on how to use the blocklet
- `screenshots`: blocklet screenshots, all live in one folder

## Meta

| Metadata |                  |
| -------- | ---------------: |
| Version  |            0.0.1 |
| Status   | Work in progress |
| Created  |       2020-11-03 |
