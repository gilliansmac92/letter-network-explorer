# Letter Network Explorer

An interactive, single-page dashboard for exploring correspondence networks in Scotland during the 1688–1692 Revolution.

**[View the live dashboard →](https://gilliansmac92.github.io/letter-network-explorer/)**

---

## About the Project

This dashboard visualises over 2,500 letters exchanged by individuals across Scotland, England, and Ireland during one of the most turbulent periods in Scottish history — the Williamite Revolution and its aftermath (1688–1692). The letters are drawn from a range of manuscript and printed collections held in Scottish archives, including the Hamilton and Brandon papers, the Leven & Melville Papers, and the Breadalbane Correspondence.

The goal is to make this rich historical network explorable: who wrote to whom, how often, from where, and across which years.

---

## Dashboard Sections

| Section | What it shows |
|---|---|
| **Overview** | Key statistics (total letters, unique people, collections), letters-per-year bar chart, and top senders/receivers tables |
| **Correspondence Progression** | Stacked bar chart by collection and year, a monthly activity heatmap for 1689 (the peak year), and a correspondence-span chart showing how long key individuals stayed in correspondence |
| **People Explorer** | Select any person to see their ego network — who they wrote to and received from — rendered as a force-directed graph. Click any connected node to pivot to that person. Toggle "Show Top Network" to see the global top-50 network |
| **Locations** | Top sending and receiving places, the most-travelled letter routes, and a place-network graph showing flows between locations |

---

## Raw Data

The raw data lives at [`letters-raw.csv`](./letters-raw.csv) in the repository root.

Each row represents a single letter (or other document) with the following columns:

| Column | Description |
|---|---|
| `From Type` | Type of sender (Person, Organization, Group…) |
| `From Name` | Name of the sender |
| `From Place` | Place the letter was sent from |
| `Edge Type` | Relationship type (WROTE LETTER TO, Commission, Warrant…) |
| `To Type` | Type of recipient |
| `To Name` | Name of the recipient |
| `To Place` | Destination place |
| `Date` | Date of the letter (several formats; see below) |
| `Weight` | Numeric weight/count |
| `Identifier` | Archive collection name |
| `Reference` | Archival reference number |

### Date formats in the raw data

The `Date` column uses several formats: `"1689, Jan 20"`, `"1/20/1689"`, `"09.08.1690"`, `"1690"`, `"c. 1690"`, `"undated"`, etc. The dashboard parser handles all of these.

### Name normalisation

Names in the raw data are inconsistent — some people appear by their full name and also by a shorter estate/title name (e.g. `"Carwhin"` = `"Colin Campbell of Carwhin"`, `"Balcarres"` = `"Colin Lindsay, Earl of Balcarres"`). The dashboard normalises these using a built-in alias map, and trims trailing whitespace from all names.

---

## Using This as a Template

This repository is structured as a minimal, self-contained template. To adapt it for your own letter/network dataset:

1. **Replace `letters-raw.csv`** with your own CSV. Keep the same column names, or update the column references in the `<script>` section of `index.html`.
2. **Update `NAME_ALIASES`** in `index.html` to reflect your own normalisation needs.
3. **Update the title and subtitle** in the `<header>` of `index.html`.
4. **Deploy to GitHub Pages** by going to *Settings → Pages* and selecting *Deploy from branch → main → / (root)*.

No build tools, bundlers, or servers are required. The dashboard is pure HTML/CSS/JS and loads the CSV at runtime using [PapaParse](https://www.papaparse.com/) and renders visualisations with [D3 v7](https://d3js.org/).

---

## Tech Stack

- [PapaParse 5](https://www.papaparse.com/) — client-side CSV parsing
- [D3.js v7](https://d3js.org/) — force-directed network graphs, bar charts, heatmaps
- Vanilla HTML/CSS/JS — no framework, no bundler
- GitHub Pages — static hosting from `main` branch root
