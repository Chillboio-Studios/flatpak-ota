# Chillboi Studios Flatpak OTA

This repository hosts the shared Flatpak remote, app metadata, and downloadable
Flatpak bundles used for install and updates.

## Domain

This repository is intended to be served at:

- https://flatpak-ota.chillboiostudios.com

## Structure

- `repo/`: Aggregated OSTree repository for all apps (single remote users add once)
- `chillboio.flatpakrepo`: Root remote definition that points to `repo/`
- `apps/<app-id>/repo/`: Per-app staging repo content merged into root `repo/`
- `apps/<app-id>/*.flatpakref`: App-specific install refs
- `apps/<app-id>/bundles/*.flatpak`: Downloadable Flatpak bundles per architecture
- `apps/index.txt`: Published app index
- `CNAME`: GitHub Pages custom domain mapping

## DawnChat

DawnChat app id:

- `com.chillboiostudios.dawnchat`

Suggested DawnChat paths in this repo:

- `apps/dawnchat/repo/`
- `apps/dawnchat/bundles/`

## Publishing

Your CI should:

1. Build Flatpak artifacts and OSTree repo content.
2. Sync per-app OSTree data into `apps/<app>/repo/`.
3. Sync generated bundles into `apps/<app>/bundles/`.
4. Merge all app repos into root `repo/` and run `flatpak build-update-repo --generate-static-deltas --prune`.
5. Regenerate app `.flatpakref` files to point at this domain.
6. Ensure `chillboio.flatpakrepo` points to `https://<domain>/repo/`.
7. Push to the branch used by Pages.
