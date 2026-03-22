# Slavic Mythology Deities API

A free, static JSON API providing structured data on **30 Slavic mythology deities** across **6 languages**. Each deity includes rich mythological content — domains, symbols, sacred animals, worship practices, relationships, and imagery — ready to use in apps, games, educational tools, or visualizations.

**Live API base URL:**
```
https://slavic-api.github.io/API
```

**Documentation landing page:** [slavic-api.github.io/API](https://slavic-api.github.io/API)

---

## Table of Contents

- [Data Overview](#data-overview)
- [Repository Structure](#repository-structure)
- [Endpoints](#endpoints)
- [Data Schema](#data-schema)
  - [Individual Deity File](#individual-deity-file)
  - [Bundle File](#bundle-file)
  - [deities\_list.json Entry](#deities_listjson-entry)
  - [Search Index Entry](#search-index-entry)
  - [Full Example — Perun](#full-example--perun)
- [Languages](#languages)
- [Deity Types](#deity-types)
- [How to Use](#how-to-use)
- [Filtering and Querying](#filtering-and-querying)
- [Available Tags](#available-tags)
- [Complete Deity List](#complete-deity-list)
- [Deploy to GitHub Pages](#deploy-to-github-pages)
- [Contributing](#contributing)
- [License](#license)

---

## Data Overview

| Property | Value |
|---|---|
| Total deities | 30 |
| Languages | 6 (English, Polish, Ukrainian, Bulgarian, Czech, Serbian) |
| Individual deity files | 180 (30 per language) |
| Bundle files | 6 (all 30 deities in one request per language) |
| Search index files | 6 (one per language) |
| Deity list files | 6 (one per language) |
| Root master list | 1 (`deities_list.json`) |
| Image assets | 60 (thumbnail + detail image per deity) |
| API manifest | `api.json` |
| Documentation | `index.html` (interactive landing page) |

Each deity file contains:

- Canonical name and alternate historical names across Slavic cultures
- Type classification (god, goddess, spirit, creature, etc.)
- Geographic origin (East Slavic, West Slavic, South Slavic)
- Short description and extended mythology narrative
- Structured attributes (domains, symbols, sacred animals, sacred plants, element, season, associated concepts)
- Relationship graph (rivals, family, allies — cross-referenced by deity ID)
- Worship details (regions, festivals, traditional offerings)
- Searchable tags (in English across all languages, for consistent filtering)
- Thumbnail and detail image URLs

---

## Repository Structure

```
API/
├── index.html                 # Interactive API documentation landing page
├── api.json                   # Machine-readable API manifest
├── README.md
├── .nojekyll                  # Bypasses Jekyll — required for GitHub Pages
├── 404.html                   # Custom 404 error page
│
├── deities_list.json          # Root master list — all 30 deities (English, with type/origin/tags)
│
├── en/                        # English
│   ├── deities_list.json      # Localized list (name + description + type + origin + tags)
│   ├── deities.json           # ⚡ Bundle — all 30 full deity objects in one file
│   └── deities/
│       ├── 001.json           # Perun
│       ├── 002.json           # Dazhbog
│       └── ...                # 003–030
│
├── pl/                        # Polish
│   ├── deities_list.json
│   ├── deities.json           # Bundle
│   └── deities/
│       └── 001.json – 030.json
│
├── ua/                        # Ukrainian (Cyrillic)
│   ├── deities_list.json
│   ├── deities.json
│   └── deities/
│       └── 001.json – 030.json
│
├── bg/                        # Bulgarian (Cyrillic)
│   ├── deities_list.json
│   ├── deities.json
│   └── deities/
│       └── 001.json – 030.json
│
├── cz/                        # Czech
│   ├── deities_list.json
│   ├── deities.json
│   └── deities/
│       └── 001.json – 030.json
│
├── sr/                        # Serbian (Latin)
│   ├── deities_list.json
│   ├── deities.json
│   └── deities/
│       └── 001.json – 030.json
│
├── search/                    # Search-optimized indexes
│   ├── en.json
│   ├── pl.json
│   ├── ua.json
│   ├── bg.json
│   ├── cz.json
│   └── sr.json
│
└── images/
    └── deities/
        ├── 001/
        │   ├── thumbnail.png      # ~160KB
        │   └── detailImage.png    # ~2.3MB
        └── 002/ – 030/
```

---

## Endpoints

All endpoints return JSON. No authentication, no rate limits, full CORS support.

| Method | URL | Description |
|---|---|---|
| `GET` | `/deities_list.json` | Root master list of all 30 deities (English, includes type/origin/tags) |
| `GET` | `/{lang}/deities_list.json` | Localized list — all 6 languages |
| `GET` | `/{lang}/deities.json` | **Bundle** — all 30 full deity objects in one request |
| `GET` | `/{lang}/deities/{id}.json` | Full details for a single deity |
| `GET` | `/search/{lang}.json` | Search-optimized flat index for client-side filtering |
| `GET` | `/images/deities/{id}/thumbnail.png` | Deity thumbnail (~160KB) |
| `GET` | `/images/deities/{id}/detailImage.png` | Full detail image (~2.3MB) |
| `GET` | `/api.json` | Machine-readable API manifest with schema documentation |

**Parameters:**
- `{lang}` — language code: `en` `pl` `ua` `bg` `cz` `sr`
- `{id}` — zero-padded 3-digit deity ID: `001` through `030`

> **Tip:** Use the bundle endpoint (`/{lang}/deities.json`) when you need all deities. It saves 29 HTTP requests compared to fetching individual files.

---

## Data Schema

### Individual Deity File

Path pattern: `/{lang}/deities/{id}.json`

| Field | Type | Description |
|---|---|---|
| `id` | `string` | Zero-padded 3-digit identifier, e.g. `"001"` |
| `name` | `string` | Primary name in the target language |
| `alternateNames` | `string[]` | Historical or regional variant names (original languages) |
| `type` | `string` | Classification — see [Deity Types](#deity-types) (always English) |
| `origin` | `string[]` | Slavic sub-regions of attestation (always English) |
| `description` | `string` | One- or two-sentence localized summary |
| `mythology` | `string` | Extended localized narrative covering myths, roles, and lore |
| `attributes.Domains` | `string[]` | Areas of divine authority (localized) |
| `attributes.Symbols` | `string[]` | Sacred objects or images (localized) |
| `attributes.Sacred Animals` | `string[]` | Animals sacred to the deity (localized) |
| `attributes.Sacred Plants` | `string[]` | Plants sacred to the deity (localized) |
| `attributes.Element` | `string` | Primary classical element (localized) |
| `attributes.Season` | `string` | Season of primary association, if applicable (localized) |
| `attributes.Associated Concepts` | `string[]` | Abstract concepts embodied by the deity (localized) |
| `relationships.rivals` | `string[]` | IDs of rival/opposing deities |
| `relationships.family` | `string[]` | IDs of family deities |
| `relationships.allies` | `string[]` | IDs of allied deities |
| `worship.regions` | `string[]` | Geographic regions of worship (always English) |
| `worship.festivals` | `string[]` | Associated festivals and holy days (localized) |
| `worship.offerings` | `string[]` | Traditional offerings (localized) |
| `tags` | `string[]` | Flat tag list for filtering — always English across all languages |
| `thumbnailUrl` | `string` | Relative path to thumbnail PNG |
| `detailImageUrl` | `string` | Relative path to detail PNG |

---

### Bundle File

Path pattern: `/{lang}/deities.json`

```json
{
  "lang": "en",
  "version": "1.0.0",
  "total": 30,
  "deities": [ /* array of 30 full deity objects */ ]
}
```

---

### deities_list.json Entry

Lightweight summary suitable for listing views. Available at root and per language.

| Field | Type | Description |
|---|---|---|
| `id` | `string` | Zero-padded 3-digit identifier |
| `name` | `string` | Deity name (localized) |
| `type` | `string` | Deity type classification (English) |
| `origin` | `string[]` | Slavic sub-regions of attestation (English) |
| `description` | `string` | Short localized description |
| `tags` | `string[]` | Flat tag list (English) |
| `thumbnailUrl` | `string` | Relative path to thumbnail image |

---

### Search Index Entry

Path pattern: `/search/{lang}.json`

Optimized for client-side search and filtering — flattened structure, no nested objects, includes a mythology preview.

| Field | Type | Description |
|---|---|---|
| `id` | `string` | Deity ID |
| `name` | `string` | Localized name |
| `alternateNames` | `string[]` | Historical variant names |
| `type` | `string` | Type classification (English) |
| `origin` | `string[]` | Slavic sub-regions (English) |
| `tags` | `string[]` | Filtering tags (English) |
| `domains` | `string[]` | Domains extracted from attributes (localized) |
| `symbols` | `string[]` | Symbols extracted from attributes (localized) |
| `element` | `string` | Primary element (localized) |
| `description` | `string` | Short description (localized) |
| `mythologyPreview` | `string` | First 200 characters of mythology text |
| `thumbnailUrl` | `string` | Relative path to thumbnail |

---

### Full Example — Perun

**`en/deities/001.json`**

```json
{
  "id": "001",
  "name": "Perun",
  "alternateNames": ["Perkunas", "Perkons", "Perún", "Pirun"],
  "type": "god",
  "origin": ["East Slavic", "South Slavic", "West Slavic"],
  "description": "Slavic god of thunder and lightning. Protector of warriors and upholder of cosmic law.",
  "mythology": "Perun is the supreme deity of the Slavic pantheon, ruling thunder, lightning, storms, rain, law, war, and fertility from the highest branches of the World Tree — a great cosmic oak. His eternal enemy is Veles, the serpentine underworld god, who steals his cattle, wife, or children. Perun pursues Veles across the sky hurling thunderbolts, while Veles hides in the form of animals, trees, or people. This cosmic battle brings rain to the earth and maintains cosmic order. Perun is depicted as a middle-aged man with a copper beard wielding an axe or hammer. Sacred oak trees and hilltops served as his shrines. He was the patron of the warrior class and the prince's retinue in Kyivan Rus.",
  "attributes": {
    "Domains": ["Thunder", "Lightning", "War", "Law", "Sky", "Rain", "Fertility"],
    "Symbols": ["Axe", "Thunderbolt", "Eagle", "Hammer", "Oak"],
    "Sacred Animals": ["Eagle", "Bull", "Aurochs"],
    "Sacred Plants": ["Oak", "Iris"],
    "Element": "Air",
    "Season": "Summer",
    "Associated Concepts": ["Justice", "Power", "Protection", "Cosmic Order"]
  },
  "relationships": {
    "rivals": ["004"],
    "family": [],
    "allies": []
  },
  "worship": {
    "regions": ["Russia", "Ukraine", "Poland", "Belarus", "Serbia", "Croatia"],
    "festivals": ["Perun's Day (July 20 / syncretized with Elijah's Day)"],
    "offerings": ["Ox", "Bull", "Oak wood", "Bread", "Honey wine"]
  },
  "tags": ["major deity", "warrior", "sky", "weather", "thunder", "oak", "Kiev pantheon"],
  "thumbnailUrl": "images/deities/001/thumbnail.png",
  "detailImageUrl": "images/deities/001/detailImage.png"
}
```

---

## Languages

All 30 deities are available in every language. The `name`, `description`, `mythology`, `attributes`, and `worship` fields are fully localized. The `type`, `origin`, `tags`, `worship.regions`, and `alternateNames` fields always remain in English for consistent filtering.

| Code | Language | Script | Individual Files | Bundle | Search Index | List File |
|---|---|---|---|---|---|---|
| `en` | English | Latin | 30 | ✓ | ✓ | ✓ |
| `pl` | Polish | Latin | 30 | ✓ | ✓ | ✓ |
| `ua` | Ukrainian | Cyrillic | 30 | ✓ | ✓ | ✓ |
| `bg` | Bulgarian | Cyrillic | 30 | ✓ | ✓ | ✓ |
| `cz` | Czech | Latin | 30 | ✓ | ✓ | ✓ |
| `sr` | Serbian | Latin | 30 | ✓ | ✓ | ✓ |

The root `deities_list.json` at the repository root is the canonical master index (English, includes type, origin, and tags on all 30 entries).

---

## Deity Types

| Type | Description | Examples |
|---|---|---|
| `god` | Major male divine figure | Perun, Veles, Dazhbog, Svarog, Stribog |
| `goddess` | Major female divine figure | Mokosh, Marzanna, Lada, Zorya, Zhiva |
| `spirit` | Nature or household spirit | Domovoi, Leshy, Rusałka, Baba Yaga, Morozko |
| `creature` | Mythical divine animal or beast | Simargl |
| `personification` | Abstract concept given divine form | Domovina, Dnipro |
| `deity pair` | Two deities worshipped as a unified pair | Kupala and Kupalo, Dolya and Sudba |
| `mythical place` | Sacred or cosmic location treated as an entity | Zhivini Pole |
| `primordial god` | Creator or first-generation deity | Rod |
| `deity` | Deity with ambiguous or mixed classification | Veleslav, Triglav, Yasen, Dobrovij |

---

## How to Use

Base URL: `https://slavic-api.github.io/API`

### Load all 30 deities at once (recommended)

```javascript
const BASE = 'https://slavic-api.github.io/API';

const { deities } = await fetch(`${BASE}/en/deities.json`).then(r => r.json());
console.log(deities.length); // 30
```

### Load a single deity

```javascript
const perun = await fetch(`${BASE}/en/deities/001.json`).then(r => r.json());
console.log(perun.name);              // "Perun"
console.log(perun.attributes.Domains); // ["Thunder", "Lightning", ...]
console.log(perun.mythology);         // full narrative text
```

### Load in a specific language

```javascript
const perunUA = await fetch(`${BASE}/ua/deities/001.json`).then(r => r.json());
// { name: "Перун", mythology: "Перун є верховним ...", ... }

const velesPolish = await fetch(`${BASE}/pl/deities/004.json`).then(r => r.json());
// { name: "Weles", mythology: "Weles jest wielkim ...", ... }
```

### Use the search index for filtering

```javascript
const { deities } = await fetch(`${BASE}/search/en.json`).then(r => r.json());

// Filter by type
const gods = deities.filter(d => d.type === 'god');

// Filter by tag
const warriors = deities.filter(d => d.tags.includes('warrior'));

// Search by name (case-insensitive)
const query = 'vel';
const results = deities.filter(d =>
  d.name.toLowerCase().includes(query) ||
  d.alternateNames.some(n => n.toLowerCase().includes(query))
);

// Filter by origin
const eastSlavic = deities.filter(d => d.origin.includes('East Slavic'));
```

### Resolve image URLs

Image paths in JSON are relative. Prepend the base URL:

```javascript
const BASE = 'https://slavic-api.github.io/API';
const thumbnail = `${BASE}/${deity.thumbnailUrl}`;
const detail    = `${BASE}/${deity.detailImageUrl}`;
// → https://slavic-api.github.io/API/images/deities/001/thumbnail.png
```

### Python

```python
import httpx

BASE = "https://slavic-api.github.io/API"

# All deities in one request
deities = httpx.get(f"{BASE}/en/deities.json").json()["deities"]

# Single deity in Ukrainian
perun = httpx.get(f"{BASE}/ua/deities/001.json").json()

# Filter by origin
east_slavic = [d for d in deities if "East Slavic" in d["origin"]]
```

### Swift

```swift
let base = "https://slavic-api.github.io/API"

struct DeitiesBundle: Decodable {
    let lang: String
    let total: Int
    let deities: [Deity]
}

let url = URL(string: "\(base)/en/deities.json")!
let (data, _) = try await URLSession.shared.data(from: url)
let bundle = try JSONDecoder().decode(DeitiesBundle.self, from: data)
```

---

## Filtering and Querying

The `tags`, `type`, and `origin` fields are always in English across all language files, so you can filter consistently regardless of the active language. Use the **search index** (`/search/{lang}.json`) for efficient client-side search — it's lightweight and pre-flattened.

### Combine filters

```javascript
// East Slavic spirits only
const eastSlavicSpirits = deities.filter(d =>
  d.type === 'spirit' && d.origin.includes('East Slavic')
);

// Major deities from the Kiev pantheon
const kievPantheon = deities.filter(d =>
  d.tags.includes('Kiev pantheon')
);

// Deities associated with winter
const winterDeities = deities.filter(d =>
  d.tags.includes('winter') || d.tags.includes('cold') || d.tags.includes('frost')
);
```

---

## Available Tags

All tags used across the dataset. Tags are always in English regardless of the active language.

**Deity rank / pantheon**
`major deity` · `minor deity` · `primordial` · `Kiev pantheon` · `Baltic Slavic`

**Domain / role**
`warrior` · `sky` · `weather` · `thunder` · `sun` · `solar` · `fire` · `wind` · `air` · `water` · `earth` · `underworld` · `winter` · `cold` · `frost` · `spring` · `summer solstice` · `seasonal` · `night`

**Nature and environment**
`forest` · `nature spirit` · `forest spirit` · `river` · `water spirit` · `trees` · `oak` · `ash tree` · `world tree` · `animals` · `wilderness` · `wild` · `primal`

**Life themes**
`fertility` · `agriculture` · `birth` · `motherhood` · `life` · `death` · `rebirth` · `transformation` · `fate` · `destiny` · `fortune` · `luck`

**Cultural / social**
`love` · `beauty` · `harmony` · `marriage` · `music` · `weaving` · `women` · `domestic` · `household spirit` · `ancestor spirit` · `homeland` · `cultural` · `history` · `Ukrainian` · `trade`

**Character traits**
`trickster` · `shapeshifter` · `wisdom` · `knowledge` · `bard` · `prophecy` · `elder`

**Mythology themes**
`duality` · `cosmic` · `triform` · `chaos` · `darkness` · `evil` · `cosmic order` · `creator` · `ancestors`

**Creature / entity**
`creature` · `guardian` · `divine animal` · `sacred fire` · `seeds` · `witch` · `hag` · `death boundary` · `unquiet dead`

**Other**
`fairy tale` · `gift-giver` · `major festival` · `afterlife` · `paradise` · `mythical location` · `righteous dead` · `personification` · `celestial` · `warrior maiden` · `dawn` · `dusk` · `stars` · `craftsman` · `father deity` · `smithing` · `prosperity` · `earth mother` · `counterpart to death` · `moral deity` · `benevolence` · `virtue` · `goodness` · `omen` · `dangerous` · `female`

---

## Complete Deity List

| ID | Name | Type | Origin |
|---|---|---|---|
| 001 | Perun | god | East · West · South Slavic |
| 002 | Dazhbog | god | East · South Slavic |
| 003 | Mokosh | goddess | East Slavic |
| 004 | Veles | god | East · West · South Slavic |
| 005 | Rod | primordial god | East · South Slavic |
| 006 | Domovoi | spirit | East · West Slavic |
| 007 | Morozko | spirit | East Slavic |
| 008 | Zorya | goddess | East · South Slavic |
| 009 | Chernobog | god | West · East Slavic |
| 010 | Svarog | god | East · West Slavic |
| 011 | Marzanna | goddess | East · West · South Slavic |
| 012 | Baba Yaga | spirit | East · West Slavic |
| 013 | Kupala and Kupalo | deity pair | East · West · South Slavic |
| 014 | Stribog | god | East Slavic |
| 015 | Leshy | spirit | East · West Slavic |
| 016 | Rusałka | spirit | East · West · South Slavic |
| 017 | Domovina | personification | All Slavic |
| 018 | Jarilo | god | East · West · South Slavic |
| 019 | Dolya and Sudba | deity pair | East · South Slavic |
| 020 | Simargl | creature | East Slavic |
| 021 | Veleslav | deity | East Slavic |
| 022 | Zhiva | goddess | East · West · South Slavic |
| 023 | Divi | spirit | South · East Slavic |
| 024 | Triglav | deity | West Slavic |
| 025 | Zhivini Pole | mythical place | East · South Slavic |
| 026 | Roda | goddess | East Slavic |
| 027 | Yasen | deity | East Slavic |
| 028 | Lada | goddess | East · West · South Slavic |
| 029 | Dnipro | personification | East Slavic |
| 030 | Dobrovij | deity | East · South Slavic |

---

## Deploy to GitHub Pages

This API is designed to be served as-is via GitHub Pages.

1. Go to your repository → **Settings** → **Pages**
2. Set source to **Deploy from a branch** → branch `main`, folder `/` (root)
3. Save — your API will be live within a few minutes at:
   ```
   https://{your-username}.github.io/{repo-name}/
   ```

The `.nojekyll` file in the root ensures GitHub Pages bypasses Jekyll processing and serves all JSON files, including those in directories that would otherwise be ignored.

No build step, no server, no configuration required.

---

## Contributing

Contributions are welcome. Here are some ways to help:

- **Improve translations** — correct or enrich localized `description` and `mythology` in any language file
- **Add new languages** — create a new language directory (e.g. `ru/`, `sk/`, `de/`) following the existing structure; include a `deities.json` bundle and entries in `search/`
- **Expand relationships** — fill in `relationships.family` and `relationships.allies` using cross-referenced IDs
- **Add more deities** — Slavic mythology has many more than 30; new entries should follow the existing schema exactly
- **Fix inaccuracies** — open an issue if you spot a mythological or historical error
- **Improve image assets** — higher resolution or more accurate representations welcome

### Contribution steps

1. Fork the repository
2. Create a branch: `git checkout -b feature/your-change`
3. Make your changes and validate all JSON files
4. If adding/modifying deities, update the bundle file for that language: combine all individual files into `{lang}/deities.json`
5. Open a pull request with a clear description of what changed and why

All `id` cross-references in `relationships` must point to existing deity IDs (`001`–`030`). Validate JSON before submitting.

---

## License

License to be determined. All mythological content is based on public domain historical and folkloric sources.
