# Aplikacje desktopowe <img align="top" src="https://github.com/user-attachments/assets/38b3a274-ac3b-4f93-823b-d79c866ccf5a" width="48" height="48" /> / <img align="top" src="https://github.com/user-attachments/assets/4bb7db71-c03a-4a5f-afd7-3957340e38e1" width="48" height="48" />

Repozytorium poświęcone aplikacjom desktopowym tworzonym w języku Python i frameworku graficznego interfejsu "Tkinter".


---
Aby zacząć w ogóle tworzyć aplikacje desktopowe należy zainstalować pakiet tkinter
```console
pip install tk
```

Kolejnym krokiem jest zaimportowanie biblioteki szkieletu programistycznego do naszego projektu
```python
import tkinter
```

``tkinter`` jest bazową klasą, dzięki której możemy manipulować naszą aplikacją desktopową, to ona tworzy nam okienka i nimi zarządza.

Aby utworzyć nowe okno należy wywołać metodę
```python
root = tkinter.Tk()
root.mainloop()
```

Zmienna root jest od teraz skrótem samego źródła naszej aplikacji czyli okna najwyższego stopnia, takie okno może mieć podokna, a nawet ramki wewnątrz siebie, które są pewnego rodzaju oknami wewnątrz tego okna.

Natomiast metoda ``mainloop()`` jest niczym innym jak wywołaniem tego okna w pętli, ponieważ każdy program który istnieje i wykorzystuje odświeżanie jest wygenerowany w pętli i potrzebuje odświeżać się lub jak później zobaczymy "malować się" na ekranie naszego komputera co jakiś konkretny czas (w tym przypadku w zależności od prędkości odświeżania ekranu).

Jeżeli zechcemy zmienić wielkość pojawiającego się okna należy wykorzystać metodę ``geometry``, która przyjmuje ciąg znaków jako wymiar okna
```python
root = tkinter.Tk()
root.geometry("600x400")
root.mainloop()
```

Następnym krokiem będzie dodanie przycisku, który najzwyczajniej będzie zamykał nam okno aplikacji.
```python
root = tkinter.Tk()
root.geometry("600x400")
btn = tkinter.Button(
    root,
    text="Zamknij to okno człowieku",
    width=32,
    command=root.quit)
btn.pack()
root.mainloop()
```

Jak widać tkinter posiada metody, które generują nam tak zwane "widgety", każdy widget musi być przypisany do jakiegoś elementu rodzica, dlatego też w nawiasie w pierwszej kolejności widać zmienną ``root``, następnie taki widget może przyjmować wiele atrybutów, przycisk przyjmuje chociażby tekst, szerokość, a nawet polecenie do wykonania gdy zostanie kliknięty. 
Każdy widget musi być po utworzeniu "spakowany" aby został wyświetlony w sposób prawidłowy w naszym oknie. Takie pakowanie posiada też swój zestaw możliwości jeżeli chodzi o umieszczenie widgetu, np. pady, gdzie oznacza padding dla osi x czyli odpowiednia odległość w pionie od góry i od dołu.
