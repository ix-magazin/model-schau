# Unterschied zwischen `pivot` und `crosstab` in pandas

Sowohl `pivot` als auch `crosstab` dienen in der Python-Bibliothek `pandas` dazu, Daten von einem Langformat in ein Breitformat zu transformieren. Der entscheidende Unterschied liegt jedoch im **Umgang mit Duplikaten** und der **standardmäßigen Aggregation**.

## Vergleichstabelle

| Merkmal | `pivot` | `crosstab` |
| :--- | :--- | :--- |
| **Typ** | Methode eines `DataFrame`-Objekts | Top-Level Funktion von `pandas` |
| **Aggregation** | Keine (wirft Fehler bei Duplikaten) | Ja (standardmäßig Häufigkeitszählung) |
| **Hauptzweck** | Umstrukturierung bestehender Werte | Erstellung von Kreuztabellen (Häufigkeiten) |
| **Input** | Benötigt explizite Spalten für Index, Columns, Values | Kann Arrays, Series oder DataFrame-Spalten nehmen |
| **Flexibilität** | Geringer bei aggregierten Daten | Hoch (unterstützt `normalize`, `margins`) |

## 1. Die `pivot`-Methode

`pivot` wird verwendet, wenn jede Kombination aus Index und Spalte **eindeutig** ist. Es gibt keine Aggregation statt. Wenn es mehrere Werte für dieselbe Kombination gibt, wird eine `ValueError`-Ausnahme ausgelöst.

**Syntax:**
```python
df.pivot(index=None, columns=None, values=None)
```

**Beispiel:**
```python
import pandas as pd

data = {
    'Produkt': ['A', 'A', 'B', 'B'],
    'Datum': ['2023-01', '2023-02', '2023-01', '2023-02'],
    'Preis': [10, 15, 20, 25]
}
df = pd.DataFrame(data)

# Funktioniert, da jede Kombination eindeutig ist
pivot_df = df.pivot(index='Produkt', columns='Datum', values='Preis')
```

**Einschränkung:**
Wenn im obigen Beispiel zwei Preise für `Produkt A` im `Datum 2023-01` existieren würden, würde `pivot` fehlschlagen. Mathematisch ausgedrückt erfordert `pivot` eine injektive Abbildung der Kombination $(Index, Column)$ auf den $Value$.

## 2. Die `crosstab`-Funktion

`crosstab` (Kreuztabelle) berechnet standardmäßig eine **Häufigkeitstabelle**. Es aggregiert Daten automatisch, wenn Duplikate vorhanden sind. Es ist flexibler, wenn man wissen möchte, wie oft bestimmte Kombinationen vorkommen.

**Syntax:**
```python
pd.crosstab(index, columns, values=None, aggfunc=None, normalize=False)
```

**Beispiel:**
```python
import pandas as pd

data = {
    'Geschlecht': ['m', 'w', 'm', 'w', 'm'],
    'Abteilung': ['IT', 'IT', 'HR', 'HR', 'IT']
}
df = pd.DataFrame(data)

# Zählt automatisch die Häufigkeiten
cross_df = pd.crosstab(index=df['Geschlecht'], columns=df['Abteilung'])
```

**Ergebnis:**
Die Zellen enthalten die Anzahl der Vorkommen $N_{i,j}$ für jede Kombination.

## Zusammenfassung der Wahl

*   Nutzen Sie `pivot`, wenn Sie eine Tabelle einfach nur **umdrehen** wollen und sicher sind, dass keine Duplikate existieren.
*   Nutzen Sie `crosstab`, wenn Sie **Häufigkeiten** zählen wollen oder wenn Duplikate vorhanden sind, die aggregiert werden müssen.

<details>
<summary><strong>Erweiterung: Die Rolle von `pivot_table`</strong></summary>

Es gibt eine dritte Methode, die oft als Kompromiss verwendet wird: `pivot_table`.

### `pivot_table` im Vergleich

`pivot_table` kombiniert die Eigenschaften von `pivot` und `crosstab`.

*   Wie `pivot`: Es arbeitet auf einem `DataFrame` und nutzt Spaltennamen.
*   Wie `crosstab`: Es führt eine Aggregation durch (standardmäßig `mean`), wenn Duplikate vorhanden sind.

**Mathematische Betrachtung der Aggregation:**
Während `crosstab` standardmäßig die Summe der Einsen berechnet (Count):
$$ \text{Count}_{i,j} = \sum_{k \in S_{i,j}} 1 $$

Kann `pivot_table` beliebige Funktionen $f$ anwenden:
$$ \text{Value}_{i,j} = f(\{v_k \mid k \in S_{i,j}\}) $$

**Beispielcode:**
```python
# Aggregiert Duplikate durch Mittelwertbildung statt Fehler zu werfen
pivot_table_df = df.pivot_table(
    index='Produkt', 
    columns='Datum', 
    values='Preis', 
    aggfunc='mean'
)
```

### Wann welches Tool?

1.  **`pivot`**: Schnelles Reshaping bei eindeutigen Schlüsseln.
2.  **`crosstab`**: Schnelle Häufigkeitsanalysen zwischen zwei oder mehr Variablen.
3.  **`pivot_table`**: Komplexes Reshaping mit benutzerdefinierter Aggregation (Summe, Mittelwert, etc.).

</details>
