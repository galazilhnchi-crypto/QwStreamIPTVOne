# **IsoaPlayerIPTV**

## **Requirements Traceability Matrix (RTM)**

*Professional IPTV application for Samsung Smart TVs*

**Version 1.1  |  English Edition**

Issue date: 18 November 2026

> *Independent project baseline - no existing project or source code is assumed.*

# Document Control

| **Field** | **Value** |
| --- | --- |
| Document name | IsoaPlayerIPTV_RTM_v1.1 |
| Version | 1.1 |
| Issue date | 18 November 2026 |
| Baseline document | IsoaPlayerIPTV_Requirements_v1.0 |
| Document status | Reconciled traceability baseline - not an implementation or test report |

# Project Status Notice

This matrix was prepared from the requirements document only. No implementation source code, WGT package, runtime records, or test logs were provided as evidence. Therefore, every requirement and test case is currently marked Not Implemented / Not Tested. This document is not proof that any feature is complete.

| **Declared totals** | **Priority** | **Acceptance criteria** |
| --- | --- | --- |
| 86 requirements/constraints | MUST: 78  \\| SHOULD: 8 | 15 |

# 1. Document Summary

This matrix links the requirements and constraints declared in the baseline to responsible components, verification methods, initial test cases, and acceptance criteria. It also records the 15 acceptance criteria from the original requirements document.

# 2. Purpose and Scope

The purpose is to ensure that every requirement can be traced from its source to a system component, test status, and acceptance evidence. It supports forward traceability from a requirement to its test and reverse traceability from an acceptance criterion to the requirements it covers.

Traceability scope includes: up to 9 Xtream/M3U sources; Live TV, Movies, and Series; EPG/XMLTV; Catch-up when the provider supports it; AVPlay media player; phone Companion and secure pairing; backup; security and privacy; Tizen 5.5-10.0 compatibility; performance, stability, and remote-control UX.

# 3. Traceability Method and Status Definitions

- MUST - mandatory requirement for release 1 according to the baseline document.

- SHOULD - recommended requirement; deferral requires a documented decision and product-owner approval.

- Not Implemented / Not Tested - current status for all items because no implementation or test results were supplied.

- In Progress - work has started and a work-item or development-build reference exists, but implementation is incomplete.

- Implemented - implementation exists in a specified version, but testing may not be complete.

- Tested - passed the specified test case with reviewable evidence.

- Approved - passed final acceptance and the product owner/QA approved the evidence.

- Blocked - cannot be implemented because of a documented constraint; an exception/decision must be opened and the issue must not be hidden.

# 4. Evidence and Update Rules

- A requirement status must not become Implemented without a specific release, commit, or WGT build number.

- A status must not become Tested without repeatable steps, an actual result, and evidence; record TV model, Tizen version, and firmware.

- Passwords, session tokens, and secret-bearing stream URLs must be redacted from screenshots, logs, and crash reports.

- Provider-dependent functions such as EPG, Catch-up, codec playback, and subtitles must be tested using an authorized source that actually supplies the feature.

- API success or channel-list loading is not evidence of successful video playback.

# 5. Coverage Summary by Domain

| **Group** | **Count** | **Priority split** | **Main components** |
| --- | --- | --- | --- |
| Live channels and streaming | 8 | MUST: 7 / SHOULD: 1 | Channel Service / Live TV UI |
| Movies and series | 7 | MUST: 5 / SHOULD: 2 | VOD Library / Media Player |
| Source and subscription management | 14 | MUST: 12 / SHOULD: 2 | Source Manager / Provider Connectors |
| Settings and backup | 5 | MUST: 4 / SHOULD: 1 | Settings / Backup |
| Electronic Program Guide (EPG) | 7 | MUST: 6 / SHOULD: 1 | EPG Service / XMLTV Parser |
| Catch-up and Replay | 6 | MUST: 5 / SHOULD: 1 | Catch-up / Replay Adapter |
| Security and privacy | 10 | MUST: 10 / SHOULD: 0 | Security and Privacy Layer |
| Non-functional quality | 6 | MUST: 6 / SHOULD: 0 | Quality and Platform Engineering |
| Phone pairing | 8 | MUST: 8 / SHOULD: 0 | Phone Page / Relay |
| Samsung Tizen platform | 2 | MUST: 2 / SHOULD: 0 | Capability Adapter / Platform Compatibility and Publishing |
| Media playback | 4 | MUST: 4 / SHOULD: 0 | Media Engine Adapter |
| User experience and localization | 2 | MUST: 2 / SHOULD: 0 | Design System / Localization; TV UI / Remote Navigation |
| Reliability and operations | 3 | MUST: 3 / SHOULD: 0 | Diagnostics / Provider Adapters; Performance / Data Services; Resilience / Cache Layer |
| Performance and stability | 4 | MUST: 4 / SHOULD: 0 | Caching / Search; Load / Stability QA; Performance Engineering; TV UI / Performance |

Reconciliation note: RTM v1.0 contained 83 detailed rows while its summary declared 85 (77 MUST / 8 SHOULD), including a two-item Samsung Tizen platform allocation with no detailed PLAT records. This edition adds PLAT-001 and PLAT-002 from the unnumbered platform requirements in SRS §2. A separate traceability gap was also found: SRS §8.2 explicitly defines NFR-I18N, but RTM v1.0 had no standalone row for it; UX-002 covers the release-1 Arabic/English interface and theme, but does not cover the requirement to architect for additional languages. NFR-I18N is therefore recorded separately. The reconciled register contains 86 traceability records (78 MUST / 8 SHOULD). These additions preserve existing source scope and do not assert implementation or test completion.

# 6. Detailed Requirements Traceability Matrix

Requirements are presented by group. Original requirement IDs are retained. PLAT-001 and PLAT-002 are explicit traceability identifiers assigned in this RTM to the two unnumbered platform requirements in SRS §2. NFR-I18N is carried as a separate row because it is explicitly identified in SRS §8.2 and is not fully covered by UX-002.

## Source management and search

#### FR-SRCH-001
- **Priority:** MUST
- **Requirement description:** Unified search across channels, movies, and series, with filtering by type and source.
- **Responsible component:** Source Manager / Provider Connectors
- **Test / acceptance reference:** TC-FR-SRCH-001<br>AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13
- **Current status:** Not Implemented / Not Tested

#### FR-SRCH-002
- **Priority:** MUST
- **Requirement description:** Progressive indexing; users do not need to wait for all sources to finish before initial results appear.
- **Responsible component:** Source Manager / Provider Connectors
- **Test / acceptance reference:** TC-FR-SRCH-002<br>AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13
- **Current status:** Not Implemented / Not Tested

#### FR-SRCH-003
- **Priority:** SHOULD
- **Requirement description:** Clearable recent-search history and options to exclude selected sources.
- **Responsible component:** Source Manager / Provider Connectors
- **Test / acceptance reference:** TC-FR-SRCH-003<br>AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13
- **Current status:** Not Implemented / Not Tested

#### FR-SRCH-004
- **Priority:** MUST
- **Requirement description:** Optional deduplication using provider IDs or item-data fingerprints, with an option to keep multiple copies.
- **Responsible component:** Source Manager / Provider Connectors
- **Test / acceptance reference:** TC-FR-SRCH-004<br>AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13
- **Current status:** Not Implemented / Not Tested

#### FR-SRC-001
- **Priority:** MUST
- **Requirement description:** Allow up to 9 independent connection profiles/sources in release 1.
- **Responsible component:** Source Manager / Provider Connectors
- **Test / acceptance reference:** TC-FR-SRC-001<br>AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13
- **Current status:** Not Implemented / Not Tested

#### FR-SRC-002
- **Priority:** MUST
- **Requirement description:** Support Xtream Codes using server address, port, username, and password, with an optional source display name.
- **Responsible component:** Source Manager / Provider Connectors
- **Test / acceptance reference:** TC-FR-SRC-002<br>AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13
- **Current status:** Not Implemented / Not Tested

#### FR-SRC-003
- **Priority:** MUST
- **Requirement description:** Support M3U and M3U8 playlists by URL, and local file import if Tizen file API testing succeeds on target devices.
- **Responsible component:** Source Manager / Provider Connectors
- **Test / acceptance reference:** TC-FR-SRC-003<br>AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13
- **Current status:** Not Implemented / Not Tested

#### FR-SRC-004
- **Priority:** MUST
- **Requirement description:** Allow source creation, editing, deletion, disabling, renaming, and connection testing from the TV interface.
- **Responsible component:** Source Manager / Provider Connectors
- **Test / acceptance reference:** TC-FR-SRC-004<br>AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13
- **Current status:** Not Implemented / Not Tested

#### FR-SRC-005
- **Priority:** MUST
- **Requirement description:** Allow source addition/editing/deletion from the phone through secure pairing, then present it for TV approval before saving.
- **Responsible component:** Source Manager / Provider Connectors
- **Test / acceptance reference:** TC-FR-SRC-005<br>AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13
- **Current status:** Not Implemented / Not Tested

#### FR-SRC-006
- **Priority:** MUST
- **Requirement description:** Show each source status: not tested, connected, invalid credentials, DNS/TLS failure, timeout, or data-fetch failure.
- **Responsible component:** Source Manager / Provider Connectors
- **Test / acceptance reference:** TC-FR-SRC-006<br>AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13
- **Current status:** Not Implemented / Not Tested

#### FR-SRC-007
- **Priority:** MUST
- **Requirement description:** Provide separate playlists per source and a unified mode that merges sources while identifying each item’s source.
- **Responsible component:** Source Manager / Provider Connectors
- **Test / acceptance reference:** TC-FR-SRC-007<br>AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13
- **Current status:** Not Implemented / Not Tested

#### FR-SRC-008
- **Priority:** MUST
- **Requirement description:** Refreshing a source must not delete favorites, history, or another source’s data; use stable IDs and configurable matching.
- **Responsible component:** Source Manager / Provider Connectors
- **Test / acceptance reference:** TC-FR-SRC-008<br>AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13
- **Current status:** Not Implemented / Not Tested

#### FR-SRC-009
- **Priority:** SHOULD
- **Requirement description:** Provide manual refresh and flexible scheduled refresh with concurrency limits and pause/resume.
- **Responsible component:** Source Manager / Provider Connectors
- **Test / acceptance reference:** TC-FR-SRC-009<br>AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13
- **Current status:** Not Implemented / Not Tested

#### FR-SRC-010
- **Priority:** MUST
- **Requirement description:** Show structural connection-test results separately from actual stream playback tests; API success does not prove video playback.
- **Responsible component:** Source Manager / Provider Connectors
- **Test / acceptance reference:** TC-FR-SRC-010<br>AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13
- **Current status:** Not Implemented / Not Tested

## Live channels and streaming

#### FR-LIVE-001
- **Priority:** MUST
- **Requirement description:** Display channels by source, category, and favorites, with ascending, descending, or manual sorting.
- **Responsible component:** Channel Service / Live TV UI
- **Test / acceptance reference:** TC-FR-LIVE-001<br>AC-03,  AC-07,  AC-10,  AC-11,  AC-12
- **Current status:** Not Implemented / Not Tested

#### FR-LIVE-002
- **Priority:** MUST
- **Requirement description:** Provide instant name search, Arabic/English support, and normalization of common Arabic character variants.
- **Responsible component:** Channel Service / Live TV UI
- **Test / acceptance reference:** TC-FR-LIVE-002<br>AC-03,  AC-07,  AC-10,  AC-11,  AC-12
- **Current status:** Not Implemented / Not Tested

#### FR-LIVE-003
- **Priority:** MUST
- **Requirement description:** Provide previous/next channel and a quick channel list that appears without leaving the player.
- **Responsible component:** Channel Service / Live TV UI
- **Test / acceptance reference:** TC-FR-LIVE-003<br>AC-03,  AC-07,  AC-10,  AC-11,  AC-12
- **Current status:** Not Implemented / Not Tested

#### FR-LIVE-004
- **Priority:** MUST
- **Requirement description:** Allow channels to be added to/removed from favorites and optionally lock a category/channel with a PIN.
- **Responsible component:** Channel Service / Live TV UI
- **Test / acceptance reference:** TC-FR-LIVE-004<br>AC-03,  AC-07,  AC-10,  AC-11,  AC-12
- **Current status:** Not Implemented / Not Tested

#### FR-LIVE-005
- **Priority:** MUST
- **Requirement description:** Show channel logo, name, number, source, and program-guide data when available.
- **Responsible component:** Channel Service / Live TV UI
- **Test / acceptance reference:** TC-FR-LIVE-005<br>AC-03,  AC-07,  AC-10,  AC-11,  AC-12
- **Current status:** Not Implemented / Not Tested

#### FR-LIVE-006
- **Priority:** MUST
- **Requirement description:** Remember the last channel and source, with an optional auto-start setting.
- **Responsible component:** Channel Service / Live TV UI
- **Test / acceptance reference:** TC-FR-LIVE-006<br>AC-03,  AC-07,  AC-10,  AC-11,  AC-12
- **Current status:** Not Implemented / Not Tested

#### FR-LIVE-007
- **Priority:** SHOULD
- **Requirement description:** Support filtering by quality, language, or source when data is available.
- **Responsible component:** Channel Service / Live TV UI
- **Test / acceptance reference:** TC-FR-LIVE-007<br>AC-03,  AC-07,  AC-10,  AC-11,  AC-12
- **Current status:** Not Implemented / Not Tested

#### FR-LIVE-008
- **Priority:** MUST
- **Requirement description:** Clearly show Loading/Buffering/Disconnected states without freezing the UI.
- **Responsible component:** Channel Service / Live TV UI
- **Test / acceptance reference:** TC-FR-LIVE-008<br>AC-03,  AC-07,  AC-10,  AC-11,  AC-12
- **Current status:** Not Implemented / Not Tested

## Movies and series

#### FR-VOD-001
- **Priority:** MUST
- **Requirement description:** Display movies and series in separate sections with categories and source groups.
- **Responsible component:** VOD Library / Media Player
- **Test / acceptance reference:** TC-FR-VOD-001<br>AC-03,  AC-07,  AC-11,  AC-12
- **Current status:** Not Implemented / Not Tested

#### FR-VOD-002
- **Priority:** MUST
- **Requirement description:** Show VOD item details: name, poster, description, release year, genre, and duration if supplied by the source.
- **Responsible component:** VOD Library / Media Player
- **Test / acceptance reference:** TC-FR-VOD-002<br>AC-03,  AC-07,  AC-11,  AC-12
- **Current status:** Not Implemented / Not Tested

#### FR-VOD-003
- **Priority:** MUST
- **Requirement description:** Manage seasons and episodes for series, ordered according to source data; do not invent missing episodes.
- **Responsible component:** VOD Library / Media Player
- **Test / acceptance reference:** TC-FR-VOD-003<br>AC-03,  AC-07,  AC-11,  AC-12
- **Current status:** Not Implemented / Not Tested

#### FR-VOD-004
- **Priority:** MUST
- **Requirement description:** Resume movies and episodes from their previous position when time seeking is supported.
- **Responsible component:** VOD Library / Media Player
- **Test / acceptance reference:** TC-FR-VOD-004<br>AC-03,  AC-07,  AC-11,  AC-12
- **Current status:** Not Implemented / Not Tested

#### FR-VOD-005
- **Priority:** MUST
- **Requirement description:** Store recent viewing and favorites locally and restore them after restart.
- **Responsible component:** VOD Library / Media Player
- **Test / acceptance reference:** TC-FR-VOD-005<br>AC-03,  AC-07,  AC-11,  AC-12
- **Current status:** Not Implemented / Not Tested

#### FR-VOD-006
- **Priority:** SHOULD
- **Requirement description:** Suggest the next episode after completion, with an option to disable autoplay.
- **Responsible component:** VOD Library / Media Player
- **Test / acceptance reference:** TC-FR-VOD-006<br>AC-03,  AC-07,  AC-11,  AC-12
- **Current status:** Not Implemented / Not Tested

#### FR-VOD-007
- **Priority:** SHOULD
- **Requirement description:** Filter by year, genre, and rating when data exists; do not invent metadata.
- **Responsible component:** VOD Library / Media Player
- **Test / acceptance reference:** TC-FR-VOD-007<br>AC-03,  AC-07,  AC-11,  AC-12
- **Current status:** Not Implemented / Not Tested

## Settings and backup

#### FR-SET-001
- **Priority:** MUST
- **Requirement description:** Save language, theme, time zone, section order, and player settings.
- **Responsible component:** Settings / Backup
- **Test / acceptance reference:** TC-FR-SET-001<br>AC-09,  AC-14
- **Current status:** Not Implemented / Not Tested

#### FR-SET-002
- **Priority:** MUST
- **Requirement description:** Optional PIN to lock settings, sources, or selected categories, with a clear recovery path that does not rely on a hidden password.
- **Responsible component:** Settings / Backup
- **Test / acceptance reference:** TC-FR-SET-002<br>AC-09,  AC-14
- **Current status:** Not Implemented / Not Tested

#### FR-SET-003
- **Priority:** MUST
- **Requirement description:** Export settings and sources in JSON; encrypt credentials with a password on export and do not create unencrypted secret backups by default.
- **Responsible component:** Settings / Backup
- **Test / acceptance reference:** TC-FR-SET-003<br>AC-09,  AC-14
- **Current status:** Not Implemented / Not Tested

#### FR-SET-004
- **Priority:** MUST
- **Requirement description:** Import a backup after validating schema and version, with preview and replace/merge options before writing.
- **Responsible component:** Settings / Backup
- **Test / acceptance reference:** TC-FR-SET-004<br>AC-09,  AC-14
- **Current status:** Not Implemented / Not Tested

#### FR-SET-005
- **Priority:** SHOULD
- **Requirement description:** Migrate the database schema between app versions with an automatic backup before upgrade.
- **Responsible component:** Settings / Backup
- **Test / acceptance reference:** TC-FR-SET-005<br>AC-09,  AC-14
- **Current status:** Not Implemented / Not Tested

## Electronic Program Guide (EPG)

#### FR-EPG-001
- **Priority:** MUST
- **Requirement description:** Show the current and next program for a channel, start/end times, and a progress bar relative to current time.
- **Responsible component:** EPG Service / XMLTV Parser
- **Test / acceptance reference:** TC-FR-EPG-001<br>AC-05
- **Current status:** Not Implemented / Not Tested

#### FR-EPG-002
- **Priority:** MUST
- **Requirement description:** Show a time grid for at least the current day and allow previous/next days within available data, up to 7 days or the provider limit.
- **Responsible component:** EPG Service / XMLTV Parser
- **Test / acceptance reference:** TC-FR-EPG-002<br>AC-05
- **Current status:** Not Implemented / Not Tested

#### FR-EPG-003
- **Priority:** MUST
- **Requirement description:** Support XMLTV and channel mapping through tvg-id, with correction/manual mapping when matching fails.
- **Responsible component:** EPG Service / XMLTV Parser
- **Test / acceptance reference:** TC-FR-EPG-003<br>AC-05
- **Current status:** Not Implemented / Not Tested

#### FR-EPG-004
- **Priority:** MUST
- **Requirement description:** Handle time zones, daylight saving, and UTC offsets without an incorrect one-hour program shift.
- **Responsible component:** EPG Service / XMLTV Parser
- **Test / acceptance reference:** TC-FR-EPG-004<br>AC-05
- **Current status:** Not Implemented / Not Tested

#### FR-EPG-005
- **Priority:** MUST
- **Requirement description:** Refresh EPG independently from VOD image fetching; cache by source and record the known refresh time.
- **Responsible component:** EPG Service / XMLTV Parser
- **Test / acceptance reference:** TC-FR-EPG-005<br>AC-05
- **Current status:** Not Implemented / Not Tested

#### FR-EPG-006
- **Priority:** SHOULD
- **Requirement description:** Search program data, such as program title or description, if the source provides it.
- **Responsible component:** EPG Service / XMLTV Parser
- **Test / acceptance reference:** TC-FR-EPG-006<br>AC-05
- **Current status:** Not Implemented / Not Tested

#### FR-EPG-007
- **Priority:** MUST
- **Requirement description:** Do not invent a schedule when EPG is missing; show “No program guide data available.”
- **Responsible component:** EPG Service / XMLTV Parser
- **Test / acceptance reference:** TC-FR-EPG-007<br>AC-05
- **Current status:** Not Implemented / Not Tested

## Catch-up and Replay

#### FR-CU-001
- **Priority:** MUST
- **Requirement description:** Show a Catch-up indicator for a program/channel only if the source declares archive support or valid data is available.
- **Responsible component:** Catch-up / Replay Adapter
- **Test / acceptance reference:** TC-FR-CU-001<br>AC-06
- **Current status:** Not Implemented / Not Tested

#### FR-CU-002
- **Priority:** MUST
- **Requirement description:** Build a Replay URL using start time and duration or a known provider template, validating time boundaries.
- **Responsible component:** Catch-up / Replay Adapter
- **Test / acceptance reference:** TC-FR-CU-002<br>AC-06
- **Current status:** Not Implemented / Not Tested

#### FR-CU-003
- **Priority:** MUST
- **Requirement description:** Provide date/time selection or EPG program selection to start an archive when data is available.
- **Responsible component:** Catch-up / Replay Adapter
- **Test / acceptance reference:** TC-FR-CU-003<br>AC-06
- **Current status:** Not Implemented / Not Tested

#### FR-CU-004
- **Priority:** MUST
- **Requirement description:** Handle archive-window expiration, unavailable programs, and server rejection without treating them as general application failures.
- **Responsible component:** Catch-up / Replay Adapter
- **Test / acceptance reference:** TC-FR-CU-004<br>AC-06
- **Current status:** Not Implemented / Not Tested

#### FR-CU-005
- **Priority:** SHOULD
- **Requirement description:** Provide Restart/Start Over from the beginning if supported by the provider.
- **Responsible component:** Catch-up / Replay Adapter
- **Test / acceptance reference:** TC-FR-CU-005<br>AC-06
- **Current status:** Not Implemented / Not Tested

#### FR-CU-006
- **Priority:** MUST
- **Requirement description:** Do not claim Catch-up support for all channels; the feature varies by channel, provider, and allowed duration.
- **Responsible component:** Catch-up / Replay Adapter
- **Test / acceptance reference:** TC-FR-CU-006<br>AC-06
- **Current status:** Not Implemented / Not Tested

## Phone pairing

#### FR-PHONE-001
- **Priority:** MUST
- **Requirement description:** Create a random, short-lived pairing session (5 minutes by default) that expires automatically and cannot be reused.
- **Responsible component:** Phone Page / Relay
- **Test / acceptance reference:** TC-FR-PHONE-001<br>AC-08,  AC-09
- **Current status:** Not Implemented / Not Tested

#### FR-PHONE-002
- **Priority:** MUST
- **Requirement description:** The QR code must not contain username, password, or a URL with secrets; it may contain only a session ID, public key, or pairing token.
- **Responsible component:** Phone Page / Relay
- **Test / acceptance reference:** TC-FR-PHONE-002<br>AC-08,  AC-09
- **Current status:** Not Implemented / Not Tested

#### FR-PHONE-003
- **Priority:** MUST
- **Requirement description:** Encrypt the source payload end-to-end from phone to TV when Web Crypto/a trusted alternative is proven compatible with Tizen 5.5+; the transport intermediary cannot decrypt it.
- **Responsible component:** Phone Page / Relay
- **Test / acceptance reference:** TC-FR-PHONE-003<br>AC-08,  AC-09
- **Current status:** Not Implemented / Not Tested

#### FR-PHONE-004
- **Priority:** MUST
- **Requirement description:** Require explicit approval on the TV before storing source details; scanning the QR alone must not save anything.
- **Responsible component:** Phone Page / Relay
- **Test / acceptance reference:** TC-FR-PHONE-004<br>AC-08,  AC-09
- **Current status:** Not Implemented / Not Tested

#### FR-PHONE-005
- **Priority:** MUST
- **Requirement description:** Revoke the session after transfer success, rejection, or timeout, and prevent replay of the same payload.
- **Responsible component:** Phone Page / Relay
- **Test / acceptance reference:** TC-FR-PHONE-005<br>AC-08,  AC-09
- **Current status:** Not Implemented / Not Tested

#### FR-PHONE-006
- **Priority:** MUST
- **Requirement description:** The optional intermediary must not store passwords in plaintext or log payload contents; delete packets after delivery or TTL.
- **Responsible component:** Phone Page / Relay
- **Test / acceptance reference:** TC-FR-PHONE-006<br>AC-08,  AC-09
- **Current status:** Not Implemented / Not Tested

#### FR-PHONE-007
- **Priority:** MUST
- **Requirement description:** Provide a manual TV-entry fallback if pairing fails or the device does not support the required encryption.
- **Responsible component:** Phone Page / Relay
- **Test / acceptance reference:** TC-FR-PHONE-007<br>AC-08,  AC-09
- **Current status:** Not Implemented / Not Tested

#### FR-PHONE-008
- **Priority:** MUST
- **Requirement description:** Serve the phone page over HTTPS with CSRF/CSP protection and request-rate limits.
- **Responsible component:** Phone Page / Relay
- **Test / acceptance reference:** TC-FR-PHONE-008<br>AC-08,  AC-09
- **Current status:** Not Implemented / Not Tested

## Security and privacy

#### SEC-001
- **Priority:** MUST
- **Requirement description:** HTTPS is the default for all product and pairing-service connections; HTTP for legacy user sources is allowed only with a clear warning and informed consent.
- **Responsible component:** Security and Privacy Layer
- **Test / acceptance reference:** TC-SEC-001<br>AC-08,  AC-09,  AC-14,  AC-15
- **Current status:** Not Implemented / Not Tested

#### SEC-002
- **Priority:** MUST
- **Requirement description:** Never write passwords, session tokens, or secret-bearing stream URLs to logs, crash reports, or analytics.
- **Responsible component:** Security and Privacy Layer
- **Test / acceptance reference:** TC-SEC-002<br>AC-08,  AC-09,  AC-14,  AC-15
- **Current status:** Not Implemented / Not Tested

#### SEC-003
- **Priority:** MUST
- **Requirement description:** Mask/redact credentials in screens and diagnostics; do not place credentials in QR codes or phone-page URLs.
- **Responsible component:** Security and Privacy Layer
- **Test / acceptance reference:** TC-SEC-003<br>AC-08,  AC-09,  AC-14,  AC-15
- **Current status:** Not Implemented / Not Tested

#### SEC-004
- **Priority:** MUST
- **Requirement description:** Validate TLS certificates; do not disable validation or automatically accept self-signed certificates.
- **Responsible component:** Security and Privacy Layer
- **Test / acceptance reference:** TC-SEC-004<br>AC-08,  AC-09,  AC-14,  AC-15
- **Current status:** Not Implemented / Not Tested

#### SEC-005
- **Priority:** MUST
- **Requirement description:** Validate URLs, schemes, and redirect targets; prevent HTML/JavaScript execution from channel names, EPG, or metadata.
- **Responsible component:** Security and Privacy Layer
- **Test / acceptance reference:** TC-SEC-005<br>AC-08,  AC-09,  AC-14,  AC-15
- **Current status:** Not Implemented / Not Tested

#### SEC-006
- **Priority:** MUST
- **Requirement description:** Use the least privileges possible in config.xml and document the reason for every required privilege. [R5]
- **Responsible component:** Security and Privacy Layer
- **Test / acceptance reference:** TC-SEC-006<br>AC-08,  AC-09,  AC-14,  AC-15
- **Current status:** Not Implemented / Not Tested

#### SEC-007
- **Priority:** MUST
- **Requirement description:** Protect the local PIN with a suitably parameterized hash and repeated-guess protection; never store the PIN in plaintext.
- **Responsible component:** Security and Privacy Layer
- **Test / acceptance reference:** TC-SEC-007<br>AC-08,  AC-09,  AC-14,  AC-15
- **Current status:** Not Implemented / Not Tested

#### SEC-008
- **Priority:** MUST
- **Requirement description:** The Relay must not decrypt source data or retain it beyond TTL; use rate limits, nonce, and one-time use.
- **Responsible component:** Security and Privacy Layer
- **Test / acceptance reference:** TC-SEC-008<br>AC-08,  AC-09,  AC-14,  AC-15
- **Current status:** Not Implemented / Not Tested

#### SEC-009
- **Priority:** MUST
- **Requirement description:** No behavioral tracking or telemetry by default; external diagnostics require explicit consent and an opt-out.
- **Responsible component:** Security and Privacy Layer
- **Test / acceptance reference:** TC-SEC-009<br>AC-08,  AC-09,  AC-14,  AC-15
- **Current status:** Not Implemented / Not Tested

#### SEC-010
- **Priority:** MUST
- **Requirement description:** Delete local app data on uninstall according to published Samsung requirements and provide clear source deletion in the app. [R4]
- **Responsible component:** Security and Privacy Layer
- **Test / acceptance reference:** TC-SEC-010<br>AC-08,  AC-09,  AC-14,  AC-15
- **Current status:** Not Implemented / Not Tested

## Non-functional quality

#### NFR-REL
- **Priority:** MUST
- **Requirement description:** No unjustified loss of favorites or source settings after app closure or TV restart.
- **Responsible component:** Quality and Platform Engineering
- **Test / acceptance reference:** TC-NFR-REL<br>AC-01,  AC-10,  AC-11,  AC-12,  AC-13,  AC-15
- **Current status:** Not Implemented / Not Tested

#### NFR-COMP
- **Priority:** MUST
- **Requirement description:** Core functions work on Tizen 5.5 and later; optional features adapt to detected capabilities.
- **Responsible component:** Quality and Platform Engineering
- **Test / acceptance reference:** TC-NFR-COMP<br>AC-01,  AC-10,  AC-11,  AC-12,  AC-13,  AC-15
- **Current status:** Not Implemented / Not Tested

#### NFR-UX
- **Priority:** MUST
- **Requirement description:** Every loading, error, or empty-data state has a visible representation and a user action/exit.
- **Responsible component:** Quality and Platform Engineering
- **Test / acceptance reference:** TC-NFR-UX<br>AC-01,  AC-10,  AC-11,  AC-12,  AC-13,  AC-15
- **Current status:** Not Implemented / Not Tested

#### NFR-MAINT
- **Priority:** MUST
- **Requirement description:** Modular architecture, tests, documentation, and change tracking; no secrets in the repository or build files.
- **Responsible component:** Quality and Platform Engineering
- **Test / acceptance reference:** TC-NFR-MAINT<br>AC-01,  AC-10,  AC-11,  AC-12,  AC-13,  AC-15
- **Current status:** Not Implemented / Not Tested

#### NFR-PRIV
- **Priority:** MUST
- **Requirement description:** No viewing data or credentials collected in the background without user knowledge and consent.
- **Responsible component:** Quality and Platform Engineering
- **Test / acceptance reference:** TC-NFR-PRIV<br>AC-01,  AC-10,  AC-11,  AC-12,  AC-13,  AC-15
- **Current status:** Not Implemented / Not Tested

#### NFR-I18N
- **Priority:** MUST (baseline classification; confirm during requirements sign-off)
- **Requirement description:** Arabic RTL and English are supported from release 1, with architecture for additional languages.
- **Responsible component:** Design System / Localization
- **Test / acceptance reference:** TC-NFR-I18N<br>AC-15
- **Current status:** Not Implemented / Not Tested

## Media playback

#### MED-001
- **Priority:** MUST
- **Requirement description:** Use Samsung AVPlay for advanced TV features; use HTML5 video as a fallback only after compatibility is proven.
- **Responsible component:** Media Engine Adapter
- **Test / acceptance reference:** TC-MED-001<br>AC-03,  AC-07,  AC-15
- **Current status:** Not Implemented / Not Tested

#### MED-002
- **Priority:** MUST
- **Requirement description:** Support HLS/M3U8 and MPEG-DASH where actual device specifications and codecs allow.
- **Responsible component:** Media Engine Adapter
- **Test / acceptance reference:** TC-MED-002<br>AC-03,  AC-07,  AC-15
- **Current status:** Not Implemented / Not Tested

#### MED-003
- **Priority:** MUST
- **Requirement description:** Manage AVPlay lifecycle, events, errors, and asynchronous preparation using prepareAsync.
- **Responsible component:** Media Engine Adapter
- **Test / acceptance reference:** TC-MED-003<br>AC-07,  AC-12,  AC-15
- **Current status:** Not Implemented / Not Tested

#### OPS-004
- **Priority:** MUST
- **Requirement description:** Disable the screensaver during video playback and handle subtitle display/synchronization as supported by Samsung.
- **Responsible component:** Media Engine Adapter
- **Test / acceptance reference:** TC-OPS-004<br>AC-07,  AC-15
- **Current status:** Not Implemented / Not Tested

## User experience and localization

#### UX-001
- **Priority:** MUST
- **Requirement description:** Full remote navigation with visible, consistent focus management for directional, OK, and Back keys.
- **Responsible component:** TV UI / Remote Navigation
- **Test / acceptance reference:** TC-UX-001<br>AC-10,  AC-15
- **Current status:** Not Implemented / Not Tested

#### UX-002
- **Priority:** MUST
- **Requirement description:** Arabic RTL and English LTR UI, with a dark black/charcoal, red, and white theme and no glow effects.
- **Responsible component:** Design System / Localization
- **Test / acceptance reference:** TC-UX-002<br>AC-15
- **Current status:** Not Implemented / Not Tested

## Reliability and operations

#### OPS-001
- **Priority:** MUST
- **Requirement description:** Progressive loading and chunked indexing; do not block the UI while fetching playlists or refreshing EPG.
- **Responsible component:** Performance / Data Services
- **Test / acceptance reference:** TC-OPS-001<br>AC-10,  AC-11,  AC-12
- **Current status:** Not Implemented / Not Tested

#### OPS-002
- **Priority:** MUST
- **Requirement description:** Separate diagnostics for DNS, TLS, HTTP, credentials, API, and media-format errors.
- **Responsible component:** Diagnostics / Provider Adapters
- **Test / acceptance reference:** TC-OPS-002<br>AC-02,  AC-03,  AC-13
- **Current status:** Not Implemented / Not Tested

#### OPS-003
- **Priority:** MUST
- **Requirement description:** Retain cached responses when the network is lost and isolate one provider’s failure from other sources.
- **Responsible component:** Resilience / Cache Layer
- **Test / acceptance reference:** TC-OPS-003<br>AC-13
- **Current status:** Not Implemented / Not Tested

## Performance and stability

#### PERF-001
- **Priority:** MUST
- **Requirement description:** Launch the app within 10 seconds maximum, targeting 5 seconds, and show the first screen without waiting for the catalog.
- **Responsible component:** Performance Engineering
- **Test / acceptance reference:** TC-PERF-001<br>AC-10,  AC-15
- **Current status:** Not Implemented / Not Tested

#### PERF-002
- **Priority:** MUST
- **Requirement description:** Remote response p95 must not exceed 150 ms during normal navigation.
- **Responsible component:** TV UI / Performance
- **Test / acceptance reference:** TC-PERF-002<br>AC-10,  AC-11
- **Current status:** Not Implemented / Not Tested

#### PERF-003
- **Priority:** MUST
- **Requirement description:** Load the first list from cache within a 3-second target, and keep local search p95 at or below 500 ms after indexing.
- **Responsible component:** Caching / Search
- **Test / acceptance reference:** TC-PERF-003<br>AC-10,  AC-11
- **Current status:** Not Implemented / Not Tested

#### PERF-004
- **Priority:** MUST
- **Requirement description:** Test 9 sources and 30,000 items, plus 4 hours of continuous operation, without a crash or material resource leak.
- **Responsible component:** Load / Stability QA
- **Test / acceptance reference:** TC-PERF-004<br>AC-11,  AC-12
- **Current status:** Not Implemented / Not Tested

## Samsung Tizen platform

#### PLAT-001
- **Priority:** MUST
- **Requirement description:** Package the TV client as a Samsung Tizen Web application using HTML, CSS, JavaScript, and config.xml, and build/sign it as a WGT package; do not target Android APK or TPK.
- **Responsible component:** Platform Compatibility and Publishing
- **Test / acceptance reference:** TC-PLAT-001<br>AC-01, AC-15
- **Current status:** Not Implemented / Not Tested

#### PLAT-002
- **Priority:** MUST
- **Requirement description:** Support Samsung TV model years 2020 and later (Tizen 5.5+) by detecting the actual Tizen version, web-engine version, and runtime capabilities; use a Capability Adapter to gate optional features instead of relying on model year or assuming newer APIs.
- **Responsible component:** Capability Adapter / Platform Compatibility
- **Test / acceptance reference:** TC-PLAT-002<br>AC-01, AC-10, AC-11, AC-15
- **Current status:** Not Implemented / Not Tested

# 7. Acceptance Criteria Register

The following acceptance criteria are copied from the requirements baseline and must be treated as release gates, not as a cosmetic checklist.

| **ID** | **Acceptance criterion** | **Status** |
| --- | --- | --- |
| AC-01 | Install the signed WGT package and launch successfully on a real device from every year/OS group in the test matrix. | Not Started |
| AC-02 | Add 9 sources, mixing Xtream and M3U; edit, delete, disable, and test each source without affecting the others. | Not Started |
| AC-03 | Load Live, Movies, and Series from authorized test sources with valid categories and data. | Not Started |
| AC-04 | Import M3U with UTF-8, BOM, and tvg/group-title fields; handle a partially corrupt playlist without crashing. | Not Started |
| AC-05 | Load XMLTV, map channels, and display Now/Next and timeline grid while testing time zone and daylight-saving behavior. | Not Started |
| AC-06 | Catch-up works on a test channel with a real archive; when no archive exists, no invalid play button appears. | Not Started |
| AC-07 | Switch audio and subtitle tracks on supported device samples; no obvious synchronization loss. | Not Started |
| AC-08 | Add a source from the phone by QR and short session; TV approval, session expiration, and replay protection work. | Not Started |
| AC-09 | Credentials or secret links do not appear in logs, QR codes, crash reports, or unencrypted backups. | Not Started |
| AC-10 | Launch within <=10 seconds in Samsung measurement, targeting <=5 seconds, and show the first UI without waiting for the full catalog. | Not Started |
| AC-11 | Test 9 sources and 30,000 items without crashing; lists remain navigable and remote control remains responsive within the performance target. | Not Started |
| AC-12 | Run continuously for 4 hours with repeated channel switching and no crash or material resource leak. | Not Started |
| AC-13 | When the network disconnects, show a clear message, retain cached data, and resume refresh without duplication or corruption. | Not Started |
| AC-14 | Import/export works with encryption, wrong password, and older-version data; user settings are not silently lost. | Not Started |
| AC-15 | Complete Samsung Mandatory Quality Checklist, including network, media, screensaver, subtitles, performance, and privileges. | Not Started |

# 8. Evidence Required to Close Each Requirement

- Implementation reference: Commit, Pull Request, or WGT Build number.

- Test environment: actual Samsung model, model year, Tizen version, firmware version, and country/app store where publication is relevant.

- Test data: authorized IPTV source, protocol type, playlist/item count, and known EPG/Catch-up properties.

- Result evidence: test log, actual versus expected result, screenshots/video when needed, and an error log redacted of secrets.

- Independent review for high-risk security or privacy requirements.

# 9. Open Assumptions and Constraints

- Catch-up and EPG depend on content-provider/channel data; the app cannot create an archive that does not exist.

- Codec, resolution, audio, and subtitle compatibility varies by TV model and AVPlay capabilities; real-device testing is required.

- Local M3U file import is conditional on proving the Tizen file API on target devices.

- Subscription-secret storage and phone-pairing encryption require an early technical spike on Tizen 5.5 / Chromium M69 and later; the matrix must not assume success before testing.

- Application approval and publication in Samsung Seller Office are subject to Samsung review/policies and country requirements; development success does not guarantee approval.

# 10. Document Revision History

| **Version** | **Date** | **Change** | **Status** |
| --- | --- | --- | --- |
| 1.0 | 16 November 2026 | Created the first traceability matrix from the PRD/SRS v1.0 baseline; declared as 85 requirements/constraints and 15 acceptance criteria. | Initial baseline |
| 1.1 | 18 November 2026 | Added PLAT-001/002, separately traced NFR-I18N, corrected totals and documented the reconciled source-to-RTM mapping. | Reconciled baseline; implementation remains unverified |

## RTM Baseline Note

No requirement is marked Implemented, Tested, or Approved in this baseline. Update each row only when the implementation reference and verifiable test evidence exist. Version 1.1 reconciles the two missing platform rows and the separately identified NFR-I18N row; the reconciled register contains 86 records.

---

*Markdown traceability edition based on the SRS v1.0 baseline. Existing requirement wording and acceptance criteria are preserved; PLAT-001/002 are assigned to the two unnumbered platform requirements in SRS §2, and NFR-I18N is separately traced from SRS §8.2. Version 1.1 reconciles 86 traceability records (78 MUST / 8 SHOULD). No implementation or test completion is claimed.*
