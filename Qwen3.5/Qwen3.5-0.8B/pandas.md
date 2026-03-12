In Python (und in der Pandas Bibliothek `pandas`) gibt es **nicht** zwei völlig verschiedene Funktionen namens `pivot` und `crosstab` im engeren Sinne. Stattdessen handelt es sich um **Eigene Funktionen** von Pandas, die oft mit Namen wie `pivot_table` oder `cross_table` assoziiert werden.

Das ist eine häufige Verwechslung durch die englische Bezeichnung (was für `pivot` ist) und das technische Verständnis. Hier ist die detaillierte Erklärung der Unterschiede:

### 1. `pivot` (Eigene Funktion von Pandas)
Das Wort **pivot** stammt von dem englischen Begriff **„pivot"** (das „Frische Aufstellen"), was in der Statistik und Datenanalyse bedeutet: **„die Daten aus der richtigen Reihenfolge anordnen"**.

*   **Funktionsziele:** Es erstellt eine **Tabell (Matrix)**, in der die einzelnen Zellen eine Kombination aus mehreren Variablen enthalten.
*   **Typische Anwendung:**
    *   **Verzweigen:** Wenn eine Tabelle mehrere Kolonnen (Variablen) hat, wird diese als eine Zeile (Row) im neuen Tabellenformat verwendet.
    *   **Gleichungsbildung:** Es ermöglicht es, Beziehungen zwischen zwei Tabellen zu visualisieren.
    *   **Grenzen:** Es hilft, Daten zu extrahieren, wenn eine bestimmte Struktur des Tabels gewünscht ist.

**Beispiel:**
Wenn Sie eine Tabelle `df` haben, die 3 Variablen (`x`, `y`, `z`) hat, kann Sie `pivot()` verwenden, um in eine 3-Zeilkolonne-Tabell zu verwandeln.

```python
import pandas as pd

# Vorherige Tabelle (z.B. Daten mit Variablen x, y, z)
df = pd.DataFrame({
    'x': [1, 2, 3],
    'y': [4, 5, 6],
    'z': [7, 8, 9]
})

# Verwendung von pivot: Um eine Tabelle zu erstellen, in der die Variablen als Zeilen sind
pivot_df = df.pivot(index='x', columns='y', values='z')
# Ergebnis: Eine neue DataFrame mit 3 Zellen (1,4; 2,5; 3,6), die zueinander verknüpft sind
```

---

### 2. `crosstab` (Eigene Funktion von Pandas)
Das Wort **cross-tab** (oder **cross**) bedeutet **„den Kreuztasten"**.

*   **Funktionsziele:** Es erstellt eine **Tabell**, in der **jede Zelle eine Kombination aus mehreren Variablen** enthält.
*   **Typische Anwendung:**
    *   Es wird verwendet, um Daten zu analysieren, wenn eine einzige Variable (z.B. `z`) als Hauptvariante und mehrere Zellen als Variablen (z.B. `x`, `y`) im Tabellensatz ist.
    *   Es hilft bei der Zusammenfassung von Daten, die mehrere Werte pro Zeile haben.
*   **Unterschied zu `pivot`:**
    *   `pivot` hat **die Variablen als Zellen**.
    *   `crosstab` hat **die Variablen als Zeilen**.

**Beispiel:**
Wenn Sie eine Tabelle `df` haben, die 3 Variablen (`x`, `y`, `z`) hat, und eine einzige Variable `z` als Hauptvariante (`axis='index')` hat, kann Sie `crosstab()` verwenden, um in eine 3-Zeilkolonne-Tabell zu verwandeln.

```python
# Verwendung von crosstab: Um eine Tabelle zu erstellen, in der jede Zelle eine Kombination aus Variablen ist
crosstab_df = df.crosstab(index='z', columns=['x', 'y'])
# Ergebnis: Eine neue DataFrame mit 3 Zellen (1,4; 2,5; 3,6), die zueinander verknüpft sind
```

---

### Zusammenfassung: Das „Vertrauen"

| Merkmal | `pivot` | `crosstab` |
| :--- | :--- | :--- |
| **Grammatikalisch** | `pivot` (von „pivot" -> „aufstellen") | `cross-tab` (von „cross" -> „Kreuztasten") |
| **Verbindet?** | Die Variablen sind in den **Zellen** | Die Variablen sind in den **Zellen** |
| **Hauptfunktion** | Verwenden von Variablen als **Zeilen** (Zellen) | Verwenden von Variablen als **Zeilen** (Zeilen) |
| **Häufigkeit im Code** | Sehr häufig (z.B. `df.pivot()`) | Sehr häufig (z.B. `df.crosstab()`) |
| **Unterschied** | Die Variablen sind in den **Zellen** | Die Variablen sind in den **Zeilen** |

### Der "Vertragsvertragsfehler" (Küchel-Hofstätt)
In Python gibt es keine direkte Funktion namens `pivot_table` oder `cross_table`. Das ist ein bekannter Fehler, der oft in Datenanalyse-Prozessen oder bei internen Diskussionen vorkommt, als man meint:
*   `df.pivot_table()` (Funktionsname von `pivot`)
*   `df.crosstab()` (Funktionsname von `cross-tab`)

### Fazit
Es gibt keine Funktion mit dem Namen `pivot` oder `crosstab` im Pandas-Code. Sie sind **eigene Funktionen** (`pivot` und `crosstab`), die beide dazu dienen, Tabellen zu erstellen, aber mit **verschiedenen Variablen als Zellen** zu verknüpfen.

*   Wenn Sie eine **Zellmatrix** (z.B. 2 Zellen: A und B) erstellen wollen, verwenden Sie `pivot` (und `pivot_table`).
*   Wenn Sie eine **Zeilenmatrix** (z.B. 3 Zeilen: A, B, C) erstellen wollen, verwenden Sie `crosstab` (und `cross-tab`).
