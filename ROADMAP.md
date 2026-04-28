# Vestigo Roadmap

This document outlines the planned development phases for Vestigo. Each phase builds on the previous one and represents a releasable milestone.

Status markers:
- `- [x]` -- complete
- `- in progress` -- actively being worked on
- `- [ ]` -- not yet started

---

## Overall Progress

![Overall](https://progress-bar.xyz/10/?title=Overall&width=400&style=flat)

---

## Phase 1 -- Foundation

![Phase 1](https://progress-bar.xyz/50/?title=Phase+1&width=400&style=flat)

Core infrastructure and basic email analysis. Target: first usable build.

- [x] Project scaffold (Tauri 2 + React + TypeScript)
- [x] Rust module structure and Cargo.toml dependencies
- [x] React UI shell: three-panel layout (email tree / main content / analysis)
- [x] Local file ingestion: EML, HTML, TXT, PDF
- [x] SQLite schema: emails, accounts, watched folders, known-good URLs
- [x] Ingest-and-store: all ingested emails copied to internal storage and indexed
- [x] Left panel: inbox view grouped by date (Today / Yesterday / Day+Date / Last Week / Last Month / Older / Deleted)
- [x] Left panel: unactioned emails shown bold with blue accent
- [x] Left panel: clicking an email marks it as actioned after 5 seconds
- [x] Left panel: context menu -- Mark as Resolved, Mark as Unresolved, Delete
- [x] Left panel: Delete moves email to Deleted section, not permanently removed
- [x] Attachment hash display (SHA-256, SHA-1) in analysis panel
- [x] Known-good URL library with per-email classification
- [x] Domain summary per email
- in progress Left panel: email entries expandable as folders when attachments present
- in progress Left panel: nested emails treated as expandable folders, clickable separately
- in progress Left panel: parent email remains accented if any child is unresolved
- [ ] Left panel: children cannot be deleted -- only top-level emails
- [ ] Left panel: children can be flagged independently
- [ ] Left panel: colour flags on emails (8 colours, user-nameable in settings)
- [ ] Left panel: context menu flag submenu for all items
- [ ] Left panel: right-click on children -- flag options only (no delete)
- [ ] Drag and drop EML/MSG/PDF/HTML/TXT onto the window to ingest
- [ ] Ctrl+O and File > Open for ad-hoc ingestion
- [ ] Newly ingested file sorted by email timestamp, list scrolls to it
- [ ] Search bar: filter by sender, recipient, subject, flag colour
- [ ] Copy-on-click for all key string values (subject, from, to, hashes, body text, IOCs)
- [ ] Global font size: Ctrl+Plus / Ctrl+Minus / Ctrl+Scroll; Shift limits to pane under mouse
- [ ] Full header viewer (toggle to see all raw headers)
- [ ] Envelope / Return-Path address shown alongside From in header display
- [ ] Disable default WebView context menu globally
- [ ] Known-good library: support root domain (covers all subdomains) and specific subdomain entries
- [ ] Settings window: mail accounts, watched folders, flag colour names, general preferences

---

## Phase 2 -- Header and Authentication Analysis

![Phase 2](https://progress-bar.xyz/0/?title=Phase+2&width=400&style=flat)

- [ ] SPF validation
- [ ] DKIM validation
- [ ] DMARC validation
- [ ] Email timeline reconstruction from Received: header chain
- [ ] Sender / routing anomaly highlighting

---

## Phase 3 -- Link and Redirect Analysis

![Phase 3](https://progress-bar.xyz/0/?title=Phase+3&width=400&style=flat)

- [ ] HTTP redirect chain tracing (hop-by-hop to final destination)
- [ ] Toggleable link preview panel
- [ ] Headless screenshot capture of linked URLs (chromiumoxide)
- [ ] URL deobfuscation (encoded characters, URL shorteners)

---

## Phase 4 -- File and Attachment Analysis

![Phase 4](https://progress-bar.xyz/0/?title=Phase+4&width=400&style=flat)

- [ ] PDF content and metadata extraction (lopdf)
- [ ] Attachment hash computation: SHA-256 and SHA-1
- [ ] VirusTotal hash lookup
- [ ] IOC extraction: IP addresses, domains, file hashes, Bitcoin addresses, CVEs
- [ ] SQLite local cache for hashes and reputation results

---

## Phase 5 -- Threat Intelligence Integration

![Phase 5](https://progress-bar.xyz/0/?title=Phase+5&width=400&style=flat)

- [ ] VirusTotal API: domain reputation and file hash queries
- [ ] URLhaus / Abuse.ch feed (offline-capable local mirror)
- [ ] AbuseIPDB: IP reputation queries
- [ ] WHOIS lookups with historical record display
- [ ] Domain reputation scoring and flagging

---

## Phase 6 -- OSINT Enrichment

![Phase 6](https://progress-bar.xyz/0/?title=Phase+6&width=400&style=flat)

- [ ] Shodan integration
- [ ] IPInfo integration
- [ ] GreyNoise integration
- [ ] Consolidated OSINT panel per IOC

---

## Phase 7 -- Mail Source Integrations

![Phase 7](https://progress-bar.xyz/0/?title=Phase+7&width=400&style=flat)

Vestigo connects to mailboxes read-only. Emails are downloaded and stored locally;
copies are left on the server. Multiple accounts from different providers can be
configured simultaneously via the settings window.

- [ ] Settings window: add / remove / enable / disable mail accounts
- [ ] Microsoft 365 via MS Graph API (Mail.Read scope, MSAL auth)
- [ ] Gmail via Gmail API (gmail.readonly scope, OAuth2)
- [ ] Yahoo Mail and other providers via IMAP (readonly)
- [ ] Generic IMAP support
- [ ] Exchange Server on-premises via EWS/SOAP
- [ ] Monitored folder support: watch one or more local directories for new EML files
- [ ] Background polling with configurable interval per account
- [ ] In-app notification for new mail

---

## Phase 8 -- Corpus Analysis and Reporting

![Phase 8](https://progress-bar.xyz/0/?title=Phase+8&width=400&style=flat)

- [ ] Similarity scoring across ingested email corpus
- [ ] Phishing campaign clustering and surfacing
- [ ] One-click investigation report export (PDF)
- [ ] One-click investigation report export (Markdown)

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
