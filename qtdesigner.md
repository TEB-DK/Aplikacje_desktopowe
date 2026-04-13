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

Tło: <img width="800" height="640" alt="templatex2 (1)" src="https://github.com/user-attachments/assets/54f1217a-f6e7-4887-a15c-b23e9167029f" />

Polecenie: Odtworzyć wygląd aplikacji oraz wyświetlić okienko z wprowadzonymy informacjami po zatwierdzeniu, hasło ma wyświetlić 2 ostatnie znaki, początek ma być zagwiazdkowany.

### Zadanie 8

<img width="69%" alt="Group 1" src="https://github.com/user-attachments/assets/19641465-57fc-4bb9-8408-dc73585ad97b" />

Polecenie: Odtwórz wygląd aplikacji oraz dodaj funkcjonalność tworzenia okna na podstawie danych przekazanych do pierwotnej aplikacji. Pojawiające się utworzone okno ma mieć nazwę, kolor, wielkość oraz tekst dodatkowy pobierany z pól wprowadzania przez użytkownika.

* - Dodatkowo wykonaj podgląd okna w aplikacji, który aktualizuje swój wygląd przy każdej wprowadzonej zmianie wartości.

- <img width="597" height="175" alt="image" src="https://github.com/user-attachments/assets/014bcf9c-34ae-466b-8d27-9a329ab95a71" />
- Okno podglądowe aplikacji powinno wyglądać następująco oraz mieć możliwość wyliczenia wartości która wyświetli się w okienku potwierdzającym.

### Zadanie 9

- <img width="989" height="402" alt="Group 1 (1)" src="https://github.com/user-attachments/assets/8ba77f33-6d15-41fb-8e29-53439ca2ff9a" />

Polecenie: Wykonaj kolejną aplikację TODO, po kliknięciu przycisku "Dodaj do listy", aplikacja ma dodawać nowe zadanie do listy zadań która jest listą przesuwaną.


* - <img width="685" height="402" alt="Group 2" src="https://github.com/user-attachments/assets/8b8c8bcb-b7dd-4cac-a35c-099dfca2b9e3" />
Polecenie: Wykonaj wersje uproszczoną zadania 9


### Zadanie 10 - Projekt
Utwórz aplikację do wyszukiwania posiłków wraz w wykorzystaniem darmowego API (przykładowe API podane poniżej).
Aplikacja ma możliwość:
- Wyszukiwarki posiłków na podstawie słowa np. "kurczak".
- Dodania posiłku do ulubionych.
- Usunięcia posiłku z ulubionych.
- Dodanie funkcjonalnych filtrów dań regionalnych, np. Meksykańskie, Greckie, Włoskie, Hamerykańskie..
- Dodanie podglądu składników oraz przepisu po kliknięciu na dany posiłek.
- Ulubione dania mają mieć możliwość bycia zapisanymi do pliku, z którego potem będą odczytywane i wprowadzane do miejsca "ulubione"
- Możliwość wyczyszczenia ulubionych jednym przyciskiem (wraz z usunięciem pliku .txt)
- 🌟 Zaprojektowanie bazy danych w MySQLite i wykorzystanie jej do logowania oraz dodawania ulubionych posiłków.
- 🌟 Dodatkowej dowolnej funkcjonalności, która jest unikalna na tle klasy. (Dodatkowe punkty uznania)
- 🌟 Panel logowania do aplikacji (możliwe wykorzystanie lokalnych sposobów "bazy danych")

Przykładowy wygląd aplikacji

<img width="69%" alt="Surface Pro 8 - 1" src="https://github.com/user-attachments/assets/e9afc504-9c72-4cd0-af74-463fbcc3a29c" />


Przykładowy kod pobrania posiłków z darmowego [API](https://www.themealdb.com/api.php) 
```python
def search_recipes(query):
    url = f"https://www.themealdb.com/api/json/v1/1/search.php?s={query}"
    
    response = requests.get(url)
    data = response.json()

 if data["meals"]:
        for meal in data["meals"]:
           print(meal["strMeal"])
    else:
        print("Brak wyników")
```



### Zadanie 11 

Aplikacja ma za zadanie przyjąć z pola wprowadzania wartość tekstową, a po zatwierdzeniu przyciskiem wyświetlić wprowadzony tekst w nowym oknie.

<img width="743" height="901" alt="Surface Pro 8 - 2" src="https://github.com/user-attachments/assets/387f1a1d-88f4-4451-a250-bf3e1865d21d" />
