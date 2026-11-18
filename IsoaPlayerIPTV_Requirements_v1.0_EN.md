# **IsoaPlayerIPTV**

## **Product & System Requirements**

*Professional, integrated, high-performance IPTV application for Samsung Smart TVs running Tizen OS*

**Version 1.0  |  English Edition**

Issue date: 16 November 2026

> *Independent project baseline - no existing project or source code is assumed.*

# Document Control

| **Field** | **Value** |
| --- | --- |
| Product name | IsoaPlayerIPTV |
| Document type | Product Requirements Document (PRD) and System Requirements Specification (SRS) |
| Version | 1.0 - Initial implementation baseline |
| Document date | 16 November 2026 |
| Target platform | Samsung Smart TV / Tizen OS, model years 2020 and later |
| Application form | Tizen Web Application packaged as a signed WGT |
| Audience | Product owner, UX team, Tizen developers, QA, security, and publishing/release team |
| Requirements status | Proposed requirements; convert them into implementation tasks and tests before release |

# Executive Summary

IsoaPlayerIPTV is an independent IPTV player, not a streaming service or content provider. It accepts user-owned source details through Xtream Codes or M3U/M3U8, organizes them into one unified library or separate playlists, and presents Live TV, Movies, and Series with an advanced EPG. Catch-up/Replay is available only when supported by the content provider.

The specification combines practical capabilities expected from advanced IPTV players: adding and managing multiple sources, playlists, favorites, categories, advanced search, a time-based program guide, VOD details, resume playback, and remote-control-first TV navigation. It adds a performance, security, and compatibility-test layer designed for the differences across Samsung Tizen generations.

> ****Core architecture decision****
>
> The TV application is an independent Tizen Web client. It uses Samsung-supported APIs, especially AVPlay for advanced media playback. Video remains a direct stream from the user’s provider to the TV; the IsoaPlayerIPTV server must not proxy or restream content.

# Contents

- 1. Vision, Scope, and Constraints

- 2. Samsung Tizen Platform and Target Compatibility

- 3. User Experience and Interfaces

- 4. Functional Requirements

- 5. Media Playback and Program Guide

- 6. Source Management and Phone Pairing

- 7. Architecture, Data, Security, and Privacy

- 8. Performance and Quality Requirements

- 9. Testing and Acceptance Criteria

- 10. Release Plan and Deliverables

- 11. Risks and Open Decisions

- 12. Official Technical References

# 1. Vision, Scope, and Constraints

## 1.1 Vision

Provide a unified, fast, and easy IPTV viewing and management experience on the TV screen. The product should combine advanced flexibility for managing channels, libraries, and the program guide with the convenience of managing subscriptions from a phone, without relying on Android applications or assuming that Android apps can be installed on Tizen.

## 1.2 Product Goals

- Play live channels, movies, and series from IPTV sources that the user adds.

- Support both Xtream Codes and M3U/M3U8 connection types, with up to 9 independent connection profiles/sources in the first release.

- Provide an advanced EPG for up to 7 days, or as much as the source supplies; map channels to programs and expose Catch-up when available.

- Allow source management directly on the TV or through a securely paired phone page.

- Provide near-instant remote navigation, progressive data loading, and protection against UI freezes while processing large playlists.

- Build an independent application that can be signed and published through Samsung TV Seller Office, with real-device testing across different model years.

## 1.3 Primary User Personas

| **Persona** | **Need** |
| --- | --- |
| Everyday viewer | Open the app, resume viewing, and move quickly between channels and sections. |
| Multi-source user | Add 4-9 subscriptions, name them, enable or merge them, and refresh each source independently. |
| EPG and Catch-up user | See what is on now and next, open program details, and return to an earlier program when the source supports it. |
| Family administrator | Manage favorites, arrange sections, and optionally protect selected settings/sources with a PIN. |
| Phone user | Enter subscription details using the phone keyboard and send them to the TV without typing with the remote. |

## 1.4 In Scope

- Samsung Tizen TV application in WGT format, with Arabic RTL and English UI; French may be added later.

- Live TV, VOD, and Series player, plus favorites library, viewing history, and resume playback.

- Xtream Codes and M3U/M3U8 connectors; EPG in XMLTV or equivalent provider-supplied data.

- Management of up to 9 sources in release 1, plus a phone-compatible web page/portal for adding and managing sources.

- Backup import/export with credential protection, plus non-sensitive error messages and diagnostics.

- Compatibility, performance, and security testing on real devices, and preparation of a signed WGT package.

## 1.5 Out of Scope or Conditional

- Providing IPTV subscriptions, channels, movies, links, or ready-made login credentials.

- Restreaming video through product servers or storing content transferred from a provider.

- Bypassing encryption, DRM, geographic restrictions, or provider access controls.

- PVR recording or permanent downloads in release 1; consider later only if technical support and explicit rights exist.

- Guaranteeing every codec, protocol, or unusual format merely because a provider advertises it; support is subject to Samsung’s matrix and device testing.

- Copying source code, interfaces, logos, or protected visual identity from competing applications.

> ****Responsibility boundary****
>
> Users are responsible for the legality of their sources and subscriptions. IsoaPlayerIPTV only plays and manages content the user is entitled to access; it does not provide content, keys, or circumvention methods.

# 2. Samsung Tizen Platform and Target Compatibility

Implement IsoaPlayerIPTV as a Samsung TV Web application using HTML, CSS, JavaScript, and config.xml, then build and sign it as a WGT package. This is the documented TV Web application path; do not assume support for Android APK or TPK packages on Samsung TVs. [R1][R5][R6]

| **Model year** | **Listed Tizen version** | **Listed web engine** | **Test priority** |
| --- | --- | --- | --- |
| 2020 | Tizen 5.5 | Chromium M69 | Minimum baseline - high priority |
| 2021 | Tizen 6.0 | Chromium M76 | High priority |
| 2022 | Tizen 6.5 | Chromium M85 | High priority |
| 2023 | Tizen 7.0 | Chromium M94 | High priority |
| 2024 | Tizen 8.0 | Chromium M108 | Baseline testing |
| 2025 | Tizen 9.0 | Chromium M120 | Baseline testing |
| 2026 | Tizen 10.0 | Chromium M130 | Baseline testing |

Source: Samsung official tables for model years, Tizen versions, and web engines. Starting with the 2023 lineup, the installed OS version may change as a result of OS updates. Therefore, the app must not rely on model year alone; it must detect the actual platform version, web engine, and runtime capabilities. [R1][R2]

## 2.1 Compatibility Policy

- The 2020 / Tizen 5.5 model is the oldest supported baseline. Core functions must work there without assuming newer APIs are available.

- Target the Web UI for all model years 2020-2026. Codec, resolution, and frame-rate support must be determined from the actual model’s video specifications.

- Use a Capability Adapter to detect AVPlay, codecs, protocols, subtitle tracks, and available features instead of assuming all devices are identical.

- Test entry-level and lower-performance models, not only flagship devices. Record each device model, firmware, Tizen version, and web-engine version.

- Avoid heavy dependencies or JavaScript APIs unavailable in Chromium M69. Transpile/polyfill where required and verify on real hardware.

## 2.2 Media Player

Build a player layer based on Samsung AVPlay for advanced TV features. HTML5 video may be used as a fallback only if testing proves the use case is supported on the target model. Samsung recommends AVPlay for capabilities beyond HTML5 video, such as adaptive streaming, certain subtitle formats, and 4K. [R3]

- Play HLS/M3U8 and MPEG-DASH where supported by the platform; validate container type, codecs, and required HLS tags. [R1]

- Initialize media using prepareAsync rather than blocking the UI thread with synchronous preparation. [R3]

- Support seek, pause/resume, and audio/subtitle track switching when those tracks are available in the stream. [R3]

- Manage the full AVPlay lifecycle: open, prepare, play, stop, close, and handle buffering, error, and completion events. [R3]

- Do not claim 4K/HDR/HEVC, Dolby, or any codec compatibility until it has been checked against the actual year/model specifications and test source.

## 2.3 Platform Constraints to Respect

Samsung documentation identifies differences between model years in web engine, streaming, subtitles, and DRM capabilities. It also identifies PlayReady as deprecated and not recommended for new models, and Widevine Classic as unsupported since Tizen 4.0. The product must not rely on legacy DRM or assume all sources use the same protection method. [R1]

# 3. User Experience and Interfaces

## 3.1 Design Principles

- TV-distance interface: large controls, clear text, high contrast, and comfortable spacing.

- Full remote navigation without a mouse or touch input; the current focus must always be visible.

- Predictable behavior for directional keys, OK, and Back, respecting Samsung Back-key policy.

- Professional dark interface: black/charcoal, red accent, and white text, without glow or distracting effects.

- Progressive loading; do not block the interface while fetching data or refreshing EPG.

- Meaningful empty states and errors with a clear next action: retry, edit source, or view safe diagnostic details.

## 3.2 Main Navigation Map

| **Screen / section** | **Main content and functions** |
| --- | --- |
| Home | Continue Watching, recently watched, favorites, new additions from sources, source selection, quick access to Live / Movies / Series / EPG. |
| Live TV | Channel and group lists, search, filters by source/category/language, mini channel list during playback, quick channel switching. |
| EPG Guide | Now/Next, timeline grid, date selection, program details, progress bar, Catch-up button when available. |
| Movies | Posters, categories, search and filters, movie details, playback source, subtitle and audio selection. |
| Series | Series, seasons, episodes, episode ordering, next-episode continuation, resume position. |
| Favorites and History | Favorite channels/content, recently watched, Continue Watching, remove item or clear history. |
| Source Management | Add/edit/delete/test, enable/disable, reorder, merge or separate playlists, last refresh status. |
| Settings | Language, appearance, EPG and time zone, player, subtitles/audio, privacy, backup, PIN. |

## 3.3 Remote Control Rules

- Every interactive item must be reachable in a logical focus order; no item may be inaccessible using directional keys.

- OK opens the selected item or performs its action; Back closes the current layer before returning to the previous screen.

- Provide shortcuts only for keys documented and permitted by Samsung and the device; do not intercept reserved system keys.

- During playback: OK shows controls; Back presents a clear return option; arrows seek or navigate according to player mode.

- Restore the previous focus position after returning from another screen whenever possible.

## 3.4 Localization and Accessibility

- Full Arabic RTL, including menus, grids, dates, and errors; English LTR from release 1; French remains an addable option.

- Detect the time zone automatically with a manual override; do not assume XMLTV uses local time.

- Allow text-size and contrast adjustments without clipping long titles or channel names.

- Do not rely on color alone to indicate selection or error; also provide suitable text or an icon.

# 4. Functional Requirements

The requirements below use stable identifiers and MUST / SHOULD / COULD priorities. Every MUST requirement is mandatory for release 1 unless it is explicitly conditional on the content source or device capability.

## 4.1 Source and Subscription Management

| **ID** | **Priority** | **Requirement** |
| --- | --- | --- |
| FR-SRC-001 | MUST | The app shall allow up to 9 independent connection profiles/sources in release 1. |
| FR-SRC-002 | MUST | Support Xtream Codes using server address, port, username, and password, with an optional display name for the source. |
| FR-SRC-003 | MUST | Support M3U and M3U8 playlists by URL, and local-file import if testing of the Tizen file API succeeds on target devices. |
| FR-SRC-004 | MUST | Allow the user to add, edit, delete, disable, rename, and test a source from the TV interface. |
| FR-SRC-005 | MUST | Allow a source to be added, edited, or deleted from the phone through a secure pairing session, then present it for TV approval before saving. |
| FR-SRC-006 | MUST | Show each source status: not tested, connected, invalid credentials, DNS/TLS failure, timeout, or data-fetch failure. |
| FR-SRC-007 | MUST | Provide two modes: separate playlists per source, and a unified mode that merges sources while showing each item’s source. |
| FR-SRC-008 | MUST | Refreshing a source must not delete favorites, history, or data belonging to another source; use stable IDs and configurable matching. |
| FR-SRC-009 | SHOULD | Provide manual refresh and flexible scheduled refresh, with concurrency limits and pause/resume. |
| FR-SRC-010 | MUST | Show structural connection-test results separately from actual stream-playback tests; API success does not prove video playback success. |

## 4.2 Live TV and Channels

- FR-LIVE-001  [MUST]  Display channels by source, category, and favorites, with ascending, descending, or manual sorting.

- FR-LIVE-002  [MUST]  Provide instant name search, support Arabic and English, and normalize common Arabic character variants.

- FR-LIVE-003  [MUST]  Provide previous/next channel and a quick channel list that opens without leaving the player.

- FR-LIVE-004  [MUST]  Allow adding/removing favorites and optionally locking a category/channel with a PIN.

- FR-LIVE-005  [MUST]  Show channel logo, name, number, source, and program guide information when available.

- FR-LIVE-006  [MUST]  Remember the last channel and source, with an optional auto-start setting.

- FR-LIVE-007  [SHOULD]  Filter by quality, language, or source when the data is available.

- FR-LIVE-008  [MUST]  Clearly show Loading / Buffering / Disconnected states without freezing the UI.

## 4.3 Movies and Series (VOD)

- FR-VOD-001  [MUST]  Display movies and series in separate sections, with categories and source groups.

- FR-VOD-002  [MUST]  Show VOD details: name, poster, description, release year, genre, and duration when supplied by the source.

- FR-VOD-003  [MUST]  Manage series seasons and episodes, ordering episodes according to source data and never inventing missing episodes.

- FR-VOD-004  [MUST]  Resume movies and episodes from their previous position when time seeking is supported.

- FR-VOD-005  [MUST]  Store recently watched items and favorites locally and restore them after restart.

- FR-VOD-006  [SHOULD]  Suggest the next episode when an episode completes, with an option to disable autoplay.

- FR-VOD-007  [SHOULD]  Filter by year, genre, and rating when data exists; do not invent metadata.

## 4.4 Search and Categorization

- FR-SRCH-001  [MUST]  Unified search across channels, movies, and series, with filtering by type and source.

- FR-SRCH-002  [MUST]  Index progressively; users must see initial results without waiting for every source to finish loading.

- FR-SRCH-003  [SHOULD]  Provide a clearable recent-search history and options to exclude selected sources.

- FR-SRCH-004  [MUST]  Optionally deduplicate using provider IDs or item-data fingerprints, while allowing duplicate copies to remain visible.

## 4.5 Settings and Backup

- FR-SET-001  [MUST]  Save language, theme, time zone, section order, and player preferences.

- FR-SET-002  [MUST]  Provide an optional PIN to lock settings, sources, or selected categories, with a clear recovery path that does not depend on a hidden password.

- FR-SET-003  [MUST]  Export settings and sources as JSON; credentials must be encrypted with a password during export. Do not create an unencrypted secrets export by default.

- FR-SET-004  [MUST]  Import a backup only after validating structure and version, and provide preview plus replace/merge choices before writing.

- FR-SET-005  [SHOULD]  Migrate the database schema between app versions, with an automatic backup before upgrade.

# 5. Media Playback and Program Guide

## 5.1 Input Formats and Sources

| **Input** | **Requirements** |
| --- | --- |
| Xtream Codes | Compatible API connection; fetch live categories/streams, VOD categories/streams, series/categories/episodes, and EPG when the endpoint is available. |
| M3U/M3U8 playlist | Parse EXTINF, group-title, tvg-id, tvg-name, tvg-logo, and known Catch-up metadata; carefully handle UTF-8, BOM, and relative URLs. |
| EPG XMLTV | Separate URL or source attachment; map channel ID to tvg-id and normalize UTC/offset times. |
| Video stream | HLS/M3U8 and MPEG-DASH where the device supports them, plus direct HTTP(S) links with containers/codecs listed in Samsung specifications for the model. |
| Subtitles and audio | Embedded or external tracks in AVPlay-supported formats; subtitle synchronization and audio-track switching must be tested on-device. |

> ****Important distinction****
>
> M3U/M3U8 may refer to an IPTV playlist containing multiple links. M3U8 may also be an HLS playlist for a single video stream. The parser must identify the context and must not treat every M3U file as one video or necessarily as a channel list.

## 5.2 Advanced EPG

- FR-EPG-001  [MUST]  Show the current and next program for a channel, start/end times, and a progress bar relative to current time.

- FR-EPG-002  [MUST]  Show a timeline grid for at least the current day and allow previous/next days within available data, up to 7 days or the provider limit.

- FR-EPG-003  [MUST]  Support XMLTV and channel mapping through tvg-id, with a correction/manual-mapping UI when matching fails.

- FR-EPG-004  [MUST]  Handle time zones, daylight saving time, and UTC offsets without shifting a program by one hour due to incorrect interpretation.

- FR-EPG-005  [MUST]  Refresh EPG independently of VOD image fetching; cache by source and record the known refresh time.

- FR-EPG-006  [SHOULD]  Search program data by program title or description if the source supplies it.

- FR-EPG-007  [MUST]  Never fabricate a schedule when EPG is absent; show “No program guide data available.”

## 5.3 Catch-up / Replay / Timeshift

Catch-up is not a feature the player can create by itself. The provider must expose an archive or time-based URL and duration/date metadata. The app must understand Catch-up metadata declared in M3U or available Xtream settings/endpoints, construct the playback URL according to the provider’s specified template, and show a replay option only when availability can be verified.

- FR-CU-001  [MUST]  Show a Catch-up indicator for a program/channel only when the source declares archive support or valid data is available.

- FR-CU-002  [MUST]  Build a Replay URL using start time and duration or a known provider template, validating time boundaries.

- FR-CU-003  [MUST]  Provide date/time selection or EPG-program selection to start an archive when data is available.

- FR-CU-004  [MUST]  Handle archive-window expiration, unavailable programs, and server rejection without treating them as general app failures.

- FR-CU-005  [SHOULD]  Provide Restart/Start Over from the beginning when supported by the provider.

- FR-CU-006  [MUST]  Do not claim Catch-up is available on every channel; support varies by channel, provider, and permitted archive duration.

## 5.4 Player Controls

- Play/pause/resume/stop, reopen channel, seek forward/back for seekable content, and change picture-fit mode.

- Show channel/movie name, source, time, progress, buffering state, and available track controls.

- Select alternate audio or subtitles; enable/disable subtitles and adjust size/position within system capabilities.

- Handle buffering, errors, stream completion, network loss, timeouts, and limited retries.

- Ensure the screensaver is disabled during video playback as required by Samsung, and synchronize subtitles when available. [R4]

## 5.5 Media Compatibility Requirements

Build an actual test matrix for every format, codec, resolution, audio track, and subtitle format used in the target market. Samsung’s official matrix documents HLS, MPEG-DASH, seeking, multiple audio tracks, and subtitle support by engine/model; it does not replace testing reference files on real devices. [R1][R3]

# 6. Source Management and Phone Pairing

## 6.1 Add a Source from the TV

- Use a short wizard: select Xtream or M3U, enter details, test, select EPG, name the source, then save.

- Provide a TV-friendly keyboard and a show/hide password control.

- Allow at least 9 connection profiles and show used/remaining count.

- Do not refresh library content or delete user items until the new connection has been confirmed successful.

- Provide separate diagnostics for DNS, TLS, HTTP, credentials, API, or unsupported stream format.

## 6.2 Phone Pairing

Provide a responsive Companion Web/PWA page that works in a phone browser without mandatory installation. The TV starts a pairing session and displays a QR code plus a short one-time code. The phone opens the source-entry page and sends the connection profile to the TV. The TV then displays a source summary for approval before saving.

| **ID** | **Security / functional requirement** |
| --- | --- |
| FR-PHONE-001 | Create a random, short-lived pairing session (5 minutes by default); it expires automatically and cannot be reused. |
| FR-PHONE-002 | The QR code must not contain username, password, or a URL containing secrets; it contains only a session ID, public key, or pairing token. |
| FR-PHONE-003 | Encrypt the source payload end-to-end from phone to TV if Web Crypto or a trusted alternative is proven compatible with Tizen 5.5+; the transport intermediary must not be able to decrypt it. |
| FR-PHONE-004 | Require explicit approval on the TV before storing source details; scanning the QR code alone must not save anything. |
| FR-PHONE-005 | Revoke the session after successful transfer, rejection, or timeout, and prevent replay of the same payload. |
| FR-PHONE-006 | The optional intermediary must not store passwords in plaintext or log payload contents; delete packets after delivery or TTL. |
| FR-PHONE-007 | Provide a manual TV-entry fallback if pairing fails or the device does not support the required encryption. |
| FR-PHONE-008 | Serve the phone page over HTTPS with CSRF/CSP protection and request-rate limits. |

## 6.3 Pairing-Service Architecture Decision

The release 1 architecture does not require the Tizen TV to host a local server on a LAN port. The default option is a limited-function HTTPS Relay that transfers an end-to-end encrypted payload without inspecting it. Video playback remains direct from the provider to the TV. Direct local communication may be studied later, after the required network/listening APIs are proven in practice on each generation.

## 6.4 Backup and Transfer

- Export JSON with schemaVersion and stable IDs; import older backups through migrations.

- Encrypt backups containing credentials with a strong password; do not provide a default “export secrets in plaintext” function.

- Preview sources and channel counts before merge/replace; resolve ID conflicts without overwriting unintended data.

- Test power/app interruption during import; the operation must be atomic or recoverable.

# 7. Architecture, Data, Security, and Privacy

## 7.1 Proposed Architecture

| **Layer** | **Responsibility** |
| --- | --- |
| Tizen TV UI | Screens, remote navigation, focus, app state, languages, error display. |
| Application Core | Use cases, source management, search, favorites, history, settings, migrations. |
| Provider Adapters | Xtream connector, M3U parser, XMLTV importer, normalized channel and VOD data. |
| Media Engine Adapter | Unified interface over AVPlay/tested alternatives; lifecycle, tracks, seek, and error management. |
| Local Data Layer | IndexedDB or a supported/tested storage mechanism; local settings, indexes, and cache. |
| Optional Phone Companion + Relay | HTTPS phone page and short pairing sessions; transfer encrypted payload only, never video. |
| Observability | Local technical log without secrets; optional diagnostics with user consent. |

## 7.2 Engineering Rules

- Use clear modules and separate the application UI from provider connectors and media player.

- Use JavaScript/TypeScript with a build output compatible with the oldest target engine; do not ship untested syntax or Web APIs.

- Do not bind UI directly to provider responses; pass data through validated, normalized models.

- Use incremental refresh, pagination/chunking, and on-demand indexing; do not load every VOD image and all lists at once.

- Manage task, network, and player lifecycles when the app is suspended/resumed; cancel stale requests.

- Create unit tests for parsers/provider adapters and integration tests for AVPlay and real devices.

## 7.3 Core Data Model

| **Entity** | **Key fields** |
| --- | --- |
| SourceProfile | id, label, type, baseUrl, username/secretRef, enabled, createdAt, lastTest, epgConfig, sortOrder |
| Channel | stableId, sourceId, providerId, name, group, logo, streamUrlRef, tvgId, language, catchupCapabilities |
| Program | channelId, title, description, startUtc, endUtc, category, catchupReference |
| VodItem | stableId, sourceId, type, title, poster, description, year, duration, genres, streamRef |
| SeriesEpisode | seriesId, seasonNumber, episodeNumber, title, duration, streamRef |
| UserState | favorites, lastWatched, resumePosition, hiddenGroups, parentalSettings |
| AppSettings | locale, theme, timeZone, playerPreferences, epgRefresh, schemaVersion |

## 7.4 Security and Privacy

| **ID** | **Priority** | **Security / privacy requirement** |
| --- | --- | --- |
| SEC-001 | MUST | HTTPS is the default for all product and pairing-service connections. HTTP for legacy user sources is allowed only with a clear warning and informed consent. |
| SEC-002 | MUST | Never write passwords, session tokens, or secret-bearing stream URLs to logs, crash reports, or analytics. |
| SEC-003 | MUST | Mask/redact credentials in screens and diagnostics; do not place credentials in QR codes or phone-page URLs. |
| SEC-004 | MUST | Validate TLS certificates; do not disable validation or automatically accept self-signed certificates. |
| SEC-005 | MUST | Validate URLs, schemes, and redirect targets; prevent execution of HTML/JavaScript originating in channel names, EPG, or metadata. |
| SEC-006 | MUST | Use the least privileges possible in config.xml and document the reason for every required privilege. [R5] |
| SEC-007 | MUST | Protect the local PIN using an appropriately parameterized hash and rate-limit repeated guesses; never store the PIN in plaintext. |
| SEC-008 | MUST | The Relay must not decrypt source data or retain it beyond TTL; use rate limits, nonce, and one-time use. |
| SEC-009 | MUST | No behavioral tracking or telemetry by default; external diagnostics require explicit consent and an opt-out. |
| SEC-010 | MUST | Delete local app data on uninstall according to published Samsung requirements; provide clear source deletion inside the app. [R4] |

> ****Secret-storage note****
>
> Run an early technical spike to identify an approved, protectable secret-storage method on Tizen 5.5-10.0. Do not describe local database encryption as strong protection if its decryption key is stored beside it without adequate protection. If a device lacks a secure method, reduce retention duration and disclose the actual protection level to the user.

## 7.5 Stability and Fault Tolerance

- Network unavailable: show a clear notice, keep cached data visible, and provide controllable retry. [R4]

- Provider unavailable: do not block other sources; show a separate failure status for each source.

- Corrupt EPG or playlist: isolate invalid entries instead of failing the entire load.

- App update: migrate data safely with backup; do not lose favorites or viewing history.

- AVPlay failure: show an understandable reason and allow retry, source change, or return to the list.

# 8. Performance and Quality Requirements

Samsung sets a maximum app-launch time of 10 seconds and identifies 5 seconds as ideal. It also requires the app to run without freezing or crashing, notify the user when the network is disconnected, and handle media and subtitles correctly. Treat these as minimum requirements, with stricter product-specific goals below. [R4]

| **Metric** | **IsoaPlayerIPTV target** | **Measurement method** |
| --- | --- | --- |
| App launch | Target <= 5 seconds; must not exceed 10 seconds in Samsung testing. | From selecting the app icon to the first interactive screen; cold and warm launches. |
| First Home UI | <= 3 seconds from local cache after the first screen appears. | Time to first interactive content with saved data. |
| Remote response | p95 <= 150 ms in normal navigation; no focus jumps or accumulated lag. | From key event to visible focus update. |
| First list display | <= 3 seconds from a representative source cache; network updates remaining pages progressively. | Known reference dataset and time to first selectable items. |
| Stream start | Target <= 5 seconds p75 on test network and valid reference source; isolate provider latency. | From channel selection to first frame/audio, recording buffering. |
| Search | <= 500 ms p95 on a medium local index after indexing completes. | Channel/title search on a defined test dataset. |
| Playback stability | 4-hour continuous test without crash or growing memory leak that harms use. | Channel switching, pause/resume, and resource monitoring. |
| Library size | Load test with 9 sources and 30,000 total items using progressive indexing/display. | Response time, memory, and navigation on the lowest supported device. |

## 8.1 Performance Optimization Rules

- Do not load all channel, movie, and image lists before showing Home.

- Defer images and load them when visible; use thumbnails and a cache with a clear size limit.

- Update EPG in time/channel batches, cancel stale requests, and prevent duplicate work.

- Do not store all data in one large localStorage JSON object; separate settings from catalog and indexes.

- Do not perform heavy XML parsing or playlist processing on the UI thread without chunking or an approved mechanism.

- Limit parallel provider requests and use backoff on errors instead of repeated pressure.

- Clean up the media player, resources, images, and requests when changing screens or leaving content.

## 8.2 Non-Functional Quality Requirements

- NFR-REL: No unjustified loss of favorites or source settings after app closure or TV restart.

- NFR-COMP: Core functions work on Tizen 5.5 and later; optional features adapt to detected capabilities.

- NFR-UX: Every loading, error, or empty-data state has a visible representation and a user exit/action.

- NFR-MAINT: Modular architecture, tests, documentation, and change records; no secrets in the repository or build files.

- NFR-PRIV: No viewing data or credentials collected in the background without the user’s knowledge and consent.

- NFR-I18N: Arabic RTL and English are supported from release 1, with architecture for additional languages.

# 9. Testing and Acceptance Criteria

## 9.1 Device Matrix

| **Group** | **Minimum QA plan** |
| --- | --- |
| 2020 / Tizen 5.5 | At least one real entry/mid-range device; installation, launch, remote, and AVPlay tests. |
| 2021 / Tizen 6.0 | Real device; regression of basics, subtitles, and connectivity. |
| 2022 / Tizen 6.5 | Real device; full Live/VOD/EPG/Catch-up test suite. |
| 2023 / Tizen 7.0 | Real device; compatibility with potential OS updates. |
| 2024 / Tizen 8.0 | Real device; performance and media. |
| 2025 / Tizen 9.0 | Real device; current OS generation. |
| 2026 / Tizen 10.0 | Real device or latest available production device; regression testing. |

The emulator and TV Simulator are useful for UI and scenario testing, but they do not replace real devices for AVPlay, codecs, performance, networking, or Samsung-specific APIs. [R4][R7]

## 9.2 Required Test Suites

- Unit tests: M3U parser, XMLTV parser, mapping, time zone, Catch-up URL builder, normalizers, migrations.

- Integration tests: Xtream API variants, pagination, token/credential handling, error mapping, source isolation.

- Player tests: HLS MPEG-TS, HLS fMP4, DASH where supported, audio switching, subtitles, seek, buffering, stream completion.

- Remote tests: arrows/OK/Back, focus on all screens, return during playback, navigation among Live/VOD/Settings.

- Scale tests: 9 sources and 30,000 items, dense EPG, many logos, slow network, remote responsiveness during updates.

- Network interruption tests: during loading, during playback, on Catch-up start, and after reconnection.

- Security tests: log inspection, malicious URLs, HTML/JS in metadata, QR replay, session expiration, PIN brute-force attempts.

- Backup tests: corrupt file, old schema, wrong password, partial import, interruption during write.

- Lifecycle tests: app suspend/resume, sleep/wake, uninstall, and app-data deletion.

## 9.3 Main Acceptance Criteria (Definition of Done)

| **ID** | **Verifiable acceptance criterion** |
| --- | --- |
| AC-01 | Install the signed WGT package and launch successfully on a real device from every year/OS group in the test matrix. |
| AC-02 | Add 9 sources, mixing Xtream and M3U; edit, delete, disable, and test each source without affecting the others. |
| AC-03 | Load Live, Movies, and Series from authorized test sources with valid categories and data. |
| AC-04 | Import M3U with UTF-8, BOM, and tvg/group-title fields; handle a partially corrupt playlist without crashing. |
| AC-05 | Load XMLTV, map channels, and display Now/Next and timeline grid, testing time zones and daylight saving. |
| AC-06 | Catch-up works on a test channel with a real archive; when no archive exists, no invalid play button is shown. |
| AC-07 | Switch audio and subtitle tracks on supported device samples; no obvious synchronization loss. |
| AC-08 | Add a source from phone using QR and a short-lived session; TV approval, expiration, and replay protection work. |
| AC-09 | Credentials or secret URLs do not appear in logs, QR, crash reports, or unencrypted backups. |
| AC-10 | Launch within <=10 seconds in Samsung measurement, targeting <=5 seconds, and show the first UI without waiting for the full catalog. |
| AC-11 | Test 9 sources and 30,000 items without crashing; lists remain navigable and the remote remains responsive within the performance target. |
| AC-12 | Run continuously for 4 hours with repeated channel switching and no crash or harmful resource leak. |
| AC-13 | When the network is disconnected, show a clear message, keep cached data available, and resume refresh without duplicates or corruption. |
| AC-14 | Import/export works with encryption, wrong passwords, and older-version data; settings are not silently lost. |
| AC-15 | Complete Samsung Mandatory Quality Checklist, including network, media, screensaver, subtitles, performance, and privileges. |

## 9.4 Required Test Materials

- Legal, authorized test data for each connection type; other people’s accounts or links must not be used.

- One small and one large M3U playlist, UTF-8/BOM, Arabic names, multiple groups, logos, and varied Catch-up fields.

- XMLTV file with time zones, overlapping events, missing data, and unmatched tvg-id cases.

- Multi-track HLS and DASH samples, plus subtitle/audio samples for each codec planned for support.

- Per-device results matrix: model number, Model Code, Firmware, Tizen, Web Engine, installation test, startup time, format results, and failures.

# 10. Release Plan and Deliverables

## 10.1 Proposed Implementation Phases

| **Phase** | **Scope** | **Exit gate** |
| --- | --- | --- |
| P0 - Platform proof | Empty WGT project, version detection, AVPlay on Tizen 5.5 and a recent version, network, storage, remote keys. | Successfully play a reference video with audio and subtitles on a real 2020 device and a recent device; measure memory/performance. |
| P1 - Player MVP | Manage one source then 9; Xtream and M3U; Live/Movies/Series; search, favorites, local settings. | AC-01 to AC-04 and initial AC-10. |
| P2 - Program Guide | XMLTV, EPG grid, channel mapping, Catch-up according to provider metadata, subtitles and audio. | AC-05 to AC-07 on a test provider that supports them. |
| P3 - Companion | Phone page, QR, short session, end-to-end encryption/TV approval, encrypted backup. | AC-08, AC-09, AC-14, and independent security testing. |
| P4 - Optimization and Release | 9-source load, UX/performance optimization, model-year compatibility, publishing documentation. | Meet acceptance criteria and Samsung checklist; prepare Seller Office submission. |

## 10.2 Mandatory Project Deliverables

- Complete, organized source repository with clear build instructions and pinned dependency versions.

- Tizen Web project files: config.xml, HTML/CSS/JS, assets, and AVPlay layer.

- Signed, installable WGT package; private keys/certificates must not be included in the repository.

- Companion Web/PWA page and Relay components if adopted in P3, with API and deployment configuration documentation.

- Unit/integration/e2e tests and result reports on real devices; failures must be recorded, not hidden.

- Engineering/architecture document, data model, flow diagram, security/privacy policy, and user guide.

- Device/format compatibility list and codec/EPG/Catch-up matrix, with before/after performance measurements.

- Samsung Seller Office materials such as app details, screenshots, and UI description when publishing starts. [R6]

## 10.3 Release Policy

- Use MAJOR.MINOR.PATCH semantic versioning; each release includes a change log and data-migration requirements.

- Link each production build to a Git commit/tag, artifact fingerprint, and test results.

- Do not sign builds with developer keys in public CI; signing secrets must be kept outside the source repository.

- Run an internal release candidate before publishing; do not claim support for a device generation before testing a real device from that generation.

# 11. Risks and Open Decisions

## 11.1 Default Decisions Adopted by this Document

- Independent application built from scratch under the name IsoaPlayerIPTV; no prior project is assumed.

- Platform: Tizen Web App / WGT, not Android APK or TPK.

- Minimum: 2020 models and later, with Tizen 5.5 as the minimum representative version and runtime capabilities tested.

- Release 1 source limit: 9 manageable sources, with merge/separate modes.

- Phone pairing is optional but part of the full release requirements; short session and intermediary cannot read the payload.

- Content/video flows directly from the user’s provider to the TV; no stream proxy in the core architecture.

- Primary theme: dark charcoal/black with red and white, without glow effects.

## 11.2 Decisions Requiring Approval Before Coding

- Should Companion/Relay be part of release 1 or a later phase? Recommendation: build its UI and API contract in P1, launch in P3 after Tizen 5.5 crypto testing.

- Is the limit exactly 9 sources or should the architecture grow later? Recommendation: 9 in the release 1 UI with an extensible schema.

- Is USB M3U import mandatory? Recommendation: M3U URL first, then USB after proving the file API on real devices.

- Is commercial DRM required? Include only after defining the provider, DRM system, license, and Samsung approval.

- Which test devices are actually available? At least one 2020 or oldest-target Tizen device and one recent device are required before final design approval.

## 11.3 Risk Register

| **Risk / issue** | **Impact** | **Required mitigation** |
| --- | --- | --- |
| Differences in Web Engine and capabilities across Tizen model years | Crashes or unavailable APIs on older devices. | Test 2020 first; use Capability Adapter; avoid unguaranteed modern APIs. |
| Differences in Xtream/M3U provider behavior | Partially working sources or incompatible Catch-up. | Provider adapters, varied legal samples, detailed diagnostics, and no assumption of universal compatibility. |
| Large channel lists and EPG | Slow loading and remote lag. | Chunked loading, indexing, bounded cache, and tests at 9 sources / 30k items. |
| Local storage of subscription secrets | Credential exposure if device data is extracted or compromised. | Prove secure storage on Tizen 5.5+; minimize retention; redact logs; disclose protection limits. |
| Pairing encryption on older browser | Required Crypto APIs may be unavailable in the app environment. | Spike on M69; choose compatible standard algorithms; prohibit weak fallback; retain manual entry. |
| DRM licensing and broadcast rights | Publishing rejection or failure to play protected content. | Neutral player; no bundled content; DRM only with license and Samsung review. |
| Samsung Store policy and publication availability | Requirements vary by country, category, or review. | Verify Seller Office and country requirements before submission; do not assume pre-approval. |
| Performance differences among TV tiers | Good performance on premium models but poor on entry-level devices. | Real-device matrix and performance thresholds on the weakest supported device. |

> ****Final completion criterion****
>
> IsoaPlayerIPTV is not complete merely because the UI appears or one source connects. The release is complete when functional requirements are met, playback/EPG/Catch-up tests pass with a suitable test provider, navigation remains responsive with 9 sources and a large catalog, and results are documented for every targeted device.

# 12. Official Technical References

The following references establish Samsung platform boundaries and quality requirements. All links are official Samsung Developer or Samsung TV Seller Office sources; verification date recorded in the source baseline: 16 November 2026.

**[R1] Samsung Developer - General Specifications**

Tizen versions by model year; media, streaming, HLS/DASH, subtitle, and DRM capabilities.  https://developer.samsung.com/smarttv/develop/specifications/general-specifications.html

**[R2] Samsung Developer - Web Engine Specifications**

Chromium and web-engine versions by model year.  https://developer.samsung.com/smarttv/develop/specifications/web-engine-specifications.html

**[R3] Samsung Developer - Playback Using AVPlay**

AVPlay lifecycle, asynchronous preparation, buffering events, seek, and audio tracks.  https://developer.samsung.com/smarttv/develop/guides/multimedia/media-playback/using-avplay.html

**[R4] Samsung Developer - Mandatory Features for Quality**

Mandatory quality requirements: app stability, network, media, subtitles, screensaver, and launch time.  https://developer.samsung.com/smarttv/develop/development-checklist/mandatory-features.html

**[R5] Samsung Developer - Configuring Web Applications**

config.xml, app ID/version, and privileges required by Web applications.  https://developer.samsung.com/smarttv/develop/guides/fundamentals/configuring-tv-applications.html?device=htv

**[R6] Samsung TV Seller Office - Application Publication Process**

WGT package preparation and app information/assets required for publication.  https://developer.samsung.com/tv-seller-office/application-publication-process.html

**[R7] Samsung Developer - Application Testing Q&A**

Samsung TV testing limitations, WGT vs TPK support, and real-device testing.  https://developer.samsung.com/smarttv/develop/faq/application-testing.html

## Closing Note

This document is a requirements baseline that can be converted into a backlog and acceptance tests. It does not mean the application has been built, tested, or approved by Samsung. Any claim of compatibility, performance, codec support, or Catch-up capability must be supported by a test record for an actual device/model and an authorized content source, with results attached.

---

*Markdown edition generated from the approved English Word baseline. Requirement wording, identifiers, priorities, totals, statuses, and acceptance criteria have been preserved; layout has been converted for Markdown readability.*
