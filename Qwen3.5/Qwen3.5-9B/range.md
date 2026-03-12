Das liegt an der Funktionsweise der Python-Funktion `range()`.

In Python ist `range()` im oberen Bereich **ausschließlich (exclusive)**. Das bedeutet:

1.  **Startwert:** Die Zählung beginnt immer bei **0**.
2.  **Endwert:** Das Argument, das du ange gibst (hier `100`), ist der **Stopp**, aber die Zahl selbst wird **nicht** ausgegeben.

Wenn du also `range(100)` schreibst, erzeugt Python die Zahlen von `0` bis `99`.

### Mathematisch betrachtet
Da bei 100 die Schleife aufhört, aber bei 0 gestartet hat, sind das **genau 100 Zahlen** (0 bis 99). Es fehlen nicht wirklich Zahlen, sondern der Wert 100 wird nicht erreicht.

### Lösung
Wenn du wirklich bis und mit 100 gehen möchtest, musst du den Wert um 1 erhöhen, damit die 100 noch im Intervall liegt:

```python
for i in range(101):  # Hier bis 100!
    print(i)
```

### Warum ist das so?
In der Informatik (und besonders in der Programmierung) wird fast immer **0-Indexierung** verwendet. Das dient dazu, dass Arrays, Listen und Schleifen leichter mathematisch handhabbar sind. Man spricht oft von einem „Index 0 bis Index N-1".

