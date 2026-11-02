# Firmware format and static analysis

## Scope and sample

All complete image binaries reside outside the repository in `~/.local/share/echo-mini-firmware-research/artifacts/`. The primary inspected samples were V4.0.0 8 GB (`HIFIEC40.IMG`), V4.0.0 512 MB (`MINIV400.IMG`), V3.9.0 8 GB and 512 MB, V3.8.0 8 GB and 512 MB, and V1.2.5 8 GB. Their byte sizes and SHA-256 digests are in the private `reports/image-inventory.json`; the V4.0.0 8 GB image SHA-256 is `651e8a3080c246c0fb7d3acea080a0507bf15fcf094bf3557b59866eb65f8197`.

## Confirmed observations

- [Confirmed, high confidence] The V4.0.0 image length is 33,554,436 bytes (32 MiB plus four bytes). `RKnanoFW` occurs at offset 504 and again near offset 533,268. `RKnano SDK 1.0` is present near the beginning and near the resource region. These are literal byte/string observations from the local image.
- [Confirmed, high confidence] At offset `0x1f8`, the V4 image has the words `RKnanoFW`, followed by little-endian values including `0x03050000`, `0x5b`, and address-like values `0x030795cc`, `0x03050000`, `0x00027d30`, `0x030a52fc`, and `0x03004000`. Values resemble load addresses and sizes; field meanings have not been independently reconstructed here.
- [Confirmed, high confidence] Near offset 351,350, the bytes `JPGJPEBMP` occur, followed by another `RKnanoFWL` marker at 360,204. A later `RKnanoFW` marker occurs at 533,268. These delimit a repeated table-like region with printable resource names. The V4 image contains 3,622 occurrences of `.BMP` (including repeated references and suffix text), which does not establish 3,622 unique or independently extractable assets.
- [Confirmed, high confidence] The end of the V4 image is mostly zero padding; the last nonzero byte before its 4-byte trailer is at offset `0x1fcc1ff`. The final four bytes are `a4 1c 7b aa`. This value is recorded as an unexplained trailer; candidate CRC calculations did not match it. Do not infer a valid checksum, signature, or authenticity result.
- [Confirmed, medium confidence] The V4 full-image Shannon entropy is about 5.59 bits/byte. A sampled early code/data region (`0x400–0x51fff`) is about 5.61 bits/byte; a larger mixed region (`0x52000–0x31ffff`) is about 4.30 bits/byte. Resource strings and zero padding account for much of the low whole-file entropy. Entropy alone cannot distinguish compression, encryption, code, or padding.
- [Confirmed] `file` reports generic binary data. `strings -a -n 8` exposed `Rockchip`, `RKnano SDK 1.0`, `RKnanoFW`, `HIFIEC40IMG`, `JPGJPEBMP`, `Version:0.0.1`, and asset names such as `E_USB_DAC_(0,0).BMP`. Printable content indicates that at least some metadata/resources are not wholly encrypted.
- [Confirmed, medium confidence] Officially named 8 GB and 512 MB images for the same release have the same length and broadly similar header layout; their hashes differ. This is consistent with separate model builds, but the exact differences have not been semantically mapped.

## Scan and extraction attempts

Tools and recorded versions: `file` 5.46, GNU `strings` 2.44, `xxd` 2024-12-07, `binwalk` 2.4.3 (Debian), `7z` 25.01, `unzip` 6.00, GNU `sha256sum` 9.5, Python 3.13.5, Capstone and Pillow (Python modules; exact module versions not captured), `arm-none-eabi-objdump` 2.44. The ARM disassembler is installed but has not been used for complete disassembly. `binwalk --version` is unsupported by Debian's v2.4.3 CLI and printed a usage error; the version was read from `binwalk -h`.

Representative commands, run on the complete private image:

```sh
file "$IMAGE"
sha256sum "$IMAGE"
xxd -s 480 -l 256 "$IMAGE"
strings -a -t d -n 8 "$IMAGE"
# Entropy over the whole image and sampled ranges (Python 3.13).
python3 -c 'import collections,math,sys; b=open(sys.argv[1],"rb").read(); ranges=[("all",b),("early",b[0x400:0x52000]),("mixed",b[0x52000:0x320000])]; [print(name,len(x),-sum((n/len(x))*math.log2(n/len(x)) for n in collections.Counter(x).values())) for name,x in ranges]' "$IMAGE"
python3 -c 'import sys; b=open(sys.argv[1],"rb").read(); [(print(x, [i for i in range(len(b)) if b.startswith(x,i)][:20], "count", b.count(x))) for x in (b"RKnanoFW",b"JPGJPEBMP",b"RKnanoFWL",b"RKnano SDK 1.0",b".BMP")]' "$IMAGE"
binwalk -B "$IMAGE"
binwalk -e "$IMAGE"
```

The binwalk signature database contains many implausible MP3/FLAC/WMA, JBOOT, ESP, Minix, Intel microcode, and X.509 hits at unrelated offsets. Treat these as heuristic false positives; their presence is not evidence of those real containers. Its extraction attempt reported that one or more files failed to extract (unsupported or absent utility). An earlier recursive extraction attempt carved multi-gigabyte false-positive outputs; those outputs were deleted from the private research directory. No payload from those carve attempts is treated as extracted firmware content.

A raw scan for standard PNG/JPEG file magic did not locate such assets in V4. This negative result does not exclude custom BMP encoding, indexed/paletted image data, embedded resource compression, or assets whose headers are represented only by tables. `binwalk` did identify several LZMA-looking sequences, but did not extract them; they have not been validated as real streams.

## Not demonstrated

- Resource table grammar, bitmap payload boundaries, image decoder behavior, and a lossless asset extraction/repack cycle.
- Executable region boundaries, entry points, architecture from an analyzed ELF, RTOS identity, or complete disassembly. There is no ELF header observed; the image appears flat/containerized, so generic `readelf` cannot establish these properties.
- Cryptographic signature presence or absence. A visible magic string or 4-byte trailer does not answer this.
- A modified image build, update acceptance, or device boot.

## Private reports and exact-model comparison

Raw ZIP/image digests and inventory JSON, scanner logs, and uncommitted carve experiments are in `~/.local/share/echo-mini-firmware-research/reports/` and `artifacts/`. Proprietary binaries and extracted payloads are intentionally not committed.

A third-party exact-model study states that it reconstructed the RKnanoFW overlay/resource layout and tested custom firmware. Those findings are useful leads only; this repository did not reproduce the parser or resource repacker in this milestone.[1]

## Sources

[1] https://github.com/berettavexee/echo-mini-newfw/tree/6020bd6f44aa3aa6232183e165244ead33011b34
