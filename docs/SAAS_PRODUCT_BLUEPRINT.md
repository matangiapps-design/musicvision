# MATANGI AI MUSIC STUDIO — SaaS Product Blueprint

## Product goal
A customer-facing web application for ordering AI-assisted songs and music videos. Customers must never need GitHub, ComfyUI, Kaggle, API keys, or model setup.

## Customer journey
1. Create an account and sign in.
2. Choose a service: music video, video-to-video, AI song, or full album.
3. Upload only assets they own or are authorised to use (audio, lyrics, images, video).
4. Choose aspect ratio, visual style, duration, and output quality.
5. Review a clear price and generation-credit estimate before checkout.
6. Pay through a supported payment provider.
7. Track the job in a dashboard; jobs can continue after the customer closes the browser.
8. Preview, download, and manage completed exports.

## Proposed launch pricing (test prices, not yet validated against GPU cost)
- Starter: $3
- Creator: $6
- Pro: $9

Do not promise unlimited generations. Enforce per-plan duration, resolution, retries, and queue priority. Recalculate prices after measuring GPU minutes, storage, bandwidth, payment fees, failed jobs, and support costs.

## System architecture
- Frontend: responsive web app, mobile-first.
- API: FastAPI; authentication, projects, uploads, billing webhooks, job status, downloads.
- Database: PostgreSQL for users, projects, orders, credits, jobs, and audit events.
- Queue: Redis + worker queue; idempotent jobs and retry limits.
- Storage: private object storage; short-lived signed download URLs.
- GPU worker: isolated worker service running MusicVision stages and model dependencies.
- Media pipeline: ACE-Step (where compatible/licensed), ComfyUI/Wan or supported MusicVision video engines, FFmpeg assembly.
- Observability: job logs, GPU time, failure reasons, cost per export, alerts.
- Deployment: frontend/API on a web host; GPU workers on a separately scalable GPU host.

## Job states
queued -> validating -> generating_audio (optional) -> planning_scenes -> generating_images -> generating_video -> assembling -> quality_check -> completed
Failure states: needs_customer_action, failed, cancelled, refunded. Persist progress and error summaries.

## Security and trust
- Never expose model credentials or worker endpoints to browsers.
- Verify payment webhooks server-side; never trust client-side payment success.
- Validate file type, size, duration, and decode safely before processing.
- Store customer uploads privately; use signed URLs and retention/deletion controls.
- Rate-limit sign-in, uploads, job creation, and downloads.
- Require rights to uploaded audio, likenesses, and video; prohibit non-consensual intimate imagery and impersonation.
- Provide terms, privacy policy, refund policy, content rules, and support contact before launch.

## Build milestones
1. Customer-facing landing page and service catalogue.
2. Authentication, upload validation, project dashboard.
3. Payment checkout and verified webhook.
4. Queue and mock worker; prove end-to-end order lifecycle without expensive generation.
5. Connect MusicVision worker; run a small private beta.
6. Measure real costs and adjust credits/prices.
7. Add subscriptions, referrals, and automated customer support only after reliable paid jobs.

## Launch gate
Do not accept paid orders until payment reconciliation, job recovery, private storage, refund handling, cost limits, and end-to-end output quality have been tested.
