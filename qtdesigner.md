# QTDesigner

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

### Zadanie 1.

Wygląd aplikacji

<img width="69%" alt="image" src="https://github.com/user-attachments/assets/a64cc619-8c9e-4743-8269-21372e6b0395" />

Polecenie: Odwzorować aplikację według obrazka, oraz zastosować odpowiednio po jednej akcji według widgetu.
