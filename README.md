# SMI-80-2026: Synthetic Multimedia Integrity Dataset

**Purpose:** controlled byte-level integrity and tamper-detection experiments for
“A Dynamic Chaotic Hash-Based Integrity Verification Mechanism for Secure Cloud Multimedia Data”.

## Dataset composition
- 80 original files: 20 each in Text, Image, Audio and Video.
- 12 tampered copies: one per category and size band, each with one bit flipped.
- Formats: TXT/PDF, JPG/PNG, WAV/MP3, MP4/AVI.
- Each category has 7 small, 7 medium and 6 large files.

## Exact target sizes
- Text: 10 KiB, 50 KiB, 200 KiB (within manuscript bands 10–50 KB, 50–200 KB, 200–500 KB).
- Image: 100 KiB, 500 KiB, 2 MiB (within 100–500 KB, 500 KB–2 MB, 2–5 MB).
- Audio: 1 MiB, 3 MiB, 6 MiB (within 1–3 MB, 3–6 MB, 6–10 MB).
- Video: 10 MiB, 30 MiB, 60 MiB (within 10–30 MB, 30–60 MB, 60–100 MB).

## Files
- `originals/`: original generated files.
- `tampered/`: controlled altered copies.
- `dataset_manifest.csv`: file IDs, categories, formats, exact sizes, generation seeds and SHA-256 digests.
- `tamper_manifest.csv`: altered byte offsets and before/after SHA-256 digests.
- `dataset_summary.json`: compact inventory.

## Important research-use caveats
This is a newly generated **synthetic** benchmark. It is not the historical 80-file sample described in the manuscript and does not reconstruct its results. The files are for byte-level hash testing, not semantic multimedia classification or perceptual-quality evaluation. The SHA-256 manifest refers to the exact bytes stored.

Some formats use size padding to place files in the target bands. In particular, MP3/AVI may contain trailing padding bytes; use `ffprobe`/decoder validation before claiming strict container conformance. MP4 uses a trailing `free` box when possible. All benchmark outcomes must be reported as a separate new evaluation, not evidence of live-cloud deployment, cryptographic security, or collision resistance.

## Suggested protocol
1. Verify every original against `dataset_manifest.csv`.
2. Compute the proposed digest, direct SHA-256 and HMAC-SHA-256 under the same environment.
3. Compare original and tampered files using the recorded byte offset.
4. Record per-file and per-run latency, software version, hardware and environment.
5. Report size-band and file-format results separately; do not infer semantic format effects from byte-only processing.
