# Kilka wksazówek jak pracować z systemem kontroli wersji Git

## 1. Wstępna konfiguracja

Nowe repozytorium inicjalizujemy komendą:
```console
git init
```
W folderze, w którym polecenie zostało uruchomione pojawi się ukryty folder o nazwie `.git`, w którym znajdują się informacje o naszym repozytorium. Zostanie również utworzona gałąź (ang. branch) `master`.
W przypadku pracu wielu osób na tym samym koncie systemu operacyjnego należy skonfigurować jeszcze parametry `user.name` oraz `user.email`, które będą się pojawiały w commitach, które w trakcie pracy będą wykonywane.
```console
git config --local user.name akowalski
git config --local user.email akowalski@gmail.com
```

W przypadku, gdy chcemy ustawić takie dane dla każdego repozytorium, które będzie tworzone na tym koncie możemy zamienić `--local` na `--global` lub `--system`. Należy wtedy pamiętać, że wciąż lokalnie dla konkretnego repozytorium możemy te wartości nadpisać.

Kolejną rzeczą, którą należy wykonać jest wyłączenie domyślnej integracji Visual Studio Code z windowsowym menedżerem poświadczeń, który będzie przechowywał dane logowania do serwisu GitHub innych użytkowników utrudniając pracę kolejnym, którzy będą chcieli wypychać zmiany do swojego zdalnego repozytorium.
Możemy to zrobić poleceniem:
```console
git config --system --unset credential.helper
```
Warto również sprawdzić czy nie ma takiego ustawienia w innych zakresach konfiguracji.
```console
git config --global -l
git config --local -l
```

Jeżeli tak to tutaj również usuwamy ten parametr.

## 2. Podstawowe komendy systemu Git

Po podstaowej konfiguracji narzędzia Git możemy teraz dodać coś do naszego repozytorium.
```console
git add plik.py
```
Powyższe polecenie dodaje plik `plik.py` do poczekalni (ang. stage area) i w Visual Studio Code będzie on oznaczony literą `A` (added czyli dodany).
Możemy również dodać wszystkie pliki w bieżącej lokalizacji:
```console
git add *
```
Należy jednak pamiętać, że różne narzędzia dodają 'coś od siebie' i mogą po pierwsze pojawić się pliki konfiguracyjne, które raczej nie będą potrzebne kiedy będziemy chcieli udostępnić repozytorium dla innych użytkowników, którzy mogą chcieć korzystać z innego narzędzia niż nasze i będą musieli samodzielnie nieco 'posprzątać' to repozytorium. Dlatego zalecanym krokiem przed dodaniem czegokolwiek do repozytorium jest przygotowanie pliku `.gitignore` zawierającego reguły (wyrażenia regularne), które spowodują, że spełaniające je zasoby będą przez narzędzie Git ignorowane przy sledzeniu zmian. Jednak należy pamiętać, że w przypadku modyfikacji `.gitignore` powinniśmy usunąć śledzenie zasobów, najwygodniej po prostu:
```console
git rm *
```
i ponownie
```console
git add *
```
aby Git dodał wszystko ignorując te zawarte w `.gitignore`.

Jeżeli zasoby, które chcemy śledzić są już dodane możemy wykonać ich zatwierdzenie.
```console
git commit -m "pierwszy commit"
```
spowoduje stworzenie nowej migawki zasobów znajdujących się w folderze roboczym (czyli wszystkiego tego co jest aktualnie widoczne w eksplorerze projektu) czyli z poczekalni. Każdy commit ma swój unikalny hashcode.

### __Podpięcie lokalnego repozytorium do nowego zdalnego repozytorium__

__Krok 1__

Tworzymy nowe repozytorium zdalne, w trakcie zajęć korzystamy z serwisu GitHub. Po jego utworzeniu wyświetlona zostanie strona z komendami, które powinny nam pomóc przy procesie synchronizacji. Komendy włączając pierwszy commit można pominąć, gdyż zostało to już zrobione w nieco inny sposób.
Dla lokalnego repozytorium wskazujemy zdalne repozytorum, do którego będziemy chcieli kod wypychać.
```console
git remote add origin https://github.com/user/repo.git
```
Powyższe polecenie jest właściwe jeżeli nie korzystamy z klucza SSH (lepsze rozwiązanie, jeżeli tylko my korzystamy z danego konta w systemie operacyjnym), gdyż nie wymaga każdorazowego podawania poświadczeń przy wypychaniu zmian. Dodajemy informację o nowym zdalnym repozytorium o aliasie origin i podanym url-u.

Jeżeli chcemy sprawdzić jaki jest adres zdalnego repozytorium to
```console 
git remote get-url origin
```
a jeżeli trzeba go zmienić
```console
git remote set-url origin https://nowy.adres.repo
```

__Krok 2__

Polecenie
```console
git push -u origin master
```
próbuje wysłać aktualną gałąź (i jej stan z wykonanego nostatnio commitu) do zdalnego repozytorium z adresu przypisanego do aliasu (origin) do zdalnej gałęzi master.
Tutaj może się pojawić kilka problemów (błędów), które mogą tę operację uniemożliwić.
Jeżeli otrzymamy komunikat, mówiący, że wypchanie nie jest możliwe, bo użytkownik o nazwie xxx nie posiada uprawnień oznacza to, że w `menedżerze poświadczeń` są zapisane poświadczenia do serwisu GitHub innego użytkownika (mogą pochodzić z innego narzędzia). Należy usunąć wszystkie poświadczenia, które odwołują się do serwisu GitHub i ponowić próbę wypchania zmian. Można ponowić operację wypchania zmian.

Może się tutaj również pojawić problem jeżeli w zdalnym repozytorium znajdują się jakieś zasoby, których lokalnie nie ma (np. dodany domyślny plik `readme.md`). Wtedy możemy wykonać polecenie push z dodatkowym parametrem, wymuszającym wypchanie (force):
```console
git push -f origin master
```

### __Pobranie repozytorium w inne miejsce/komputer__

Jeżeli chemy kontynuować pracę z zawartością repozytorium na innym komputerze, narzędziu to wystarczy przejść do folderu, w którym chcemy umieścić repozytorium, np. folder z innymi projektami i wykonać polecenie:
```console
git clone http://link.do.repo
```
To polecenie __UTWORZY__ nowy folder o nazwie takiej jak nazwa zdalnego repozytorium i umieści tam już informacje o jego stanie (folder .git) oraz informacji o remote (ten sam, z którego został sklonowany). Teraz wystarczy skonfigurować `user.name` oraz `user.email` w przestrzeni `--local`, jeżeli nie ma poprawnych ustawień globalnych (pracujemy na tym samym koncie co inni użytkownicy) i można dalej pracować, zatwierdzać zmiany i wypychać je ponownie do zdalnego repozytorium.

### __Więcej ?__

Polecam [git-scm.com/book/pl/v2](https://git-scm.com/book/pl/v2).