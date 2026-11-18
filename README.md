# QwStreamIPTVOne

**Requirements, traceability and delivery-planning repository for IsoaPlayerIPTV**

QwStreamIPTVOne currently hosts the product requirements and engineering planning baseline for **IsoaPlayerIPTV**, an independent IPTV player specification for Samsung Smart TVs running Tizen. The product specification—not the repository name—currently uses the product name IsoaPlayerIPTV. Confirm and align the public product/repository naming before a release is branded.

> **Repository status (18 November 2026):** documentation baseline only. No application source code, runnable project, WGT package, build pipeline or test result was present in the inspected baseline. This repository must not be described as an implemented or Samsung-approved IPTV application.

## Start here

| Document | Purpose |
| --- | --- |
| [Product & System Requirements (SRS) v1.0](IsoaPlayerIPTV_Requirements_v1.0_EN.md) | Product scope, functional requirements, platform constraints, architecture, security, performance, testing and release plan. |
| [Requirements Traceability Matrix (RTM) v1.1](IsoaPlayerIPTV_RTM_v1.1_EN.md) | Reconciled requirement-to-component-to-test traceability, acceptance criteria and evidence rules. |
| [Product Backlog](BACKLOG.md) | 86 actionable work items linked to source requirement IDs and verification references. |
| [RTM v1.0 — historical baseline](IsoaPlayerIPTV_RTM_v1.0_EN.md) | Original traceability edition retained for change history. |

## Product scope

The SRS defines an independent Tizen Web application packaged as a signed **WGT** for Samsung TV model years **2020 and later**, with Tizen 5.5 as the oldest supported baseline. Actual Tizen, Web Engine and runtime capabilities must be detected on-device; model year alone is not a reliable feature check.

The planned product scope includes:
- User-managed Xtream Codes and M3U/M3U8 sources, with up to nine independent profiles.
- Live TV, Movies, Series, search, favorites, viewing history and settings.
- XMLTV/EPG and Catch-up/Replay only where the provider supplies valid data.
- Samsung AVPlay-first media playback and remote-control-first TV navigation.
- Optional phone Companion/pairing and encrypted backup, subject to platform and cryptography verification.
- Arabic RTL and English LTR, with an architecture that can accommodate more languages.

IsoaPlayerIPTV is a player and source-management application, not a content provider. Users remain responsible for authorization to access their sources. The core architecture keeps video delivery direct from the user's provider to the TV; it does not introduce a stream proxy or restreaming service.

## Current planning baseline

| Measure | Current baseline |
| --- | ---: |
| Traceability records | 86 |
| MUST requirements | 78 |
| SHOULD requirements | 8 |
| Acceptance criteria | 15 |
| Functional requirements | 55 |
| Backlog work items | 86 |

RTM v1.1 reconciles the missing PLAT-001/002 platform records and separately traces NFR-I18N, which exists in SRS §8.2 but was not independently recorded in RTM v1.0. See the reconciliation notes in the RTM for provenance and counting details.

## Engineering and verification rules

1. **Evidence before status:** do not mark a requirement Implemented without a commit/build reference; do not mark it Tested without repeatable steps, an actual result and reviewable evidence.
2. **Real-device proof:** emulator or simulator results do not replace real Samsung TV checks for AVPlay, codecs, networking, performance or Samsung-specific APIs.
3. **Oldest target first:** verify Tizen 5.5 / Chromium M69 constraints before relying on newer JavaScript or Web APIs.
4. **Provider-dependent behavior:** EPG, Catch-up, stream formats, codecs, subtitles and audio tracks must be tested with an authorized provider/source that actually exposes them.
5. **Secrets stay secret:** never commit credentials, private signing material, pairing tokens or secret-bearing stream URLs. Redact them from logs and test evidence.
6. **No scope drift:** preserve the requirements' direct-stream architecture, source isolation, user data integrity and explicit TV approval for phone-submitted source changes.

## Working with the backlog

Use [BACKLOG.md](BACKLOG.md) as the implementation queue. Each work item has a stable `BL-xxx` identifier and links to its original requirement identifier and RTM test/acceptance references. Keep the original requirement ID in commit messages, pull requests and test reports (for example, `FR-LIVE-001`). SHOULD items require an explicit deferral decision and product-owner approval if omitted from a release.

## Repository contribution expectations

- Make changes on a dedicated branch and submit a pull request for review.
- Keep requirements, RTM, backlog and implementation changes synchronized.
- Include tests and evidence with changes; record blocked or deferred device tests instead of claiming them passed.
- Preserve unrelated files, assets, settings and existing behavior during future implementation or repair work.
- Do not add secrets or private WGT-signing keys/certificates to this repository.

## Official platform references

The baseline SRS records the Samsung Developer references used for platform capabilities, Web Engine versions, AVPlay, mandatory quality checks, Web application configuration and publishing. Re-check those official references and the target device documentation when implementation decisions are made; this README does not independently certify present-day Samsung compatibility.

---

*Documentation is a planning baseline, not proof of implementation, playback compatibility, device certification or Samsung Store approval.*
