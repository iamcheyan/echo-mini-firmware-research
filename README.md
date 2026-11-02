# ECHO MINI firmware research

Status: static research milestone, 2026-11-02. Physical device behavior has not been tested.

## Findings

- [Confirmed] FiiO's official product page identifies ECHO MINI as a SNOWSKY music player and documents UI themes, lyrics and embedded album art, Bluetooth, microSD, and built-in storage variants.[1]
- [Confirmed] FiiO's official firmware page lists releases V1.2.5 through V4.0.0, provides direct ZIP downloads, and distinguishes `HIFIEC*.IMG` (8 GB) from `MINI*.IMG` (512 MB).[2]
- [Confirmed] We acquired 27 distinct official ZIP packages (29 image members), and all ZIP CRC integrity checks passed. The 27 extracted image files are stored outside this Git repository; hashes and commands are in [artifact-inventory.md](docs/artifact-inventory.md).[2]
- [Confirmed] The V4.0.0 8 GB image is a fixed 32 MiB + 4-byte artifact with an `RKnanoFW` marker at offset 504, `RKnano SDK 1.0` strings, overlay/resource-like tables, BMP asset names, and a 4-byte trailing value. This is static structure observation, not proof of its checksum algorithm or boot acceptance.
- [Confirmed] Official update instructions say to copy the correctly named image to internal storage and reboot for automatic update. That describes the update path but does not identify whether a package is cryptographically signed or establish boot ROM/loader authentication behavior.[2]
- [Unknown] Exact ECHO MINI loader acceptance conditions, signature/authentication policy, full parser semantics, resource extraction/repacking, and a modified-image rebuild have not been established.

## Documents

- [Artifact inventory](docs/artifact-inventory.md)
- [Format and static analysis](docs/format-analysis.md)
- [Platform and OTA correlation](docs/platform-ota.md)
- [Per-image hashes](docs/image-hashes.md)
- [Feasibility and next steps](docs/feasibility.md)

Private ZIPs, images, and raw reports reside at `~/.local/share/echo-mini-firmware-research/`; they must not be staged or committed.

## Sources

[1] https://www.fiio.com/echomini
[2] https://forum.fiio.com/note/showNoteContent.do?id=202501210934383987154&tid=17
[3] https://github.com/EACHAN-YIN/RKNanoD_MP3_V1.3_20161102
[4] https://github.com/berettavexee/echo-mini-newfw/tree/6020bd6f44aa3aa6232183e165244ead33011b34
