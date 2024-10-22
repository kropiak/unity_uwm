# Lab 3 - Wybrane elementy API Unity. Dodawanie własnych skryptów do obiektów gry.


## **Wybrane klasy z API Unity.**

API Unity jest bardzo rozbudowane i nie sposób chociażby pobieżnie omówić wszystkie klasy tam dostępne. Są jednak takie, bez których praktycznie żaden projekt nie może
istnieć. Zostały one wymienione przez autorów dokumentacji w artykule, którym będziemy się posiłkować: https://docs.unity3d.com/2022.3/Documentation/Manual/ScriptingImportantClasses.html

> **Klasa [GameObject](https://docs.unity3d.com/2022.3/Documentation/ScriptReference/GameObject.html)**  
Jest to klasa reprezentująca dowolny element, który można umieścić na scenie. Z poziomu tej klasy możemy pobierać podpięte pod obiekt komponenty, w tym niezrozłączny komponent `Transform`. Komponent `Transform` jest dostępny poprzez właściwość klasy o nazwie `transform`.

__**Listing 1**__
```csharp
public class Ball : MonoBehaviour {

    // metoda Start() wywoływana jest przy inicjalizacji obiektu
    void Start() {
        // ustawienie obiektu w pozycji (0, 0, 0)
        transform.position = new Vector3(0.0f, 0.0f, 0.0f);
    }
}
```
Do określenia pozycji w przestrzeni 3D możemy wykorzystać klasę [Vector3](https://docs.unity3d.com/2022.3/Documentation/ScriptReference/Vector3.html) lub [Vector2](https://docs.unity3d.com/2022.3/Documentation/ScriptReference/Vector2.html) dla 2D.
Referencje do pozostałych komponentów uzyskujemy w inny sposób. Możemy to zrobić w jednorazowo (dla każdego obiektu) uruchamianej metodzie `Start()`:

__**Listing 2**__
```csharp
public class Ball : MonoBehaviour {

    public float force = 5.0f;
    
    void Start()
    {
        Rigidbody rb = GetComponent<Rigidbody>();
        rb.AddForce(0, 0, force, ForceMode.Impulse);
    }
}
```
lub możemy wynieść zmienną do wyższego zakresu i umieścić jako pole komponentu, do którego możemy teraz odwołać się z poziomu innych skryptów lub edytować przez okno inspektora (jeżeli pole posiada modyfikator dostępu `public`):

__**Listing 3**__
```csharp
public class Ball : MonoBehaviour {

    public float force = 10.0f;
    public Rigidbody rb;
    
    void Start()
    {
        rb.AddForce(Vector3.up * force, ForceMode.Impulse);
    }
}
```
Oczywiście należy pamiętać, że jeżeli nie przypiszemy obiektu typu `Rigidbody` do zmiennej `rb` w powyższym to otrzymamy stosowny wyjątek: `UnassignedReferenceException: The variable rb of Ball has not been assigned`. Podpięcie instancji komponentu `Rigidbody` pod zmienną `rb` możemy wykonać z poziomu skryptu (jeżeli w oknie inspektora taki komponent do obiektu, który ma również podpięty ten skrypt został dodany) poprzez metodę `GetComponent()` (doc: https://docs.unity3d.com/2022.3/Documentation/ScriptReference/Component.GetComponent.html) lub poprzez przeciągnięcie i upuszczenie komponentu `Rigidbody` w miejsce widocznej w inspektorze zmiennej `rb`, która obiekt tego typu może przechowywać. Jeżeli chcemy aby na dany obiekt gry działały siły fizyczne, to będziemy manipulować dodanym do niego komponentem `Rigidbody` a nie poprzez edycję komponentu `Transform`.

Jak widać w każdym powyższym fragmencie kodu każda nasza klasa dziedziczy po klasie `MonoBehaviour`. 

> **Klasa [MonoBehaviour](https://docs.unity3d.com/2022.3/Documentation/ScriptReference/MonoBehaviour.html)**  
> Jest to klasa, po której dziedziczy każdy nowy skrypt stworzony z poziomu UnityEditor. Ta klasa dostarcza mechanizm pozwalający na podpinanie skryptów pod obiekty gry oraz zapewnia interfejs pozwalający na umieszczenie kodu uruchamianego w określonym momencie pracy silnika lub po wystąpieniu określonego zdarzenia.

Poniżej przykładowy pusty szablon klasy po dodaniu nowego skryptu:

__**Listing 4**__
```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Example : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {

    }


    // Update is called once per frame
    void Update()
    {

    }
}
```

Nie wszystkie metody dziedziczone po klasie `MonoBehaviour` są tu widoczne. Metoda `Start()` jest wywoływana wraz z inicjalizacją obiektu czyli w momencie jego tworzenia lub załadowania sceny. Natomiast `Update()` uruchamiana jest raz na każdą klatkę animacji. Jeżeli kod, który zamierzamy dodać będzie manipulował właściwościami fizycznymi obiektu (poprzez Unity physics engine) to należy ten kod umieścić wewnątrz metody `FixedUpdate()`, która uruchamiana jest docelowo ze stałą częstotliwością na sekundę, o ile maszyna zdoła wykonać taka ilość operacji. Domyślnie jest to 50 razy na sekundę, a to ustawienie możemy sprawdzic i zmienić w edytorze w menu `Edit -> Project Settings -> Time -> Fixed Timestep`.

__**Listing 5**__
```csharp
public class Ball : MonoBehaviour {

    public float force = 10.0f;
    Rigidbody rb;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void FixedUpdate()
    {
        // składowa y wektora prędkości
        if(rb.velocity.y == 0)
        {
            // działamy siłą na ciało A :)
            rb.AddForce(Vector3.up * force, ForceMode.Impulse);
        }
    }
}
```

Klasą bazową dla wszystkich klas API Unity jest klasa [Object](https://docs.unity3d.com/2022.3/Documentation/ScriptReference/Object.html). Zachęcam do przeczytania krótkiego opisu pod adresem https://docs.unity3d.com/2022.3/Documentation/Manual/class-Object.html

> **Klasa [Quaternion](https://docs.unity3d.com/2022.3/Documentation/ScriptReference/Quaternion.html)**  
> Klasa Quaternion służy do przechowywania informacji o trzech składowych obiektu opisujących jego orientację w przestrzeni trójwymiarowej. Dzięki tej klasie możemy też wyznaczać względne parametry obrotu jaki trzeba wykonać, aby obrócić obiekt do wskazanej orientacji. W panelu inspektora,kąty które widzimy w komponencie Transform podane są jako [kąty Eulera](https://pl.wikipedia.org/wiki/K%C4%85ty_Eulera), ale w skryptach powinniśmy używać metod obiektu Quaternion do manipulacji rotacją obiektów. W przeciwnym wypadku może pojawić się problem nazywany `Gimbal lock` (więcej: http://pananimator.pl/gimbal-lock/).

Poniższy fragment kodu obróci obiekt przypisany do zmiennej `from` tak, aby jego wartości rotacji (orientacja) pokryły się z wartościami zapisanymi w obiekcie przypisanym do zmiennej `to`. Trzeci parametr funkcji `Quaternion.Slerp()` to procent o jaki mamy zmienić rotację. Wartości zawierają się w przedziale [0, 1].

__**Listing 6**__
```csharp
using UnityEngine;

public class QuaternionRotateToPosition : MonoBehaviour
{
    public Transform from;
    public Transform to;

    // krok rotacji, wyrazony w procentach, o jaki zostanie wykonana rotacja
    // w każdej klatce animacji
    private float percentage = 0.01f;

    void Update()
    {
        transform.rotation = Quaternion.Slerp(from.rotation, to.rotation, percentage);
    }
}
```

Manual opisujący więcej przykładów dostępny pod linkiem: https://docs.unity3d.com/2022.3/Documentation/Manual/class-Quaternion.html


Możemy również wykonywać rotacje obiektów poprzez komponent `Transform` i metody `Transform.Rotate()` oraz `Tranform.RotateAround()`, które również operują na obiektach `Quaternion`. Wartości obrotu podawane są w stopniach. Parametrem, który jeszcze musimy przekazać jest parametr `realtiveTo`,który określa czy obrót będzie odbywał się względem lokalnych czy globalnych koordynatów (`Space.Self, Space.World`).

__**Listing 7**__
```csharp
public void Update {
    cube1.transform.Rotate(xAngle, yAngle, zAngle, Space.Self);
    cube2.transform.Rotate(xAngle, yAngle, zAngle, Space.World);
}
```
> **Klasa [Time](https://docs.unity3d.com/2022.3/Documentation/ScriptReference/Time.html)**
> Klasa ta pozwala na pracę z elementami gier związanymi z czasem. Dzięki tej klasie możemy również wyznaczać czas jaki minął od momentu wygenerowania ostatniej klatki animacji. 

Opisane w manualu trzy najważniejsze składowe klasy `Time`:
* `Time.time` - zwraca czas, który minął od momentu uruchomienia projektu (gry).

* `Time.deltaTime` - zwraca czas w sekundach jaki upłynął od momentu wygenerowania poprzedniej klatki. Wykorzystywany najczęściej aby przekształcenia, które chcemy wykonać dla naszego obiektu (ruch, rotacja) odbywały się proporcjonalnie do upływającego czasu, lub inaczej ujmując, proporcjonalnie do ilości klatek, które są generowane na sekundę.

* `Time.timeScale` - zawiera informacje o szybkości upływu czasu. Manipulowanie tym parametrem pozwala na tworzenie efektów fast-forward lub slow-motion.


Rozpatrzmy poniższy przykład (prosto z manuala Unity):

__**Listing 8**__
```csharp
using UnityEngine;
using System.Collections;

public class ExampleScript : MonoBehaviour {
    public float distancePerFrame;
    
    void Update() {
        transform.Translate(0, 0, distancePerFrame);
    }
}
 //oraz
using UnityEngine;
using System.Collections;

public class ExampleScript : MonoBehaviour {
    public float distancePerSecond;
    
    void Update() {
        transform.Translate(0, 0, distancePerSecond * Time.deltaTime);
    }
}
```

Oba przypadki różnią się znacznie efektem, który osiągniemy. W pierwszym przypadku każde wywołanie metody `Update()` spowoduje przesunięcie obiektu wzdłóż osi `z` o określoną ilość pikseli i ta prędkość (w czasie), będzie bezpośrednio zależała od wartości FPS. Drugi przykład to ruch, który odbywa się ze stałą wielkością przesunięcia na sekundę - co klatkę proporcjonalnie do FPS.

Aby dodać nieco interakcji do naszego projektu i ćwiczeń poniżej zaprezentowany został przykład poruszania obiektem w płaszczyźnie `x` i `z` za pomocą klawiatury (klawisze WASD). W zależności czy komponent `Rigidbody` będzie posiadał aktywną opcję `useGravity` czy nie, będziemy mogli poruszać się po platformie lub również poza nią, bez uwzględniania sił grawitacji.

__**Listing 9**__
```csharp
using UnityEngine;

public class MovePlayer : MonoBehaviour
{
    public float speed = 2.0f;
    Rigidbody rb;
   
    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        
    }
    void FixedUpdate()
    {
        // pobranie wartości zmiany pozycji w danej osi
        // wartości są z zakresu [-1, 1]
        float mH = Input.GetAxis("Horizontal");
        float mV = Input.GetAxis("Vertical");

        // tworzymy wektor prędkości
        Vector3 velocity = new Vector3(mH, 0, mV);
        velocity = velocity.normalized * speed * Time.deltaTime;
        // wykonujemy przesunięcie Rigidbody z uwzględnieniem sił fizycznych
        rb.MovePosition(transform.position + velocity);
    }
}
```
Aby kod poprawnie działał dla wybranego obiektu należy dołączyć do niego komponent ```Rigidbody```. Bardziej szczegółowo sterowaniem zajmiemy się na kolejnym laboratorium. 




## Zadania

>W celu ujednolicenia sposobu przechowywania własnych skryptów w folderze Assets utwórz folder scripts i tam umieszczaj własne skrypty. Dla każdego zadania (poza zadaniem 1) stwórz nową scenę o nazwie równoważnej nazwie zadania (np. zadania1 lub zadanie_1). Jeżeli dla obiektów będących przedmiotem zadania zostaną stworzone prefabrykaty (zalecane) to umieszczanie obiektów na kolejnych scenach będzie dużo łatwiejsze. Warto też wykorzystać opcję `Save as...` i zapisać scenę, na której trzeba bazować, pod nową nazwą.

**Zadanie 1**  
Przeczytaj artykuł [https://docs.unity3d.com/Manual/2022.3/Documentation/VectorCookbook.html](https://docs.unity3d.com/2022.3/Documentation/Manual/VectorCookbook.html), który przypomni Ci zagadnienia związane z pojęciem wektorów odległości i sposobu na wykorzystanie tej wiedzy w środowisku Unity.

**Zadanie 2**  
Stwórz nową scenę. Dodaj do niej obiekt typu Cube o wymiarach (2, 1, 1). Napisz skrypt, z publicznym polem speed (float), który będzie przemieszczał obiekt wzdłóż osi x o 10 jednostek i w momencie wykonania takiego przesunięcia będzie wykonywał ruch powrotny.

**Zadanie 3**  
Do obiektu Cube z zadania 2 dodaj jakiś element, który będzie wskazywał na jej kierunek `forward`. Rozbuduj skrypt z zadania 2 (ale zapisz wszystko w nowym skrypcie), tak aby obiekt poruszał się 'po kwadracie' o boku 10 jednostek i docierając do wierzchołka wykonywał obrót o 90 stopni w kierunku kolejnego ruchu. 

**Zadanie 4**  
Dodaj nową scenę do swojego projektu. Stwórz obiekt, który będzie obiektem gracza (cube, sphere, cokolwiek).  Dodaj do sceny płaszczyznę o wymiarach 20x20 jednostek. Dodaj możliwość przemieszczania obiektu po płaszczyźnie. 

**Zadanie 5**  
Wykorzystując możliwość dodawania obiektów czasie wykonania (zobacz: https://docs.unity3d.com/2022.3/Documentation/Manual/InstantiatingPrefabs.html) stwórz nową scenę a w niej:
* dodaj płaszczyznę o wymiarach 10x10
* w momencie uruchomienia trybu play generuj 10 obiektów typu Cube, które umieszczaj losowo na płaszczyźnie, ale tak, żeby w danym miejscu nie znalazł się więcej niż jeden obiekt.

**Zadanie 6**  
Korzystając z przykładu w dokumentacji UNITY dostępnej pod adresem https://docs.unity3d.com/2022.3/Documentation/ScriptReference/Mathf.SmoothDamp.html zaimplementuj go dla dwóch obiektów na swojej scenie i przetestuj zmieniając położenie w trybie `game` obiektu, który 'jest śledzony'. Przetestuj również metodę `Mathf.Lerp`.
