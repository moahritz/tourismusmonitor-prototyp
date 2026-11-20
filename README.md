# Tourismusmonitor Vorarlberg – Prototyp

Monatliche Schätzung der touristischen Bruttowertschöpfung (BWS) aus Verwaltungsdaten (UVA, Lohndaten, Beherbergungsstatistik), angebunden an die Regionale Gesamtrechnung (RGR) und das regionale Tourismus-Satellitenkonto (RTSA).

**Alle Zahlen und Destinationen im Dashboard sind fiktiv.** Keine amtliche Statistik und keine Veröffentlichung des Landes Vorarlberg oder von Vorarlberg Tourismus.

## Seiten

| Seite | Inhalt |
| --- | --- |
| `index.html` | Dashboard: Kennzahlen je Gebiet und Monat, Abgleich mit dem RTSA, Ampel, Durchlauf aller Rechenschritte |
| `executive-summary.html` | Überblick über das Modell in einfacher Form |
| `modell.html` | Vollständige Modellbeschreibung mit allen Formeln (kombiniertes Modell) |
| `kennzahlenproduktion.html` | Produktion der Kennzahlen: Variablen, Quellen, Erhebungsstrategie, Kalender, Rollen |

Alle Seiten sind statisch und laden nichts von außen. Das Dashboard ist eine eigenständige Datei (Daten, d3 und Schrift eingebettet); die Unterseiten nutzen `assets/site.css` und die Schriften in `assets/fonts/`. Formeln sind MathML.

## Rechenkern des Dashboards (kombiniertes Modell)

Das Dashboard rechnet dieselben Schritte wie die Modellbeschreibung:

1. Produktionswert = UVA-Umsatz, Quartalszahler hochgerechnet
2. Vorleistungen aus Strukturmodell (LSE-Quote, preisfortgeschrieben, nach φ fix/öffnungs-/umsatzabhängig auf Monate verteilt) und Vorsteuer-Signal (Vorsteuer ÷ s̄ × (1 − inv)(1 + zus), drei Monate geglättet), gemischt mit κ = 0,5
3. BWS = PW − V; Personalaufwand = Lohnsumme × (1 + α), α aus der RGR; Betriebsüberschuss
4. Ampel auf gleitenden 12 Monaten: VL-Quote gegen LSE, Einkommensansatz gegen RGR-Lohnquote
5. Anbindung: proportionales Denton an die RGR, Tourismusanteil τ = k · τ_national am RTSA; Jahre ohne Anker übernehmen das Verhältnis des letzten angebundenen Jahres
6. Kennzahlen für Monat, Saison und 12 Monate

Eingangsdaten (fiktiv) liegen als CSV in `window.TM_CSV`: `rohdaten`, `naechtigungen`, `parameter`, `preise`, `rgr`, `rtsa`. Der Flash (Nowcast um Tag 25) ist im Prototyp nicht abgebildet.
