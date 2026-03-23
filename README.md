# Chillboi Studios Flatpak OTA

This repository hosts the Flatpak OSTree remote and app metadata used for automatic updates.

## Domain

This repository is intended to be served at:

- https://flatpak-ota.chillboiostudios.com

## Structure

- `apps/<app-id>/repo/`: OSTree repository for one app (or combined if you prefer)
- `apps/<app-id>/*.flatpakref`: App-specific install refs
- `dawnchat.flatpakrepo`: Shared remote definition for DawnChat users
- `CNAME`: GitHub Pages custom domain mapping

## DawnChat

DawnChat app id:

- `com.chillboiostudios.dawnchat`

Suggested DawnChat path in this repo:

- `apps/dawnchat/repo/`

## Publishing

Your CI should:

1. Build Flatpak artifacts and OSTree repo content.
2. Sync OSTree data into `apps/<app>/repo/`.
3. Run `flatpak build-update-repo --generate-static-deltas --prune` on the destination repo path.
4. Regenerate app `.flatpakref` files to point at this domain.
5. Push to the branch used by Pages.
