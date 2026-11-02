# Feasibility verdict and next steps

## Current verdict

[Confirmed, medium confidence] A modified firmware package can be studied and a custom image appears technically plausible: FiiO publishes complete model-specific images, and a recent independent project reports building and running alternative firmware for the exact model.[1][2] The present research independently confirms an RKnano-style container marker and resource-like tables in official images, but has not independently rebuilt a valid image or tested it on hardware.

[Unknown] Whether a modified image can be accepted and flashed by a stock ECHO MINI is unresolved. No device was available for authorized validation; no write or flash was attempted. Therefore physical-device flash status is **NOT TESTED**.

## Acceptance questions

| Question | Result | Evidence / limitation |
|---|---|---|
| Package/container format understood? | Partial | Fixed-size images, repeated `RKnanoFW`, plausible address/size words, resource markers and image tables observed. Complete parser semantics and checksum scope are unknown. |
| Resource extraction/repack demonstrated? | No | Resource names observed, no complete payload extraction or round-trip repack. |
| Modified image rebuilt? | No | No modified image generated. |
| Cryptographic blocking proven? | No | Neither a device-side signature requirement nor its absence was established. |
| Device flash demonstrated? | **NOT TESTED** | No device interaction or writes. |

## Ranked modification paths

| Path | Difficulty | Risk | Feasibility estimate | Evidence and blockers |
|---|---|---|---|---|
| A. Resource-only changes | Medium | Medium to high | Moderate if asset framing and integrity fields are reconstructible | Official changelog confirms UI themes and album-art behavior; stock image contains BMP names and resource tables. No asset payload extraction, repack, or checksum update demonstrated. A bad resource can still crash or brick if the updater accepts it. |
| B. Binary patching | High | High | Low to moderate | A fixed flat image and address-like table fields are visible; ARM binutils are available. No verified entry point, control-flow map, patch/rebuild pipeline, or acceptance behavior exists yet. |
| C. Feature additions | Very high | Very high | Low using stock binary alone; moderate as a separate clean-room project | A recent exact-model project reports a from-scratch firmware and hardware testing, making the platform more tractable than the stock image alone suggests. This is secondary evidence, not reproduced here; requires peripheral/boot/update implementation and device testing.[2] |
| D. Full custom firmware | Very high | Very high | Technically plausible, not yet independently validated by this repository | Exact-model third-party project publishes source, manuals, and release images. Its README says it supports the 8 GB device and warns against use without recovery knowledge.[2] Independent build reproducibility, 512 MB support, and stock-loader acceptance remain unknown. |

Relative order from easiest to hardest: A, B, C, D. Risk does not track difficulty exactly: any accepted low-level patch may have high recovery risk.

## Next experiments

1. Reproduce the exact-model study's image parser from its pinned public source and compare its parsed field boundaries with all 29 official images. Treat its conclusions as hypotheses until raw byte offsets and independent checks agree.
2. Use ARM disassembly with validated load addresses and cross-references from vectors/table entries. Identify executable regions and entry points without treating unvalidated disassembly as ground truth.
3. Decode the resource table and extract one small public UI bitmap. Verify dimensions, palette/encoding, payload boundary, and byte-exact round trip before attempting any repack.
4. Reconcile the final four-byte trailer against the exact-model study and test candidate checksum scopes against all official releases; do not infer cryptographic authenticity from a CRC match.
5. Compare official V3.9.0 and V4.0.0 images, including 8 GB/512 MB pairs, and map fields whose changes correlate with release or model.
6. Keep stock recovery firmware and a documented recovery path before any future hardware test. Device-owner authorization and a recoverable test unit are prerequisites for proving update acceptance. No device-write experiment is part of this milestone.

## Scope still open

This is a substantial static research milestone, not completion of the multi-year issue. The central unknown is whether a modified image is accepted and boots on physical hardware. Reproducible resource extraction/repacking and image building are also unproven. The GitHub tracking issue should remain open.

## Sources

[1] https://forum.fiio.com/note/showNoteContent.do?id=202501210934383987154&tid=17
[2] https://github.com/berettavexee/echo-mini-newfw/tree/6020bd6f44aa3aa6232183e165244ead33011b34
