# Doichain Simulation

**Eine interaktive, browserbasierte Simulation zur Kursentwicklung von Doichain (DOI)** — auf Basis von organischem Kurswachstum, Community-Wachstum und dem Metcalfe'schen Netzwerkgesetz.

> ⚠️ **Disclaimer:** Diese Simulation dient ausschließlich zu akademischen und spielerischen Lernzwecken. Sie stellt keine Anlageberatung, keine Finanzanalyse und keine Prognose dar. Alle Werte sind fiktive Modellrechnungen ohne Vorhersagekraft.

---

## Demo

➡️ **[Live-Demo auf GitHub Pages](https://[deinbenutzername].github.io/doichain-simulation)**

![Screenshot der Doichain Simulation](screenshot.png)

---

## Features

- **Live-Kursdaten** — Aktueller DOI/USDT-Kurs wird beim Laden automatisch von CoinGecko abgerufen
- **Organisches Kurswachstum** — Startrate mit konfigurierbarer monatlicher Degression
- **Community-Wachstum** — Simuliert die Entwicklung der Nutzerbasis mit eigenem Wachstumsmodell
- **Metcalfe'scher Netzwerkeffekt** — Einfluss der Community-Größe auf den Kurs über den Exponent α
- **DCA-Strategie** — Optionaler monatlicher Zukauf zum jeweils aktuellen Kurs
- **Monatliche Vorschau-Tabelle** — Kurs, Community und Boost auf einen Blick
- **Lineare & logarithmische Skalierung** — Für große Wertspannen umschaltbar
- **Anleitung & Erklärung** — Eingebauter zweiter Tab mit vollständiger Dokumentation
- **Self-contained** — Keine Installation, kein Server, kein Build-Prozess nötig

---

## Schnellstart

### Lokal (ohne Server)

```bash
# Repository klonen
git clone https://github.com/[deinbenutzername]/doichain-simulation.git

# Datei direkt im Browser öffnen
open doichain-simulation.html        # macOS
start doichain-simulation.html       # Windows
xdg-open doichain-simulation.html    # Linux
```

Oder einfach per Doppelklick auf die Datei — sie öffnet sich direkt im Browser.

### Auf GitHub Pages veröffentlichen

1. Repository auf [github.com](https://github.com) anlegen
2. `doichain-simulation.html` als `index.html` hochladen
3. **Settings → Pages → Branch: `main` → Save**
4. Nach wenigen Minuten erreichbar unter `https://[deinbenutzername].github.io/[repositoryname]`

### Auf eigenem Webserver

```bash
# Per SCP/SFTP auf den Server kopieren
scp doichain-simulation.html user@deinserver.com:/var/www/html/

# Oder per FTP in das Web-Verzeichnis hochladen
# Die Datei ist unter https://deinedomain.com/doichain-simulation.html erreichbar
```

---

## Bedienungsanleitung

### Tab 1 — Simulation

Die Simulation ist in drei Parametergruppen gegliedert:

#### Investment
| Parameter | Beschreibung |
|---|---|
| **Startkapital (USD)** | Betrag, der zum Einstiegskurs in DOI investiert wird |
| **DOI Einstiegskurs** | Kaufkurs in USD — wird beim Laden automatisch mit dem Live-Kurs befüllt |
| **Zukauf / Monat** | Optionaler monatlicher Nachkauf (DCA-Strategie) zum jeweils aktuellen Kurs |

#### Organisches Kurswachstum
| Parameter | Beschreibung |
|---|---|
| **Wachstum Monat 1** | Angenommene Kurssteigerung im ersten Monat in % |
| **Degressfaktor Kurs** | Faktor, mit dem das Wachstum jeden Monat multipliziert wird. `0,5` = Halbierung pro Monat, `1,0` = konstant |
| **Laufzeit** | Simulationszeitraum in Monaten (1–120) |

#### Community-Wachstum (Metcalfe-Modell)
| Parameter | Beschreibung |
|---|---|
| **Startgröße** | Anzahl der Mitglieder zu Beginn der Simulation |
| **Wachstum Monat 1** | Prozentuale Zunahme der Mitglieder im ersten Monat |
| **Degressfaktor Community** | Analoger Abbaufaktor für das Community-Wachstum |
| **Netzwerkeffekt-Stärke (α)** | Exponent des Metcalfe-Gesetzes — steuert, wie stark die Community den Kurs beeinflusst |

#### Metcalfe-Exponent α — Orientierungswerte

| α | Effekt |
|---|---|
| `0,1 – 0,5` | Schwacher Netzwerkeffekt — Community hat kaum Kurswirkung |
| `1,0` | Linearer Effekt — Community ×2 → Kurs ×2 |
| `1,5` | Realistisch für frühe Kryptoprojekte |
| `2,0` | Klassisches Metcalfe-Gesetz — Community ×2 → Kurs ×4 |

### Ergebnisanzeige

| Karte | Bedeutung |
|---|---|
| **DOI-Kurs organisch** | Kurs am Laufzeitende ohne Community-Effekt |
| **DOI-Kurs + Community** | Kurs mit Metcalfe-Boost |
| **Community-Boost** | Multiplikator durch Netzwerkeffekt |
| **Community-Größe (End)** | Prognostizierte Mitgliederzahl am Ende |
| **Portfoliowert (End)** | Gesamtwert der gehaltenen DOI in USD |

### Tab 2 — Anleitung & Erklärung

Vollständige Beschreibung aller Modelle, Formeln und Parameter in allgemeinverständlicher Sprache, inklusive Hinweisen zur Interpretation der Ergebnisse.

---

## Das Modell

### Organisches Kurswachstum mit Degression

```
Kurs(t+1) = Kurs(t) × (1 + Wachstum(t))
Wachstum(t) = Wachstum(Monat 1) × Degressfaktor^t
```

Das Wachstum beginnt hoch und verlangsamt sich jeden Monat — typisch für frühe Projektphasen mit anfänglichem Hype-Effekt.

### Metcalfe'scher Netzwerkeffekt

```
DOI-Kurs(gesamt) = DOI-Kurs(organisch) × (Community_t / Community_Start)^α
```

Der Wert eines Netzwerks skaliert mit der Anzahl seiner Nutzer. Bei α = 2 (klassisches Metcalfe-Gesetz) wächst der Netzwerkwert quadratisch mit der Community-Größe.

### DCA (Dollar-Cost-Averaging)

Monatliche Zukäufe werden zum jeweils aktuellen kombinierten Kurs (organisch + Community-Boost) ausgeführt:

```
Token_neu = Zukauf_USD / Kurs(t)
```

---

## Technische Details

- **Keine Abhängigkeiten** — reines HTML/CSS/JavaScript
- **Chart.js 4.4.1** — einzige externe Bibliothek, via CDN
- **Google Fonts** — Syne + DM Mono, via CDN
- **Live-Kurs** — CoinGecko Public API (`/api/v3/simple/price?ids=doichain`)
- **Offline-fähig** — fällt bei fehlendem Internet auf Fallback-Wert zurück
- **Dateigröße** — ca. 155 KB (inkl. eingebettetem Logo)

---

## Projektstruktur

```
doichain-simulation/
├── index.html          # Die vollständige Anwendung (self-contained)
├── README.md           # Diese Datei
└── LICENSE             # MIT License
```

---

## Mitmachen

Pull Requests und Issues sind willkommen. Mögliche Erweiterungen:

- Mehrere Szenarien gleichzeitig vergleichen
- CSV-Export der Monatstabelle
- Weitere Börsen-APIs als Kursquellen
- S-Kurven-Modell für realistischeres Community-Wachstum (Logistisches Wachstum)
- Einbindung von historischen DOI-Kursdaten

---

## Lizenz

MIT License — © 2025 Ottmar Neuburger

```
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
```

---

## Links

- [Doichain Projekt](https://doichain.org)
- [DOI auf CoinGecko](https://www.coingecko.com/en/coins/doichain)
- [DOI auf xt.com](https://www.xt.com/de/trade/doi_usdt)
