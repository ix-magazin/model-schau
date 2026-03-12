Das Python-Programm druckt genau die Zahlen von **0 bis 99**, nicht bis einschließlich 100. Das liegt an der Funktionsweise von `range()` in Python:

```python
for i in range(100):
    print(i)
```

### Erklärung:
- `range(100)` erzeugt eine **Folge von 100 Zahlen**: von **0** bis **99** (inklusive 0, exklusive 100).
- `range()` ist **immer exklusive** beim oberen Wert. Das bedeutet, dass `range(100)` nicht die Zahl 100 enthält.

### Zahlen, die ausgegeben werden:
```
0, 1, 2, 3, ..., 98, 99
```
Das sind genau **100 Zahlen**.

### Wenn du bis einschließlich 100 willst:
```python
for i in range(101):
    print(i)
```
Das würde `0` bis `100` ausgeben (101 Zahlen insgesamt).

### Kurz gesagt:
- `range(n)` → Zahlen von `0` bis `n-1`
- `range(100)` → Zahlen von `0` bis `99`
- `range(101)` → Zahlen von `0` bis `100`

Wenn du möchtest, kannst du auch die Zeile anpassen, um alle 100 Zahlen einzeln auszugeben:

```python
for i in range(1, 101):
    print(i)
```
Das würde `1` bis `100` ausgeben (ohne die `0`).

**Zusammenfassung:** Es sind nur die Zahlen bis 99, weil `range()` exklusive ist – das ist eine Standardfunktion von Python.
