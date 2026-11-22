# Voice Cloning Options for MATANGI Bhajan Studio

This note records candidate tools for converting or reproducing the user's own singing voice for the Jagannath bhajan project.

## Candidate tools

1. **Seed-VC** — https://github.com/Plachtaa/seed-vc
   - Open-source voice-conversion project to evaluate for reference-based voice conversion.
   - Test specifically with singing vocals and Odia pronunciation before choosing it for production.

2. **Applio** — https://github.com/IAHispano/Applio
   - Open-source RVC-based voice-model training and conversion interface.
   - Evaluate training workflow, singing quality, language pronunciation, and GPU requirements.

3. **Voice-Swap** — https://www.voice-swap.ai/
   - Hosted commercial singing-voice tool.
   - Review current pricing, terms, voice ownership/consent requirements, and availability before use.

## Recommended evaluation order

1. Start with Seed-VC for a reference-audio conversion test.
2. Compare Applio if a separately trained voice model is needed.
3. Consider Voice-Swap only if a hosted paid service is preferred.

## Required input and consent

- Use only a voice recording owned by the user or used with the speaker's explicit permission.
- Obtain a clean, dry vocal recording (no backing track, reverb, or heavy noise).
- A short test sample can establish feasibility; a longer, clean dataset may be required for model training.
- Do not claim that a voice clone exists until a model has been trained or a conversion test has succeeded.

## Integration boundary

MusicVision currently handles music-video generation from finished audio and lyrics. These voice tools are separate candidate upstream components. No voice-cloning runtime, model weights, or API integration is added by this documentation.

## Acceptance tests for the Jagannath bhajan

- Preserve the singer's identity only with the singer's consent.
- Check Odia diction and pronunciation with a native speaker.
- Check pitch stability, vibrato, breath phrasing, and devotional expression.
- Compare the converted vocal against the source performance.
- Export a clean vocal stem, then mix it with the bhajan arrangement before sending the finished audio to MusicVision.
