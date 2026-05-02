# Vestigo Roadmap

This document outlines the planned development phases for Vestigo. Each phase builds on the previous one and represents a releasable milestone.

Status markers:
- `- [x]` -- complete
- `- in progress` -- actively being worked on
- `- [ ]` -- not yet started

---

## Overall Progress

![Overall](https://progress-bar.xyz/18/?title=Overall&width=400&style=flat)

---

## Phase 1 -- Foundation

![Phase 1](https://progress-bar.xyz/80/?title=Phase+1&width=400&style=flat)

Core infrastructure and basic email analysis. Target: first usable build.

- [x] Project scaffold (Tauri 2 + React + TypeScript)
- [x] Rust module structure and Cargo.toml dependencies
- [x] React UI shell: three-panel layout (email tree / main content / analysis)
- [x] Local file ingestion: EML, HTML, TXT, PDF
- [x] SQLite schema: emails, accounts, watched folders, known-good URLs, flag colour names
- [x] Ingest-and-store: all ingested emails copied to internal storage and indexed
- [x] Left panel: inbox view grouped by date (Today / Yesterday / Day+Date / Last Week / Last Month / Older / Deleted)
- [x] Left panel: unresolved emails shown bold with colour accent bar
- [x] Left panel: clicking an email marks it as resolved after 5 seconds
- [x] Left panel: context menu -- Mark as Resolved, Mark as Unresolved, Delete, Flag
- [x] Left panel: Delete moves email to Deleted section, not permanently removed
- [x] Left panel: expand arrow on right side of tile, reveals attachment tree
- [x] Left panel: nested emails treated as expandable folders, clickable separately
- [x] Left panel: type colour coding -- EML/MSG blue, PDF red, HTML green, TXT grey
- [x] Left panel: bordered tiles per type colour
- [x] Multi-file open via dialog (Ctrl+O)
- [x] Open Folder with directory scan modal and confirm/cancel
- [x] Attachment hash display (SHA-256, SHA-1) in analysis panel
- [x] Known-good URL library with per-email classification
- [x] Links in Document section with Copy URL, Copy Domain, Add to Known Good actions
- [x] Domain summary chips per email (click to copy)
- [x] Authentication header interpretation: SPF, DKIM, ARC with pass/fail/warn badges
- [ ] Left panel: parent email remains accented if any child is unresolved
- [ ] Left panel: children can be flagged independently (context menu flag only, no delete)
- [ ] Left panel: colour flags on emails (8 colours, user-nameable in settings)
- [ ] Drag and drop EML/MSG/PDF/HTML/TXT onto the window to ingest
- [ ] Newly ingested file sorted by email timestamp, list scrolls to it
- [ ] Search bar: filter by sender, recipient, subject, flag colour
- [ ] Copy-on-click for all key string values (subject, from, to, hashes, body text, IOCs)
- [ ] Full header viewer (toggle to see all raw headers)
- [ ] Settings window: mail accounts, watched folders, flag colour names, general preferences

---

## Phase 2 -- Header and Authentication Analysis

![Phase 2](https://progress-bar.xyz/10/?title=Phase+2&width=400&style=flat)

- [x] SPF result parsing from Received-SPF header
- [x] DKIM signature detection
- [x] ARC chain detection and auth result parsing
- [ ] Full SPF validation via DNS lookup
- [ ] Full DKIM signature cryptographic verification
- [ ] Full DMARC policy lookup and validation
- [ ] Email timeline reconstruction from Received: header chain
- [ ] Sender / routing anomaly highlighting
- [ ] Return-Path vs From domain mismatch detection

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

## Phase 9 -- Connector and Add-on System

![Phase 9](https://progress-bar.xyz/0/?title=Phase+9&width=400&style=flat)

A plugin registry allowing third-party connectors to extend Vestigo with new panels,
analysis steps, and data sources.

- [ ] Connector API surface and plugin registry
- [ ] Claude AI connector: pipe email body/IOCs to Claude API for threat assessment panel
- [ ] Custom pane support: connectors can register additional panels
- [ ] VirusTotal as a swappable connector (replaces direct integration)
- [ ] Splunk / SIEM output connector
- [ ] TheHive / MISP integration connector
- [ ] Generic webhook connector (fire payload to any URL on analysis)
- [ ] Connector marketplace / registry documentation

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
separate sandboxes to share resolved/unresolved and flag state.

- Only state metadata is exchanged -- no email content, headers, or attachments
- Communication is encrypted (noise protocol or mutual TLS)
- Each instance identified by a key pair generated on first run
- Peers added manually via the settings window
- Easter egg has been laid

---

## Release Targets

| Milestone | Phases | Description | Progress |
|---|---|---|---|
| v0.1.0 -- Alpha | 1, 2 | Inbox view, file ingestion, header and auth analysis | ![](https://progress-bar.xyz/30/?style=flat&width=120) |
| v0.2.0 | 3, 4 | Redirect tracing, attachment analysis, hash lookups | ![](https://progress-bar.xyz/0/?style=flat&width=120) |
| v0.3.0 | 5, 6 | Threat intel and OSINT enrichment | ![](https://progress-bar.xyz/0/?style=flat&width=120) |
| v0.4.0 | 7 | Live mail source integrations, settings window | ![](https://progress-bar.xyz/0/?style=flat&width=120) |
| v0.5.0 | 9 | Connector and add-on system | ![](https://progress-bar.xyz/0/?style=flat&width=120) |
| v1.0.0 | 8 | Corpus analysis, campaign detection, report export | ![](https://progress-bar.xyz/0/?style=flat&width=120) |
| v1.1.0 | -- | Secure cross-sandbox network sync + easter eggs | ![](https://progress-bar.xyz/0/?style=flat&width=120) |
