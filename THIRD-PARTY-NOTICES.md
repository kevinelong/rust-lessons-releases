# Third-party notices

The video and audio assets in this repository's releases are produced with the following
tools. Neither is redistributed here — a release contains only the encoded MP4 files.

## ffmpeg

Video encoding and muxing use [ffmpeg](https://ffmpeg.org), licensed under the GNU General
Public License (GPL). The build used is the "essentials" Windows build from
[gyan.dev](https://www.gyan.dev/ffmpeg/builds/), version 9.0.2. Because ffmpeg is invoked
as a separate program and its output (H.264/AAC in MP4) is not a derivative work of
ffmpeg's code, this repository's own licence — FSL-1.1-MIT — is unaffected.

## Windows System.Speech

Narration is synthesised offline through the `System.Speech.Synthesis` API
(`Microsoft Zira`, en-US). The resulting audio is generated output; no Microsoft voice data
is redistributed.

## Fonts

Slides use the system font stack (Consolas, ui-monospace for code; the platform UI font
for headings). No font files are bundled or redistributed.

## Curriculum

The lessons mirror the structure of the Python, Java and JavaScript courses — the
`Introduction_to_computer_programming_with_Python` deck, the Java and JavaScript cohorts,
and the PDX Code Guild material. None of that material is copied into these videos or into
the source repository; the wording, code and narration are original to `rust_lessons`.
