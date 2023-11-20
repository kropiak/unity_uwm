# Lab 7 - Zadanie specjalne :)

Zadaniem do wykonania jest stworzenie trójwymiarowego modelu Waszego wyboru za pośrednictwem oprogramowania Mechroom oraz Blender lub innego pozwalającego na edycję modeli 3D.

Zdjęcia modelu musicie wykonać samodzielnie, może to być obiekt znajdujący się na zewnątrz (pomnik, ławka, drzewo, kamień itp.) lub coś co znajdziecie wokół swojego najbliższego otoczenia. Można również zrobić model samego siebie :) Aby całość się udała potrzeba co najmniej około 20 zdjęć, ale im więcej tym lepiej. Warto przed rozpoczęciem robienia zdjęć przeanalizować podlinkowane tutoriale. 
> **Do repozytorium należy dołączyć zrzut modelu, plik z modelem (może być .obj, .blend, .psb) oraz minimum 3 zdjęcia użyte do jego wygenerowania (w celu weryfikacji, pamiętajmy, że Google również pozwala na wyszukiwanie obrazem ;-) ).**


Najlepsze projekty zostaną nagrodzone +1 do oceny końcowej (jeżeli się da :) ), zachwytem prowadzącego oraz szacunkiem wśród pozostałych członków grupy :)

## **Potrzebne składniki:**   
1. **Meshroom**

Jest to oprogramowanie OpenSource w ramach projeku [AliceVision](https://alicevision.org/). Dzięki temu oprogramowaniu przy zachowaniu pewnych zasad robienia zdjęć można stworzyć z nich realistyczne modele 3D, które po obróbce mogą być wykorzystane na wiele sposobów. Oprogramowanie wykorzystuje fotogrametrię do osiągnięcia finalnego celu czyli metadanych o zdjęciu i ustawieniach urządzenia za pomocą którego zostało zrobione.

Meshroom pobieramy spod adresu: https://alicevision.org/#meshroom.

Oprogramowanie oferuje również wsparcie dla kart Nvidia z procesorami CUDA. Aby to wykorzystać należy najpierw zainstalować odpowiedni Toolkit.

Jeżeli na wyposażeniu nie ma karty Nvidia, to można spróbować obejść ten problem wykorzystując np. Google Colab i darmowy, ograniczony, dostęp do GPU od Googla.

Zobacz dokumentację tu:
* https://github.com/alicevision/meshroom/wiki/Meshroom-in-Google-Colab-(cloud)
* https://shawngraham.github.io/CCAD/notebooks/meshroom/


Podstawowy workflow po uruchomieniu programu Meshroom jest wystarczający, żeby stworzyć model i wyeksportować go to zewnętrznego programu modelującego. Przy zbyt małej ilości zdjęć lub ich nieprawidłowym wykonaniu mogą pojawić się błędy, które trzeba będzie samodzielnie rozwiązać. Najczęściej polega to na lepszym wyborze zdjęć lub ponownym ich zrobieniu przy lepszym oświetleniu i ze zbliżoną odległością od obiektu.

1. **Nvidia CUDA toolkit**

Jeżeli na wyposażeniu znajduje się przyzwoita karta Nvidia z procesorami CUDA warto przyspieszyć proces generowania modelu (który w zależności od ilości zdjęć może zająć duuuużo czasu). Meshroom (zgodnie z zapisem w dokumentacji) wspiera Nvidia toolkit w wersji 10.

Nvidia Toolkit: https://developer.nvidia.com/cuda-10.0-download-archive

3. **Oprogramowanie do modelowania**

Oprogramowanie jest niezbęde, żeby dodać szlify do modelu i pozbyć się niepotrzebnie wykrytych elementów, zbędnych detali i zredukować ilość wierzchołków modelu.

Model z Meshroom można obrobić w Blenderze, ZBrush, Maya i inne. Blender jest tu niezłym wyborem, ze względu na fakt, że jest to oprogramowanie OpenSource z bardzo dużymi możliwościami.

Blender: https://www.blender.org/download/


## Przydatne materiały

1. Tutorial z wykorzystaniem Meshroom oraz Blender do stworzenia modelu: https://www.kodeco.com/9559662-using-meshroom-to-insert-real-life-objects-in-unity
2. Manual Meshroom: https://meshroom-manual.readthedocs.io/en/latest/
3. Niezły tutorial Meshroom + Blender: https://www.youtube.com/watch?v=k4NTf0hMjtY



## Czekam na ciekawe projekty!