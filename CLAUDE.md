# ScribeInk for iOS: project memory

ScribeInk for iOS is Chartside's fork of VoiceInk for iOS, being turned into an on-device
clinical scribe. The fork stays open source. Chartside's paid tiers (support, templates,
compliance, EHR integrations) live outside this repo. This repo is self-contained: it
depends on no other Chartside repository, and nothing here should be copied from or synced
with one.

## Non-negotiables

1. **Nothing leaves the device.** No audio, transcript, note or prompt goes to a network
   service. The cloud services (`DeepgramTranscriptionService.swift`,
   `GroqTranscriptionService.swift`, `OpenAICompatibleClient.swift`, `APIKeysView.swift`)
   are to be removed or hard-disabled. Local whisper (`LibWhisper.swift`,
   `LocalModelManager.swift`) is the transcription path. Treat any new network call as a
   bug unless the operator approves it.
2. **No PHI in the repo.** Tests, fixtures, screenshots and logs use synthetic data only.
3. **Never invent clinical content.** A note holds only what was said. See the template
   rules in `clinical-templates/README.md`.
4. **Keep upstream licence and attribution.**
5. **No competitor product names** in code, templates, docs or commit messages.

## Clinical note templates

`clinical-templates/` holds the starting template set, in the format described in
`clinical-templates/SCHEMA.md`. This directory is the source of truth for the app's
templates. They aren't connected to the app yet. The plan is to use them as the prompt for
the local post-processing step (`LLMPostProcessor.swift`, modes).

The set: SOAP (single issue), SOAP by issue, internal medicine new patient (with patient
summary), cardiology SOAP, cardiology letter to referrer, psychiatric consultation,
comprehensive geriatric assessment, emergency note. The README has the backlog of templates
still to build.
