Das liegt an der Funktionsweise von `range()` in Python:

### 🔍 Wie `range()` funktioniert

Die Funktion `range(stop)` generiert eine Zahlenfolge, die **bei 0 beginnt** und **bis `stop - 1` geht**. Die angegebene Obergrenze wird **nicht** miteinbezogen.

| Parameter | Bedeutung |
|-----------|-----------|
| `0`       | Startwert (wird ausgegeben) |
| `...`     | Alle dazwischenliegenden Zahlen |
| `99`      | Letzter ausgegebener Wert |
| `100`     | **Obergrenze, wird nicht ausgegeben** |

### 📊 Warum genau so?

Das ist eine bewusste Designentscheidung in Python:

1. **Intuitive Zählung:** `range(100)` erzeugt genau **100 Zahlen** (von 0 bis 99). Das ist intuitiver für Schleifen mit einer bestimmten Anzahl von Iterationen.
2. **Mathematische Konsistenz:** In der Mathematik und Informatik ist der Bereich oft **links abgeschlossen, rechts offen** ([0, 100)).
3. **Vermeidung von Off-by-One-Fehlern:** Wenn Sie eine Liste von 100 Elementen durchlaufen wollen, ist `range(len(liste))` die natürliche Wahl.

### ✅ Beispiel zum Vergleich

```python
# Zahlen von 0 bis 99 (100 Zahlen)
for i in range(100):
    print(i)

# Wenn Sie bis 100 wollen, müssen Sie 101 angeben:
for i in range(101):
    print(i)
# Das gibt 0 bis 100 aus (101 Zahlen)
```

### 💡 Zusammenfassung

`range(100)` gibt **0 bis 99** aus, weil die Obergrenze **exklusiv** ist. Um die 100 mit einzubeziehen, müssen Sie `range(101)` verwenden.
