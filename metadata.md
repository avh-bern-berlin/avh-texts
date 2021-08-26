# AvH Bern -- Metadaten für die Schriften

Hinweis: Alle untenstehenden XPath-Angaben beginnen mit `.../`, stellvertretend für `/TEI/teiHeader/`.

## Titel

Dokumentitel: wird an 2 Stellen angegeben:

1. `.../fileDesc/titleStmt/title[@type="main"]`
1. `.../fileDesc/sourceDesc/biblFull/titleStmt/title[@type="main"]`

## Autoren und Co-Autoren

Autor(en) des Dokuments; werden an 2 Stellen angegeben, jeweils als:

1. `.../fileDesc/titleStmt/author`
1. `.../fileDesc/sourceDesc/biblFull/titleStmt/author`

Innerhalb von `<author>` erfolgt die Angabe des Namens mit einem `<persName>`-Element, das wiederum die einzelnen Elemente des Namens listet:

- `<forename>`: Vorname
- `<nameLink>`: *zu*, *von* etc.
- `<surname>`: Nachname

Mit `<persName ref="...">` ist ein Verweis auf ein Normdatenverzeichnis möglich.

Beispiel:

```xml
<author>
  <persName ref="https://d-nb.info/gnd/118554700">
    <surname>Humboldt</surname>
    <forename>Alexander</forename>
    <nameLink>von</nameLink>
  </persName>
</author>
```

## Publikationsjahr

XPath: `.../fileDesc/sourceDesc/biblFull/publicationStmt/date[@type="publication"]`

Hinweis: Bitte nur die vierstellige Jahreszahl angeben.

### Beispiel

```xml
<date type="publication">1832</date>
```

## Publikationsort(e)

XPath: `.../fileDesc/sourceDesc/biblFull/publicationStmt/pubPlace`

Mehrere Angaben von `<pubPlace>` sind möglich.

### Beispiel aus `1858-xxx_Brief_an_Vogel-07-neu.xml`

```xml
<pubPlace>Haarlem</pubPlace>
<pubPlace>Den Haag</pubPlace>
```

## Bibliografischer Nachweis

XPath: `.../fileDesc/sourceDesc/biblFull/seriesStmt/title[@type="full"]`

Binnenmarkierungen mittels `<i>...</i>` sind möglich, wobei dieses (HTML-)Markup maskiert werden muss: `&lt;i&gt;...&lt;/i&gt;`.

### Beispiel aus `1859-xxx_Ruf_um_Huelfe-104.xml`

```xml
<title type="full">in: &lt;i&gt;Bonplandia. Zeitschrift für die gesammte Botanik&lt;/i&gt; 7:7 (15. April 1859), S. [85]. </title>
```

## Bibliografischer Nachweis en détail    

XPath: `.../fileDesc/sourceDesc/biblFull/seriesStmt`

Dieser Abschnitt muss noch geschrieben werden.

## Schriftart

XPath: `.../fileDesc/sourceDesc/msDesc/physDesc/typeDesc/p`

### Beispiel:

```xml
<physDesc>
  <typeDesc>
    <p>Antiqua</p>
  </typeDesc>
</physDesc>
```

## Dokumentsprache(n)

XPath: `.../profileDesc/langUsage/language`

Das Element `<language ident="...">...</language>` kann mehrfach vergeben werden und enthält, neben dem deutschen Namen der Sprache als Textinhalt das Attribut `@ident` mit dem dreibuchstabigen Sprachkürzel nach [ISO 639-3](https://de.wikipedia.org/wiki/Listen_der_ISO-639-3-Codes), z. B. so:

- Dänisch: `dan`
- Deutsch: `deu`
- Englisch: `eng`
- Französisch: `fra`
- Hebräisch: `heb`
- Italienisch: `ita`
- Latein: `lat`
- Niederländisch: `nld`
- Norwegisch: `nor`
- Portugiesisch: `por`
- Polnisch: `pol`
- Russisch: `rus`
- Spanisch: `spa`
- Schwedisch: `swe`
- Ungarisch: `hun`

### Beispiel aus `1840-Schrift_und_Freiheit-1.xml`

```xml
<profileDesc>
  <langUsage>
    <language ident="deu">Deutsch</language>
    <language ident="spa">Spanisch</language>
    <language ident="lat">Latein</language>
  </langUsage>
</profileDesc>
```

## Identifikatoren

### Sigle Print

Verweis auf die Druckausgabe.

XPath: `.../fileDesc/publicationStmt/idno/idno[@type="print"]`

### Dateiname (Nomenklatur)

Dateiname ohne die Endung `.xml`.

XPath: `.../fileDesc/publicationStmt/idno/idno[@type="basename"]`

### Publikationstyp

XPath: `.../fileDesc/publicationStmt/idno/idno[@type="type"]`

Mit folgenden Werten:

- Primärpublikation: `primary`
- Sekunderpublikation: `secondary`

### Beispiel aus `1840-Schrift_und_Freiheit-1.xml`

```xml
<idno>
  <idno type="print">VI.8</idno>
  <idno type="basename">1840-Schrift_und_Freiheit-1</idno>
  <idno type="type">primary</idno>
</idno>
```

## Dokumentenfamilie

Jedes Dokument innerhalb einer Dokumentenfamilie -- der Primärdruck, andere Sekundärdrucke und das Dokument selbst -- werden angegeben als

XPath: `.../fileDesc/notesStmt/relatedItem`

Das Element `<relatedItem>` enthält keinen Text und folgende Attribute:

- `@target`: zugehörige Datei mit Dateiendung `.xml`
- `@type`:
    - `primary`: zugehöriger Primärdruck
    - `secondary`: zugehöriger Sekundärdruck
    - `self`: das Dokument selbst

Gehört das Dokument zu keiner Familie, kann die Angabe weggelassen werden. Für das Dokument selbst (auch wenn es Primärdruck ist), wird stets `@type="self"` angegeben. Die Reihenfolge ist signifikant!

### Beispiel aus `1820-Sur_la_Limite-1.xml`

```xml
<relatedItem target="1820-Sur_la_Limite-1.xml" type="self"/>
<relatedItem target="1820-Sur_la_Limite-2.xml" type="secondary"/>
<relatedItem target="1820-Sur_la_Limite-3.xml" type="secondary"/>
<relatedItem target="1820-Sur_la_Limite-4-neu.xml" type="secondary"/>
```

### Beispiel aus `1820-Sur_la_Limite-3.xml`

```xml
<relatedItem target="1820-Sur_la_Limite-1.xml" type="primary"/>
<relatedItem target="1820-Sur_la_Limite-2.xml" type="secondary"/>
<relatedItem target="1820-Sur_la_Limite-3.xml" type="self"/>
<relatedItem target="1820-Sur_la_Limite-4-neu.xml" type="secondary"/>
```

## Textverwandtschaft mit selbständig erschienenem Werk

XPath: `.../fileDesc/notesStmt/relatedItem[@type="related"]/bibl`

Inhalt dieses Elements (das mehrfach vergeben werden kann) ist jeweils die bibliografische Angabe. Binnenmarkierungen mittels `<i>...</i>` sind möglich, wobei dieses (HTML-)Markup maskiert werden muss: `&lt;i&gt;...&lt;/i&gt;`.

### Beispiel aus `1846-A_Lofty_Conception-1-neu.xml`

```xml
<relatedItem type="related">
  <bibl>Alexander von Humboldt, &lt;i&gt;Kosmos: A General Survey of the physical phenomena of the universe&lt;/i&gt;, Bd. 1, London: Hippolyte Baillière 1845, S. 158. (Abweichende Übersetzung.)</bibl>
</relatedItem>
<relatedItem type="related">
  <bibl>Alexander von Humboldt, &lt;i&gt;Cosmos: A sketch of a physical description of the universe&lt;/i&gt;, übersetzt von Elise C. Otté, London: Henry G. Bohn 1849, S. 139–140. (Abweichende Übersetzung.)</bibl>
</relatedItem>
<relatedItem type="related">
  <bibl>Alexander von Humboldt,&lt;i&gt; Kosmos. Entwurf einer physischen Weltbeschreibung&lt;/i&gt;, Band 1, Stuttgart und Tübingen: J. G. Cotta 1845, S. 155.</bibl>
</relatedItem>
```

## Posthumer Nachdruck

XPath: `.../fileDesc/sourceDesc/biblFull/notesStmt/relatedItem[@type="reprint"]/bibl`

Inhalt dieses Elements (das mehrfach vergeben werden kann) ist jeweils die bibliografische Angabe. Binnenmarkierungen mittels `<i>...</i>` sind möglich, wobei dieses (HTML-)Markup maskiert werden muss: `&lt;i&gt;...&lt;/i&gt;`.

### Beispiel aus `1817-Des_lignes_isothermes-01.xml`

```xml
<relatedItem type="reprint">
  <bibl>übersetzt, in: Alexander von Humboldt, &lt;i&gt;Schriften zur Physikalischen Geographie&lt;/i&gt;, herausgegeben von Hanno Beck, Darmstadt 1989, S. 18–97. (Studienausgabe Band VI)</bibl>
</relatedItem>
```

## Verweise auf Bilddigitalisate

XPath: `.../fileDesc/sourceDesc/msDesc/msIdentifier/repository/ref`

Das Element `<ref>` enthält ein Attribut `@target` mit dem entsprechenden URL. Als Textinhalt kann eine Beschreibung der Quelle angeben werden.

### Beispiel aus `1799-Alexander_von_Humboldt-1.xml`

```xml
<msIdentifier>
  <repository>
    <ref target="https://www.deutschestextarchiv.de/humboldt_moll_1799">Deutsches Textarchiv</ref>
  </repository>
</msIdentifier>
```
