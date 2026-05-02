# Vestigo

A cross-platform desktop application for phishing email investigation and analysis.

Vestigo ingests emails from Microsoft 365, Google Workspace, Exchange Server, and local files, then performs deep security analysis without opening files in native applications. It is built with Tauri 2 (Rust backend, React/TypeScript frontend) and is designed for security analysts, incident responders, and threat intelligence teams.

> The name comes from the Latin *vestigare* -- to track, trace, and investigate.

![Overall Progress](https://progress-bar.xyz/18/?title=Overall+Progress&width=400&style=flat)

---

## Features

### Email Ingestion
- Local file support: EML, MSG, PDF, HTML, TXT
- Microsoft 365 via MS Graph API (Mail.Read scope)
- Google Workspace via Gmail API (gmail.readonly scope)
- Exchange Server / EWS (planned -- see roadmap)

### Email Analysis
- Hierarchical email panel with nested attachments as expandable folders
- Full MIME and nested RFC822 parsing at any nesting level
- Complete email header extraction and display
- SPF, DMARC, and DKIM validation
- Email timeline reconstructed from Received: header chain

### Link Analysis
- Extraction of all hyperlinks from emails and attachments at any nesting level
- HTTP redirect chain tracing (hop-by-hop to final destination)
- Toggleable link preview
- Headless screenshot capture of linked URLs

### Threat Intelligence
- Domain reputation analysis with historical records
- Attachment hash analysis (SHA-256 / MD5) queried against VirusTotal
- IOC extraction: IP addresses, domains, file hashes, Bitcoin addresses, CVEs
- URLhaus / Abuse.ch feed integration (offline-capable)
- AbuseIPDB for IP reputation

### OSINT Enrichment
- Shodan
- IPInfo
- GreyNoise

### Reporting
- One-click investigation report export (PDF or Markdown)
- Similarity scoring across email corpus to surface phishing campaigns

---

## Tech Stack

| Layer | Technology |
|---|---|
| Desktop shell | Tauri 2 |
| Frontend | React + TypeScript (Vite) |
| Backend | Rust |
| Async runtime | tokio |
| Email parsing | mail-parser |
| SPF / DKIM / DMARC | mail-auth |
| DNS resolution | hickory-resolver |
| HTML parsing | scraper |
| HTTP / redirect tracing | reqwest |
| HTML sanitization | ammonia |
| PDF extraction | lopdf |
| Local cache / reputation DB | rusqlite (SQLite) |
| WHOIS lookups | whois-rust |
| Headless browser | chromiumoxide |

---

## API Keys

Vestigo integrates with several external services. None are required to run the application, but functionality will be limited without them.

| Service | Purpose | Free Tier |
|---|---|---|
| VirusTotal | File hash and domain reputation | Yes (limited) |
| AbuseIPDB | IP reputation | Yes |
| Shodan | OSINT / host intelligence | Yes (limited) |
| IPInfo | IP geolocation and ASN | Yes |
| GreyNoise | IP noise classification | Yes |

API keys are entered in the application settings and stored locally. They are never transmitted anywhere other than the relevant service.

---

## Project Structure

```
vestigo/
  src/                  React/TypeScript frontend
  src-tauri/            Rust backend
    src/
      main.rs           Tauri entry point
      lib.rs            Tauri command registration
      types.rs          Shared data structures
      ingest/           Local file ingestion (EML, MSG, PDF, HTML, TXT)
      email/            Email parsing and header analysis
      analysis/         Link extraction, IOC detection, redirect tracing
      intel/            Threat intelligence integrations
      osint/            OSINT enrichment
      mail_sources/     Microsoft 365, Google Workspace connectors
      db/               SQLite cache and reputation database
  public/               Static frontend assets
```

---

## Planned Progression

| Milestone | Phases | Description | Progress |
|---|---|---|---|
| v0.1.0 -- Alpha | 1, 2 | Local file ingestion, header and auth analysis | ![](https://progress-bar.xyz/30/?style=flat&width=120) |
| v0.2.0 | 3, 4 | Redirect tracing, attachment analysis, hash lookups | ![](https://progress-bar.xyz/0/?style=flat&width=120) |
| v0.3.0 | 5, 6 | Threat intel and OSINT enrichment | ![](https://progress-bar.xyz/0/?style=flat&width=120) |
| v0.4.0 | 7 | Live mail source integrations | ![](https://progress-bar.xyz/0/?style=flat&width=120) |
| v1.0.0 | 8 | Corpus analysis, campaign detection, report export | ![](https://progress-bar.xyz/0/?style=flat&width=120) |

---

## Roadmap

See [ROADMAP.md](ROADMAP.md) for the full phased development plan.

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

---

## License

MIT -- see [LICENSE](LICENSE).
