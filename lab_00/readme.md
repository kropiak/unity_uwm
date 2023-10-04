# Lab 00 - Instalacja i konfiguracja środowiska UNITY

## 0. Wstęp.

Unity występuje w kilku wersjach (więcej pod adresem https://unity.com/faq) w zależności od wielkości organizacji i przychodów, które osiąga w danym roku. Wersja, która będzie wykorzystywana w trakcie zajęć to edycja Personal. Tabelka porównująca poszczególne plany dostępna jest pod adresem: https://unity.com/compare-plans.

W ostatnim czasie pojawiły się informacje od kierownictwa Unity o chęci zmiany cennika, które odbiły sie szerokim echem wśród społeczności i ostatecznie skloniły firmę do daleko idących ustępstw. Więcej można przeczytać w liscie otwartym: https://blog.unity.com/news/open-letter-on-runtime-fee.

## 1. Instalacja UNITY

Możliwa jest instalacja wielu wersji UNITY na jednym koncie użytkownika systemu operacyjnego i dlatego zarządzanie wersjami oraz projektami UNITY odbywa się poprzez dodatkowe oprogramowanie - **Unity Hub**. 

Aby korzystać w pełni z oprogramowania Unity należy założyć konto na portalu unity.com i założenie tzw. **Unity ID**.

Po instalcja Unity Hub i jego uruchomieniu możemy wybrać jedną z czterech kategorii: 
* Projects
* Learn
* Community
* Installs

Opcje dostępne w **Projects** pozwalają przeglądać istniejące projekty, dodawać nowe lub zmienić wersję środowiska UNITY istniejącego projektu (tutaj nie zawsze wszystko musi pójść zgodnie z planem).

Część **Learn** pozwala na dodanie istniejących projektów gier, stworzonych w celach edukacyjnych. Wystarczy wybrać projekt i opcję "DOWNLOAD PROJECT". Warto zwrócić uwagę na wersję Unity, dla której projekt został stworzony, będzie to gwarancja kompatybilności.

**Community** to zbiór przydatnych linków do materiałów dla i od społeczności zgromadzonej wokół Unity.

Ostatnia, ale nie najmniej ważna opcja, to **Installs** gdzie możemy pobrać i zainstalować kolejne wersje środowiska, odinstalować istniejące lub zarządzać modułami dla konkretnej zainstalowanej wersji.

W trakcie zajęć wykorzystywana będzie wersja **2022.3.10f1 LTS**. Jest to wersja o długim wsparciu technicznym. Pobranie i instalacja wymaga sporo czasu (dużo zależy od szybkości łącza internetowego) więc należy wybrać miejsce z wystarczająco dużą ilością wolnego miejsca. Moduły, które wybieramy na początku to:
* **Windows Build support** lub **Linux build support** lub **Mac build support** w zależności od używanego systemeu operacyjnego,
* **Microsoft Visual Studio 2022 Community** lub **Visual Studio Code**,
* **Documentation** (opcjonalnie) - jeżeli ktoś planuje pracę w trybie offline i nie będzie miał dostępu do dokumentacji dostępnej w Internecie.

Kod w śorodiwsku UNITY piszemy w języku C# i można wybrać inny edytor niż **Visual Studio 2022 Community**, ale to rozwiązanie ze względu na oficjalne wsparcie wydaje się dobrym połączeniem na start i będzie wykorzystywane w trakcie zajęć. Używanie Visual Studio Code nie powinno powodować większych problemów. 


## 2. Konfiguracja systemu Git dla projektu Unity.

Jeżeli nie pracowałeś/-ał wcześniej z systemem Git, możesz zapoznać się z informacjami i konfiguracji oraz podstawowych poleceniach przedstawionych w dokumencie [konfiguracja_git](konfiguracja_git.md).

Korzystanie z systemów kontroli wersji jest w dzisiejszych czasach absolutnym standardem. Unity w trkacie naszej pracy nad projektem "produkuje" wiele plików tymczasowych, plików binarnych, których ani nie będziemy potrzebować w gotowej już grze, ani nie chcemy marnować czasu na ich synchronizację ze zdalnym repozytorium. Dlatego w naszych projektach (mimo, że docelowo może nie pojawić się wiele dużych plików) wykorzystamy wersję Git LFS (Large File Storage), która została stworzona specjalnie dla takich sytuacji. Wersję dla systemy Windows i krótką instrukcję instalacji znajdziemy pod adresem [https://git-lfs.github.com/](https://git-lfs.github.com/). Dodatkowo wykorzystamy plugin GitHub for Unity, który ułatwi nam pracę z Unity i Git-em oraz utworzy odpowiedni plik **.gitignore**, który usprawni i przyspieszy pracę z repozytorium poprzez redukcję ilości plików zarządzanych przez system Git.

W celu wydajniejszego zarządzania plikami binarnymi (assety) zalecane jest pobranie i instalacja Git LFS, czyli modułu, który usprawnia pracę GIT-a właśnie a tego rodzaju zasobami.
Dla projektów o objętości liczonej w gigabajtach warto rozważyć repozytorium hostowane w usłudze Azure DevOps. Dla zespołu do 5 użytkowników nie jest pobierana opłata wstępna (możliwe są opłaty za przekroczenie dostepnego miejsca - do samodzielnego sprawdzenia). 

Przydatne wskazówki znajdziemy również w artykule pod adresem: https://www.anchorpoint.app/blog/github-and-unity