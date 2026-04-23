# Vestigo Roadmap

This document outlines the planned development phases for Vestigo. Each phase builds on the previous one and represents a releasable milestone.

Status markers:
- `[done]` -- complete
- `[in progress]` -- actively being worked on
- `[planned]` -- not yet started

---

## Overall Progress

![Overall](https://progress-bar.xyz/10/?title=Overall&width=400&style=flat)

---

## Phase 1 -- Foundation

![Phase 1](https://progress-bar.xyz/50/?title=Phase+1&width=400&style=flat)

Core infrastructure and basic email analysis. Target: first usable build.

- [done] Project scaffold (Tauri 2 + React + TypeScript)
- [done] Rust module structure and Cargo.toml dependencies
- [done] React UI shell: three-panel layout (email tree / main content / analysis)
- [done] Local file ingestion: EML, HTML, TXT, PDF
- [done] SQLite schema: emails, accounts, watched folders, known-good URLs
- [done] Ingest-and-store: all ingested emails copied to internal storage and indexed
- [done] Left panel: inbox view grouped by date (Today / Yesterday / Day+Date / Last Week / Last Month / Older / Deleted)
- [done] Left panel: unactioned emails shown bold with blue accent
- [done] Left panel: clicking an email marks it as actioned after 5 seconds
- [done] Left panel: context menu -- Mark as Resolved, Mark as Unresolved, Delete
- [done] Left panel: Delete moves email to Deleted section, not permanently removed
- [done] Attachment hash display (SHA-256, SHA-1) in analysis panel
- [done] Known-good URL library with per-email classification
- [done] Domain summary per email
- [in progress] Left panel: email entries expandable as folders when attachments present
- [in progress] Left panel: nested emails treated as expandable folders, clickable separately
- [in progress] Left panel: parent email remains accented if any child is unresolved
- [planned] Left panel: children cannot be deleted -- only top-level emails
- [planned] Left panel: children can be flagged independently
- [planned] Left panel: colour flags on emails (8 colours, user-nameable in settings)
- [planned] Left panel: context menu flag submenu for all items
- [planned] Left panel: right-click on children -- flag options only (no delete)
- [planned] Drag and drop EML/MSG/PDF/HTML/TXT onto the window to ingest
- [planned] Ctrl+O and File > Open for ad-hoc ingestion
- [planned] Newly ingested file sorted by email timestamp, list scrolls to it
- [planned] Search bar: filter by sender, recipient, subject, flag colour
- [planned] Copy-on-click for all key string values (subject, from, to, hashes, body text, IOCs)
- [planned] Global font size: Ctrl+Plus / Ctrl+Minus / Ctrl+Scroll; Shift limits to pane under mouse
- [planned] Full header viewer (toggle to see all raw headers)
- [planned] Envelope / Return-Path address shown alongside From in header display
- [planned] Disable default WebView context menu globally
- [planned] Known-good library: support root domain (covers all subdomains) and specific subdomain entries
- [planned] Settings window: mail accounts, watched folders, flag colour names, general preferences

---

## Phase 2 -- Header and Authentication Analysis

![Phase 2](https://progress-bar.xyz/0/?title=Phase+2&width=400&style=flat)

- [planned] SPF validation
- [planned] DKIM validation
- [planned] DMARC validation
- [planned] Email timeline reconstruction from Received: header chain
- [planned] Sender / routing anomaly highlighting

---

## Phase 3 -- Link and Redirect Analysis

![Phase 3](https://progress-bar.xyz/0/?title=Phase+3&width=400&style=flat)

- [planned] HTTP redirect chain tracing (hop-by-hop to final destination)
- [planned] Toggleable link preview panel
- [planned] Headless screenshot capture of linked URLs (chromiumoxide)
- [planned] URL deobfuscation (encoded characters, URL shorteners)

---

## Phase 4 -- File and Attachment Analysis

![Phase 4](https://progress-bar.xyz/0/?title=Phase+4&width=400&style=flat)

- [planned] PDF content and metadata extraction (lopdf)
- [planned] Attachment hash computation: SHA-256 and SHA-1
- [planned] VirusTotal hash lookup
- [planned] IOC extraction: IP addresses, domains, file hashes, Bitcoin addresses, CVEs
- [planned] SQLite local cache for hashes and reputation results

---

## Phase 5 -- Threat Intelligence Integration

![Phase 5](https://progress-bar.xyz/0/?title=Phase+5&width=400&style=flat)

- [planned] VirusTotal API: domain reputation and file hash queries
- [planned] URLhaus / Abuse.ch feed (offline-capable local mirror)
- [planned] AbuseIPDB: IP reputation queries
- [planned] WHOIS lookups with historical record display
- [planned] Domain reputation scoring and flagging

---

## Phase 6 -- OSINT Enrichment

![Phase 6](https://progress-bar.xyz/0/?title=Phase+6&width=400&style=flat)

- [planned] Shodan integration
- [planned] IPInfo integration
- [planned] GreyNoise integration
- [planned] Consolidated OSINT panel per IOC

---

## Phase 7 -- Mail Source Integrations

![Phase 7](https://progress-bar.xyz/0/?title=Phase+7&width=400&style=flat)

Vestigo connects to mailboxes read-only. Emails are downloaded and stored locally;
copies are left on the server. Multiple accounts from different providers can be
configured simultaneously via the settings window.

- [planned] Settings window: add / remove / enable / disable mail accounts
- [planned] Microsoft 365 via MS Graph API (Mail.Read scope, MSAL auth)
- [planned] Gmail via Gmail API (gmail.readonly scope, OAuth2)
- [planned] Yahoo Mail and other providers via IMAP (readonly)
- [planned] Generic IMAP support
- [planned] Exchange Server on-premises via EWS/SOAP
- [planned] Monitored folder support: watch one or more local directories for new EML files
- [planned] Background polling with configurable interval per account
- [planned] In-app notification for new mail

---

## Phase 8 -- Corpus Analysis and Reporting

![Phase 8](https://progress-bar.xyz/0/?title=Phase+8&width=400&style=flat)

- [planned] Similarity scoring across ingested email corpus
- [planned] Phishing campaign clustering and surfacing
- [planned] One-click investigation report export (PDF)
- [planned] One-click investigation report export (Markdown)

---

## Future / Unscheduled

- Theme support: dark mode, light mode, and OS-linked automatic switching
- YARA rule matching against email bodies and attachments
- Sandboxed attachment detonation via external API (e.g. Any.run, Hybrid Analysis)
- MITRE ATT&CK technique tagging
- Configurable alert rules and watchlists

---

## v1.1 -- Network Sync

A secure peer-to-peer sync layer allowing multiple Vestigo instances running in
separate sandboxes to share actioned/unactioned and flag state.

- Only state metadata is exchanged -- no email content, headers, or attachments
- Communication is encrypted (noise protocol or mutual TLS)
- Each instance identified by a key pair generated on first run
- Peers added manually via the settings window

---

## Release Targets

| Milestone | Phases | Description | Progress |
|---|---|---|---|
| v0.1.0 -- Alpha | 1, 2 | Inbox view, file ingestion, header and auth analysis | ![](https://progress-bar.xyz/10/?style=flat&width=120) |
| v0.2.0 | 3, 4 | Redirect tracing, attachment analysis, hash lookups | ![](https://progress-bar.xyz/0/?style=flat&width=120) |
| v0.3.0 | 5, 6 | Threat intel and OSINT enrichment | ![](https://progress-bar.xyz/0/?style=flat&width=120) |
| v0.4.0 | 7 | Live mail source integrations, settings window | ![](https://progress-bar.xyz/0/?style=flat&width=120) |
| v1.0.0 | 8 | Corpus analysis, campaign detection, report export | ![](https://progress-bar.xyz/0/?style=flat&width=120) |
| v1.1.0 | -- | Secure cross-sandbox network sync | ![](https://progress-bar.xyz/0/?style=flat&width=120) |
