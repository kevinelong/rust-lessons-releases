# rust-lessons-releases

Downloadable, narrated videos for the **rust_lessons** course — an introduction to
programming taught in Rust. Source, lessons and tests:
**https://github.com/kevinelong/rust_lessons**

The videos are build artefacts, not source. They live in release assets and never in git,
because a course that keeps its MP4s in the repository repeats the mistake it was written
to avoid: a 45 MB PowerPoint that cannot be diffed.

## What is in a release

Each release carries one MP4 per section, 1920×1080, H.264 video with AAC audio:

Current release **v0.8.0** — all twenty sections with the diagrams embedded, narrated by
Kokoro-82M (Apache-2.0), voice `af_heart`. 1920×1080, H.264 + AAC, 24 kHz mono:

| Asset | Length | Size | Covers |
|---|---|---|---|
| `section_01.mp4` | 1:25 | 1.79 MB | comments and identifiers |
| `section_02.mp4` | 1:28 | 1.89 MB | variables and data types |
| `section_03.mp4` | 1:00 | 1.22 MB | operators and expressions |
| `section_04.mp4` | 1:20 | 1.66 MB | strings, numbers and conversion |
| `section_05.mp4` | 0:50 | 1.08 MB | booleans and conditionals |
| `section_06.mp4` | 1:07 | 1.51 MB | enums |
| `section_07.mp4` | 1:14 | 1.55 MB | vectors |
| `section_08.mp4` | 1:06 | 1.42 MB | maps |
| `section_09.mp4` | 1:01 | 1.30 MB | ranges and iterators |
| `section_10.mp4` | 0:54 | 1.20 MB | loops |
| `section_11.mp4` | 2:27 | 3.21 MB | functions |
| `section_12.mp4` | 1:17 | 1.72 MB | capstone: guess the number |
| `section_13.mp4` | 1:26 | 1.80 MB | structs, methods and traits |
| `section_14.mp4` | 1:16 | 1.60 MB | networks, IP, DNS and URLs |
| `section_15.mp4` | 1:30 | 1.92 MB | clients and servers |
| `section_16.mp4` | 1:37 | 2.05 MB | tables and SQL |
| `section_17.mp4` | 1:30 | 1.84 MB | ownership and moves |
| `section_18.mp4` | 1:27 | 1.78 MB | errors |
| `section_19.mp4` | 1:38 | 2.19 MB | the keyboard and the disk |
| `section_20.mp4` | 1:15 | 1.79 MB | testing |
| **total** | **26:59** | **34.5 MB** | 20 sections |

Earlier releases remain for comparison: `v0.6.0` is the same twenty sections before the
diagrams were embedded, `v0.5.0` four sections re-narrated with Kokoro, `v0.4.0` the same
four with Windows SAPI (`Zira`), 20–25 % longer.

## Verify a download

Each release attaches a `SHA256SUMS` file next to the videos:

```bash
sha256sum -c SHA256SUMS          # GNU coreutils, Linux/WSL
shasum -a 256 -c SHA256SUMS      # macOS
Get-FileHash section_01.mp4 -Algorithm SHA256   # PowerShell
```

## How a video is produced

Nothing here is recorded or edited by hand. `cargo run --bin narrate -- N` in the source
repository parses section N's lesson prose into beats, writes one HTML slide per beat and
the narration text, and generates two scripts: one that synthesises the audio with Windows
SAPI, and one that holds each slide for exactly the length of its own narration and muxes
the result with ffmpeg.

Consequences worth knowing:

* **Timing is narration-driven.** When the lesson prose changes, the video re-derives;
  there is no performance to re-record and no drift between voice and slide.
* **Narration is synthetic, locally generated.** Kokoro-82M (`af_heart`) through
  `kokoro-onnx`, on CPU at RTF 0.15 — no narration service, nothing leaves the machine.
  The earlier `v0.4.0` release used Windows SAPI (`Zira`); `tts.ps1` still exists as the
  dependency-free fallback.
* **Code, tables and diagram pointers are shown silently** for a fixed beat, because
  reading Rust aloud is worse than letting the reader look at it.

Full detail: `docs/video.md` in the source repository.

## Third-party

The videos are rendered with [ffmpeg](https://ffmpeg.org) (GPL) and synthesised with the
Windows `System.Speech` API. Neither is redistributed here; the artefacts are the encoded
video and audio only. See `THIRD-PARTY-NOTICES.md`.

## Licence

The videos and their narration are FSL-1.1-MIT — see [LICENSE.md](LICENSE.md). The
curriculum they teach mirrors the Python, Java and JavaScript courses and includes none of
their material.
