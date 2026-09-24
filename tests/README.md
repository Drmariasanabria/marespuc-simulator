# AI integration verification (2026-09-22)

Run `node --test tests/maritime-ai.test.cjs`.

The six transport tests cover anonymous-model filtering, retired models, bounded rate-limit retry, empty responses, unavailable free access, and serialization. They do not claim that the external service will remain available.

Manual browser checks on localhost:
- Instructor test login and AI Lab creation.
- A human message triggered a generated Port Agent response, with the actual model shown.
- Both ITM II missions exposed the AI panel from readiness onward and returned generated responses using the visible scenario.
- Mission 2 remained completable through the final decision and writing terminal while retaining its conversation.
- API probe reproduced the previous model_unavailable error for mistral-small-3.1-24b; a currently listed model returned HTTP 200 with browser CORS enabled.

The shared transport reads the live LLM7 catalogue. It does not embed credentials and only considers chat entries explicitly marked non-usage-only in the free/turbo tiers. Availability and anonymous quotas are provider-controlled. Failures are visible; canned replies are never substituted for model output. Teacher reference retrieval uses the existing subject/module filtering. The mission result contains both sides of the AI dialogue and model IDs; AI dialogue is not graded as a measure of language competence.

The main-page update retains the local, previously unpublished group/scroll/voice UI fixes rather than reverting them to the older committed version. Microphone hardware was not tested in this AI change.

## Response-depth revision (2026-09-24)

Removed the under-100-word limit and mandatory closing question in all three AI interfaces. Increased the output allowance to 1200 tokens and retained up to 24 recent messages. A shared policy permits explanations, short correction examples and requested-language coaching while keeping operational facts constrained. Nemo is preferred when anonymously available, with the existing fallbacks retained.

Seven automated checks pass, including delivery of earlier conversation and shared instructions to the provider. A live two-turn test produced an expanded ETA/berth explanation, then a Spanish explanation without asking again for the ETA. The second answer still repeated much of the first explanation: this is a remaining qualitative limitation, not proof of pedagogical effectiveness or elimination of repetition.
