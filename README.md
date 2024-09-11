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

W przypadku gdy chcemy wyśrodkować pojawiające się okno na monitorze, możemy skorzystać z właściwości informacji systemowych o których wie nasze główne okno ``root``
```python
screen_width = root.winfo_screenwidth()
screen_height = root.winfo_screenheight()
```
Dzięki tym metodom automatycznie pobierzemy rozdzielczość naszego monitora i przy odrobinie matematyki możliwe będzie wyśrodkowanie okna, które chcemy utworzyć
```python
import tkinter

root = tkinter.Tk()
root.title('Centered!')

w_width = 600
w_height = 400 

screen_width = root.winfo_screenwidth()
screen_height = root.winfo_screenheight()

start_x = int((screen_width/2) - (w_width/2))
start_y = int((screen_height/2) - (w_height/2))

root.geometry(f'{w_width}x{w_height}+{start_x}+{start_y}')
root.mainloop()
```

#### Spróbuj wykonać 🫅🏿

1. Utwórz nowy plik ``.py`` i stwórz nowe okno aplikacji.
2. Dopasuj wielkość okna tak aby wypełniała ekran w 75% szerokości i 50% wysokości
3. Wyśrodkuj okno aplikacji w płaszczyźnie "x" (w szerokości), natomiast w płaszczyźnie "y" (w wysokości) ustaw je tak, aby odstawało od górnej krawędzi o 50px

## Widgety w Tkinter

Każdy widget posiada wspólną cechę ze wszystkimi, a jest nią zbiór argumentów. Oznacza to, że w przypadku gdy tworzymy widget np. ``tk.Button()`` to przyjmuje on w pierwszej kolejności dwa argumenty ``parent`` oraz ``options``.
```python
tk.Button(parent, options)
```
Przy czym:
- ``parent`` jest to rodzic widgetu który chcemy umiejscowić i sugeruje on tam okno (czyli rodzica) w którym ma się znajdować.
- ``options`` są to dodatkowe opcje takie jak ``text`` widgetu, ``bg`` czyli kolor tła (background color) i inne dodatkowe "smaczki".


> [!IMPORTANT]
> Każdy widget należy spakować metodą ``.pack()`` przed ``root.mainloop()`` by został wyświetlony w naszym oknie aplikacji!



#### Lista dostępnych widgetów
<ul type="square">
    <li>
        <details>
            <summary>Label</summary>
            Label to widżet służący do implementacji pól wyświetlania, w których można umieszczać tekst lub obrazy. 
			
			
   ```python
   tk.Label(root, text="Przykładowy tekst")
   ```
			
        
</details>
    </li>
    
<li>        
<details>
<summary>Button</summary>
Button jest graficznym elementem sterującym używanym do tworzenia klikalnych przycisków w graficznym interfejsie użytkownika (GUI). Zapewnia on użytkownikom sposób wyzwalania akcji lub zdarzeń po kliknięciu (odpowiada temu dodatkowa opcja ``command``).

```python
tk.Button(root, text="Przykładowy przycisk", bg="lightgreen")
```
 
</details>
</li>
    <li>        
        <details>
            <summary>Entry</summary>
            Entry jest widżetem służącym do wprowadzania lub wyświetlania pojedynczej linii tekstu. Można powiedzieć, że jest odpowiednikiem input'a w HTML. 
            
	
```python
tk.Entry(root, font=('arial', 12, 'bold'))
```


   
</details>
    </li>
    <li>        
        <details>
            <summary>Frame</summary>
            Frame to obszar na ekranie. Widżet ten może być również używany jako miejsce bazowe (rodzic) do implementacji złożonych widżetów. Służy do organizowania grupy widżetów.
            Widżet może zdawać się skomplikowany, jednak taki nie jest - służy do grupowania innych widżetów, porównalibyśmy go do znacznika `div` w HTML, możemy również dzięki niemu lepiej organizować przestrzeń naszej aplikacji. 
                
```python
first_frame = tk.Frame(root,background="blue", padx=20, pady=20)
label = tk.Label(first_frame, text="Tekst label")
button = tk.Button(first_frame, text="Przycisk", bg="lightgreen")
entry = tk.Entry(first_frame, font=('arial', 12, 'bold'))
label.pack()
button.pack()
entry.pack()
first_frame.pack(padx=20, pady=20)
	
second_frame = tk.Frame(root,background="orange", padx=20, pady=20)

label2 = tk.Label(second_frame, text="Tekst label")
button2 = tk.Button(second_frame, text="Przycisk", bg="lightgreen")
entry2 = tk.Entry(second_frame, font=('arial', 12, 'bold'))
label2.pack()
button2.pack()
entry2.pack()
second_frame.pack(padx=20, pady=20)
```

Jak widać ramka może posiadać sporą ilość widżetów, które trzeba spakować, aby nieco ułatwić sobie życie "pakowaniem" można zastosować prostą pętle, która tyczy się wszystkich dzieci naszej ramki (czyli widżetów)
```python
for dziecko in first_frame.children.values():
    dziecko.pack()
```

</details>
    </li>
    <li>        
        <details>
            <summary>Checkbutton</summary>
            Checkbutton jest standardowym widżetem Tkinter, który jest używany do implementacji opcji włączania/wyłączania. Przyciski wyboru mogą zawierać tekst lub obrazy. 

```python
tk.Checkbutton(root, text="Check mate!", onvalue=1, offvalue=0)
```
			
</details>
    </li>
    <li>        
        <details>
            <summary>Radiobutton</summary>
            Radiobutton jest standardowym widżetem używanym do implementacji wyboru "jeden z wielu". Radiobuttony mogą zawierać tekst lub obrazy, a z każdym przyciskiem można powiązać funkcję lub metodę języka Pythona.
            
```python
tk.Radiobutton(root, text="First option of many!", value=1)
```
			
</details>
    </li>
    <li>        
        <details>
            <summary>Listbox</summary>
            Listbox służy do wyświetlania listy elementów. 
			Elementy te muszą mieć ten sam typ czcionki i ten sam kolor czcionki.
			Elementy muszą być również typu Text. Użytkownik może wybrać jeden lub więcej elementów z podanej listy zgodnie z wymaganiami.
            
```python
listbox = tk.Listbox(first_frame, bg="lightblue", fg="black", font=("Helvetica", 10))
listbox.insert(1,"First")
listbox.insert(2,"Second")
listbox.insert(3,"Third")
listbox.insert(4,"Forth")
```
			
</details>
    </li>
    <li>        
        <details>
            <summary>Menu</summary>
            Powszechnym zastosowaniem menu jest zapewnienie wygodnego dostępu do różnych operacji, takich jak zapisywanie lub otwieranie pliku, zamykanie programu lub manipulowanie danymi. Menu najwyższego poziomu są wyświetlane tuż pod paskiem tytułu okna głównego lub innych okien najwyższego poziomu.
			
```python
menu = tk.Menu(root)

first_menu = tk.Menu(menu, tearoff=0)
menu.add_cascade(label="Option", menu=first_menu)
first_menu.add_command(label="> Suboption 1", command=donothing)
first_menu.add_command(label="> Suboption 2", command=donothing)
first_menu.add_command(label="> Suboption 3", command=donothing)

second_menu = tk.Menu(menu, tearoff=0)
menu.add_cascade(label="Edit", menu=second_menu)
second_menu.add_command(label="> Subedit 1", command=donothing)
second_menu.add_command(label="> Subedit 2", command=donothing)
second_menu.add_command(label="> Subedit 3", command=donothing)

root.config(menu=menu)
```

1. Najpierw tworzony jest widżet Menu i dodawany do naszego okna głównego (root).
2. Następnie tworzone jest pierwsze menu którego rodzicem jest widżet "menu".
3. Aby dodać rozwijaną opcje z "pod opcjami" należy wykorzystać metode ``add_cascade()``, która określa nazwe opcji rozwijanej oraz jej główne menu (utworzone linie wcześniej).
4. Ostecznie by dodać podopcje wykorzystywana jest metoda ``add_command()``, przyjmująca przykładowy tekst oraz polecenie do wykonania.

##### Należy również do głównego okna aplikacji dodać configuracje, która wskazuje, które menu będzie podpięte pod to okno.

</details>
    </li>
</ul>

#### Spróbuj wykonać 🫅🏿
1. Utwórz przycisk i dodaj go do aplikacji z nazwą ``Click`` oraz tłem ``Crimson``
2. Utwórz nowe menu ``Options`` które będzie posiadało 3 podopcje o nazwach ``Check system``, ``Insert file`` oraz ``Exit``
3. Wypozycjonuj 3 dowolne widżety w oknie aplikacji oraz zmodyfikuj ich wygląd.


## Pozycjonowanie elementów

### Pozycjonowanie ``ABSOLUTNE``

### Układ ``SIATKOWY``

### Układ ``WYPEŁNIAJĄCY``
