# Live-Action 15-Scene Remake — Production Brief

## Project intent
Create a photorealistic live-action remake from the user-provided source video. Preserve the recognizable adult male subject across all scenes while changing locations and visual atmosphere. This document is a production brief and scene-prompt package; it does not contain rendered video, extracted reference assets, or model weights.

## Source and delivery
- Source: user-uploaded MP4 in the ChatGPT conversation (not committed to this repository).
- Source appearance noted during review: adult man with long dark hair, beard, sunglasses, visible arm tattoos, and a white T-shirt; original setting is a rainy, lantern-lit alley.
- Output target: 15 connected scenes, portrait 9:16 to match source; 4K UHD upscale target (2160 × 3840).
- Keep the source audio only if the user requests it and it is technically suitable. Otherwise use a separately approved soundtrack.
- Final delivery target: MP4, H.264 or H.265, with audio muxed once at assembly.

## Character continuity bible
Use a clean frame from the supplied source as the identity/reference image. Do not infer or invent a new face. Maintain the same adult male identity, facial structure, age appearance, long dark wavy hair, beard, sunglasses, tattoo placement, and body proportions in every generated scene. Keep the white T-shirt as the default outfit. If weather requires an outer layer, keep it simple and remove it in subsequent scenes; never alter tattoos or facial hair. Generate a small approved character-reference sheet before video generation and use it consistently as the reference asset for all scenes.

## Global visual direction
Photorealistic live-action cinematography; realistic skin, hair, fabric, hands and movement; natural environmental physics; controlled cinematic contrast; motivated practical lighting; subtle film grain; realistic lens depth of field. Avoid animation, illustration, plastic skin, face morphing, flicker, duplicated people, distorted hands, changing tattoos, random text, logos and watermarks.

## Scene plan and prompts
Each scene should be generated as a separate short clip. Use the same approved character reference and the same continuity bible in every prompt.

1. **Rainy old-city alley — opening.** Medium-wide establishing shot. The man sits beneath warm lanterns in a wet stone alley, checks his phone, then slowly looks up. Preserve the source's moody rainy atmosphere while making the image photorealistic.
2. **Empty railway platform.** He stands alone under a station canopy as a train passes in the background. Cool dawn light, wet platform reflections, restrained tracking shot.
3. **Mountain highway.** He walks along a safe roadside pull-off with vast misty mountains behind him. Wind moves his hair naturally; wide cinematic landscape shot.
4. **Abandoned cinema.** He enters a quiet, old movie theater. Dust floats in a shaft of projector light; slow push-in, realistic aged seats and architecture.
5. **Neon night market.** He walks through a busy but softly defocused night market. Neon reflections on wet pavement; keep the subject's face and clothing stable.
6. **Coastal cliff.** He stands at a safe viewpoint above the ocean, looking toward the horizon. Wind and sea spray, expansive wide shot.
7. **Desert road.** He walks beside an empty desert highway at golden hour. Heat haze and distant dust, low-angle tracking shot.
8. **Forest cabin.** Interior, storm outside the window. He sits quietly beside the window; warm practical lamp against cool rain light.
9. **Underground parking garage.** He walks toward a pool of light at the far end of a concrete garage. Symmetrical composition, controlled shadows.
10. **Rooftop at sunrise.** He stands on a rooftop overlooking a waking city. Warm backlight, gentle camera orbit, natural expression.
11. **Historic stone street.** He walks through a narrow historic street at blue hour. Warm shop windows, realistic extras in soft focus, steady tracking shot.
12. **Snow-covered village.** He stands in gentle falling snow among mountain-village buildings. Breath subtly visible; preserve hair, beard, sunglasses and tattoos.
13. **Modern glass building.** Reflection-led shot as he walks past a glass facade. Keep reflections physically plausible and do not create a second version of the character.
14. **Seaside at sunset.** He walks along the shoreline with waves washing over the sand. Warm sunset rim light, rear three-quarter tracking shot.
15. **Final close-up.** Tight cinematic close-up. He turns toward the camera and holds a calm, confident expression. Background lights fall into soft bokeh; end on a clean, stable frame suitable for a fade-out.

## Suggested generation workflow
1. Import the original video into a new MusicVision project and extract representative frames locally; do not upload the source video to GitHub.
2. Select a clear, well-lit frame showing the subject's face and tattoos. Create an approved character reference sheet from the source.
3. Create one storyboard image per scene using the same character reference. Review identity, hair, beard, sunglasses, tattoos, clothing and anatomy before rendering clips.
4. Generate short clips per scene with a supported video engine. Prefer the cinematic engine for environment/action shots; use audio-driven/lip-sync generation only if the final audio requires visible singing or speech.
5. Review every clip for identity drift, flicker, anatomy errors and scene continuity. Regenerate failures rather than hiding them with an upscale.
6. Upscale approved clips to the target resolution, then assemble in the intended order. Preserve the original audio only if explicitly selected.
7. Verify final aspect ratio, frame rate, audio sync, duration and playback before calling the MP4 complete.

## MusicVision compatibility notes
The repository README documents image generation, HuMo and LTX-Video 2 video engines, scene-by-scene regeneration, upscaling presets, and MP4 assembly. It lists 4K as an upscale target. This brief does not assert that a particular GPU, model checkpoint, or cloud instance is installed or running. The README's documented engine output ceilings and hardware requirements still apply; 4K is an upscale/delivery target, not a guarantee of native 4K generation.

## Required before rendering
- The original MP4 must be available in the runtime that runs MusicVision.
- An approved character reference image must be extracted/generated locally.
- GPU hardware and required model weights must be available.
- Confirm whether to retain the source soundtrack or replace it.
- Confirm whether to keep the source portrait 9:16 aspect ratio (recommended for this project).

## Acceptance checklist
- [ ] Same recognizable character in all 15 scenes.
- [ ] Hair, beard, sunglasses, tattoos and body proportions remain consistent.
- [ ] All 15 locations are distinct and match the scene plan.
- [ ] No visible face drift, flicker, duplicate subject or severe anatomy defects.
- [ ] Clips are ordered correctly with smooth transitions.
- [ ] Audio choice is approved and synchronized.
- [ ] Final MP4 plays through and meets the requested 4K portrait delivery target.
