# IsoaPlayerIPTV — Product Backlog

**Version:** 1.0  
**Date:** 18 November 2026  
**Source baseline:** `IsoaPlayerIPTV_Requirements_v1.0_EN.md` and reconciled `IsoaPlayerIPTV_RTM_v1.1_EN.md`  
**Status:** Planning baseline only — no implementation is claimed.

## 1. Backlog baseline

This backlog converts every traceability record into one actionable work item. It contains **86 work items** mapped to **86 requirement identifiers**: 55 functional requirements (`FR-xxx`) and 31 platform, security, quality, media, UX, operations and performance requirements. Priorities are **78 MUST** and **8 SHOULD**.

All items start as **Not Started**. Do not mark a task complete merely because a screen, mock, API response or build exists. Completion requires the implementation reference, mapped test result and evidence required by the RTM. Real-device claims must include the Samsung model, model year, firmware, Tizen version and Web Engine version. Provider-dependent tests must use authorized sources that actually expose the feature.

> **Traceability rule:** Requirement identifiers are preserved. Backlog IDs (`BL-001`…`BL-086`) are work-item identifiers only; they do not replace `FR-xxx`, `PLAT-xxx`, `SEC-xxx`, or other source identifiers.

## 2. Definition of Done

A backlog item is complete only when:
- Its stated acceptance criteria pass using the corresponding RTM test case.
- The change is linked to a commit or pull request and a reproducible test result.
- Applicable acceptance gates (`AC-01`…`AC-15`) are satisfied or explicitly recorded as blocked/deferred with evidence and an owner decision.
- No credentials, tokens or secret-bearing stream URLs are present in source, logs, screenshots or test artifacts.
- Regression checks demonstrate no unrelated loss or degradation.

## 3. Functional backlog

### Search and source management

| Backlog ID | Requirement | Priority | Implementation task | Acceptance criteria | Verification |
| --- | --- | --- | --- | --- | --- |
| BL-001 | [FR-SRCH-001](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-srch-001) | MUST | Deliver unified catalog search — Unified search across channels, movies, and series, with filtering by type and source. | A query can return matching Live channels, Movies and Series; type and source filters narrow the result set without returning out-of-scope items. | TC-FR-SRCH-001; AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13 |
| BL-002 | [FR-SRCH-002](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-srch-002) | MUST | Index sources progressively — Progressive indexing; users do not need to wait for all sources to finish before initial results appear. | The first matching records become selectable before every source finishes indexing; subsequent batches appear without blocking remote input or resetting current results. | TC-FR-SRCH-002; AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13 |
| BL-003 | [FR-SRCH-003](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-srch-003) | SHOULD | Manage recent searches and exclusions — Clearable recent-search history and options to exclude selected sources. | The user can clear recent-search history, and excluded sources are omitted from search results until explicitly re-enabled. | TC-FR-SRCH-003; AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13 |
| BL-004 | [FR-SRCH-004](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-srch-004) | MUST | Provide optional result deduplication — Optional deduplication using provider IDs or item-data fingerprints, with an option to keep multiple copies. | When enabled, duplicate items are matched by provider ID or the defined fingerprint; when disabled, source copies remain separately visible. | TC-FR-SRCH-004; AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13 |
| BL-005 | [FR-SRC-001](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-src-001) | MUST | Support nine independent source profiles — Allow up to 9 independent connection profiles/sources in release 1. | Nine profiles can be created and managed independently; a tenth add attempt is rejected clearly without altering existing profiles. | TC-FR-SRC-001; AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13 |
| BL-006 | [FR-SRC-002](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-src-002) | MUST | Implement the Xtream Codes connector — Support Xtream Codes using server address, port, username, and password, with an optional source display name. | The connector accepts server, port, username and password, permits an optional display name, and reports invalid or successful connection results without exposing secrets. | TC-FR-SRC-002; AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13 |
| BL-007 | [FR-SRC-003](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-src-003) | MUST | Implement M3U/M3U8 source import — Support M3U and M3U8 playlists by URL, and local file import if Tizen file API testing succeeds on target devices. | A valid M3U/M3U8 URL imports and parses; local-file import is exposed only after the target Tizen file API is verified, otherwise the limitation is clear and non-destructive. | TC-FR-SRC-003; AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13 |
| BL-008 | [FR-SRC-004](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-src-004) | MUST | Implement TV-side source management — Allow source creation, editing, deletion, disabling, renaming, and connection testing from the TV interface. | The TV UI can create, edit, delete, disable, rename and test a source; each action affects only the selected source. | TC-FR-SRC-004; AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13 |
| BL-009 | [FR-SRC-005](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-src-005) | MUST | Integrate phone-side source management with TV approval — Allow source addition/editing/deletion from the phone through secure pairing, then present it for TV approval before saving. | Phone add/edit/delete requests are transferred through the approved pairing flow; no change is persisted until the TV user explicitly approves it. | TC-FR-SRC-005; AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13 |
| BL-010 | [FR-SRC-006](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-src-006) | MUST | Expose structured source connection states — Show each source status: not tested, connected, invalid credentials, DNS/TLS failure, timeout, or data-fetch failure. | Each source can independently display all defined outcomes: not tested, connected, invalid credentials, DNS/TLS failure, timeout and data-fetch failure. | TC-FR-SRC-006; AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13 |
| BL-011 | [FR-SRC-007](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-src-007) | MUST | Support separate and unified source views — Provide separate playlists per source and a unified mode that merges sources while identifying each item’s source. | Separate mode preserves per-source playlists; unified mode merges catalog entries while retaining each item's source identity. | TC-FR-SRC-007; AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13 |
| BL-012 | [FR-SRC-008](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-src-008) | MUST | Preserve user data during source refresh — Refreshing a source must not delete favorites, history, or another source’s data; use stable IDs and configurable matching. | Refreshing one source preserves favorites, history and all other source data; stable IDs/matching rules retain valid associations. | TC-FR-SRC-008; AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13 |
| BL-013 | [FR-SRC-009](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-src-009) | SHOULD | Add controllable source refresh scheduling — Provide manual refresh and flexible scheduled refresh with concurrency limits and pause/resume. | Manual and scheduled refresh work with configured concurrency limits; the user can pause and resume scheduled work. | TC-FR-SRC-009; AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13 |
| BL-014 | [FR-SRC-010](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-src-010) | MUST | Separate connection checks from playback checks — Show structural connection-test results separately from actual stream playback tests; API success does not prove video playback. | The UI reports API/playlist connection success separately from stream playback; a successful API response never marks an untested stream as playable. | TC-FR-SRC-010; AC-02,  AC-03,  AC-08,  AC-10,  AC-11,  AC-13 |

### Live TV and channels

| Backlog ID | Requirement | Priority | Implementation task | Acceptance criteria | Verification |
| --- | --- | --- | --- | --- | --- |
| BL-015 | [FR-LIVE-001](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-live-001) | MUST | Build channel views and sorting — Display channels by source, category, and favorites, with ascending, descending, or manual sorting. | Channels can be viewed by source, category and favorites; ascending, descending and manual sort orders produce the expected list. | TC-FR-LIVE-001; AC-03,  AC-07,  AC-10,  AC-11,  AC-12 |
| BL-016 | [FR-LIVE-002](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-live-002) | MUST | Add bilingual channel-name search — Provide instant name search, Arabic/English support, and normalization of common Arabic character variants. | Search responds to channel names in Arabic and English and normalizes the specified common Arabic character variants. | TC-FR-LIVE-002; AC-03,  AC-07,  AC-10,  AC-11,  AC-12 |
| BL-017 | [FR-LIVE-003](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-live-003) | MUST | Implement player channel switching and quick list — Provide previous/next channel and a quick channel list that appears without leaving the player. | Previous/next channel changes the playing channel, and the quick list opens over the player without navigating away from playback. | TC-FR-LIVE-003; AC-03,  AC-07,  AC-10,  AC-11,  AC-12 |
| BL-018 | [FR-LIVE-004](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-live-004) | MUST | Implement channel favorites and optional PIN lock — Allow channels to be added to/removed from favorites and optionally lock a category/channel with a PIN. | A channel can be added/removed from favorites; enabled category/channel locks require the configured PIN and do not lock unrelated entries. | TC-FR-LIVE-004; AC-03,  AC-07,  AC-10,  AC-11,  AC-12 |
| BL-019 | [FR-LIVE-005](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-live-005) | MUST | Display channel and programme metadata — Show channel logo, name, number, source, and program-guide data when available. | Available logo, name, number, source and EPG data are shown accurately; absent provider fields are not fabricated. | TC-FR-LIVE-005; AC-03,  AC-07,  AC-10,  AC-11,  AC-12 |
| BL-020 | [FR-LIVE-006](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-live-006) | MUST | Persist last channel and source — Remember the last channel and source, with an optional auto-start setting. | The last selected channel/source is restored after app restart; auto-start occurs only when the user has enabled that setting. | TC-FR-LIVE-006; AC-03,  AC-07,  AC-10,  AC-11,  AC-12 |
| BL-021 | [FR-LIVE-007](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-live-007) | SHOULD | Add metadata-dependent channel filters — Support filtering by quality, language, or source when data is available. | Quality, language and source filters are available only when their fields exist and do not invent missing values. | TC-FR-LIVE-007; AC-03,  AC-07,  AC-10,  AC-11,  AC-12 |
| BL-022 | [FR-LIVE-008](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-live-008) | MUST | Present playback loading and connection states — Clearly show Loading/Buffering/Disconnected states without freezing the UI. | Loading, buffering and disconnected states are visibly distinguishable while remote navigation and the rest of the UI remain responsive. | TC-FR-LIVE-008; AC-03,  AC-07,  AC-10,  AC-11,  AC-12 |

### Movies and series

| Backlog ID | Requirement | Priority | Implementation task | Acceptance criteria | Verification |
| --- | --- | --- | --- | --- | --- |
| BL-023 | [FR-VOD-001](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-vod-001) | MUST | Build separate Movies and Series libraries — Display movies and series in separate sections with categories and source groups. | Movies and Series appear in separate sections with their provider-supplied categories and source groupings. | TC-FR-VOD-001; AC-03,  AC-07,  AC-11,  AC-12 |
| BL-024 | [FR-VOD-002](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-vod-002) | MUST | Render VOD item details — Show VOD item details: name, poster, description, release year, genre, and duration if supplied by the source. | A selected item displays the available name, poster, description, year, genre and duration; missing source metadata remains absent rather than fabricated. | TC-FR-VOD-002; AC-03,  AC-07,  AC-11,  AC-12 |
| BL-025 | [FR-VOD-003](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-vod-003) | MUST | Build provider-ordered seasons and episodes — Manage seasons and episodes for series, ordered according to source data; do not invent missing episodes. | Series seasons/episodes follow source ordering; missing episodes are not created and incomplete provider data is handled safely. | TC-FR-VOD-003; AC-03,  AC-07,  AC-11,  AC-12 |
| BL-026 | [FR-VOD-004](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-vod-004) | MUST | Implement resume playback — Resume movies and episodes from their previous position when time seeking is supported. | A movie or episode resumes from its previously saved position when seeking is supported; unsupported sources show no false resume promise. | TC-FR-VOD-004; AC-03,  AC-07,  AC-11,  AC-12 |
| BL-027 | [FR-VOD-005](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-vod-005) | MUST | Persist watch history and favorites — Store recent viewing and favorites locally and restore them after restart. | Recent viewing and favorites survive app closure and TV restart and remain associated with the correct item/source. | TC-FR-VOD-005; AC-03,  AC-07,  AC-11,  AC-12 |
| BL-028 | [FR-VOD-006](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-vod-006) | SHOULD | Offer next-episode playback controls — Suggest the next episode after completion, with an option to disable autoplay. | After an episode completes, the next episode is suggested when known; autoplay follows the saved enable/disable preference. | TC-FR-VOD-006; AC-03,  AC-07,  AC-11,  AC-12 |
| BL-029 | [FR-VOD-007](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-vod-007) | SHOULD | Add metadata-based VOD filters — Filter by year, genre, and rating when data exists; do not invent metadata. | Year, genre and rating filters use available metadata only and return correct items without inventing missing metadata. | TC-FR-VOD-007; AC-03,  AC-07,  AC-11,  AC-12 |

### Settings and backup

| Backlog ID | Requirement | Priority | Implementation task | Acceptance criteria | Verification |
| --- | --- | --- | --- | --- | --- |
| BL-030 | [FR-SET-001](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-set-001) | MUST | Persist application preferences — Save language, theme, time zone, section order, and player settings. | Language, theme, time zone, section order and player settings remain saved after navigation and app/TV restart. | TC-FR-SET-001; AC-09,  AC-14 |
| BL-031 | [FR-SET-002](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-set-002) | MUST | Protect settings and selected content with optional PIN — Optional PIN to lock settings, sources, or selected categories, with a clear recovery path that does not rely on a hidden password. | When enabled, the PIN gates the configured settings/sources/categories; recovery follows the documented user-visible process and no hidden password is used. | TC-FR-SET-002; AC-09,  AC-14 |
| BL-032 | [FR-SET-003](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-set-003) | MUST | Implement encrypted JSON backup export — Export settings and sources in JSON; encrypt credentials with a password on export and do not create unencrypted secret backups by default. | Export produces a schema-versioned JSON backup; credentials are password-encrypted and no secret-bearing plaintext backup is created by default. | TC-FR-SET-003; AC-09,  AC-14 |
| BL-033 | [FR-SET-004](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-set-004) | MUST | Implement validated backup import — Import a backup after validating schema and version, with preview and replace/merge options before writing. | Invalid schema/version or wrong password is rejected before writes; the user can preview and choose replace/merge before data is changed. | TC-FR-SET-004; AC-09,  AC-14 |
| BL-034 | [FR-SET-005](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-set-005) | SHOULD | Add safe database schema migration — Migrate the database schema between app versions with an automatic backup before upgrade. | An upgrade migration creates a recoverable backup first and preserves settings, sources, favorites and history across the supported version transition. | TC-FR-SET-005; AC-09,  AC-14 |

### Electronic Program Guide (EPG)

| Backlog ID | Requirement | Priority | Implementation task | Acceptance criteria | Verification |
| --- | --- | --- | --- | --- | --- |
| BL-035 | [FR-EPG-001](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-epg-001) | MUST | Display Now/Next programme details — Show the current and next program for a channel, start/end times, and a progress bar relative to current time. | For a channel with EPG data, current/next title and start/end times are correct and the progress bar reflects current time. | TC-FR-EPG-001; AC-05 |
| BL-036 | [FR-EPG-002](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-epg-002) | MUST | Build the multi-day EPG grid — Show a time grid for at least the current day and allow previous/next days within available data, up to 7 days or the provider limit. | The grid shows the current day and navigates to previous/next available days, capped at seven days or the provider's available range. | TC-FR-EPG-002; AC-05 |
| BL-037 | [FR-EPG-003](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-epg-003) | MUST | Parse XMLTV and map channels — Support XMLTV and channel mapping through tvg-id, with correction/manual mapping when matching fails. | XMLTV data is parsed; tvg-id mapping works and unmatched channels can be corrected or mapped manually. | TC-FR-EPG-003; AC-05 |
| BL-038 | [FR-EPG-004](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-epg-004) | MUST | Normalize programme time zones — Handle time zones, daylight saving, and UTC offsets without an incorrect one-hour program shift. | UTC offsets, configured time zones and daylight-saving transitions render programmes at the correct local time without a spurious one-hour shift. | TC-FR-EPG-004; AC-05 |
| BL-039 | [FR-EPG-005](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-epg-005) | MUST | Refresh and cache EPG independently — Refresh EPG independently from VOD image fetching; cache by source and record the known refresh time. | EPG refresh runs independently of VOD image fetches, caches data by source and displays its known last-refresh time. | TC-FR-EPG-005; AC-05 |
| BL-040 | [FR-EPG-006](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-epg-006) | SHOULD | Search EPG programme metadata — Search program data, such as program title or description, if the source provides it. | When programme titles/descriptions are supplied, search finds matching programmes; unsupported or absent metadata is handled without fabricated results. | TC-FR-EPG-006; AC-05 |
| BL-041 | [FR-EPG-007](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-epg-007) | MUST | Show an explicit no-guide-data state — Do not invent a schedule when EPG is missing; show “No program guide data available.” | When guide data is unavailable, the UI displays “No program guide data available” and never invents a schedule. | TC-FR-EPG-007; AC-05 |

### Catch-up and replay

| Backlog ID | Requirement | Priority | Implementation task | Acceptance criteria | Verification |
| --- | --- | --- | --- | --- | --- |
| BL-042 | [FR-CU-001](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-cu-001) | MUST | Show Catch-up only when source support exists — Show a Catch-up indicator for a program/channel only if the source declares archive support or valid data is available. | The Catch-up indicator appears only when archive support or valid archive data is declared for that channel/programme. | TC-FR-CU-001; AC-06 |
| BL-043 | [FR-CU-002](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-cu-002) | MUST | Build validated replay URLs — Build a Replay URL using start time and duration or a known provider template, validating time boundaries. | Replay URLs use the supported start-time/duration or provider template; invalid, out-of-range or malformed time values are rejected. | TC-FR-CU-002; AC-06 |
| BL-044 | [FR-CU-003](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-cu-003) | MUST | Provide archive date/time selection — Provide date/time selection or EPG program selection to start an archive when data is available. | The user can select a supported EPG programme or date/time and start its archive when the provider exposes the required data. | TC-FR-CU-003; AC-06 |
| BL-045 | [FR-CU-004](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-cu-004) | MUST | Handle Catch-up-specific failures — Handle archive-window expiration, unavailable programs, and server rejection without treating them as general application failures. | Expired archive windows, unavailable programmes and provider rejections produce distinct recoverable messages and do not become generic app failures. | TC-FR-CU-004; AC-06 |
| BL-046 | [FR-CU-005](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-cu-005) | SHOULD | Offer Restart/Start Over when supported — Provide Restart/Start Over from the beginning if supported by the provider. | Restart/Start Over is shown and works only when the provider supports it; unsupported sources do not display a non-functional control. | TC-FR-CU-005; AC-06 |
| BL-047 | [FR-CU-006](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-cu-006) | MUST | Enforce provider-specific Catch-up capability — Do not claim Catch-up support for all channels; the feature varies by channel, provider, and allowed duration. | The product makes no universal Catch-up claim; availability and allowed archive duration are based on each channel/provider's actual capability. | TC-FR-CU-006; AC-06 |

### Phone pairing

| Backlog ID | Requirement | Priority | Implementation task | Acceptance criteria | Verification |
| --- | --- | --- | --- | --- | --- |
| BL-048 | [FR-PHONE-001](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-phone-001) | MUST | Create expiring one-time pairing sessions — Create a random, short-lived pairing session (5 minutes by default) that expires automatically and cannot be reused. | A pairing session uses an unpredictable identifier/token, expires after the configured default five minutes and cannot be reused after expiry or completion. | TC-FR-PHONE-001; AC-08,  AC-09 |
| BL-049 | [FR-PHONE-002](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-phone-002) | MUST | Keep credentials out of QR payloads — The QR code must not contain username, password, or a URL with secrets; it may contain only a session ID, public key, or pairing token. | QR content contains only the permitted session/public-key/pairing-token material; no username, password or secret-bearing source URL is present. | TC-FR-PHONE-002; AC-08,  AC-09 |
| BL-050 | [FR-PHONE-003](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-phone-003) | MUST | Encrypt phone-to-TV source payload end-to-end — Encrypt the source payload end-to-end from phone to TV when Web Crypto/a trusted alternative is proven compatible with Tizen 5.5+; the transport intermediary cannot decrypt it. | The phone payload is encrypted so the intermediary cannot decrypt it on each supported target; if compatible cryptography is not proven, pairing is disabled rather than downgraded insecurely. | TC-FR-PHONE-003; AC-08,  AC-09 |
| BL-051 | [FR-PHONE-004](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-phone-004) | MUST | Require explicit TV approval before saving — Require explicit approval on the TV before storing source details; scanning the QR alone must not save anything. | Scanning/transferring a QR payload only stages a pending request; source details are stored only after explicit approval on the TV. | TC-FR-PHONE-004; AC-08,  AC-09 |
| BL-052 | [FR-PHONE-005](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-phone-005) | MUST | Revoke sessions and block replay — Revoke the session after transfer success, rejection, or timeout, and prevent replay of the same payload. | Success, rejection or timeout revokes the session; repeating the same token/payload is rejected without changing saved settings. | TC-FR-PHONE-005; AC-08,  AC-09 |
| BL-053 | [FR-PHONE-006](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-phone-006) | MUST | Limit Relay payload exposure and retention — The optional intermediary must not store passwords in plaintext or log payload contents; delete packets after delivery or TTL. | The optional Relay neither stores plaintext passwords nor logs payload contents; queued packets are removed after delivery or TTL and rate/nonce controls are enforced. | TC-FR-PHONE-006; AC-08,  AC-09 |
| BL-054 | [FR-PHONE-007](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-phone-007) | MUST | Provide safe manual source-entry fallback — Provide a manual TV-entry fallback if pairing fails or the device does not support the required encryption. | Manual TV entry remains available when pairing or required cryptography is unsupported; fallback does not weaken pairing security. | TC-FR-PHONE-007; AC-08,  AC-09 |
| BL-055 | [FR-PHONE-008](IsoaPlayerIPTV_RTM_v1.1_EN.md#fr-phone-008) | MUST | Harden the Companion page transport — Serve the phone page over HTTPS with CSRF/CSP protection and request-rate limits. | The phone page is served over HTTPS and enforces the specified CSRF/CSP protections and request-rate limits. | TC-FR-PHONE-008; AC-08,  AC-09 |

## 4. Cross-cutting and engineering backlog

### Security and privacy

| Backlog ID | Requirement | Priority | Implementation task | Acceptance criteria | Verification |
| --- | --- | --- | --- | --- | --- |
| BL-056 | [SEC-001](IsoaPlayerIPTV_RTM_v1.1_EN.md#sec-001) | MUST | Enforce secure transport defaults — HTTPS is the default for all product and pairing-service connections; HTTP for legacy user sources is allowed only with a clear warning and informed consent. | Product and pairing connections use HTTPS by default; any legacy HTTP source requires a clear warning and informed user consent. | TC-SEC-001; AC-08,  AC-09,  AC-14,  AC-15 |
| BL-057 | [SEC-002](IsoaPlayerIPTV_RTM_v1.1_EN.md#sec-002) | MUST | Prevent secrets from entering logs and telemetry — Never write passwords, session tokens, or secret-bearing stream URLs to logs, crash reports, or analytics. | Test logs, crash reports and analytics contain no password, session token or secret-bearing stream URL. | TC-SEC-002; AC-08,  AC-09,  AC-14,  AC-15 |
| BL-058 | [SEC-003](IsoaPlayerIPTV_RTM_v1.1_EN.md#sec-003) | MUST | Redact secrets from UI, QR and diagnostics — Mask/redact credentials in screens and diagnostics; do not place credentials in QR codes or phone-page URLs. | Credentials are masked in UI/diagnostics and no credentials or secret-bearing source URL appears in QR or the phone-page URL. | TC-SEC-003; AC-08,  AC-09,  AC-14,  AC-15 |
| BL-059 | [SEC-004](IsoaPlayerIPTV_RTM_v1.1_EN.md#sec-004) | MUST | Validate TLS certificates — Validate TLS certificates; do not disable validation or automatically accept self-signed certificates. | Invalid or self-signed certificates are not silently accepted; failed validation stops the secure connection with a clear error. | TC-SEC-004; AC-08,  AC-09,  AC-14,  AC-15 |
| BL-060 | [SEC-005](IsoaPlayerIPTV_RTM_v1.1_EN.md#sec-005) | MUST | Validate URLs and neutralize untrusted metadata — Validate URLs, schemes, and redirect targets; prevent HTML/JavaScript execution from channel names, EPG, or metadata. | Unsupported schemes and unsafe redirects are rejected; HTML/JavaScript embedded in names, EPG or metadata is displayed as data and never executed. | TC-SEC-005; AC-08,  AC-09,  AC-14,  AC-15 |
| BL-061 | [SEC-006](IsoaPlayerIPTV_RTM_v1.1_EN.md#sec-006) | MUST | Apply least-privilege Tizen configuration — Use the least privileges possible in config.xml and document the reason for every required privilege. [R5] | Every permission in config.xml is necessary, least-privileged and documented with its purpose; unused privileges are removed. | TC-SEC-006; AC-08,  AC-09,  AC-14,  AC-15 |
| BL-062 | [SEC-007](IsoaPlayerIPTV_RTM_v1.1_EN.md#sec-007) | MUST | Protect PIN storage and resist guessing — Protect the local PIN with a suitably parameterized hash and repeated-guess protection; never store the PIN in plaintext. | PINs are not stored in plaintext; the selected hash parameters and repeated-guess rate limits are verified by security tests. | TC-SEC-007; AC-08,  AC-09,  AC-14,  AC-15 |
| BL-063 | [SEC-008](IsoaPlayerIPTV_RTM_v1.1_EN.md#sec-008) | MUST | Keep Relay blind to encrypted source data — The Relay must not decrypt source data or retain it beyond TTL; use rate limits, nonce, and one-time use. | Relay cannot decrypt the end-to-end payload; TTL, rate limits, nonce and one-time-use checks are demonstrated. | TC-SEC-008; AC-08,  AC-09,  AC-14,  AC-15 |
| BL-064 | [SEC-009](IsoaPlayerIPTV_RTM_v1.1_EN.md#sec-009) | MUST | Disable behavioral tracking by default — No behavioral tracking or telemetry by default; external diagnostics require explicit consent and an opt-out. | No behavioral telemetry runs by default; external diagnostics require explicit consent and can be opted out of. | TC-SEC-009; AC-08,  AC-09,  AC-14,  AC-15 |
| BL-065 | [SEC-010](IsoaPlayerIPTV_RTM_v1.1_EN.md#sec-010) | MUST | Implement clear source deletion and uninstall handling — Delete local app data on uninstall according to published Samsung requirements and provide clear source deletion in the app. [R4] | Users can delete sources in-app; uninstall data handling follows the applicable published Samsung requirements and is tested on-device. | TC-SEC-010; AC-08,  AC-09,  AC-14,  AC-15 |

### Non-functional quality

| Backlog ID | Requirement | Priority | Implementation task | Acceptance criteria | Verification |
| --- | --- | --- | --- | --- | --- |
| BL-066 | [NFR-REL](IsoaPlayerIPTV_RTM_v1.1_EN.md#nfr-rel) | MUST | Preserve user state across restarts — No unjustified loss of favorites or source settings after app closure or TV restart. | After forced app closure and TV restart, saved source settings and favorites are intact and consistent. | TC-NFR-REL; AC-01,  AC-10,  AC-11,  AC-12,  AC-13,  AC-15 |
| BL-067 | [NFR-COMP](IsoaPlayerIPTV_RTM_v1.1_EN.md#nfr-comp) | MUST | Verify Tizen 5.5+ core compatibility — Core functions work on Tizen 5.5 and later; optional features adapt to detected capabilities. | Core flows run on Tizen 5.5 and later; optional controls/features are hidden or disabled when runtime capabilities are absent. | TC-NFR-COMP; AC-01,  AC-10,  AC-11,  AC-12,  AC-13,  AC-15 |
| BL-068 | [NFR-UX](IsoaPlayerIPTV_RTM_v1.1_EN.md#nfr-ux) | MUST | Provide complete loading, error and empty states — Every loading, error, or empty-data state has a visible representation and a user action/exit. | Every loading/error/empty state has a visible message and at least one valid user action or exit; no dead-end state remains. | TC-NFR-UX; AC-01,  AC-10,  AC-11,  AC-12,  AC-13,  AC-15 |
| BL-069 | [NFR-MAINT](IsoaPlayerIPTV_RTM_v1.1_EN.md#nfr-maint) | MUST | Enforce maintainable and secret-free engineering practices — Modular architecture, tests, documentation, and change tracking; no secrets in the repository or build files. | The change set contains modular implementation, relevant tests/docs/change records and no secrets in tracked repository/build files. | TC-NFR-MAINT; AC-01,  AC-10,  AC-11,  AC-12,  AC-13,  AC-15 |
| BL-070 | [NFR-PRIV](IsoaPlayerIPTV_RTM_v1.1_EN.md#nfr-priv) | MUST | Require transparent, consent-based data handling — No viewing data or credentials collected in the background without user knowledge and consent. | No viewing data or credentials are collected in the background without user awareness and consent; privacy behavior is testable and documented. | TC-NFR-PRIV; AC-01,  AC-10,  AC-11,  AC-12,  AC-13,  AC-15 |
| BL-071 | [NFR-I18N](IsoaPlayerIPTV_RTM_v1.1_EN.md#nfr-i18n) | MUST | Deliver Arabic/English and extensible localization — Arabic RTL and English are supported from release 1, with architecture for additional languages. | Release-1 screens support Arabic RTL and English LTR; locale switching preserves layout/focus, and adding another language uses the localization structure rather than rewriting screen logic. | TC-NFR-I18N; AC-15 |

### Media playback

| Backlog ID | Requirement | Priority | Implementation task | Acceptance criteria | Verification |
| --- | --- | --- | --- | --- | --- |
| BL-072 | [MED-001](IsoaPlayerIPTV_RTM_v1.1_EN.md#med-001) | MUST | Use AVPlay as the advanced TV media engine — Use Samsung AVPlay for advanced TV features; use HTML5 video as a fallback only after compatibility is proven. | Advanced playback uses Samsung AVPlay; any HTML5 fallback is enabled only for a documented and tested compatible scenario. | TC-MED-001; AC-03,  AC-07,  AC-15 |
| BL-073 | [MED-002](IsoaPlayerIPTV_RTM_v1.1_EN.md#med-002) | MUST | Validate HLS and DASH by device capability — Support HLS/M3U8 and MPEG-DASH where actual device specifications and codecs allow. | HLS/M3U8 and MPEG-DASH play only for supported model/codec/container combinations; unsupported formats fail clearly without a false support claim. | TC-MED-002; AC-03,  AC-07,  AC-15 |
| BL-074 | [MED-003](IsoaPlayerIPTV_RTM_v1.1_EN.md#med-003) | MUST | Manage asynchronous AVPlay lifecycle — Manage AVPlay lifecycle, events, errors, and asynchronous preparation using prepareAsync. | Playback uses prepareAsync and handles open/prepare/play/stop/close plus buffering, error and completion events without blocking the UI. | TC-MED-003; AC-07,  AC-12,  AC-15 |
| BL-075 | [OPS-004](IsoaPlayerIPTV_RTM_v1.1_EN.md#ops-004) | MUST | Manage screensaver and subtitle behavior during playback — Disable the screensaver during video playback and handle subtitle display/synchronization as supported by Samsung. | The screensaver is disabled during video playback as required; supported subtitle rendering/synchronization is verified on the applicable Samsung device. | TC-OPS-004; AC-07,  AC-15 |

### User experience and localization

| Backlog ID | Requirement | Priority | Implementation task | Acceptance criteria | Verification |
| --- | --- | --- | --- | --- | --- |
| BL-076 | [UX-001](IsoaPlayerIPTV_RTM_v1.1_EN.md#ux-001) | MUST | Implement full remote-control navigation and visible focus — Full remote navigation with visible, consistent focus management for directional, OK, and Back keys. | Directional, OK and Back navigation works across all screens with consistent visible focus and no trapped/lost focus in the defined test paths. | TC-UX-001; AC-10,  AC-15 |
| BL-077 | [UX-002](IsoaPlayerIPTV_RTM_v1.1_EN.md#ux-002) | MUST | Apply the specified bilingual visual system — Arabic RTL and English LTR UI, with a dark black/charcoal, red, and white theme and no glow effects. | Arabic RTL and English LTR layouts render correctly with the dark black/charcoal, red and white palette and without glow effects. | TC-UX-002; AC-15 |

### Reliability and operations

| Backlog ID | Requirement | Priority | Implementation task | Acceptance criteria | Verification |
| --- | --- | --- | --- | --- | --- |
| BL-078 | [OPS-001](IsoaPlayerIPTV_RTM_v1.1_EN.md#ops-001) | MUST | Implement progressive loading and chunked indexing — Progressive loading and chunked indexing; do not block the UI while fetching playlists or refreshing EPG. | Playlist/EPG work is chunked or incremental; initial UI remains responsive and first results appear before background work completes. | TC-OPS-001; AC-10,  AC-11,  AC-12 |
| BL-079 | [OPS-002](IsoaPlayerIPTV_RTM_v1.1_EN.md#ops-002) | MUST | Separate provider and media diagnostics — Separate diagnostics for DNS, TLS, HTTP, credentials, API, and media-format errors. | DNS, TLS, HTTP, credential, API and media-format failures are distinguishable in diagnostics with secrets redacted. | TC-OPS-002; AC-02,  AC-03,  AC-13 |
| BL-080 | [OPS-003](IsoaPlayerIPTV_RTM_v1.1_EN.md#ops-003) | MUST | Retain caches and isolate provider failures — Retain cached responses when the network is lost and isolate one provider’s failure from other sources. | During network loss cached data remains accessible; one provider's failure does not block or corrupt another source. | TC-OPS-003; AC-13 |

### Performance and stability

| Backlog ID | Requirement | Priority | Implementation task | Acceptance criteria | Verification |
| --- | --- | --- | --- | --- | --- |
| BL-081 | [PERF-001](IsoaPlayerIPTV_RTM_v1.1_EN.md#perf-001) | MUST | Meet application startup thresholds — Launch the app within 10 seconds maximum, targeting 5 seconds, and show the first screen without waiting for the catalog. | Cold/warm launch is measured; the app never exceeds the 10-second maximum target and aims for 5 seconds, showing the first screen before catalog completion. | TC-PERF-001; AC-10,  AC-15 |
| BL-082 | [PERF-002](IsoaPlayerIPTV_RTM_v1.1_EN.md#perf-002) | MUST | Meet remote-response latency target — Remote response p95 must not exceed 150 ms during normal navigation. | A defined normal-navigation measurement reports p95 key-to-visible-focus latency at or below 150 ms, without accumulated lag or focus jumps. | TC-PERF-002; AC-10,  AC-11 |
| BL-083 | [PERF-003](IsoaPlayerIPTV_RTM_v1.1_EN.md#perf-003) | MUST | Meet first-list and search performance targets — Load the first list from cache within a 3-second target, and keep local search p95 at or below 500 ms after indexing. | A cached first list appears within the 3-second target and local search remains at or below 500 ms p95 after indexing on the agreed dataset. | TC-PERF-003; AC-10,  AC-11 |
| BL-084 | [PERF-004](IsoaPlayerIPTV_RTM_v1.1_EN.md#perf-004) | MUST | Pass scale and endurance verification — Test 9 sources and 30,000 items, plus 4 hours of continuous operation, without a crash or material resource leak. | The app is exercised with 9 sources, 30,000 items and a 4-hour continuous run without crash or a material resource leak. | TC-PERF-004; AC-11,  AC-12 |

### Samsung Tizen platform

| Backlog ID | Requirement | Priority | Implementation task | Acceptance criteria | Verification |
| --- | --- | --- | --- | --- | --- |
| BL-085 | [PLAT-001](IsoaPlayerIPTV_RTM_v1.1_EN.md#plat-001) | MUST | Build and package the Tizen Web application as WGT — Package the TV client as a Samsung Tizen Web application using HTML, CSS, JavaScript, and config.xml, and build/sign it as a WGT package; do not target Android APK or TPK. | A signed WGT installs and launches on real target Samsung hardware; package metadata and privileges are valid, and no APK/TPK target is introduced. | TC-PLAT-001; AC-01, AC-15 |
| BL-086 | [PLAT-002](IsoaPlayerIPTV_RTM_v1.1_EN.md#plat-002) | MUST | Detect Tizen and runtime capabilities safely — Support Samsung TV model years 2020 and later (Tizen 5.5+) by detecting the actual Tizen version, web-engine version, and runtime capabilities; use a Capability Adapter to gate optional features instead of relying on model year or assuming newer APIs. | The app records actual model/firmware/Tizen/Web Engine details and gates optional APIs/features via capability checks; the oldest Tizen 5.5 baseline does not execute unsupported APIs. | TC-PLAT-002; AC-01, AC-10, AC-11, AC-15 |

## 5. Release sequencing guidance

1. **P0 — Platform proof:** PLAT-001/002, MED-001/002/003 and the earliest security/secret-storage feasibility checks. Prove installation, AVPlay, remote keys, storage and network behavior on the oldest target before assuming newer APIs.
2. **P1 — Player MVP:** source management, Live TV, Movies/Series, search, settings, favorites/history, core UX and reliability.
3. **P2 — Guide and replay:** EPG and Catch-up, gated by actual provider data and archive capability.
4. **P3 — Companion and backup:** phone pairing, cryptography compatibility, TV approval, Relay controls and encrypted backup.
5. **P4 — Optimization and release:** scale/endurance/performance verification, full device matrix, Samsung quality checklist and publishing deliverables.

This is sequencing guidance from the SRS phase plan, not a claim that any phase has started. Dependencies and risk should determine the actual batch size.

## 6. Decisions and constraints to preserve

- Target Samsung TV model years 2020+ with Tizen 5.5 as the oldest baseline; detect actual runtime capabilities rather than relying on model year alone.
- Build a Tizen Web application packaged as a signed WGT. Do not assume Android APK or TPK support on Samsung TV.
- Use AVPlay for advanced playback; only enable alternatives after target-device verification.
- Keep video streams direct from the user's authorized provider to the TV; the application must not proxy or restream content.
- EPG, Catch-up, codecs, subtitles and audio tracks are provider/device-dependent. Never invent availability.
- The QR code must not expose credentials. TV approval, expiry and replay protection are mandatory; do not introduce an insecure cryptography fallback.
- Preserve all saved sources, favorites, history and settings during refreshes, migrations and repairs.

## 7. Traceability reconciliation

RTM v1.0 had 83 detail rows, despite declaring 85 and allocating two Samsung platform items. The v1.1 RTM adds PLAT-001/002. It also adds NFR-I18N as a separate traceability record because that ID exists in SRS §8.2 and UX-002 does not cover extensibility for additional languages. The reconciled total is therefore 86 records (78 MUST / 8 SHOULD). No implementation or verification status has been upgraded by this documentation change.
