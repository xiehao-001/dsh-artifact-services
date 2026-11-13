# Shared Artifact Services

`@eduwork/dsh-artifact-services` · v0.3.4 · MulanPSL-2.0 AND MIT

Shared Artifact Services is the artifact backend behind EduWork's Office generation, speech, image and video features. It provides Office creation and preview, TTS/ASR provider registries, image generation and Remotion-based media rendering, and it is consumed both by DSH conversation tools and by ordinary Node applications through subpath imports.

The package does not depend on Studio, its index, institutional login or a desktop shell. A DSH host loads the `/dsh` adapter once; other applications import only the entries they need.

## Highlights

- Office tools: `office_document` (create, edit, inspect, validate, convert), `office_spreadsheet` (plus recalculate), `office_presentation` (create, inspect, validate, convert) and `office_pdf` (create, inspect, merge, extract, validate), all using workspace-relative paths.
- DSH assembly: `@eduwork/dsh-artifact-services/dsh` registers `artifactServices`, six bundled skills (`artifact-documents`, `artifact-spreadsheets`, `artifact-presentations`, `artifact-pdfs`, `artifact-speech`, `artifact-video`) and `artifact-images` when image providers are enabled and available, with ten default tools and three optional image tools.
- Speech and transcription: one provider contract (`voices()` / `synthesize()`) with a built-in `system` provider (System.Speech on Windows, `say` on macOS), real WAV output with measured duration, plus `speech_voices`, `speech_synthesize`, `speech_transcription_providers` and `speech_transcribe`.
- Image generation: `ImageService` with declared capabilities, workspace-bounded input and output, file-signature validation and optional `edit()` support, exposed as `image_providers`, `image_generate` and `image_edit`.
- Video: `media_render` for structured clips and `video_project` for editable Remotion projects, with staged source, integrity-bound narration tasks, validation, covers and quality-check frames; Remotion 4.0.520, mediabunny 1.55.5 and React 18.3.1 are pinned.
- Six instrumental BGM tracks ship with score JSON, deterministic synthesis code, 192 kbps MP3s and hash/volume/loop metadata.
- Office, image, speech and video tools reuse the session's current workspace write permission instead of adding a separate confirmation path.
- Plain Node apps can import focused entries such as `/office`, `/speech`, `/images`, `/media`, `/runtime` and `/providers`.

## Install

Install this directory as a local DSH plugin bundle. From a shell:

```bash
dsh plugin --profile web add /absolute/path/to/dsh-artifact-services
```

Or add the directory through the **Plugins** panel in DSH (local bundle). Restart the DSH app after installation; plugins are activated from the bundle patch (`cordis.patch.yml`).

## Configuration

No configuration keys are shipped: the bundle patch inserts the plugin with defaults.

Image generation is off unless a deployment adds `images: { enabled: true }` to the ArtifactServices plugin configuration, which turns on the image tools, the `artifact-images` skill and provider calls together. Local images used by Office and video are not affected by this switch.

## Requirements

- DeepSeek Harness `>=0.2.1 <0.3.0`
- Node `>=24.18.0`
- Peer packages: `@deepseek-ai/cordis`, `@deepseek-ai/dsh-skill`, `@deepseek-ai/dsh-tools`

## Notes and limits

- Office requires Python 3.12+ and the dependencies in `python/requirements.txt`; point `DSH_OFFICE_PYTHON` at the interpreter. The legacy `CHATECNU_WORK_OFFICE_PYTHON` variable is still read. Installing the npm package does not install Python libraries, ASR models or browsers.
- The upstream README targets a complete, version-matched 0.2.1-rc.2 host or a compatible 0.2.x stable host and explicitly warns against `--force` or `--legacy-peer-deps`; this package's engine range is `>=0.2.1 <0.3.0`.
- macOS system voices need a Chinese voice installed; other platforms need a registered speech provider, and on-device ASR needs a whisper.cpp executable and model supplied by the host.
- Office support covers the OOXML and PDF features documented in `docs/OFFICE_PROCESSING.md`; macros, revision history and animation editing are out of scope.

## 中文文档

[README.zh-CN.md](./README.zh-CN.md)

## License

MulanPSL-2.0 AND MIT — see [LICENSE](./LICENSE) and, where present, [LICENSE-MIT](./LICENSE-MIT). Extracted from the ECNU EduWork distribution (https://github.com/ECNU/EduWork); upstream copyright and license notices are preserved.
