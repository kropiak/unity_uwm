# Lab 9. Tworzenie gry 2D, część 3. Wrogowie. A* pathfinding. 

> Projekt startowy, który można wykorzystać: [starter](lab_9_starter_light_2022.zip)
> W projekcie jest jedna scena, a na niej postać głównego bohatera z dodanym skryptem do poruszania się po przykładowym poziomie.
> Zaimplementowana jest również kamera śledząca głównego bohatera oraz reset poziomu po updaku z platformy.
> Dodana jest również część animacji, ale nie wszystkie przejścia w maszynie stanów animacji są dokończone.

**Zadanie 1**  

Zadanie polega na stworzeniu postaci wroga naziemnego, która będzie poruszała się stale między puntem A i B dopóki postać naszego bohatera nie pojawi się w promieniu "reakcji" wroga. Punkty A i B mogą być umieszczane dowolnie (ale wciąż sensownie dla wroga naziemnego). Jeżeli bohater (player) pojawi się w promieniu zasięgu wroga będzie on poruszał się w kierunku naszego bohatera aż dotrze do niego, ale tylko pomiędzy punktami A oraz B. To na razie uprości implementację rozwiązania i nie pozwoli wrogom na niekontrolowane spadanie z platform. Jeżeli oddalimy się od wroga poza zasięg reakcji powinien powrócić do swojego wcześniejszego "zajęcia".

> **Opcjonalnie!**  
> Jeżeli chcesz użyć czegoś bardziej wyrafinowanego, w stylu Field of View (FoV) zobacz te tutoriale:
> * https://www.youtube.com/watch?v=CSeUMTaNFYk (część 1)
> * https://www.youtube.com/watch?v=3-jPo2wzvdw (część 2)
> 
> lub
> * https://www.youtube.com/watch?v=rQG9aUWarwE (część 1)
> * https://www.youtube.com/watch?v=73Dc5JTCmKI (część 2)


_Import postaci wroga_
  
Postać przykładowego wroga możesz pobrać z adresu: https://craftpix.net/freebies/free-minotaur-tiny-style-2d-sprites/

Ten pakiet zawiera również gotowy pakiet Unity, który wystarczy zaimportować aby wykorzystać m.in. animacje, które zostały już dla tej postaci stworzone. Problemem, który się pojawi może być kolejność renderowania sprite'ów w warstwach. Można to zmienić poprzez wartość pola `order in layer` poszczególnych sprite'ów.

Po zaimportowaniu element, ten dostępny jest jako prefabrykat.

Wykorzystaj tylko animację idle (domyślna) oraz animację ruchu wroga. Dodaj skrypt, który będzie wykorzystywany do sterowania wrogiem - możesz wykorzystać zmodyfikowaną wersję skryptów z poprzednich zajęć (`CharacterController2D`). Pamiętaj o dodaniu odpowiednich komponentów (Rigidbody2D, odpowiedni collider 2D).

Postaraj się zaplanować dodanie komponentów i skryptów tak, aby ten element był reużywalny. Będzie to oznaczało, że będzie możliwe dodanie innej postaci wroga, zmodyfikowanie położenia punktów A i B dla każdej instancji wroga.

**Zadanie 2**  

Obejrzyj film dostępny pod adresem https://www.youtube.com/watch?v=jvtFUfJ6CP8 a następnie dodaj wroga powietrznego na podstawie informacji z obejrzanego materiału wykorzystując gotowy pakiet implementujący algorytm A*. Link znajdziesz w opisie filmu.

Film jest podzielony na dwie części, gdzie w pierwszej wykorzystane są gotowe możliwości pakietu, a w drugiej skrypt sterujący postacią wroga jest pisany krok po kroku. Wybierz jeden ze sposobów dla swojego zadania.

Postać latającego wroga możesz wykorzystać używając gotowego pakietu https://craftpix.net/freebies/free-wraith-tiny-style-2d-sprites/ lub dowolnego wybranego przez siebie (bez łamania praw autorskich).
