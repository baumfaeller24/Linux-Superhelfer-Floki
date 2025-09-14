# FinPattern-Engine

Ein modulares System für Mustererkennung in Finanzmarktdaten (Tick- und Bardaten) mit Fokus auf reproduzierbare Trading-Strategien.

## 🎯 Zielsetzung

FinPattern-Engine ist ein umfassendes Backtesting- und Forschungssystem für Trading-Strategien, das zwei komplementäre Ansätze zur Mustererkennung unterstützt:

- **Freie Mustererkennung**: Datengetriebene Entdeckung von Mustern mittels Machine Learning
- **Template-basierte Suche**: Mustererkennung basierend auf vordefiniertem Indikator-Katalog

Alle Ergebnisse sind vollständig reproduzierbar und können direkt als PineScript v5 für TradingView exportiert werden.

## 🏗️ Architektur

Das System basiert auf einer modularen Pipeline-Architektur mit 14 Kernmodulen:

```
DataIngest → Labeling → FeatureEngine → Splitter → [FreeSearch|DBSearch] 
    → RLParamTuner → Backtester → Validator → Exporter → Reporter
```

Gesteuert wird der gesamte Ablauf durch einen zentralen **Orchestrator** (State Machine), der die Koordination zwischen den Modulen übernimmt.

## 📋 Module

| Modul | Beschreibung |
|-------|-------------|
| **DataIngest** | Tickdaten einlesen, normalisieren, Bars erzeugen |
| **Labeling** | Triple-Barrier Labels (TP/SL/Timeout) |
| **FeatureEngine** | Technische Indikatoren berechnen |
| **Splitter** | Walk-Forward, Purged/Embargo CV, Session-Splits |
| **FreeSearch** | Datengetriebene Musterfindung (Trees, RuleFit) |
| **DBSearch** | Musterkatalog + Parametertuning |
| **RLParamTuner** | Reinforcement Learning für Parametrisierung |
| **Backtester** | Kennzahlen pro Regel |
| **Validator** | OOS-Kriterien prüfen |
| **Exporter** | Pine v5, Markdown, CSV |
| **Reporter** | Charts, Reports |
| **Orchestrator** | Ablaufsteuerung |
| **Persistence** | Versionierung, Resume |
| **GUI** | Buttons + Visualisierung |

## 🚀 Schnellstart

### Voraussetzungen

- Python 3.11+
- Linux-Umgebung
- Mindestens 16GB RAM (empfohlen: 32GB+)
- SSD-Speicher für optimale Performance

### Installation

```bash
git clone https://github.com/baumfaeller24/Linux-Superhelfer-Floki.git
cd Linux-Superhelfer-Floki
python3.11 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### Erste Schritte

```bash
# GUI starten
python src/gui/main.py

# Oder direkt über CLI
python src/orchestrator/main.py --config configs/example_eurusd.yaml
```

## 📊 Datenformat

### Eingabe
- **Tickdaten**: CSV/Parquet mit Spalten `timestamp`, `bid`, `ask`, `[volume]`
- **Konfiguration**: YAML/JSON für Run-Parameter

### Ausgabe
- **Regeln**: JSON mit gefundenen Mustern und Parametern
- **Backtest-Ergebnisse**: CSV mit Trade-Details, JSON mit Kennzahlen
- **Charts**: PNG-Visualisierungen der Performance
- **PineScript**: Direkt importierbare Trading-Strategien für TradingView

## 🎯 Performance-Ziele

- **Datenvolumen**: Monatsdaten EUR/USD (ca. 1-2 Mio. Ticks) in <4h
- **RAM-Nutzung**: ≤100 GB bei Bar-Bildung
- **Reproduzierbarkeit**: Identische Ergebnisse bei gleichem Seed
- **Modularität**: Jedes Modul einzeln testbar und austauschbar

## 📁 Projektstruktur

```
finpattern-engine/
├── src/
│   ├── modules/           # 14 Kernmodule
│   ├── orchestrator/      # State Machine Controller
│   ├── gui/              # Streamlit/Dash Interface
│   └── utils/            # Hilfsfunktionen
├── tests/                # Unit- und Integrationstests
├── configs/              # YAML-Konfigurationen
├── data/                 # Beispieldaten
├── docs/                 # Dokumentation
└── runs/                 # Output-Verzeichnis für Läufe
```

## 🔧 Entwicklung

### Entwicklungsumgebung

```bash
# Development Dependencies installieren
pip install -r requirements-dev.txt

# Tests ausführen
pytest tests/

# Code-Qualität prüfen
black src/
flake8 src/
mypy src/
```

### Beitragen

1. Fork des Repositories
2. Feature-Branch erstellen (`git checkout -b feature/amazing-feature`)
3. Änderungen committen (`git commit -m 'Add amazing feature'`)
4. Branch pushen (`git push origin feature/amazing-feature`)
5. Pull Request erstellen

## 📄 Lizenz

Dieses Projekt steht unter der MIT-Lizenz. Siehe [LICENSE](LICENSE) für Details.

## 🤝 Support

Bei Fragen oder Problemen:
- GitHub Issues für Bug-Reports und Feature-Requests
- Dokumentation unter `docs/`
- Beispiel-Konfigurationen unter `configs/`

---

**Entwickelt für professionelle Trading-Strategieentwicklung mit Fokus auf Reproduzierbarkeit und wissenschaftliche Rigorosität.**
