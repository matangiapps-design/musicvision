# ACE-Step Integration — MATANGI Bhajan Studio

**Status:** Integration design committed on a feature branch; runtime integration is not yet implemented or tested.

## Goal

Add an optional, self-hosted song-generation stage before MusicVision's existing five-stage music-video pipeline. The first target is the original 5–6 minute Odia Jagannath bhajan:

- Title: **Jaya Mahaprabhu, Jaya Trilokanatha**
- Style: classic, devotional 1990s Odia bhajan
- Arrangement brief: harmonium, mridanga, manjira/jhanja, bamboo flute, temple bells and conch opening
- Target tempo: 72–78 BPM
- Singer credit: Manas
- Production: MATANGIAPPS PRODUCTIONS

## Upstream engine

Use the official [ACE-Step repository](https://github.com/ace-step/ACE-Step), pinned to a tested release/commit during implementation. ACE-Step exposes text caption, lyrics, instrumental mode, BPM, key/scale, time signature and duration controls. Its documentation lists multiple vocal languages, but does not establish reliable Odia singing support. Odia output must therefore be treated as experimental and evaluated by native Odia listeners before release.

Do not describe generated vocals as Manas's real voice. Voice-reference or voice-cloning features must only be used with Manas's explicit consent and a recording he owns or is authorized to use.

## Proposed workflow

1. **Song brief and lyrics** — retain the approved Odia Unicode lyrics and section labels (opening, mukhda/refrain, antara, instrumental interlude, final refrain).
2. **Optional Ollama text helper** — use a locally hosted Ollama model only for lyric drafting, transliteration/phonetic hints, metadata and prompt preparation. It does not generate the sung audio.
3. **ACE-Step generation** — generate an instrumental arrangement and/or vocal draft using caption, lyrics, BPM and duration. Save each generation as a separate take.
4. **Human review** — listen for Odia pronunciation, lyric fidelity, devotional tone, melodic continuity and unwanted artifacts. Reject takes that garble lyrics.
5. **Audio finishing** — allow manual replacement/recording of the lead vocal, then mix/master the approved audio.
6. **MusicVision intake** — import the approved final WAV and exact lyrics into the existing MusicVision project workflow. Do not send an unapproved AI draft to video rendering.
7. **Video and export** — use the existing storyboard, image, video, upscale and assembly stages. Preserve the original full-length master audio during final assembly.

## Runtime architecture

Keep ACE-Step as an optional external local service/process rather than importing its PyTorch stack into MusicVision's current environment. This avoids dependency conflicts and gives the GPU scheduler a clear model boundary.

Suggested configuration (names are proposals, not existing settings):

- `ACE_STEP_ENABLED=false` by default
- `ACE_STEP_BASE_URL=http://127.0.0.1:8001` when using its API service
- `ACE_STEP_TIMEOUT_SECONDS=3600`
- `OLLAMA_BASE_URL=http://127.0.0.1:11434` when the optional text helper is enabled

Never store API tokens, private voice recordings, or personal credentials in the repository. Keep generated audio and model weights out of Git.

## GPU and job safety

MusicVision's pipeline specification requires serial GPU stages and a single process to own GPU state. The ACE-Step integration must respect that rule:

- Do not run ACE-Step generation concurrently with FLUX, HuMo, LTX or upscaling on the same GPU.
- Add an explicit GPU-stage lock/queue before enabling generation from the GUI.
- Unload ACE-Step weights before starting MusicVision image/video stages.
- Expose clear queued/running/succeeded/failed states and capture logs without leaking secrets.
- Start with a small test generation; do not launch a full 5–6 minute render until duration, memory use and audio export are verified.

## Acceptance tests

- ACE-Step service health check succeeds or the UI clearly reports it unavailable.
- A short test prompt produces a readable WAV with expected sample rate, channels and non-zero duration.
- User-supplied Odia lyrics are preserved exactly in the request payload.
- The system never claims Odia quality is supported until a listening test passes.
- Failed generation leaves the MusicVision project and source audio unchanged.
- GPU lock prevents ACE-Step and video-model jobs from overlapping.
- Approved master WAV imports into MusicVision; final MP4 duration matches the original audio within the existing pipeline tolerance.
- Tests use mocked ACE-Step responses in CI; GPU inference tests are opt-in and run only on provisioned hardware.

## Implementation sequence

1. Add configuration and a health-check client behind a disabled-by-default feature flag.
2. Add a generation request schema and job wrapper; persist request metadata, not model weights or private audio.
3. Add a minimal UI panel for prompt, lyrics, duration, BPM and take selection.
4. Add GPU-stage serialization and explicit model unload/release.
5. Add integration tests with mocked responses, then a real GPU smoke test.
6. Only after the smoke test passes, connect the approved WAV directly to MusicVision intake.

## References

- [ACE-Step official GitHub](https://github.com/ace-step/ACE-Step)
- [ACE-Step inference parameters](https://github.com/ace-step/ACE-Step-1.5/blob/main/docs/en/INFERENCE.md)
- Existing MusicVision pipeline contract: [PIPELINE_SPEC.md](PIPELINE_SPEC.md)
- Existing GPU smoke-test guide: [MUSICVISION_GPU_TEST.md](MUSICVISION_GPU_TEST.md)
