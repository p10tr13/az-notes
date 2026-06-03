---
typ: twierdzenie
egzamin: true
status: do_nauczenia
trudnosc: "5"
utworzono: 2026-06-03
powiazania:
  - "[[Index_Egzamin]]"
---

# Poprawność algorytmu najbliższej pary punktów (ograniczenie do 7 punktów)

> [!abstract] Cel egzaminacyjny
> Umiem podać treść twierdzenia i odtworzyć dowód bez patrzenia w notatkę.

## Treść twierdzenia

> [!quote] Twierdzenie
> W fazie łączenia ("Zwyciężaj") algorytmu Dziel i Zwyciężaj dla problemu pary najbliższych punktów, wystarczy sprawdzać odległości jedynie między rozpatrywanym punktem a co najwyżej 7 następującymi po nim punktami w posortowanej tablicy $Y^{\prime}$. 

*(Uwaga: Algorytm jest poprawny w całości, a pierwszy warunek to trywialne ograniczenie rekursji dla $|P| \le 3$, by nie dzielić pojedynczego punktu. Główny dowód dotyczy ograniczenia liczby sprawdzanych punktów w pasie do 7).*

## Założenia

- Zbiór punktów został podzielony pionową prostą $l$ na lewą połowę ($P_L$) i prawą ($P_R$).
- Obliczono minimalną odległość dla punktów po lewej stronie ($\delta_L$) oraz po prawej stronie ($\delta_R$).
- Określono minimum z tych dwóch odległości: $\delta = \min(\delta_L, \delta_R)$.
- Tablica $Y^{\prime}$ zawiera wyłącznie punkty z pionowego pasa o szerokości $2\delta$ (po $\delta$ w każdą stronę od prostej $l$), posortowane rosnąco według współrzędnej $y$.

## Co trzeba pokazać

Należy udowodnić, że w obszarze (prostokącie), w którym mogłaby się znajdować para punktów z różnych stron prostej $l$ leżących bliżej siebie niż $\delta$, z geometrycznych powodów nie da się fizycznie zmieścić więcej niż 8 punktów. Skoro w obszarze jest maksymalnie 8 punktów, to dla dowolnego punktu $p_L$ w tym obszarze, jego szukany sąsiad $p_R$ z drugiej strony prostej musi znajdować się na jednej z 7 kolejnych pozycji w tablicy $Y^{\prime}$.

## Intuicja

Dlaczego to twierdzenie jest prawdziwe i po co jest potrzebne?
Gdy łączymy lewą i prawą stronę, boimy się, że punkt leżący tuż przy granicy po lewej stronie może mieć bardzo blisko sąsiada po prawej stronie. Gdybyśmy chcieli sprawdzać każdy punkt w pasie granicznym z każdym innym, stracilibyśmy całą wydajność algorytmu Dziel i Zwyciężaj. Na szczęście, po obu stronach granicy punkty są "rozrzedzone" – wiemy przecież, że odległość między dowolnymi dwoma po tej samej stronie wynosi *co najmniej* $\delta$. To tak, jakby każdy punkt odpychał inne na odległość $\delta$. W małym prostokątnym oknie na granicy nie da się "upchnąć" wielu takich odpychających się punktów – wejdzie ich maksymalnie 8. Dzięki temu każdy punkt wystarczy porównać zaledwie z siedmioma sąsiadami.

## Szkielet dowodu

> [!tip] Plan dowodu
> 1. Założyć przypadek, w którym para najbliższych punktów to $p_L \in P_L$ i $p_R \in P_R$, a ich odległość $\delta^{\prime} < \delta$.
> 2. Wykazać, że $p_L$ i $p_R$ muszą leżeć w prostokącie ograniczającym o wymiarach $\delta \times 2\delta$, symetrycznym do prostej $l$.
> 3. Podzielić ten prostokąt pionowo na dwa kwadraty o wymiarach $\delta \times \delta$ (jeden z lewej, drugi z prawej).
> 4. Zauważyć, że wszystkie punkty wewnątrz lewego kwadratu pochodzą z $P_L$, więc są oddalone od siebie o co najmniej $\delta$.
> 5. Wywnioskować, że w takim kwadracie mieszczą się co najwyżej 4 punkty (w rogach kwadratu).
> 6. Podsumować: $4$ punkty z lewej $+ 4$ z prawej $= 8$ punktów całkowicie. Zatem po $p_L$ w tablicy może wystąpić co najwyżej 7 innych punktów.

## Pełny dowód

Przypuśćmy, że na pewnym poziomie rekursji parę najmniej odległych punktów stanowią $p_L \in P_L$ i $p_R \in P_R$. Zatem odległość $\delta^{\prime}$ między nimi jest ostro mniejsza niż $\delta$.

Punkt $p_L$ musi leżeć na prostej $l$ lub na lewo od niej, ale nie dalej niż odległość $\delta$. Podobnie $p_R$ leży na $l$ lub na prawo od niej, w odległości mniejszej niż $\delta$. Co więcej, odległość w poziomie między $p_L$ a $p_R$ jest mniejsza niż $\delta$. Zatem $p_L$ i $p_R$ na pewno mieszczą się wewnątrz prostokąta o wymiarach $\delta$ (wysokość) $\times\ 2\delta$ (szerokość), położonego symetrycznie względem prostej $l$.

Pokażemy teraz, że w owym prostokącie $\delta \times 2\delta$ może znajdować się co najwyżej 8 punktów ze zbioru. Rozważmy kwadrat $\delta \times \delta$ stanowiący lewą połowę tego prostokąta.

Ponieważ wszystkie punkty zbioru $P_L$ są z definicji odległe od siebie o przynajmniej $\delta$, wewnątrz tego kwadratu mogą znajdować się co najwyżej cztery punkty (nawet jeśli leżą one dokładnie w jego narożnikach). Podobnie, co najwyżej cztery punkty ze zbioru $P_R$ mogą znajdować się w kwadracie $\delta \times \delta$ stanowiącym prawą połowę prostokąta. (Na samej prostej dzielącej również mogą leżeć punkty obu podzbiorów, ale układ rogów pozostaje najgęstszym upakowaniem).

Zatem w sumie w prostokącie $\delta \times 2\delta$ może znajdować się co najwyżej 8 punktów. Wiedząc to, łatwo stwierdzić, że wystarczy sprawdzać po 7 punktów następujących po każdym punkcie w tablicy $Y^{\prime}$. Zakładając bez straty ogólności, że $p_L$ występuje w tablicy przed $p_R$, nawet jeśli $p_L$ jest pierwsze w tym pudełku, a $p_R$ ostatnie, to i tak $p_R$ będzie zaledwie jedną z maksymalnie 7 pozycji następujących po $p_L$. Wykazuje to pełną poprawność ograniczenia fazy łączenia.

## Wersja do powiedzenia na głos

Skoro zeszliśmy do tego etapu, to wiemy już, że z lewej strony minimalna odległość to $\delta$, z prawej tak samo. Boimy się tylko sytuacji, w której punkt z lewej strony jest połączony z punktem z prawej strony i ta nowa odległość jest mniejsza niż $\delta$.
Gdyby taka odległość faktycznie istniała, to oba te punkty musiałyby zamknąć się w bardzo wąskim okienku – prostokącie wysokości $\delta$ i szerokości $2\delta$ położonym równo na granicy. Tniemy ten prostokąt wzdłuż granicy na dwa kwadraty $\delta \times \delta$. Teraz pomyślmy logicznie: ile punktów z lewej strony można zmieścić w kwadracie $\delta \times \delta$, wiedząc że żadne dwa nie mogą być bliżej siebie niż $\delta$? Maksymalnie 4 – upychając je w samych rogach. Analogicznie 4 wejdą do prawego kwadratu.
Mamy więc łącznie 8 punktów w całym oknie. Jeśli posortowaliśmy te punkty pionowo i weźmiemy jeden z nich, to jego szukany "partner" musi być jednym z 7 pozostałych punktów znajdujących się poniżej niego. Dlatego sprawdzanie zaledwie 7 sąsiadów w zupełności nam wystarczy i gwarantuje poprawność!

## Typowe pułapki

> [!warning] Uważaj na
> - Zrozumienie wymiarów okna — pamiętaj, że okno ma szerokość $2\delta$ (po $\delta$ z każdej ze stron), ale interesuje nas wysokość równa dokładnie $\delta$, ponieważ badamy otoczenie w pionie o maksymalnej odległości mniejszej niż $\delta$.
> - Uzasadnienie liczby 4 — punkty po lewej stronie mogą być od siebie w odległości dokładnie $\delta$ (lub większej), więc można je rozłożyć w rogach kwadratu $\delta \times \delta$. Gdyby bok wynosił mniej niż $\delta$, do kwadratu wszedłby tylko 1 punkt.
> - Wyjaśnienie prostej $l$ — punkty idealnie na prostej granicznej mogą sprawiać problemy intuicyjne. Trzeba pamiętać, że podział przydziela je twardo do $P_L$ lub $P_R$, więc obostrzenie braku kolizji z mniejszym dystansem niż $\delta$ w poszczególnych podzbiorach nadal działa.

## Checklista egzaminacyjna

- [ ] podać pełną treść twierdzenia
- [ ] wymienić założenia
- [ ] powiedzieć, co dokładnie trzeba udowodnić
- [ ] odtworzyć szkielet dowodu
- [ ] odtworzyć pełny dowód
- [ ] wyjaśnić intuicję dowodu własnymi słowami
- [ ] wskazać typowe pułapki

## Mini-fiszki

**Q:** Na czym polega ograniczenie w fazie łączenia w problemie najbliższej pary punktów?  
**A:** Wystarczy sprawdzić odległość rozpatrywanego punktu zaledwie z 7 kolejnymi punktami (następującymi po nim) w tablicy pasa granicznego.

**Q:** Oznaczając minimalną odległość w lewej i prawej połowie jako $\delta$, jakie wymiary ma analizowany prostokąt na granicy podziału?  
**A:** Ma szerokość $2\delta$ (rozłożoną po równo na obu stronach prostej) i wysokość $\delta$.

**Q:** Dlaczego dzielimy prostokąt $\delta \times 2\delta$ na dwa kwadraty?  
**A:** Aby rozpatrywać gęstość upakowania oddzielnie dla punktów z grupy lewej ($P_L$) oraz prawej ($P_R$), wiedząc że w obrębie tej samej grupy odległość wynosi minimum $\delta$.

**Q:** Ile punktów z tej samej połowy grafu ($P_L$ lub $P_R$) może zmieścić się w kwadracie $\delta \times \delta$?  
**A:** Maksymalnie cztery (wyłącznie w przypadku umieszczenia ich w samych wierzchołkach tego kwadratu).

**Q:** Jak łączymy całkowitą liczbę 8 punktów z limitem 7 sprawdzeń w tablicy $Y^{\prime}$?  
**A:** Jeżeli dany punkt ma swojego najbliższego sąsiada w tym obszarze, to sąsiad ten jest jednym z maksymalnie 7 pozostałych punktów, a posortowana tablica gwarantuje nam, że będzie on w obrębie 7 następnych indeksów.

## Powiązania i źródła

**Źródła:**
- [[AZ.pdf]] (Algorytmy Dziel i Zwyciężaj - Znajdowanie pary najbliższych punktów)

**Powiązane algorytmy / pojęcia:**
- Paradygmat Dziel i Zwyciężaj
- Złożoność obliczeniowa $\mathcal{O}(n \log n)$