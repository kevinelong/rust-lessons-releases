# rust-lessons-releases

Downloadable, narrated videos for the **rust_lessons** course — an introduction to
programming taught in Rust. Source, lessons and tests:
**https://github.com/kevinelong/rust_lessons**

The videos are build artefacts, not source. They live in release assets and never in git,
because a course that keeps its MP4s in the repository repeats the mistake it was written
to avoid: a 45 MB PowerPoint that cannot be diffed.

## What is in a release

Each release carries one MP4 per section, 1920×1080, H.264 video with AAC audio:

Current release **v0.5.0** — narrated by Kokoro-82M (Apache-2.0), voice `af_heart`:

| Asset | Length | Size | Covers |
|---|---|---|---|
| `section_01.mp4` | 1:25 | 1.79 MB | comments and identifiers |
| `section_02.mp4` | 1:29 | 1.89 MB | variables and data types |
| `section_03.mp4` | 1:00 | 1.22 MB | operators and expressions |
| `section_04.mp4` | 1:21 | 1.65 MB | strings, numbers and conversion |

`v0.4.0` remains available: the same four videos narrated by Windows SAPI (`Zira`),
20–25 % longer, for comparison.

Later releases extend this list; Track B (sections 17–20) and the remaining sections of
the deck will appear as the videos are generated.

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
