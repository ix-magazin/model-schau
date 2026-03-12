Das liegt an der spezifischen Funktionsweise der `range()`-Funktion in Python. Die obere Grenze ist **exklusiv**.

## Die Erklärung

Wenn du `range(100)` aufrufst, generiert Python eine Sequenz von Zahlen, die bei $0$ beginnt und bei $99$ endet. Die Zahl $100$ ist der **Stop-Wert**, wird aber selbst nicht mehr in die Sequenz aufgenommen.

| Parameter | Bedeutung | Wert im Beispiel |
| :--- | :--- | :--- |
| **Start** | Beginnwert (inklusive) | $0$ (Standardwert) |
| **Stop** | Endwert (exklusiv) | $100$ |
| **Step** | Schrittweite | $1$ (Standardwert) |

Daher lautet die generierte Sequenz:
$$0, 1, 2, \dots, 99$$

## Lösung: Wie man bis 100 kommt

Wenn du möchtest, dass die Zahl $100$ ebenfalls ausgegeben wird, musst du den Stop-Wert um $1$ erhöhen:

```python
for i in range(101):
    print(i)
```

Dies generiert die Sequenz von $0$ bis $100$ (insgesamt $101$ Zahlen).

<details>
<summary><strong>Hintergrundwissen: Zero-Based Indexing</strong></summary>

Dieses Verhalten ist in vielen Programmiersprachen üblich und hängt mit dem **zero-based indexing** (nullbasierte Indizierung) zusammen.

*   Eine Liste mit $100$ Elementen hat die Indizes $0$ bis $99$.
*   `range(n)` wird oft verwendet, um genau über solche Indizes zu iterieren.
*   Würde `range(100)` die $100$ einschließen, hätte man $101$ Elemente, was bei Listen der Länge $100$ zu einem `IndexError` führen würde.

Die Formel für die Anzahl der erzeugten Zahlen lautet:
$$ \text{Anzahl} = \text{Stop} - \text{Start} $$

Im Fall von `range(100)`:
$$ \text{Anzahl} = 100 - 0 = 100 $$
Es werden also genau $100$ Zahlen ausgegeben ($0$ bis $99$).

</details>
