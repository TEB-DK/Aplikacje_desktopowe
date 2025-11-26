# QTDesigner
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
### Instalacja

W terminalu uruchomić polecenie instalacyjne

```python
pip install PySide6
```
  ASDASD

>[!NOTE]
> Plik `designer.exe` znajduje się PRAWDOPODOBNIE w ``%APPDATA%/Python/Python312/Lib/site-packages/PySide6``

>[!IMPORTANT]
>Aby uruchomić skopiowany kod z Qt Designer należy dodać poniższą linijkę na końcu pliku `.py`.
> ```python
> app = QApplication()
> window = QMainWindow()
> main = Ui_MainWindow()
> main.setupUi(window)
> window.show()
> app.exec()
> ```

### Funkcjonalność sygnałów

Aby dodać własną funkcjonalność do sygnału, należy zapisać funkcję o dowolnej nazwie.
```python
def foobar():
    print("FOO\tBAR")
```

Następnie `połączyć (connect)` do naszego chociażby przycisku po kliknięciu, który ma określoną akcje.
```python
self.pushButton.clicked.connect(foobar)
```

---

### Tworzenie sygnałów wraz z własnym kodem `Python`

W pierwszej kolejności importujemy widgety które nas interesują wraz `QtCore`.
```python
from PySide6.QtWidgets import QApplication, QMainWindow, QPushButton
from PySide6.QtCore import Qt
import sys
```

Reakcja hover `nie występuje domyślnie` dla przycisków, ale możemy utworzyć jej klase aby dodać jej funkcjonalność wraz z dwoma metodami. Klasa ta dziedziczy po widgecie QPushButton właściwości i modyfikuje już obiekt `QAction`, który tą możliwość dostarcza.
```python
# ----------- Klasa dodająca reakcję na "hover" -----------
class HoverButton(QPushButton):
    def enterEvent(self, event):
        print("Mouse entered button")
        super().enterEvent(event)

    def leaveEvent(self, event):
        print("Mouse left button")
        super().leaveEvent(event)
```

Podłączenie samych sygnałów do utworzonego przycisku wystepuje w głównej klasie `MainWindow` za pomocą składni `self.<nazwa_przycisku>.<sygnał>.connect(<nazwa_metody>)`.
```python
# ----------- Główne okno aplikacji -----------
class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()

        self.setWindowTitle("Test przycisku PySide6")
        self.setGeometry(200, 200, 400, 300)

        # Tworzymy własny przycisk z obsługą hover
        self.button = HoverButton("Kliknij mnie", self)
        self.button.setGeometry(150, 120, 120, 40)

        # Włączamy tryb przełączania dla testów (toggle)
        self.button.setCheckable(True)

        # Podłączamy różne sygnały
        self.button.clicked.connect(self.on_clicked)
        self.button.pressed.connect(self.on_pressed)
        self.button.released.connect(self.on_released)
        self.button.toggled.connect(self.on_toggled)
```

Metody klasy dla sygnałów
```python
    # ------------ Obsługa sygnałów ------------

    def on_clicked(self):
        print("Signal: clicked")

    def on_pressed(self):
        print("Signal: pressed")

    def on_released(self):
        print("Signal: released")

    def on_toggled(self, state):
        print(f"Signal: toggled -> {state}")
```


### Zadanie 1.

Wygląd aplikacji

<img width="69%" alt="image" src="https://github.com/user-attachments/assets/a64cc619-8c9e-4743-8269-21372e6b0395" />

Polecenie: Odwzorować aplikację według obrazka, oraz zastosować odpowiednio po jednej akcji według widgetu.

### Zadanie 2.

Wygląd aplikacji

<img width="69%" alt="image" src="https://github.com/user-attachments/assets/e2936a1c-e1c5-46e8-b325-47b77d3061b5" />

Polecenie: Odwzoruj aplikacje widoczną powyżej i zastosuj nowe możliwości powiązania przycisków z metodami w kodzie.

* - Wykorzystując odwołanie do `setStyleSheet` zaimplementuj do dowolnego przycisku efekt zmiany styli dla dowolnego widgetu w aplikacji.


### Zadanie 3.

Wygląd aplikacji 

<img width="69%" alt="image" src="https://github.com/user-attachments/assets/8be48f03-9b7d-40e5-b612-337b8d5d4263" />

Polecenie: [Arkusz](https://github.com/Technikum-TEB-Edukacja-we-Wroclawiu/INF.04-rozwiazania/blob/main/_arkusze/2023-01/inf_04_2023_01_01_SG_kolor.pdf)

* - Zaimplementuj funkcjonalność losowego koloru tła aplikacji za każdym otworzeniem jej. Z wykorzystaniem `setStyleSheet`.

x
x
x
x
x
x
x
x
d
x
x
x
x
x
x
x
x
X
