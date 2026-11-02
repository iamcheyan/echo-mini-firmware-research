# Official firmware artifact inventory

Acquired on 2026-11-02 from URLs linked in FiiO's official ECHO MINI firmware post.[1] All 27 downloads are complete ZIP files: the Python `zipfile.ZipFile.testzip()` CRC validation returned `None` for each package. The 27 extracted image files (29 total image members) are stored outside this Git repository; each extracted image was byte-compared to its ZIP member. ZIP size and SHA-256 below can be reproduced against the private files at `~/.local/share/echo-mini-firmware-research/artifacts/official-zips/`. The SHA-256 is a local acquisition identifier, not a vendor-published authenticity signature.
The linked official post directly exposes ZIP URLs. Newer downloads use `https://fiio-firmware.fiio.net/ECHO%20MINI/` or FiiO's Aliyun OSS endpoint; early packages in the table use the exact filenames shown. The V3.8.0 package URLs are `https://fiio-firmware.oss-us-west-1.aliyuncs.com/ECHO%20MINI/ECHO%20MINI%20V3.8.0-8G.zip` and `https://fiio-firmware.oss-us-west-1.aliyuncs.com/ECHO%20MINI/ECHO%20MINI%20V3.8.0-512M.zip`. The V3.7.0 512 MB package is `https://fiio-firmware.fiio.net/ECHO%20MINI/ECHO%20MINI%20V3.7%20512M.zip`; other package URLs follow the official link names in the table, with the V1.3 URL retaining FiiO's published `EHCO` spelling.
The exact ZIP download URLs are listed in the private `reports/package-inventory.json` with the acquisition metadata; they can be regenerated from the official page HTML at the URL in Sources. This repository records package names, model applicability, release version/date when FiiO publishes it, size, completeness, and ZIP/image hashes. The private manifest preserves the exact download URLs and member paths for all 27 packages and 29 images.
| Release | Package | ZIP bytes | SHA-256 | Firmware image member(s) |
|---|---|---:|---|---|
| 1.2.5 | `ECHO MINI V1.2.5.zip` | 4,769,549 | `415a3298a8e33d2dfdc64abe500905d45919a2ce8776f73aa3c8d7d53cd831c0` | `HIFIEC25.IMG` |
| 1.2.7 | `ECHO MINI V1.2.7.zip` | 4,791,904 | `4ca62a75bcebf8a9670c029c69da64899857274432ab1f30f7e17f9adbbb7cfa` | `HIFIEC27.IMG` |
| 1.3.0 | `EHCO MINI V1.3.0.zip` | 4,604,286 | `b2ac6356612bcf5b95aee3566c087fa38e15e118780eb4452f07dd658170b0dd` | `HIFIEC30.IMG` |
| 1.4.0 | `ECHO MINI V1.4.0.zip` | 4,869,190 | `cc10b732711798ac6a08bb8f92c9d73c867c5c31eb389c95ee6b97c1c81a5581` | `HIFIEC40.IMG` |
| 1.4.6 | `ECHO MINI V1.4.6.zip` | 4,892,978 | `3a1f7d7e32e3f741a48a389643f06787666a2597504f3ef7721b0bcc723f159e` | `HIFIEC46.IMG` |
| 1.5.0 | `ECHO MINI V1.5.0 .zip` | 5,049,165 | `0a64711d5a4908677a47879d73ee3c97850a137812dc59343e5d102bb1f8bdce` | `HIFIEC50.IMG` |
| 1.6.2 | `ECHO MINI V1.6.2.zip` | 5,049,229 | `970301ff533ab75528ea49e2bd01e6fdd7dfd3b992ac92376a68da9015ca1769` | `HIFIEC62.IMG` |
| 1.7.0 | `ECHO MINI V1.7.0.zip` | 5,062,142 | `01d76f3de050f4bbbc16ce1be61c2c378d62633bf5d1fc2e5db82499ba9426da` | `HIFIEC70.IMG` |
| 1.8.0 | `ECHO MINI V1.8.0.zip` | 4,970,037 | `787fbbb36efc2f6bdd4ab643ca9d54871ee01c81ada527665c539bbfd2729641` | `HIFIEC80.IMG` |
| 2.4.0 | `ECHO MINI V2.4.0.zip` | 5,771,821 | `2ad7be24e32a4796e9c9a8474a8eb754d1ffda338923cf7be453d1373da978ee` | `HIFIEC40.IMG` |
| 2.5.0 | `ECHO MINI V2.5.0.zip` | 5,771,897 | `bbbdb6469af02ba547e30abb1d93672605a6c2928cbeb4a3f004df8c319b9c79` | `HIFIEC50.IMG` |
| 2.6.0 | `ECHO MINI V2.6.0.zip` | 5,772,187 | `ed43c2d3664319845c99f88e70c1b0061abc37d1ebb509399026f50437daf585` | `HIFIEC60.IMG` |
| 2.7.0 | `ECHO MINI V2.7.0.zip` | 5,794,454 | `14564cc900d6b2f56aeba3edbf2d486a32a035c81a2a7f44a448a030ff7dd17d` | `HIFIEC70.IMG` |
| 2.8.0 | `ECHO MINI V2.8.0.zip` | 5,822,488 | `043a28242d1c34f25f20bd8250f46891714353dc3c502ad5b4d02be68b8b75fd` | `HIFIEC80.IMG` |
| 3.0.0 | `ECHO MINI V3.0.0.zip` | 5,819,818 | `91255e951914fb7ea579df64d214064ce3e317a48ecc9513cfd22ee5b9301bb0` | `HIFIEC00.IMG` |
| 3.1.0 | `ECHO MINI V3.1.0.zip` | 5,979,631 | `1d80548a9f4acdc918b8d51bc5bcbb1c2ee2fd8da8279efe179a721d623ab12e` | `HIFIEC10.IMG` |
| 3.2.0 | `ECHO MINI V3.2.0.zip` | 5,979,795 | `ed05447385b4cebe2e8c1f10eeee35a2873a82d9156e7027d66ade93ece9b2cb` | `HIFIEC20.IMG` |
| 3.3.0 | `ECHO MINI V3.3.0.zip` | 5,980,039 | `00c974a4ce3b32696d965e3bdb84bf0d66b2d810fd910645c291361f922e1ebd` | `HIFIEC33.IMG` |
| 3.4.0 | `ECHO MINI V3.4.0.zip` | 6,005,221 | `f51ac0e925fa71ff84ddeb051de08c33fd85b80b8568b9fae5e23acf7abfb616` | `HIFIEC34.IMG` |
| 3.5.0 | `ECHO MINI V3.5.0.zip` | 5,999,937 | `4bf268febe8106d1c6175effc09051f6346086303babfbbb0372e43ed5d2b1f6` | `HIFIEC35.IMG` |
| 3.6.0 | `ECHO MINI V3.6.0.zip` | 6,001,983 | `2f723c13d891a75f771947f4f5e3a0cb21d48b3028ace23599d28882a7609b29` | `HIFIEC36.IMG` |
| 3.7.0 | `ECHO MINI V3.7.0.zip` | 6,007,488 | `6a3f0fa561c5084e12002c39330dd159efa2cb78cd250f0ee7f9eea36cbfc37d` | `HIFIEC37.IMG` (8 GB) |
| 3.7.0 | `ECHO MINI V3.7 512M.zip` | 6,009,747 | `a78a36f495b71b8f81839b64050523d2758a4f7bbe48e68c31de01eb1d1c0467` | `MINIV370.IMG` (512 MB) |
| 3.8.0 | `ECHO MINI V3.8.0-8G.zip` | 6,024,023 | `ff88080c928c76d80e1fd94d00152f20b4b05b6d11096b73076b8590a4e59591` | `HIFIEC38.IMG` (8 GB) |
| 3.8.0 | `ECHO MINI V3.8.0-512M.zip` | 6,024,888 | `629ea64dd5d3bfabc205ae41863e25d1af4c0a4901ace914d80ee4a4012afe03` | `MINIV380.IMG` (512 MB) |
| 3.9.0 | `ECHO MINI V3.9.0.zip` | 12,043,718 | `dfdbd3ac785fc2657a12f907ce372ce8988289fecfebf8b0cacc960f42880f68` | `HIFIEC39.IMG` (8 GB), `MINIV390.IMG` (512 MB) |
| 4.0.0 | `ECHO MINI V4.0.0.zip` | 12,087,321 | `c0e6a230502592ea5eee7998f2df8a3c5df3d6f1398c4d3b1929ec3f06335cc5` | `HIFIEC40.IMG` (8 GB), `MINIV400.IMG` (512 MB) |

The V3.8 ZIP members have non-UTF8 bytes in their directory names, but both entries were read through Python's ZIP library, extracted completely, and verified against the ZIP CRC. This is a member-name encoding issue; no package bytes were partial.

## Reproduction

```sh
ART="$HOME/.local/share/echo-mini-firmware-research/artifacts"
for f in "$ART"/official-zips/*.zip; do
  unzip -t "$f"
  sha256sum "$f"
done
```

Source: [1] https://forum.fiio.com/note/showNoteContent.do?id=202501210934383987154&tid=17
