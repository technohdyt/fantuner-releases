# fantuner-releases

Public release channel for **FanTuner** — a Mac fan control app.

This repository holds no source code. It exists so that:

- every FanTuner release is published as a **GitHub Release** in this repo
  with the signed `FanTuner-X.Y.dmg` attached, and
- `appcast.xml` on the `main` branch is the **Sparkle update feed** the app
  polls at
  `https://raw.githubusercontent.com/matthewjgl/fantuner-releases/main/appcast.xml`.

## How a release works

1. The maintainer publishes a GitHub Release here with the DMG attached.
2. The workflow in `.github/workflows/appcast.yml` downloads the DMG,
   recomputes the Sparkle EdDSA signature, and commits a regenerated
   `appcast.xml`.
3. Installed apps notice the new item, download the DMG from the release
   assets, verify the signature and code signature, install, and relaunch.

## Setup (one time)

The appcast workflow needs the Sparkle EdDSA private key as a repository
secret:

```sh
gh secret set SPARKLE_ED25519_KEY --repo matthewjgl/fantuner-releases < ~/.config/fantuner/ed25519-private.key
```

The key must never be committed anywhere. The matching public key is embedded
in the app (`SUPublicEDKey`).

## Downloads

Get the latest FanTuner from the [Releases page](../../releases) or
[fantuner.com](https://fantuner.com).
