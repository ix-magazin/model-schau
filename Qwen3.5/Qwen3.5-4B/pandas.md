In pandas gibt es einen wichtigen Hinweis vorab: Die Funktion **`pivot`** wurde bereits in neueren Versionen von pandas (ab Version 0.20) entfernt oder als veraltet markiert. Der moderne Standard ist **`pivot_table`**.

Manche Nutzer sprechen dennoch noch von „pivot", aber technisch vergleichen sollte man **`pivot_table`** mit **`crosstab`**.

Hier sind die wesentlichen Unterschiede:

### 1. Der Hauptunterschied: Zweck und Flexibilität

| Merkmal | `pivot_table` | `crosstab` |
| :--- | :--- | :--- |
| **Zweck** | **Allgemein:** Um Daten zu reshaping (Umfeldung) und Aggregation (Summe, Durchschnitt, Mittelwert, etc.) | **Spezifisch:** Für Kontingenztabellen (Häufigkeitstabsellen) von kategorischen Daten. |
| **Parameter** | Nimmt `index`, `columns`, `values`, `aggfunc`, `dropna`, etc. | Nimmt `index`, `columns`, `values` (optional). |
| **Aggregation** | Kann beliebige Funktionen wählen (Summe, Mittelwert, Min, Max, Count, etc.) | Standardmäßig **Zählung (count)**. Wenn `values` angegeben wird, kann man auch andere Funktionen wählen, aber `crosstab` ist auf Zählung optimiert. |
| **Datenarten** | Funktioniert mit beliebigen Daten (numerisch, kategorisch, Datetime). | Besteht meist für kategorische Daten, aber kann auch numerisch funktionieren. |
| **Syntax** | `df.pivot_table(...)` | `pd.crosstab(...)` |

### 2. Beispiel `pivot_table` (Allgemein)
Hier wird oft eine Summe oder ein Durchschnitt berechnet.

```python
import pandas as pd

df = pd.DataFrame({
    'Region': ['Nord', 'Nord', 'Süd', 'Süd'],
    'Produkt': ['Auto', 'Auto', 'Auto', 'Auto'],
    'Umsatz': [1000, 2000, 1500, 3000]
})

# Pivot-Table: Summe des Umsatzes nach Region und Produkt
table = df.pivot_table(
    index='Region',
    columns='Produkt',
    values='Umsatz',
    aggfunc='sum'
)
```
Ergebnis:
```
Produkt    Auto
Region               
Nord        3000
Süd          4500
```

### 3. Beispiel `crosstab` (Häufigkeit)
Hier werden einfach die Häufigkeiten gezählt.

```python
df = pd.DataFrame({
    'Status': ['Aktiv', 'Inaktiv', 'Aktiv', 'Inaktiv', 'Aktiv'],
    'Alter': ['Junge', 'Junge', 'Älter', 'Älter', 'Junge']
})

# Crosstab: Anzahl der Vorkommen pro Gruppe
ct = pd.crosstab(df['Status'], df['Alter'])
```
Ergebnis:
```
Alter
Status    Junge  Älter
Aktiv      3       0
Inaktiv    1       1
```

### 4. Wann wofür?

*   **Verwende `pivot_table`, wenn:**
    *   Du eine Summe, einen Durchschnitt oder andere Aggregationsfunktionen brauchst (z.B. Umsatz pro Kunde).
    *   Du mit numerischen Daten arbeitest.
    *   Du mehr Kontrolle über die Struktur der Tabelle hast (z.B. `normalize=True`).

*   **Verwende `crosstab`, wenn:**
    *   Du einfach nur die Häufigkeit (Counts) bestimmter Kategorien zählen möchtest.
    *   Du eine Kontingenztafel für statistische Tests (z.B. Chi-Quadrat-Test) vorbereiten willst.
    *   Du die Syntax für eine reine Häufigkeitstabellen einfach halten möchtest.
    *   *Hinweis:* `crosstab` ist im Grunde eine Spezialversion von `pivot_table` mit `values=None` und `aggfunc=count`.

### 5. Zusammenfassung

*   **`pivot_table`** ist der **allround-taugliche Werkzeug** für das Umformen und Zusammenfassen von Daten.
*   **`crosstab`** ist ein **spezialisiertes Werkzeug** für die Erstellung von Häufigkeitstabsellen (Kontingenztabellen).

Wenn du einfach nur die Häufigkeit zählen willst, ist `crosstab` oft schneller zu schreiben. Wenn du komplexe Analysen mit Aggregationen brauchst, ist `pivot_table` die richtige Wahl.
