# apt-openehr-explorer

Self-hosted apt repository for [openEHR Explorer](https://github.com/platzhersh/openehr-explorer).

This repository is updated automatically by openEHR Explorer's release CI — see
[`.github/workflows/apt-repo.yml`](https://github.com/platzhersh/openehr-explorer/blob/main/.github/workflows/apt-repo.yml)
in the main repo. You shouldn't need to touch anything here by hand; the files
are served straight off the `main` branch via `raw.githubusercontent.com`
(no GitHub Pages setup required).

## Installing openEHR Explorer via apt

```bash
# 1. Add the signing key
curl -fsSL https://raw.githubusercontent.com/platzhersh/apt-openehr-explorer/main/openehr-explorer.gpg \
  | sudo gpg --dearmor -o /usr/share/keyrings/openehr-explorer.gpg

# 2. Add the repository
echo "deb [signed-by=/usr/share/keyrings/openehr-explorer.gpg] \
https://raw.githubusercontent.com/platzhersh/apt-openehr-explorer/main stable main" \
  | sudo tee /etc/apt/sources.list.d/openehr-explorer.list

# 3. Install
sudo apt update
sudo apt install open-ehr-explorer
```

Once installed, future releases arrive via the normal `sudo apt upgrade` flow.

## Repository layout

```
openehr-explorer.gpg              # public signing key (ASCII-armored)
pool/main/o/open-ehr-explorer/    # .deb packages
dists/stable/
  Release                         # signed metadata
  Release.gpg
  InRelease
  main/binary-amd64/
    Packages
    Packages.gz
```

Standard Debian archive layout, generated with `apt-ftparchive`.

## Signing key

Packages are signed with a GPG key dedicated to this repository (not the
Tauri updater key used for auto-update signatures). The public key is
published as `openehr-explorer.gpg` in this repo's root.

## Supported architecture

`amd64` only, matching the `.deb` currently produced by the main repo's
Tauri build. `arm64` may be added later if/when the main build pipeline
produces an arm64 `.deb`.
