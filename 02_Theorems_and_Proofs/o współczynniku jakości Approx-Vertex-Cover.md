---
typ: twierdzenie
egzamin: true
status: nauczone
trudnosc: "1"
utworzono: 2026-06-03
powiazania:
  - "[[Index_Egzamin]]"
---

# Ograniczenie względne algorytmu Approx-Vertex-Cover

> [!abstract] Cel egzaminacyjny
> Umiem podać treść twierdzenia i odtworzyć dowód bez patrzenia w notatkę.

## Treść twierdzenia

> [!quote] Twierdzenie
> Ograniczenie względne (współczynnik aproksymacji) algorytmu ApproxVertexCover wynosi 2. Oznacza to, że znajduje on pokrycie wierzchołkowe nie więcej niż dwukrotnie większe od pokrycia optymalnego.

## Założenia

- Mamy dany graf $G=(V, E)$.
- Algorytm w pętli wybiera dowolną niepokrytą krawędź $(u,v)$, dodaje oba jej końce ($u$ oraz $v$) do zbioru rozwiązania $C$, a następnie usuwa z grafu wszystkie krawędzie incydentne z $u$ lub $v$. Pętla trwa, dopóki w grafie są jakieś niepokryte krawędzie.

## Co trzeba pokazać

Należy udowodnić dwie rzeczy:
1. Zbiór $C$ zwracany przez algorytm jest faktycznie poprawnym pokryciem wierzchołkowym.
2. Rozmiar znalezionego pokrycia $|C|$ spełnia nierówność $|C| \le 2|C^*|$, gdzie $C^*$ to optymalne (najmniejsze możliwe) pokrycie wierzchołkowe tego grafu.

## Intuicja

Dlaczego to twierdzenie jest prawdziwe i po co jest potrzebne?
Algorytm jest bardzo "brutalny" – widząc niepokrytą krawędź, dla świętego spokoju bierze do rozwiązania oba jej końce. W trakcie tego procesu mimowolnie znajduje zestaw krawędzi, które nie mają ze sobą absolutnie żadnych wspólnych wierzchołków. Optymalne rozwiązanie, żeby pokryć ten zbiór niezależnych krawędzi, musi wziąć po co najmniej jednym wierzchołku z każdej z nich. My bierzemy po dwa. Dlatego nasz wynik jest zawsze co najwyżej dwukrotnie gorszy od ideału.

## Szkielet dowodu

> [!tip] Plan dowodu
> 1. Wykazać poprawność algorytmu (pętla działa do momentu wyczerpania wszystkich krawędzi).
> 2. Zdefiniować zbiór $A$ jako zestaw krawędzi wyciągniętych bezpośrednio w kroku wyboru algorytmu.
> 3. Pokazać, że krawędzie ze zbioru $A$ są parami rozłączne (nie mają wspólnych wierzchołków).
> 4. Zauważyć, że nasz zbiór $C$ składa się dokładnie z obu końców każdej krawędzi z $A$, więc $|C| = 2|A|$.
> 5. Uzasadnić, że pokrycie optymalne $C^*$ musi pokryć wszystkie krawędzie z $A$, używając na to co najmniej $|A|$ wierzchołków ($|A| \le |C^*|$).
> 6. Połączyć powyższe fakty w ostateczną nierówność $|C| \le 2|C^*|$.

## Pełny dowód

Zbiór $C$ skonstruowany przez procedurę jest pokryciem wierzchołkowym, ponieważ pętla w algorytmie jest wykonywana tak długo, aż każda krawędź z $E[G]$ zostanie pokryta przez jakiś wierzchołek z $C$ i usunięta. 

Żeby przekonać się, że algorytm oblicza pokrycie wierzchołkowe co najwyżej dwukrotnie większe od optymalnego, oznaczmy przez $A$ zbiór krawędzi wybranych wewnątrz pętli procedury. 

Żadne dwie krawędzie z $A$ nie mają wspólnego wierzchołka, ponieważ za każdym razem, kiedy wybierana jest krawędź, wszystkie inne krawędzie incydentne z jej końcami zostają natychmiast usunięte z grafu i nie mogą być wybrane w kolejnych krokach. Każde dołożenie krawędzi z $A$ dodaje dokładnie dwa nowe wierzchołki do $C$, zatem mamy bezpośrednią zależność: $|C| = 2|A|$.

Aby pokryć wszystkie krawędzie ze zbioru $A$, każde prawidłowe pokrycie wierzchołkowe – w tym pokrycie optymalne $C^*$ – musi zawierać przynajmniej jeden z końców każdej krawędzi należącej do $A$. Ponieważ żadne dwie krawędzie w $A$ nie mają wspólnego końca, żaden wierzchołek optymalnego pokrycia nie jest w stanie pokryć więcej niż jednej krawędzi z $A$. Wymusza to nierówność:
$|A| \le |C^*|$

Łącząc obie relacje otrzymujemy:
$|C| = 2|A| \le 2|C^*|$
Co kończy dowód twierdzenia.

## Wersja do powiedzenia na głos

Nasz algorytm działa tak, że losuje krawędź, bierze jej dwa wierzchołki do wyniku, wywala wszystkie krawędzie, które dotykały tych wierzchołków i powtarza to w kółko. 
Zauważmy ciekawą rzecz: te krawędzie, które sobie wylosowaliśmy (nazwijmy je zbiorem A), w ogóle się ze sobą nie stykają. Nie mają wspólnych wierzchołków, bo po wylosowaniu pierwszej od razu usunęliśmy całe jej sąsiedztwo. Skoro daliśmy do wyniku oba końce każdej takiej krawędzi, to rozmiar naszego wyniku to po prostu $2 \cdot |A|$. 
A co musi zrobić algorytm optymalny? Musi pokryć jakoś nasz zbiór rozłącznych krawędzi A. Skoro nie mają punktów wspólnych, to optymalny algorytm na każdą krawędź z A musi zużyć przynajmniej jeden wierzchołek. Czyli jego rozmiar to minimum $|A|$. Porównując: optymalny bierze przynajmniej jeden wierzchołek, my bierzemy zawsze dwa, więc nasz wynik jest maksymalnie dwa razy większy.

## Typowe pułapki

> [!warning] Uważaj na
> - Mylenie zbioru krawędzi ze zbiorem wierzchołków — pamiętaj, że do zbioru rozwiązania $C$ wrzucamy wierzchołki, ale do dowodu definiujemy pomocniczy zbiór krawędzi $A$.
> - Pominięcie dowodu poprawności — dowód to nie tylko wykazanie współczynnika równego 2, ale na samym wstępie pokazanie, że pętla while (`while E' nie jest puste`) w ogóle gwarantuje pokrycie całości.

## Checklista egzaminacyjna

- [ ] podać pełną treść twierdzenia
- [ ] wymienić założenia
- [ ] powiedzieć, co dokładnie trzeba udowodnić
- [ ] odtworzyć szkielet dowodu
- [ ] odtworzyć pełny dowód
- [ ] wyjaśnić intuicję dowodu własnymi słowami
- [ ] wskazać typowe pułapki

## Mini-fiszki

**Q:** Jaki współczynnik aproksymacji ma algorytm zachłanny Approx