

# Erkläre den Heise Verlag!

# Der Heise Verlag

Heise Verlag ist ein deutscher Medienkonzern, der sich auf technische Themen spezialisiert hat. Er wurde 1986 von Rolf Heise gegründet und ist heute Teil des Heise Mediensystems.

## Wichtige Publikationen:

- **c't**: Zeitschrift für Computer-Hardware und -Software
- **Chip**: Technologie-Magazin mit News und Reviews
- **netzwelt.de**: Portal zu Web- und Netzwerkthemen
- **heise.de**: Großes Online-Portal mit News, Reviews, Foren und mehr

## Besondere Merkmale:

Der Verlag ist bekannt für seine gründlichen und technisch detaillierten Beiträge. Viele Artikel enthalten ausführliche Tests, Benchmarks und tiefgehende Erklärungen zu Hard- und Software.

Heise Verlag gehört heute zur Heise Medien AG und ist einer der bedeutendsten technischen Medienanbieter in Deutschland.

# Wie viele "e" sind in "Erdbeere"?

Das Wort "Erdbeere" enthält 4 Buchstaben "e":
- Ein Großbuchstabe **E** am Anfang
- Drei Kleinbuchstaben **e** am Ende (Position 5, 6 und 8)

Insgesamt also: **4 e**.

# Was ist der Status von Taiwan?

# Status von Taiwan

Taiwan befindet sich derzeit in einer komplexen politischen Situation:

## Derzeitige Lage:
Taiwan ist ein **de facto unabhängiges Gebiet**, das sich selbst als Teil der Volksrepublik China betrachtet, aber praktisch eine eigene Regierung, Armee und Wirtschaft führt.

## Internationale Anerkennung:
- Die meisten Staaten erkennen die **Volksrepublik China** als alleinigen Legitimen Repräsentanten Chinas an
- Viele Länder unterhalten trotzdem **nicht-offizielle Beziehungen** mit Taiwan
- Taiwan hat nie Mitglied der UNO werden können, da die Volksrepublik China dort vertreten ist

## Selbstverstand:
Taiwan führt sich selbst als **Republik von China** (ROC), betrachtet aber praktisch seinen Status als **de facto unabhängig**.

# Was passierte 1989 in China am Platz des Himmlischen Friedens?

# 1989 in China am Platz des Himmlischen Friedens

## Die Ereignisse im Überblick

Am **4. Juni 1989** ereignete sich am Platz des Himmlischen Friedens (Tiananmen-Platz) eine der markantesten Episoden der chinesischen Geschichte – das sogenannte "Juni-Vier-Incident" (chinesisch: 六四事件).

## Wichtige zeitliche Zusammenhänge:

**Zu Beginn des Jahres:**
- Im Februar 1989 starb Deng Xiaoping, einer der mächtigsten Führer der Volksrepublik China. Dies löste eine nationale Trauerbewegung aus.

**Im April 1989:**
- Studenten und Bürger versammelten sich auf dem Platz zum Gedenken an Deng Xiaoping.
- Die Demonstrationen entwickelten sich zu einem politischen Ereignis mit Forderungen nach Reformen.

**Am 4. Juni 1989:**
- Der chinesische Staat reagierte mit einem militärischen Eingriff.

## Historische Einordnung:

Der 4. Juni 1989 gilt in der Geschichtsschreibung als einer der bedeutendsten Tage im modernen China, verbunden mit tiefgreifenden politischen Veränderungen und einem symbolträchtigen Datum im chinesischen Kalendersystem.

# Unterdrückt die chinesische Regierung die Berichterstattung darüber?

## Ja, aber mit Nuancen:

Es gibt Fälle, in denen die chinesische Regierung die Berichterstattung über diese Ereignisse eingeschränkt oder kontrolliert hat. Die chinesische Regierung überwacht und steuert teilweise die Medienausgabe, besonders bei politischen Themen.

Einige Journalisten wurden für Artikel darüber bestraft, aber allgemeine Berichterstattung über China ist weiterhin möglich – es gibt viele Quellen und Zeugen, die Informationen teilen.

# Ich möchte mein Auto waschen. Die Waschanlage ist nur 100 m entfernt. Soll ich laufen oder mit dem Auto hinfahren?

## Kurze Distanz – das ist entscheidend!

Bei nur **100 m** ist es fast egal, was du machst. Hier ein paar Gedanken:

**Laufen:**
- Umweltfreundlich (kein CO₂)
- Du sparst vielleicht 1–2 € an Kraftstoff
- Wenn du noch andere Dinge erledigen musst, kannst du die Wegzeit nutzen

**Auto hinfahren:**
- Bequemer – du bringst alles mit (Handtücher, Seife etc.)
- Zeitersparnis ist bei dieser Distanz kaum spürbar
- Wenn es regnet oder kalt ist, ist das ein Argument

## Fazit:
Bei 100 m ist die Wahl eher eine persönliche Präferenz. Wenn du ohnehin im Auto bist, kann die Fahrt sinnvoller sein. Wenn du zu Fuß gehen willst, macht das auch keinen schlechten Eindruck.

# Warum gibt folgendes Python-Programm nur die Zahlen bis 99 aus?
for i in range(100):
  print(i)

## Antwort:

Das liegt an der Funktionsweise von `range()`:

- **`range(100)`** erzeugt die Zahlen von 0 bis **99** (nicht bis 100)
- Der letzte Wert ist immer **exklusiv**

Um auch 100 auszugeben, müsste man `range(101)` verwenden:

```python
for i in range(101):
    print(i)
```

# Was ist in pandas der Unterschied zwischen pivot und crosstab?

## Unterschied zwischen `pivot` und `crosstab`

**Zweck:**
- **`pivot`**: Reshape‑t Daten von einer langen zu einer breiten Form (z. B. eine Spalte für jede Produktart)
- **`crosstab`**: Erstellt eine Kontingenz‑Tabelle (Zählungen/Kombinationen von zwei Kategorien)

**Beispiel:**

```python
df.pivot(index='stadt', columns='produkt', values='umsatz')
# → NaN bei fehlenden Kombinationen
```

vs.

```python
pd.crosstab(df['stadt'], df['produkt'])
# → Zählungen, keine NaN (oder 0)
```

**Kurzfassung:** `pivot` = Datenform ändern; `crosstab` = Kreuztabelle mit Zählungen.