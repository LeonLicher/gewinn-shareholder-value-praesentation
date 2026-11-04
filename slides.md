---
theme: default
highlighter: shiki
favicon: /images/favicon.png
title: Gewinn vs. Shareholder Value
fonts:
  sans: 'Nunito Sans'
  serif: 'Nunito Sans'
  mono: 'Fira Code'
  weights: '400, 500, 600,700'
presentationInfo:
  title: 'Gewinn als Zielgröße'
  subtitle: 'Grenzen und Vergleich mit Shareholder Value'
  semester: 'WiSe 2026/27 · Gruppe 1'
  authors:
    - name: 'Christian Dörschug'
    - name: 'Mathis Arends'
    - name: 'Matteo Krandick'
    - name: 'Leon Licher'
    - name: 'Daniel Fischer'
  chapters:
    - number: 1
      title: 'Gewinn als Ziel'
    - number: 2
      title: 'Gewinn vs. Shareholder Value'
    - number: 3
      title: 'Anhang'
---
layout: cover

---
layout: team
title: Vorstellung
---

---
title: Gewinn als Unternehmensziel
subtitle: Unzulänglichkeiten – und warum er trotzdem so beliebt ist
chapter: 1
class: profit-overview muted-lists
clicks: 2
---

<Columns columns="1.15fr 0.85fr" gap="1.25rem">
  <BulletedList v-click="1" title="Unzulänglichkeiten des Gewinns">
    <li>
      <b>Bewertungswahlrechte</b><Footnote text="Rappaport, A. (1999): Shareholder Value, 2. Aufl., Stuttgart, S. 16–23." />
      <SubText>LIFO/FIFO, Abschreibungsmethoden, Goodwill: Gewinn ändert sich, Cashflow und Wert nicht.</SubText>
    </li>
    <li>
      <b>Investitionsbedarf wird ausgeblendet</b>
      <SubText>Mehr Forderungen, Vorräte und Anlagen binden Liquidität, erscheinen aber nicht als Aufwand.</SubText>
    </li>
    <li>
      <b>Kein Zeitwert des Geldes</b>
      <SubText>Gewinn ist eine Periodengröße und wird nicht abgezinst; Zahlungszeitpunkte bleiben unberücksichtigt.</SubText>
    </li>
    <li>
      <b>Risiko bleibt unberücksichtigt</b>
      <SubText>Geschäfts- und Finanzierungsrisiko sowie die Kapitalkosten fehlen in der Gewinngröße.</SubText>
    </li>
  </BulletedList>

  <BulletedList v-click="2" title="Gründe für die Beliebtheit">
    <li>
      <b>Einfach &amp; verfügbar</b>
      <SubText>Wird pro Periode ermittelt, ist leicht verständlich und schnell kommuniziert.</SubText>
    </li>
    <li>
      <b>Normiert &amp; geprüft</b>
      <SubText>HGB/IFRS und die Abschlussprüfung schaffen Vergleichbarkeit und Vertrauen.</SubText>
    </li>
    <li>
      <b>Kapitalmarkt-Fokus auf EPS</b><Footnote text="Rappaport, A. (1999): Shareholder Value, 2. Aufl., Stuttgart, S. 15. Übrige Gründe: eigene Ergänzung." />
      <SubText>Presse und Analysten berichten über Gewinn pro Aktie und KGV.</SubText>
    </li>
    <li>
      <b>Anknüpfungspunkt</b>
      <SubText>Grundlage für Ausschüttung, Steuern und Managementvergütung.</SubText>
    </li>
  </BulletedList>
</Columns>

<!--
Animation: Klick 1 blendet die linke Spalte vollständig ein, Klick 2 die rechte. Nur dezentes Einblenden, keine Bewegung.

Kernaussage: Der Gewinn misst Periodenerfolg nach Buchhaltungsregeln, nicht die Veränderung des ökonomischen Unternehmenswerts.

Rappaport nennt drei Gründe (S. 16 ff.):
1. Alternative Bewertungsverfahren (LIFO/FIFO, linear vs. degressiv, Goodwill). Beispiel IBM/Lotus: Mehr als die Hälfte des Kaufpreises von 3,2 Mrd. $ wurde sofort als F&E abgeschrieben.
2. Investitionen ins Umlauf- und Anlagevermögen werden nicht abgezogen.
3. Der Zeitwert des Geldes wird ignoriert.
Zusätzlich fehlt das Risiko (S. 23).

Beliebtheit: Der Gewinn ist bequem, rechtlich verankert (Ausschüttungsbemessung, Steuerbilanz) und wird vom Kapitalmarkt laufend kommuniziert ("zwanghafte Beschäftigung mit EPS", S. 15).
-->

---
title: Gewinn ≠ Shareholder Value
subtitle: 'Gamma Inc.: Warum mehr Gewinn nicht automatisch mehr Wert bedeutet'
chapter: 2
clicks: 3
---

<GammaComparison v-click="1" />

<!--
Animation: zunächst leer → Klick 1: Ausgangspunkt → Klick 2: Szenario A → Klick 3: Szenario B. Mit der normalen Slidev-Steuerung fortschalten (Pfeiltaste rechts oder Leertaste); Pfeiltaste links geht zurück.

Mechanismus: Wachstum mit Investitionen kann den Gewinn auch dann steigern, wenn die Rendite unter den Kapitalkosten liegt. Der Gewinn zieht weder die Investition noch die Kapitalkosten ab.

Gamma-Rechnung (Eigenkapitalkosten 12 %, Vollausschüttung, kein Fremdkapital):
- Status quo: 18 / 0,12 = 150
- A: 19,8 / 0,12 = 165 − 15 = 150 → Gewinn +10 %, Wert unverändert (Rendite = 12 % = Kapitalkosten)
- B: 20,4 / 0,12 = 170 − 30 = 140 → Gewinn +13,3 %, Wert −10 Mio. (Rendite 2,4 / 30 = 8 % < 12 %)

Rappaport nennt für B eine Umsatzrendite von 10 % statt 15 %. Rechnerisch ergibt sich aus 34 / 240 ein Wert von ca. 14 % auf den Gesamtumsatz. Die Grenzrendite auf den Zusatzumsatz liegt bei 4 / 40 = 10 %.

Zusätzlich: Aktienkurse reagieren auf Erwartungen. Liegt der ausgewiesene Gewinn unter den Erwartungen, kann der Kurs trotz Gewinnwachstum fallen.
-->

---
layout: closing
---

---
title: Anhang A – Rechnung Gamma Inc.
subtitle: Detaillierte Überleitung nach Rappaport (1999), S. 21–23
chapter: 3
---

<Columns columns="1fr 1fr" gap="1.25rem">
  <Table
    :headers="['Mio. $', 'Status quo', 'A', 'B']"
    :rows="[
      ['Umsatz', '200,0', '220,0', '240,0'],
      ['Betriebsaufwand', '170,0', '187,0', '206,0'],
      ['Gewinn vor Steuern', '30,0', '33,0', '34,0'],
      ['Steuern (40 %)', '12,0', '13,2', '13,6'],
      ['Gewinn = Cashflow', '18,0', '19,8', '20,4'],
      ['Barwert (÷ 0,12)', '150,0', '165,0', '170,0'],
      ['− Investition', '0,0', '15,0', '30,0'],
      ['<b>Shareholder Value</b>', '<b>150,0</b>', '<b>150,0</b>', '<b>140,0</b>']
    ]"
    :columnWidths="['40%', '20%', '20%', '20%']"
    accent="blue"
    size="sm"
  />

  <div class="flex flex-col gap-3">
    <DefinitionBox title="Grenzrendite der Zusatzinvestition">
      A: 1,8 / 15 = <b>12 %</b> = Kapitalkosten → Wert bleibt gleich<br />
      B: 2,4 / 30 = <b>8 %</b> &lt; Kapitalkosten → Wert sinkt<Footnote text="Rappaport, A. (1999): Shareholder Value, 2. Aufl., Stuttgart, S. 20–23. Annahmen: kein Fremdkapital, 40 % Steuern, Vollausschüttung, konstante Cashflows, Eigenkapitalkosten 12 %." />
    </DefinitionBox>
    <ExampleBox title="Betrieblicher Cashflow (Rappaport, S. 20)">
      Umsatz − Betriebsaufwand inkl. Steuern<br />
      + Abschreibungen u. a. nicht zahlungswirksame Posten<br />
      − Zusatzinvestitionen ins Umlaufvermögen<br />
      − Zusatzinvestitionen ins Anlagevermögen
    </ExampleBox>
  </div>
</Columns>

---
title: Anhang B – Gewinn vs. Cashflow & Empirie
subtitle: Tabelle 2-1 und 2-2 nach Rappaport (1999)
chapter: 3
---

<Columns columns="1fr 1fr" gap="1.25rem">
  <Table
    :headers="['Überleitung (Tab. 2-1)', 'Tsd. $']"
    :rows="[
      ['Reingewinn', '500'],
      ['− Zunahme Forderungen', '−200'],
      ['− Zunahme Vorräte', '−300'],
      ['+ Zunahme Verbindlichkeiten (50 + 10)', '+60'],
      ['+ Abschreibungen', '+100'],
      ['− Investitionen ins Anlagevermögen', '−150'],
      ['+ Zunahme Steuerrückstellungen', '+30'],
      ['<b>Cashflow</b>', '<b>40</b>']
    ]"
    :columnWidths="['72%', '28%']"
    accent="blue"
    size="sm"
  />

  <Table
    :headers="['S&P 500', 'EPS-Wachstum', 'Aktionärsrendite']"
    :rows="[
      ['1987', '+20,9 %', '+5,2 %'],
      ['1989', '−3,6 %', '+31,5 %'],
      ['1991', '−25,2 %', '+30,6 %'],
      ['1993', '+14,6 %', '+10,0 %'],
      ['1994', '+39,9 %', '+1,3 %'],
      ['1995', '+11,0 %', '+37,4 %'],
      ['1996', '+14,0 %', '+23,1 %']
    ]"
    :columnWidths="['30%', '35%', '35%']"
    accent="gray"
    size="sm"
  />
</Columns>

<div class="mt-3 text-sm text-gray-500">
  Auswahl aus Tab. 2-2 (1986–1996). Zwischen EPS-Wachstum und Aktionärsrendite (Dividenden + Kursänderung) ist kein systematischer Zusammenhang erkennbar.<Footnote text="Rappaport, A. (1999): Shareholder Value, 2. Aufl., Stuttgart, S. 19 (Tab. 2-1) und S. 24 (Tab. 2-2); Daten: Standard &amp; Poor’s, Ibbotson Associates (1997)." />
</div>

---
title: Anhang C – Literatur
subtitle: Quellenverzeichnis
chapter: 3
---

<CitationTable
  :citations="[
    { id: '1', text: 'Rappaport, Alfred (1999): Shareholder Value. Ein Handbuch für Manager und Investoren, 2. Aufl., Stuttgart: Schäffer-Poeschel, S. 15–24.' },
    { id: '2', text: 'Standard &amp; Poor’s; Ibbotson Associates (1997): Stocks, Bonds, Bills, and Inflation – 1997 Yearbook, Chicago (zitiert nach [1], Tab. 2-2).' }
  ]"
  idWidth="10%"
/>
