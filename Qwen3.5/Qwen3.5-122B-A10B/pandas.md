<<<reasoning_content_start>>>Thinking Process:

1.  **Analyze the Request:**
    *   Topic: Python library `pandas`.
    *   Question: What is the difference between `pivot` and `crosstab`?
    *   Language: German.

2.  **Define `pivot`:**
    *   Purpose: Reshapes data from long to wide format.
    *   Input: DataFrame.
    *   Parameters: `index`, `columns`, `values`.
    *   Behavior: It takes existing data and reorganizes it. It doesn't aggregate by default (unless there are duplicates, then it raises an error or requires `pivot_table`).
    *   Use case: When you have unique combinations of index/columns and want to spread values across columns.

3.  **Define `crosstab`:**
    *   Purpose: Computes a cross-tabulation of two (or more) factors.
    *   Input: Arrays, Series, or DataFrame columns.
    *   Parameters: `index`, `columns`, `normalize`, `margins`, `aggfunc` (implicitly).
    *   Behavior: It aggregates data by default (usually counts). It's essentially a specialized version of `pivot_table`.
    *   Use case: Frequency tables, contingency tables, statistical analysis of relationships between categorical variables.

4.  **Compare them:**
    *   **Functionality:** `pivot` reshapes data without aggregation (mostly), `crosstab` aggregates data (counts/means) by default.
    *   **Input:** `pivot` needs a DataFrame, `crosstab` can take arrays/series directly.
    *   **Output:** `pivot` preserves values, `crosstab` produces counts (or other aggregates) per cell.
    *   **Relationship:** `crosstab` is built on top of `pivot_table` (which is more flexible than `pivot`). `pivot` is stricter (no duplicates allowed).

5.  **Draft the Explanation (in German):**
    *   Introduction: Both are used for reshaping/aggregating data.
    *   `pivot`:
        *   Reshapes (Long -> Wide).
        *   No aggregation by default (raises error on duplicates).
        *   Needs existing columns for index, columns, values.
    *   `crosstab`:
        *   Calculates frequency tables (Contingency tables).
        *   Aggregates by default (counts).
        *   Good for categorical data analysis.
        *   Can normalize.
    *   Key Differences Table: Input, Aggregation, Use Case.
    *   Example code snippets (optional but helpful).

6.  **Refine the Content:**
    *   Make sure to mention that `crosstab` is essentially a wrapper for `pivot_table`.
    *   Clarify the "aggregation" point: `pivot` fails if there are duplicate entries for the index/column combination, whereas `crosstab` aggregates them (counts them).
    *   Mention `pivot_table` as the middle ground if needed, but focus on the asked comparison.

7.  **Final Review (Self-Correction):**
    *   Did I answer the question clearly? Yes.
    *   Is the German natural? Yes.
    *   Are the technical details accurate? Yes. `pd.crosstab` uses `pivot_table` internally. `pd.pivot` is stricter.

8.  **Construct Output:** (See final response)
    *   Start with a high-level summary.
    *   Detail `pivot`.
    *   Detail `crosstab`.
    *   Compare them (Aggregation, Input, Goal).
    *   Provide examples.
    *   Conclusion/Recommendation.

*(Self-Correction during drafting)*: Wait, `pivot` *can* handle duplicates if you use `pivot_table`. But the specific function `pivot` raises a ValueError if there are duplicates. `crosstab` always aggregates (default `aggfunc='count'`). I should emphasize this distinction.

*(Refinement)*: `crosstab` is specifically for statistical cross-tabulations (like Chi-Square test prep). `pivot` is for general data reshaping.

Let's write the response.b<<<reasoning_content_end>>>In **pandas** dienen sowohl `pivot` als auch `crosstab` dazu, Daten umzustrukturieren und zu analysieren, aber sie haben unterschiedliche **Zwecke** und **Funktionsweisen**.

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
