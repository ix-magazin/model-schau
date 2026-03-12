<<<reasoning_content_start>>>The user is asking why the Python program only outputs numbers up to 99. Let me analyze the code:

```python
for i in range(100):
    print(i)
```

This is a basic Python for loop. The `range(100)` function creates a sequence of numbers from 0 to 99 (inclusive), not 1 to 100.

In Python, `range(n)` generates numbers from 0 up to n-1. So `range(100)` generates: 0, 1, 2, 3, ..., 98, 99.

This is by design in Python - the upper bound is exclusive. This is a common convention in programming (similar to array indexing in many languages).

So the answer is: The program outputs numbers from 0 to 99 because `range(100)` generates numbers from 0 up to (but not including) 100. If you want numbers up to 100, you would need to use `range(101)`.

Let me answer this in German since the user has been communicating in German.<<<reasoning_content_end>>>Das Programm gibt nur die Zahlen von **0 bis 99** aus, weil die Funktion `range(100)` in Python den **oberen Grenzwert ausschließt**.

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
