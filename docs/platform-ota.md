# Platform and OTA correlation

## Official ECHO MINI evidence

- [Confirmed, high confidence] FiiO's product page identifies ECHO MINI as its SNOWSKY music player and lists a retro UI with album art/lyrics, audio format support, Bluetooth 5.3, microSD expansion, and 512 MB/8 GB built-in storage variants.[1]
- [Confirmed, high confidence] FiiO's update post says firmware differs by storage version: `HIFIECXX.IMG` for 8 GB and `MINI*.IMG` for 512 MB. It instructs users to copy the corresponding image into internal storage, safely eject, and restart to initiate automatic upgrade.[2]
- [Confirmed, high confidence] The official post currently lists releases through V4.0.0, dated in the post 2026-10-24, with links to V4.0.0 and preceding releases.[2]
- [Unknown] The downloaded update package's signature format, cryptographic verification, key storage, secure boot policy, anti-rollback behavior, and exact update parser are not established by those instructions or by the static observations in this repository.

- [Confirmed, medium confidence] Public GitHub search finds repositories titled `RKNanoD_MP3_V1.3_20161102`, with startup assembly, peripheral support, codecs, SDK documentation, and firmware-generation tools.[3] This is an unofficial mirrored historical SDK tree, not an independently authenticated Rockchip distribution.
- [Confirmed, high confidence] The recent exact-model public repository `berettavexee/echo-mini-newfw` describes its target as ECHO MINI/RKNanoD and its study says it examined FiiO's V3.9.0 image. The repository commit read for this research is `6020bd6f44aa3aa6232183e165244ead33011b34` (2026-11-01).[4] Detailed findings there remain third-party claims until independently reproduced.
- [Hypothesis, low confidence] The ECHO MINI image's `RKnano SDK 1.0`, `RKnanoFW`, `JPGJPEBMP` markers, and address-like fields are consistent with an RKNano-style flat image/resource scheme. Those strings and resemblance do not prove the exact silicon, package suffix, or RTOS.
- [Unknown] The issue-supplied RTOS, RKNANOD-G variant, dual CS43131 claims, Bluetooth chipset, and flash capacity are not each confirmed by ECHO MINI-specific primary source or a direct board/chip inspection in this milestone. The official ECHO MINI marketing page calls out two ES9068AS DACs, not CS43131; the discrepancy and per-channel DAC identity require primary hardware evidence.[1]

## Relevant platform sources

- [Confirmed, high confidence as SDK content; low confidence as ECHO MINI identity] The public SDK's V1.3 release notes define `RKNANOD_G` as one package-selection macro, alongside LQFP and QFN variants. They also mention 320×240 LCD support, menu/image resource files, separate SPI NOR and eMMC image-generation tools, and update steps.[3]
- [Confirmed, high confidence as source code] SDK Cortex-M startup assembly defines a vector table and Cortex-M exception handlers.[3] This establishes what the mirrored SDK targets, not the ECHO MINI board's component or RTOS.
- [Hypothesis, low confidence] The flat image markers and the historical SDK's image/resource tooling may share conventions. No field-by-field parser match has been reproduced.
- [Unknown] Firmware loader acceptance policy, package signature/authentication, rollback checks, and the exact updater parser remain undetermined.

## Relevant sources

[1] Official product page: https://www.fiio.com/echomini

[2] Official firmware post: https://forum.fiio.com/note/showNoteContent.do?id=202501210934383987154&tid=17

[3] Unofficial historical SDK mirror, revision `6c9657140305a91bedc5602e3822d1904056a635`: https://github.com/EACHAN-YIN/RKNanoD_MP3_V1.3_20161102/tree/6c9657140305a91bedc5602e3822d1904056a635

[4] Exact-model third-party study, revision `6020bd6f44aa3aa6232183e165244ead33011b34`: https://github.com/berettavexee/echo-mini-newfw/tree/6020bd6f44aa3aa6232183e165244ead33011b34
