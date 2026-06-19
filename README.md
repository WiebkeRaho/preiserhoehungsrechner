# Microsoft 365 Preiserhöhungsrechner — Juli 2026

Kostenloser Single-Page-Rechner, der die Microsoft-365-/Office-365-Preiserhöhung
zum **01.07.2026** auf den eigenen Lizenzbestand umrechnet: Mehrkosten,
Einsparpotenzial durch vorzeitige Preissicherung und konkrete
Handlungsempfehlungen je Lizenz.

> Live: https://wiebkeraho.github.io/preiserhoehungsrechner/

---

## Funktionen

- **Lizenzbestand erfassen** – Produkt, Menge, Vertragslaufzeit,
  Abrechnungszyklus, Ablaufdatum und optional ein eigener Preis/Stück.
- **Sammel-Import aus Excel** – ganze Tabelle per Copy-&-Paste (Tab-,
  Semikolon- oder Komma-getrennt); Kopfzeile und nicht betroffene Produkte
  werden automatisch erkannt.
- **Kostenübersicht (KPIs)** – aktuelle Kosten, Renewal-Kosten ab 01.07.2026,
  Mehrkosten (1 & 3 Jahre) und maximales Einsparpotenzial.
- **Analyse je Lizenz** – Berechnungsbasis, Erhöhung, Einsparung 1-/3-Jahres-
  Preis-Lock und Empfehlung pro Position.
- **Term-Upgrade-Alternative (Proration)** – siehe unten.
- **PDF-Druck** und **Versand der Auswertung** (per Web3Forms) integriert.

---

## So wird gerechnet

| Größe | Bedeutung |
|------|-----------|
| **Stichtag** | 30.06.2026 – ab 01.07.2026 gelten die erhöhten NCE-Preise |
| **F** | aktueller Jahrespreis/Stück (EVP bzw. eigener Preis; monatliche Abrechnung × 1,05) |
| **H** | neuer Jahrespreis/Stück = F × (1 + produktspezifische Erhöhung) |
| **B** | Anzahl Lizenzen |
| **O** | Überlappungstage = max(0; Ablaufdatum − 30.06.2026) |

- **Preisbasis:** Bei **EA** gilt immer der Listenpreis (EVP). Bei **CSP** und
  **webdirect** darf ein eigener Preis/Stück die Grundlage sein, auf den die
  relativen, produktspezifischen Erhöhungen angewendet werden.
- **Brückenlizenz / Überlappung:** Bei vorzeitigem Renewal entsteht eine
  Überlappung zur Restlaufzeit. Sie wird vom 30.06. bis zum Ablaufdatum zum
  alten Preis berechnet (für SICHERN vs. BLEIBEN fair vergleichbar).
- **Preis-Lock (1/3 Jahre):** TCO-Vergleich SICHERN vs. BLEIBEN über ein 12-
  bzw. 36-Monats-Fenster; ausgewiesen wird der bessere verfügbare Wert.
- **Monatslizenzen:** Erhöhung greift sofort; eine rechnerische Ersparnis wird
  nur informativ ausgewiesen.
- **Jahreslizenzen mit Ablauf ≤ 30.06.2026** verlängern sich automatisch noch
  zum alten Preis (Jahr 1 nicht betroffen).

> Preise sind Microsoft-Listenpreise (EVP) und für Juli 2026 geschätzt – ohne
> Gewähr. Promotions sind kundenspezifisch und nicht enthalten.

---

## Term-Upgrade-Alternative (Proration)

Lohnt sich der klassische **3-Jahres-Preis-Lock** nicht oder kostet die
**Brücke/Überlappung** unnötig viel, weist der Rechner zusätzlich den
**Term-Upgrade-Pfad** aus.

Bei einem Midterm-Term-Upgrade entfällt die Überlappung: Microsoft schreibt die
ungenutzte Restlaufzeit per **Proration** gut, statt zwei Verträge parallel
laufen zu lassen. Die Preiserhöhung wird trotzdem vermieden.

```
Upgrade-Vorteil = (H − F) × B × (1.095 − O) / 365
                = 3-Jahres-Lock + weggefallene Brücke
```

- Wird ausgewiesen, **sobald das Upgrade den Lock schlägt** (Überlappung O > 0).
- **Spalte „Einsparung 3 Jahre"** zweizeilig: Zeile 1 = Preis-Lock-Wert bzw.
  „kein Lock", Zeile 2 = Term-Upgrade-Vorteil mit Hinweis „Brücke entfällt".
- **KPI-Kachel „Einsparpotenzial via Term-Upgrade (gesamt)"** in Abschnitt 2
  summiert die vollen Upgrade-Vorteile inkl. Aufschlüsselung je Position;
  blendet sich aus, wenn kein Potenzial besteht. Sie ist eine **Alternative**
  zum 3-Jahres-Lock-KPI (nicht addieren).
- Nur für betroffene Jahres-/Mehrjahreslizenzen mit verfügbarem
  3-Jahres-Vertrag (kein Business/F1/F3, Menge ≥ Mindestabnahme `min3y`).

> Annahme „keine Überlappung beim Upgrade" gilt für NCE-Transitions mit
> Proration-Gutschrift; die finale Eligibility ist im Partner-/Distributor-
> Portal zu prüfen.

---

## Nutzung

1. `index.html` im Browser öffnen (oder über GitHub Pages aufrufen).
2. Bezugsweg wählen (Pflicht nur, wenn ein eigener Preis/Stück eingetragen wird).
3. Lizenzen einzeln eintragen **oder** über „📋 Aus Excel einfügen" importieren.
4. Ergebnisse in Abschnitt 2 (Kosten) und Abschnitt 3 (Analyse je Lizenz) lesen.
5. Optional als PDF drucken oder die Auswertung an Dataciders senden.

---

## Technik

- **Eine einzige Datei** (`index.html`) – HTML, CSS und Vanilla-JavaScript,
  **keine Abhängigkeiten**, kein Build-Schritt.
- Preis-/Erhöhungsdaten liegen in der Konstante `PRICES` (oben im `<script>`).
- E-Mail-Versand der Auswertung über **Web3Forms** (Access-Key im Skript
  konfiguriert).
- Deploybar als statische Seite (z. B. GitHub Pages).

### Produktdaten pflegen

Neue SKUs oder geänderte Erhöhungen direkt in `PRICES` ergänzen:

```js
const PRICES = {
  "Microsoft 365 E5": { evp: 662.4, inc: 0.05, min3y: 100 },
  // evp   = Listenpreis/User/Jahr
  // inc   = produktspezifische Erhöhung (0.05 = 5 %)
  // min3y = Mindestabnahme für 3-Jahres-Vertrag (optional)
};
```

---

## Lizenz / Haftung

© 2026 Wiebke Raho · Dataciders SD&C GmbH. Alle Preise sind geschätzte
Microsoft-Listenpreise (EVP) für Juli 2026 – ohne Gewähr. Der Rechner ersetzt
keine finale Validierung im Distributor-/Partner-Portal.
