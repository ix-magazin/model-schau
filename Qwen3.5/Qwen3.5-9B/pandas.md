Der Unterschied zwischen **`pivot`** (genauer `DataFrame.pivot`) und **`crosstab`** (genauer `pandas.crosstab`) liegt vor allem im **Zweck**, dem **Umgang mit Duplikaten** und der **Aggregation**.

Hier ist die Zusammenfassung:

| Merkmal | `DataFrame.pivot` | `pandas.crosstab` |
| :--- | :--- | :--- |
| **Hauptzweck** | **Umformung** von "Long" zu "Wide" Daten. | **Kreuztabelle** (Kontingenz) erstellen (Zählung). |
| **Aggregation** | **Nein**. Braucht eindeutige Werte. | **Ja**. Standardmäßig zählt Vorkommen (Summe). |
| **Eingabe** | Benötigt eine strukturierte Tabelle (DataFrame). | Kann Arrays oder Indexnamen akzeptieren. |
| **Duplikate** | Falsch mit Duplikaten (wirft Fehler). | Handelt Duplikate automatisch (zählt sie mit). |

---

### 1. `pivot` (Reshaping)
Die Funktion `df.pivot` ist ein Werkzeug zum **Umlenken** deiner Daten. Sie wandelt Daten in einer langen Form (jede Zeile eine Beobachtung) in eine breite Form (jeder Spaltenwert wird eine eigene Spalte) um.

*   **Voraussetzung:** Das Index-Schema + die Spaltenkombination müssen **einzigartig** sein. Wenn du dieselbe Kombination zweimal hast, wirft `pivot` einen Fehler.
*   **Verwendung:** Wenn du bereits strukturierte Daten hast, die du "aufschlüsseln" willst.

### 2. `crosstab` (Statistik/Aggregation)
Die Funktion `pd.crosstab` ist ein statistisches Tool. Sie erstellt eine Kreuztabelle, die oft eine Häufigkeitsverteilung darstellt.

*   **Aggregation:** Sie zählt standardmäßig die Anzahl der Vorkommen. Wenn du mehrere Zeilen mit denselben Werten hast, summiert sie diese.
*   **Verwendung:** Um Zusammenhänge zwischen zwei Kategorien zu untersuchen (z.B. "Wie viele Male taucht 'Mann' in 'Gruppe A' auf?").
*   **Flexibilität:** Du kannst fast alle Aggregationsfunktionen (Summe, Durchschnitt, Max) wählen (`aggfunc`).

---

### Beispiele

**Beispiel für `pivot` (Eindeutig)**

Hier haben wir eine Tabelle, die in eine Matrix umgewandelt werden soll. Da jeder Kundenname nur ein Produkt hat, funktioniert es:

```python
import pandas as pd

# Daten (jeder Zeile eine eindeutige ID)
df = pd.DataFrame({
    'Kunde': ['A', 'A', 'B', 'C'],
    'Produkt': ['Auto', 'Laptop', 'Auto', 'Laptop'],
    'Preis': [1000, 500, 2000, 600]
})

# Pivot: Produktname wird zu Spalten
result = df.pivot(index='Kunde', columns='Produkt', values='Preis')
print(result)
# Ausgabe:
# Produkt  Auto  Laptop
# Kunde
# A        1000    500
# B        2000    NaN
# C         NaN    600
```

**Beispiel für `crosstab` (Zählung)**

Hier wollen wir wissen, wie viele Male welche Kombination von "Stadt" und "Wetter" vorkommt. Es kann Duplikate geben.

```python
df = pd.DataFrame({
    'Stadt': ['Berlin', 'Berlin', 'München', 'Berlin'],
    'Wetter': ['Sonne', 'Regen', 'Sonne', 'Regen']
})

# Crosstab: Zählt die Häufigkeiten
result = pd.crosstab(df['Stadt'], df['Wetter'])
print(result)
# Ausgabe:
# Stadt    Berlin   München
# Wetter          
# Regen        2          0
# Sonne        2          1
#
# Hinweis: Berlin hat 2x Regen und 2x Sonne, obwohl es nur 2 Zeilen in df gab
```

---

### Wichtiger Hinweis zu `pivot_table`

In der Praxis wird `pivot` oft durch **`pivot_table`** ersetzt, weil `pivot` Fehler wirft bei doppelten Einträgen.

*   **`pivot_table`** (mit `pivot`) kann **Aggregationen** (Summe, Mittelwert) durchführen und somit Duplikate verarbeiten.
*   **`crosstab`** ist im Grunde eine spezielle Form von `pivot_table`, die primär nur auf **Zählungen** ausgelegt ist.

**Regel:**
*   Willst du nur Daten **umformen**? -> `df.pivot` (Aber: `pivot_table` meist sicherer).
*   Willst du eine **Zusammenfassung/Statistik**? -> `pd.crosstab` (oder `pivot_table`).

Zusammenfassend: **`pivot` ändert die Form, `crosstab` zählt die Häufigkeiten.**
