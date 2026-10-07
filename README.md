# NetMount

**Mount your network storage as real folders on a rooted Android phone.**

NetMount makes a server, NAS or PC share show up as an ordinary folder such as `/sdcard/Server`, so every app
(file managers, emulators, game launchers, media players) can use it as if it were on the phone. It is built on
[rclone](https://rclone.org) and FUSE, and bundles everything it needs: no Termux, no Python, no Magisk module, and
nothing is downloaded at run time.

This repository holds the **downloads** for NetMount and the files the app reads to update itself.

## Download

| | Where | For whom |
|---|---|---|
| **Stable** | [Latest release](https://github.com/nomanshabbir-NoOneDev/NetMount-updates/releases/latest) | Everyone. Tested builds. |
| **Beta** | [Beta release](https://github.com/nomanshabbir-NoOneDev/NetMount-updates/releases/tag/beta) | People who want new features early. May have rough edges. |

Download `NetMount.apk` from the release you want and install it. After that, NetMount updates itself (see
[Updating](#updating)).

## Requirements

- A **rooted** phone: Magisk, KernelSU or APatch (NetMount asks your root manager for permission on first start).
- **arm64** device (almost every phone from the last several years) with **Android 8.0 or newer**.
- A kernel with **FUSE** support. Check it with a terminal app: `grep fuse /proc/filesystems` should print `fuse`.
- A server to connect to: WebDAV, SFTP, SMB (Windows or Samba share) or FTP/FTPS.

## Features

**Storage types**
- **WebDAV**, **SFTP** (password, key file or pasted key, host-key pinning), **SMB** (guest or login, any share and
  subfolder) and **FTP/FTPS** (marked BETA).
- Several storages at once, each with its own folder name, cache and options.

**Made for games and emulators**
- A *Games* preset that fetches only the pieces a game asks for, and a *Big copies* preset for fast file transfers.
- A cache that remembers what you read (30 days by default), so the second launch of a big game is far faster than the first.

**Monitor and tests**
- Live speed, latency and connection quality for each storage, shown on the back of its card.
- **Test connection** with plain-language errors (wrong password, wrong share, certificate problem, server unreachable).
- A **Benchmark** for sequential and random reads and writes, with a graph and a copyable report.

**Automation**
- **Mount at boot** and **remount when Wi-Fi returns**.
- **Keep mounted**: a small background service restarts a mount that has died.
- **Alert me when it drops**: a notification when a storage stops or its server cannot be reached, and another when it is back.
- **Only on these Wi-Fi networks**: unmount when you leave your home network, remount when you return.
- A Quick Settings tile and an optional boot script for ROMs that block boot receivers.

**Everyday comfort**
- Slim list with search, filters, pins and Mount all / Unmount all.
- **Backup**: export your storages to a file and import them on another phone. Passwords are never exported.
- Dark and light themes, optional Material You colors, haptics you can turn off.

## First steps

1. Install the APK and open NetMount. Allow root when your root manager asks.
2. Tap **+**, pick a storage type and enter the name, server address, user and password.
   A server with a self-signed certificate needs **Skip certificate check** (only on a network you trust).
3. Press **Save**, then **Test connection**.
4. Press **Mount** and open `/sdcard/<name>` in any file manager.

Closing the app does not unmount your storage. Use **Unmount** for that.

## Updating

Open **Settings, Updates**. The app checks when it opens (at most every 12 hours; you can turn that off) and when you
press **Check for updates**. When something newer exists, **Update** shows **what is new**, and **Update now** downloads
and installs it. Your storages and settings are kept, and mounts keep running during the update.

- **Stable** (the default for the Stable download) offers released versions only.
- **Beta** offers the newest beta build, and the stable release too whenever that is newer, so you are never left behind.
- Android does not allow installing an older version over a newer one. If you move from Beta back to Stable, you keep the
  beta build until a newer stable release arrives.

### How updates are kept safe

- Each update is checked against its **size** and **SHA-256** before it is installed.
- Android only accepts an update signed with the same key as the installed app, so a swapped file could not replace NetMount.
- The app contacts **only this repository**, and only to check and download. There is no analytics, advertising or telemetry.

To check a download by hand, compare `sha256sum NetMount.apk` with the `sha256` value in `version.json` of the same release.

## Privacy and permissions

NetMount needs the `INTERNET` permission **only** for the update check and download. Mounting runs through root and
rclone. Other permissions: network state, boot completed (for auto-mount), notifications (for alerts), and a short foreground
service. Passwords are stored encrypted with a key held by the Android Keystore, and never appear in logs or notifications.

## Good to know

- Tested by hand on one phone (OnePlus, Android 16, KernelSU). Magisk and APatch are expected to work but are not yet
  verified, and neither are older Android versions.
- NetMount connects by IP address, so certificates issued for a hostname do not match: use **Skip certificate check** on a trusted network.
- SMB through rclone is not faster than WebDAV. For games prefer WebDAV; avoid SFTP for anything that reads at random.
- **Anti-cheat warning:** online games with anti-cheat can react to a rooted phone or a visible FUSE mount. Use storage mounts for
  games at your own risk.

## Troubleshooting

| Message | What to do |
|---|---|
| "Already up to date" but you expect an update | Make sure the channel under Settings, Updates is the one you want. |
| No internet connection / could not reach the update server | The phone cannot reach github.com. |
| The downloaded file does not match its checksum | The download was damaged and was deleted. Try again. |
| Update failed: INSTALL_FAILED_UPDATE_INCOMPATIBLE | The installed app was signed with a different key. Uninstall it (export your storages first) and install this APK. |
| Update failed: INSTALL_FAILED_VERSION_DOWNGRADE | You have a newer build than the one offered. |
| Mount fails with `errno 1` | SELinux refused it. Turn on "Set SELinux permissive if mount is denied" in the storage's Advanced options. |
| Mount fails with `errno 19` | Your kernel has no FUSE. |
| Folder empty in other apps | NetMount retries on its own with another path; the log says which one it used. |

**Settings, Logs** shows what NetMount did and why, with a Share button (no passwords inside).

## About this repository

Everything here is published automatically by the build system:

- `NetMount.apk` and `version.json` in each release, which the app reads. `version.json` holds `versionCode`, `versionName`,
  `sha256`, `size`, a short note and the changelog.
- The release called **beta** is replaced by every beta build. Each stable release is kept.

Please do not edit releases by hand.
