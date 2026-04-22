# Automatisierter Leadgenerierungs-Workflow Proof of Concept

> **Ziel:** Skalierbare, KI-gestützte Leadrecherche – von manuellen Stunden auf automatisierte Minuten.

---

## Projektübersicht

Dieses Projekt automatisiert den gesamten Prozess der B2B-Leadgenerierung mithilfe von **n8n**, einem **Large Language Model (LLM)** und der **Apollo API**. Der Workflow übernimmt die Identifikation relevanter Jobtitel, die Leadsuche sowie die Datenanreicherung und speichert alle Ergebnisse strukturiert in **Google Sheets**.

**Anwendungskontext:** Business Development / Sales Automation

---

## Tech Stack

| Komponente | Tool |
|---|---|
| Automatisierungsplattform | [n8n](https://n8n.io/) |
| KI-Modell (LLM) | OpenAI / GPT |
| Lead-Datenquelle | [Apollo.io](https://www.apollo.io/) API |
| Ausgabe / Datenspeicherung | Google Sheets |

---

## Workflow-Architektur

Der Workflow gliedert sich in **4 Phasen**:

```
[1] Keyword-Input (n8n Chat)
       ↓
[2] Jobtitel-Generierung via LLM
       ↓
[3] Unternehmensliste aus Google Sheets lesen
       ↓
[4] Leadsuche über Apollo API aus Basis von Unternehmen und Jobtitel
       ↓
[5] Datenanreicherung & Speicherung in Google Sheets
```

---

## Phasen im Detail

### Phase 1 – Jobtitel-Generierung (LLM)

- Der Nutzer gibt über den **n8n Chat** ein Keyword (z. B. „Smart Home"*) ein
- Ein **AI-Agent** generiert auf Basis vordefinierter Prompts passende Jobtitel
- **Output:** Liste relevanter Zielrollen, z. B.:
  - Head of IoT
  - Head of Smart Home
  - Director Digital Products

### Phase 2 – Unternehmensliste aufnehmen

- Unternehmen werden automatisch aus einem **Google Sheet** geladen, die davor mitgegeben werden müssen
- Die **Domain** dient als eindeutige ID zur Identifikation
- Duplikate werden herausgefiltert, bevor die Leadsuche eingeleitet wird

### Phase 3 – Leadsuche via Apollo

- Kombination aus **Jobtiteln (Phase 1)** und **Unternehmen (Phase 2)** wird als Suchanfrage an die Apollo API übergeben
- Apollo liefert passende Kontaktdatensätze zurück
- Erste Kontaktdaten (E-Mail, Telefon) sind teilweise bereits vorhanden

### Phase 4 – Datenanreicherung & Speicherung

- Fehlende Kontaktdaten werden über eine **zusätzliche Apollo API-Abfrage** angereichert
- Begrenzung auf **max. 5 Kontakte pro Anfrage** (Rate-Limit-Steuerung)
- Vollständige Datensätze werden strukturiert in **Google Sheets** gespeichert

**Beispiel-Output:**

```
First Name:   Max
Last Name:    Mustermann
E-Mail:       max.mustermann@web.de
Phone:        +49 123 456 87
```

---

## Ergebnisse & Mehrwert

| Metrik | Vorher (manuell) | Nachher (automatisiert) |
|---|---|---|
| Recherchezeit | Stunden | Minuten |
| Skalierbarkeit | Gering | Hoch |
| Kampagnen-Readiness | Langsam | Schnell |
| Datenkonsistenz | Variabel | Standardisiert |

**Weitere Vorteile:**
- 📧 Potenzial zur direkten Integration in E-Mail-Kampagnen
- 📞 Telefonnummern für telefonische Outreach-Aktivitäten verfügbar
- 🔁 Vollständig wiederverwendbar für verschiedene Keywords und Branchen


*Dieses Projekt wurde im Rahmen der Prozessautomatisierung im Business Development entwickelt und demonstriert den praktischen Einsatz von No-Code-/Low-Code-Tools in Kombination mit KI für skalierbare Vertriebsprozesse.*
