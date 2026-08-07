# Project Wisdom Android 17 manifest

Private local manifest for the Samsung Galaxy Tab A 8.0 with S Pen LTE
(`SM-P205`, codename `wisdom`) Android 17 bring-up.

The `android-17` branch uses the LineageOS 24.0 platform and a flattened
Project Wisdom layout:

- `device/samsung/wisdom`
- `vendor/samsung/wisdom`
- `kernel/samsung/wisdom`

There are no separate universal7904 common device or vendor projects. Hardware
identifiers required by the Exynos 7904 platform remain unchanged inside the
source.

## Initialize a workspace

Authenticate Git for the private Project-Wisdom repositories first:

```bash
gh auth setup-git
```

Then initialize and sync:

```bash
mkdir lineageos24-wisdom
cd lineageos24-wisdom

repo init -u https://github.com/LineageOS/android.git -b lineage-24.0 --git-lfs
git clone -b android-17 \
  https://github.com/Project-Wisdom/android_manifest_samsung_wisdom.git \
  .repo/local_manifests

repo sync -c -j"$(nproc --all)" --force-sync --no-clone-bundle --no-tags
```

## Bring-up status

This branch is the Android 17 starting baseline, not a build or boot claim. It
preserves the latest device, vendor, kernel, IMS, and patch history from the
LineageOS 23.2 work and points external Samsung/SLSI dependencies at
`lineage-24.0`.

Before a release build, rebase and validate the platform patch queue, migrate
the legacy blob extraction scripts to the current extract-utils interface, and
complete compile, flash, boot, radio, camera, media, encryption, and SELinux
regression testing.
