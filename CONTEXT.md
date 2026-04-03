# Widget HomeZero — Project Context

## Wat is dit?

Een embeddable JavaScript-widget voor HomeZero. Klanten plaatsen een `<hz-embed>` tag op hun website; de widget rendert een formulier (adres, dropdown, telefoon, e-mail, checkbox) en stuurt de gebruiker door naar de HomeZero-applicatie.

De widget ondersteunt meerdere configuraties via `data-*` attributen en werkt in twee omgevingen:
- **Acceptance** — testomgeving (hier werken we)
- **Production** — live omgeving (nooit aanraken)

---

## Bewerkbare bestanden

| Bestand | Functie |
|---|---|
| `Acceptance/embed.js` | Hoofdlogica van de widget (2300+ regels) |
| `Acceptance/embed-styles.css` | Alle styling van het formulier |
| `Acceptance/test.html` | Lokale testpagina |

**Nooit bewerken:** `Production/*`, `*.min.js`, `*.min.css`

---

## Beschikbare `data-*` configuratie

```html
<hz-embed
  src="..."                               <!-- Vaste flow-URL (geen dropdown/kaarten) -->
  data-color="#004DF5"                    <!-- Primaire kleur -->
  data-button-text="Start"               <!-- Knoptekst -->
  data-button-radius="10px"              <!-- Border radius knop -->
  data-open-new-tab="true"               <!-- Nieuw tabblad openen -->
  data-title="Titel"                     <!-- Formulier titel -->
  data-subtitle="Subtitel"              <!-- Formulier subtitel -->
  data-address-format="dutch"            <!-- dutch | international -->
  data-language="nl"                     <!-- nl | en | fr | de -->
  data-show-phone="true"                 <!-- Toon telefoonnummerveld -->
  data-phone-required="true"             <!-- Telefoon verplicht -->
  data-show-email="true"                 <!-- Toon e-mailveld -->
  data-email-required="true"             <!-- E-mail verplicht -->
  data-google-search="true"              <!-- Google Places autocomplete -->
  data-country="nl"                      <!-- Land (voor adresformaat) -->
  data-checkbox-title="..."              <!-- Checkbox tekst (tonen als ingevuld) -->
  data-checkbox-shorttitle="..."         <!-- Checkbox parameter naam -->
  data-checkbox-required="true"          <!-- Checkbox verplicht -->
  data-installer="..."                   <!-- Installer parameter -->
  data-context="..."                     <!-- Extra context parameter -->

  <!-- Maatregelkaarten (alleen als src NIET is ingesteld) -->
  data-measurement-{type}-url="..."      <!-- Flow-URL voor deze maatregel -->
  data-measurement-{type}-title="..."    <!-- Label op de kaart -->
  data-combined-url="..."               <!-- URL voor gecombineerde flow (meerdere kaarten geselecteerd) -->
></hz-embed>
```

### Ondersteunde maatregel-types (met ingebouwd icoon)

| Type | Label |
|---|---|
| `solarpanels` | Zonnepanelen |
| `heatpump` | Warmtepomp |
| `homebattery` | Thuisbatterij |
| `airconditioning` | Airconditioning |
| `solarboiler` | Zonneboiler |
| `gasboiler` | Gasketel |
| `advicescan` | Adviesscan |
| `advisormodule` | Adviseur |
| `general` | Generiek (huis-icoon) |

---

## Lokale ontwikkelomgeving

```bash
npm run dev
```

Opent automatisch `http://localhost:3000/test.html` met live reload.
Elke wijziging in `embed.js` of `embed-styles.css` herlaadt de browser direct.

---

## Geplande aanpassingen

### Design
- [ ] Kaart-styling verder verfijnen (grootte, typografie, iconen)

### Layout / structuur
- [x] Maatregelen als kaarten tonen i.p.v. dropdown (multi-select)

### Nieuwe functionaliteit
- [x] Multi-select maatregelkaarten — 1 selectie → eigen flow, meerdere → gecombineerde flow
- [ ] Gecombineerde flow URLs per combinatie definiëren (`data-combined-url`)

---

## Beslissingen & notities

### 2026-04-01
- Dev setup opgezet: `browser-sync` als live preview tool (`npm run dev`)
- `CONTEXT.md` aangemaakt als projectdocument
- Dropdown vervangen door klikbare maatregelkaarten (multi-select)
- Bij 1 kaart geselecteerd → `data-measurement-{type}-url` wordt de flow-URL
- Bij meerdere kaarten → `data-combined-url` attribuut (nog in te vullen per combinatie)
- `setupCustomDropdown()` wordt nu alleen aangeroepen als er nog een `.dropdown-selected` in het formulier zit (backwards compatible)
