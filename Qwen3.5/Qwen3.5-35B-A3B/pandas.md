In **pandas** dienen sowohl `pivot` als auch `crosstab` dazu, Daten umzustrukturieren und zu analysieren, aber sie haben unterschiedliche **Zwecke** und **Funktionsweisen**.

Hier ist der Hauptunterschied auf einen Blick:

| Feature | `pivot` | `crosstab` |
| :--- | :--- | :--- |
| **Hauptzweck** | Umformatierung (Long → Wide) ohne Aggregation. | Erstellung von Häufigkeitstabellen (Kontingenztabelle). |
| **Aggregation** | **Nein** (Wirft Fehler bei Duplikaten). | **Ja** (Zählt standardmäßig Vorkommen). |
| **Eingabe** | Ein DataFrame. | Arrays, Series oder DataFrame-Spalten. |
| **Typische Anwendung** | Daten für Visualisierung oder Analyse vorbereiten. | Statistische Zusammenhänge zwischen kategorialen Variablen prüfen. |

---

### 1. `df.pivot()`
Die Funktion `pivot` wird verwendet, um **bestehende Daten neu anzuordnen**. Sie nimmt Spalten und macht sie zu Index oder Spaltenüberschriften.

*   **Wichtig:** Es darf keine Duplikate geben. Wenn eine Kombination aus Index und Spalte mehr als einmal vorkommt, wirft `pivot` einen Fehler (`ValueError`).
*   **Keine Aggregation:** Sie nimmt die Werte einfach so, wie sie sind, und platziert sie im neuen Grid.

```python
import pandas as pd

data = {'A': ['foo', 'foo', 'bar'], 
        'B': ['one', 'two', 'one'], 
        'C': [10, 20, 30]}
df = pd.DataFrame(data)

# Funktioniert, weil 'A' und 'B' Kombinationen eindeutig sind
pivot_df = df.pivot(index='A', columns='B', values='C')
```

### 2. `pd.crosstab()`
Die Funktion `crosstab` berechnet eine **Kreuztabelle** (Häufigkeitstabelle). Sie zählt, wie oft Kombinationen von Werten vorkommen.

*   **Aggregation:** Sie aggregiert standardmäßig (zählt die Vorkommen).
*   **Flexibilität:** Sie kann direkt mit Listen oder Series arbeiten, ohne einen DataFrame zu benötigen.
*   **Statistik:** Sie eignet sich hervorragend für kategorische Daten (z. B. "Wie oft wurde Produkt X in Region Y gekauft?").

```python
import pandas as pd

a = ['foo', 'foo', 'bar', 'bar', 'foo']
b = ['one', 'two', 'one', 'two', 'one']

# Erstellt eine Tabelle, die zählt, wie oft 'a' und 'b' kombiniert vorkommen
ct = pd.crosstab(a, b)
```

---

### Wann benutzt man was?

1.  **Benutze `pivot`, wenn:**
    *   Du eine "Long-Table" (lang) in eine "Wide-Table" (breit) umwandeln willst.
    *   Du bereits numerische Werte in einer Spalte hast, die du auf die neue Matrix verteilen willst.
    *   Du sicher bist, dass keine doppelten Einträge pro Zelle existieren.

2.  **Benutze `crosstab`, wenn:**
    *   Du die **Häufigkeit** (Anzahl) von Kombinationen wissen willst.
    *   Du statistische Analysen an kategorialen Daten durchführst (z. B. Chi-Quadrat-Test).
    *   Du Normalisierungen (Prozente statt Rohzahlen) möchtest (`normalize='index'` oder `columns`).

### Hinweis zur `pivot_table`
Oft wird `pivot` mit `pivot_table` verwechselt.
*   `pivot`: Kein Aggregieren, strikt bei Duplikaten.
*   `pivot_table`: **Mit Aggregieren** (Standard ist `mean`), erlaubt Duplikate (durch Aggregation).
*   `crosstab`: Spezialfall von `pivot_table`, optimiert für Häufigkeiten (Standard ist `count`).

**Zusammenfassend:** Willst du Daten umstrukturieren? → `pivot`. Willst du Zusammenhänge zählen? → `crosstab`.
