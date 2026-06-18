---
typ: twierdzenie
egzamin: true
status: opanowane
trudnosc: "1"
utworzono: 2026-06-03
powiazania:
  - "[[Index_Egzamin]]"
---

# Twierdzenie Berge'a o ścieżkach powiększających

> [!abstract] Cel egzaminacyjny
> Umiem podać treść twierdzenia i odtworzyć dowód bez patrzenia w notatkę.

## Treść twierdzenia

> [!quote] Twierdzenie
> Skojarzenie $M$ jest maksymalne, gdy nie istnieje względem niego żadna ścieżka powiększająca.

## Założenia

- Dane jest skojarzenie $M$ w grafie $G = (V, E)$.
- Ścieżka powiększająca to ścieżka, której krawędzie należą naprzemiennie do skojarzenia $M$ i spoza niego, a jej początek i koniec są wierzchołkami wolnymi (niebędącymi końcami żadnej krawędzi z $M$).

## Co trzeba pokazać

Należy wykazać dowód niewprost dla kluczowej części twierdzenia: udowadniamy, że jeśli w grafie nie ma żadnej ścieżki powiększającej względem $M$, to skojarzenie $M$ musi być maksymalne. W tym celu zakładamy istnienie większego skojarzenia $M'$ i pokazujemy, że doprowadzi to do nieuchronnego pojawienia się ścieżki powiększającej.

## Intuicja

Dlaczego to twierdzenie jest prawdziwe i po co jest potrzebne?
Twierdzenie Berge'a sprowadza globalny problem (czy moje skojarzenie jest największe z możliwych w całym grafie?) do problemu lokalnego przeszukiwania (czy dam radę znaleźć choć jedną ścieżkę powiększającą?). Jeśli taką ścieżkę znajdziemy, to zamieniając w niej krawędzie wolne na skojarzone i odwrotnie, łatwo powiększymy nasze skojarzenie o 1. Twierdzenie gwarantuje, że moment, w którym takich ścieżek już nie da się znaleźć, jest dokładnie tym momentem, w którym osiągnęliśmy absolutne maksimum i lepiej się nie da.

## Szkielet dowodu

> [!tip] Plan dowodu
> 1. Założyć niewprost, że istnieje inne skojarzenie $M'$ o większej liczbie krawędzi niż $M$.
> 2. Skonstruować pomocniczy graf $G'$ będący różnicą symetryczną obu skojarzeń ($M \oplus M'$).
> 3. Uzasadnić, dlaczego stopień każdego wierzchołka w $G'$ wynosi maksymalnie 2, przez co graf ten składa się wyłącznie z rozłącznych ścieżek i cykli.
> 4. Wykazać, że na każdym cyklu w $G'$ znajduje się dokładnie tyle samo krawędzi z $M$, co z $M'$.
> 5. Pokazać, że skoro $|M'| > |M|$, to w $G'$ musi istnieć co najmniej jedna ścieżka z przewagą krawędzi z $M'$.
> 6. Udowodnić, że taka ścieżka ze względu na swoją naprzemienność jest ścieżką powiększającą względem $M$, co rodzi sprzeczność.

## Pełny dowód

Załóżmy przeciwnie, że istnieje skojarzenie $M^{\prime}$ liczniejsze niż $M$ ($|M'| > |M|$). Rozważmy graf $G^{\prime}=(V,M\oplus M^{\prime})$.

Zauważmy, że w $G^{\prime}$ każdy wierzchołek ma stopień co najwyżej 2, ponieważ do jednego wierzchołka może schodzić się maksymalnie jedna krawędź należąca do $M$ oraz maksymalnie jedna krawędź należąca do $M'$. W związku z tym graf $G^{\prime}$ składa się z geometrycznie rozłącznych ścieżek i cykli.

Na każdym cyklu krawędzie muszą naprzemiennie należeć do $M$ i $M'$ (wierzchołki mają stopień 2, więc krawędzie muszą się przeplatać), z czego wynika, że cykle mają parzystą długość i występuje na nich dokładnie tyle samo krawędzi z $M$, co z $M^{\prime}$.

Natomiast w ścieżkach krawędzie również się przeplatają, w związku z czym w pojedynczej ścieżce może występować co najwyżej o jedną krawędź więcej z któregoś skojarzenia.

W grafie $G^{\prime}$ jest ogółem więcej krawędzi z $M^{\prime}$ niż z $M$ (co wynika bezpośrednio z założenia $|M'| > |M|$). Skoro na cyklach panuje idealny remis liczbowy, to cała nadwyżka krawędzi skojarzenia $M'$ musi znajdować się w ścieżkach. Zatem musi też istnieć w grafie $G'$ co najmniej jedna taka ścieżka, na której jest więcej krawędzi z $M^{\prime}$ niż z $M$.

Ponieważ krawędzie w tej ścieżce leżą naprzemiennie, a $M'$ ma przewagę ilościową, ścieżka ta musi rozpoczynać się oraz kończyć krawędziami należącymi do $M'$. To oznacza, że jej skrajne wierzchołki nie są połączone z żadną krawędzią z $M$ w grafie $G'$ (ani w grafie $G$, bo krawędzie wspólne dla $M$ i $M'$ zostały wycięte przez różnicę symetryczną) – są więc wierzchołkami wolnymi. 

Musi to być oczywiście ścieżka powiększająca względem skojarzenia $M$. Otrzymana sprzeczność kończy dowód twierdzenia.

## Wersja do powiedzenia na głos

Dowodzimy twierdzenia Berge'a niewprost. Zakładamy, że nasze skojarzenie M wcale nie jest maksymalne i da się znaleźć większe skojarzenie M'. Żeby zobaczyć, czym się różnią, wrzucamy je do jednego worka, tworząc różnicę symetryczną $M \oplus M'$. W tym nowym grafie każdy wierzchołek ma stopień najwyżej dwa, bo mógł dotykać góra jednej krawędzi z M i jednej z M'. Taki graf o stopniach manksymalnie dwa rozpada się na osobne ścieżki i cykle. Spoglądamy na cykle – krawędzie idą w nich na zmianę: M, M', M, M', więc krawędzi z obu skojarzeń jest tam dokładnie po równo. Ale przecież założyliśmy, że M' jest większe od M i ma ogółem więcej krawędzi! Skoro w cyklach jest remis, to ta nadwyżka musi siedzieć w ścieżkach. Musi istnieć choć jedna ścieżka, w której krawędzi z M' jest więcej niż z M. A skoro krawędzie muszą się przeplatać i M' wygrywa, to ścieżka ta musi zaczynać się krawędzią z M' i kończyć krawędzią z M'. To z kolei oznacza, że wierzchołki na samych końcach tej ścieżki są wolne od skojarzenia M. Taka ścieżka idealnie pasuje do definicji ścieżki powiększającej względem M. Ale przecież założyliśmy na początku, że żadnych ścieżek powiększających nie ma! Ta sprzeczność dowodzi, że nasze skojarzenie M od początku musiało być maksymalne.

## Typowe pułapki

> [!warning] Uważaj na
> - Dokładne wyjaśnienie pojęcia różnicy symetrycznej ($M \oplus M'$) — wchodzą tam krawędzie, które należą tylko do jednego z tych zbiorów, a krawędzie wspólne wypadają.
> - Wyciągnięcie wniosku o strukturze grafu $G'$ — musisz wyraźnie powiedzieć, że stopień wierzchołków $\le 2$ implikuje podział na rozłączne ścieżki i cykle.
> - Kropkę nad „i” w dowodzie — samo wskazanie ścieżki z większą liczbą krawędzi $M'$ to za mało, trzeba koniecznie dodać, że jej końce muszą być z tego powodu wierzchołkami wolnymi w $M$.

## Checklista egzaminacyjna

- [x] podać pełną treść twierdzenia ✅ 2026-06-11
- [ ] wymienić założenia
- [x] powiedzieć, co dokładnie trzeba udowodnić ✅ 2026-06-11
- [x] odtworzyć szkielet dowodu ✅ 2026-06-11
- [x] odtworzyć pełny dowód ✅ 2026-06-11
- [x] wyjaśnić intuicję dowodu własnymi słowami ✅ 2026-06-11
- [ ] wskazać typowe pułapki

## Mini-fiszki

**Q:** Jak brzmi treść twierdzenia Berge'a?  
**A:** Skojarzenie $M$ jest maksymalne wtedy i tylko wtedy, gdy nie istnieje względem niego żadna ścieżka powiększająca.

**Q:** Co to za graf $G'$ konstruowany w dowodzie?  
**A:** Graf będący różnicą symetryczną skojarzenia badaneego $M$ oraz domniemanego większego skojarzenia $M'$ ($G' = (V, M \oplus M')$).

**Q:** Dlaczego w grafie $G'$ wierzchołki mają stopień co najwyżej 2?  
**A:** Ponieważ z definicji skojarzenia żaden wierzchołek nie może należeć do więcej niż jednej krawędzi z danego skojarzenia (czyli maksymalnie jedna krawędź z $M$ i jedna z $M'$).

**Q:** Dlaczego cykle w grafie $G'$ nie wpływają na różnicę liczności między $M$ a $M'$?  
**A:** Ponieważ krawędzie w cyklu muszą się przeplatać, co wymusza parzystą długość cyklu i idealnie równą liczbę krawędzi z $M$ oraz $M'$.

**Q:** Skąd bierze się sprzeczność w dowodzie Berge'a?  
**A:** Z istnienia ścieżki z przewagą krawędzi z $M'$, która zaczynając się i kończąc krawędzią z $M'$, okazuje się być zakazaną ścieżką powiększającą dla $M$.

## Powiązania i źródła

**Źródła:**
- [[AZ.pdf]] (Algorytmy grafowe znajdowania skojarzenia - Twierdzenie 5)

**Powiązane algorytmy / pojęcia:**
- Ścieżka powiększająca, wierzchołek wolny
- Różnica symetryczna zbiorów
- Algorytm Edmondsa (szukanie skojarzeń w grafach ogólnych)