# QTDesigner


### Instalacja

W terminalu uruchomić polecenie instalacyjne

```python
pip install PySide6
```


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

* - Utwórz aplikację odwzorowaną na obrazku powyżej (zadanie 2), dodaj przycisk dzięki któremu pojawi się nowe okno z możliwością wyliczenia przesyłki na dane wojewodztwo, w zależności od wybranego wojewodztwa kwota wysyłki (pocztówki, listu, paczki) zostanie pomnożona przez dany procent, a następnie wyświetli wyliczoną kwotę wysyłki.


### Zadanie 3.

Wygląd aplikacji 

<img width="69%" alt="image" src="https://github.com/user-attachments/assets/8be48f03-9b7d-40e5-b612-337b8d5d4263" />

Polecenie: [Arkusz](https://github.com/Technikum-TEB-Edukacja-we-Wroclawiu/INF.04-rozwiazania/blob/main/_arkusze/2023-01/inf_04_2023_01_01_SG_kolor.pdf)

* - Zaimplementuj funkcjonalność losowego koloru tła aplikacji za każdym otworzeniem jej. Z wykorzystaniem `setStyleSheet`.

### Zadanie 4.

Wygląd aplikacji

<img width="69%" alt="image" src="https://github.com/user-attachments/assets/558d73c8-15e4-4975-ad54-2493caaa46a2" />

Polecenie: [Arkusz](https://github.com/Technikum-TEB-Edukacja-we-Wroclawiu/INF.04-rozwiazania/blob/main/_arkusze/2025-06/inf_04_2025_06_01_SG.pdf)

* - Dodaj dodatkowy przycisk do aplikacji wyświetlający okienko z 4-roma bloczkami odcieni wybranego koloru i wartości ( według wartości RGB )
 

### Zadanie 5

Polecenie: [Arkusz](https://github.com/Technikum-TEB-Edukacja-we-Wroclawiu/INF.04-rozwiazania/blob/main/_arkusze/2025-06/inf_04_2025_06_02_SG.pdf)

### Zadanie 6

Wygląd aplikacji

<img width="69%" alt="image" src="https://github.com/user-attachments/assets/2fc45247-db08-41d3-bd4e-472a7199448e" />

Polecenie: Stwórz działający kalkulator prosty według wyglądu aplikacji przedstawionego powyżej. Kalkulator ma posiadać funkcje takie jak: `dodawanie`, `odejmowanie`, `mnożenie`, `dzielenie`, `modulo` - wynik reszty z dzielenia.
Ponadto ma mieć możliwość czyszczenia obliczeń za pomocą przycisku `wyczyść` oraz zmiana koloru tła okna wprowadzania wartości na kolory podane w wyglądzie aplikacji.

### Zadanie 7

Wygląd aplikacji

<img width="69%" alt="Desktop - 1" src="https://github.com/user-attachments/assets/36f00978-d709-49bb-973a-829865fce374" />

Polecenie: Odtworzyć wygląd aplikacji oraz wyświetlić okienko z wprowadzonymy informacjami po zatwierdzeniu, hasło ma wyświetlić 2 ostatnie znaki, początek ma być zagwiazdkowany.


