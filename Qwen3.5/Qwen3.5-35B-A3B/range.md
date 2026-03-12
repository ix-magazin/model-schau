Das Programm gibt nur die Zahlen von **0 bis 99** aus, weil die Funktion `range(100)` in Python den **oberen Grenzwert ausschließt**.

### Wie `range()` funktioniert:
Die Funktion `range(n)` erzeugt eine Zahlenfolge:
- **Start:** 0 (standardmäßig)
- **Ende:** n-1 (das n selbst wird nicht erreicht)

Also:
```python
range(100)  →  0, 1, 2, 3, ..., 98, 99
```

Das ist ein **häufiges Muster** in der Programmierung (ähnlich wie bei Array-Indizes in vielen Sprachen, die bei 0 beginnen).

### Lösung für Zahlen bis 100
Wenn du auch die Zahl **100** ausgeben möchtest, musst du den Grenzwert um 1 erhöhen:

```python
for i in range(101):
    print(i)
```

Dadurch erhältst du: 0, 1, 2, ..., 99, 100.

### Zusammenfassung
| Code | Ausgabe |
|------|---------|
| `range(100)` | 0 bis 99 |
| `range(101)` | 0 bis 100 |

Die obere Grenze von `range()` ist also **immer exklusiv**.

