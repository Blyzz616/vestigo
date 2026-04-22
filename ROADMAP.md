# Vestigo Roadmap

This document outlines the planned development phases for Vestigo. Each phase builds on the previous one and represents a releasable milestone.

Status markers:
- `[done]` -- complete
- `[in progress]` -- actively being worked on
- `[planned]` -- not yet started

---

## Overall Progress

![Overall](https://progress-bar.xyz/8/?title=Overall&width=400&style=flat)

---

## Phase 1 -- Foundation

![Phase 1](https://progress-bar.xyz/38/?title=Phase+1&width=400&style=flat)

Core infrastructure and basic email analysis. Target: first usable build.

- [done] Project scaffold (Tauri 2 + React + TypeScript)
- [done] Rust module structure and Cargo.toml dependencies
- [done] React UI shell: three-panel layout (email tree / main content / analysis)
- [planned] Local file ingestion: EML, MSG, HTML, TXT
- [planned] MIME parsing and nested RFC822 support
- [planned] Hierarchical email panel with expandable attachment folders
- [planned] Email header extraction and display
- [planned] Hyperlink extraction from email body and attachments at all nesting levels

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
- [planned] Attachment hash computation: MD5 and SHA-256
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

- [planned] Microsoft 365 via MS Graph API (Mail.Read scope, MSAL auth)
- [planned] Google Workspace via Gmail API (gmail.readonly scope, OAuth2)
- [planned] Exchange Server on-premises via EWS/SOAP

---

## Phase 8 -- Corpus Analysis and Reporting

![Phase 8](https://progress-bar.xyz/0/?title=Phase+8&width=400&style=flat)

- [planned] Similarity scoring across ingested email corpus
- [planned] Phishing campaign clustering and surfacing
- [planned] One-click investigation report export (PDF)
- [planned] One-click investigation report export (Markdown)

---

## Future / Unscheduled

Ideas that are on the radar but not yet assigned to a phase:

- Theme support: dark mode, light mode, and OS-linked automatic switching
- YARA rule matching against email bodies and attachments
- Sandboxed attachment detonation via external API (e.g. Any.run, Hybrid Analysis)
- MITRE ATT&CK technique tagging
- Configurable alert rules and watchlists
- Team / shared investigation mode

---

## Release Targets

| Milestone | Phases | Description |
|---|---|---|
| v0.1.0 -- Alpha | 1, 2 | Local file ingestion, header analysis, link extraction |
| v0.2.0 | 3, 4 | Redirect tracing, attachment analysis, hash lookups |
| v0.3.0 | 5, 6 | Threat intel and OSINT enrichment |
| v0.4.0 | 7 | Live mail source integrations |
| v1.0.0 | 8 | Corpus analysis, campaign detection, report export |
