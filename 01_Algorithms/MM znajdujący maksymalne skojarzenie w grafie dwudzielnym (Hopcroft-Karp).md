---
typ: algorytm
egzamin: true
status: do_nauczenia
trudnosc: "3"
utworzono: 2026-06-09
powiazania:
  - "[[Index_Egzamin]]"
---

# MM znajdujący maksymalne skojarzenie w grafie dwudzielnym

> [!abstract] Cel egzaminacyjny
> Umiem wyjaśnić działanie algorytmu i przejść go krok po kroku na konkretnych danych.

## Problem

**Wejście:** Dwudzielny graf nieskierowany $G = (V_1 \cup V_2, E)$, gdzie każda krawędź łączy wierzchołek z $V_1$ z wierzchołkiem z $V_2$.
**Wyjście:** Skojarzenie $M$ (podzbiór krawędzi $E$).
**Co algorytm ma znaleźć / policzyć / skonstruować:** Maksymalne skojarzenie, czyli możliwie największy zbiór krawędzi, z których żadne dwie nie mają wspólnego wierzchołka (żaden wierzchołek nie jest "połączony" dwa razy).

## Idea

1. Zaczynamy od pustego skojarzenia ($M = \emptyset$).
2. W każdej iteracji szukamy tzw. **ścieżki powiększającej** w grafie. Jest to ścieżka, która:
   - zaczyna się w wierzchołku wolnym (nieskojarzonym) w $V_1$,
   - kończy się w wierzchołku wolnym (nieskojarzonym) w $V_2$,
   - na przemian wykorzystuje krawędzie nienależące do $M$ oraz należące do $M$.
3. Aby łatwo znaleźć taką ścieżkę, budujemy pomocniczy graf skierowany: krawędzie, które **nie są w skojarzeniu**, kierujemy z $V_1$ do $V_2$, a krawędzie, które **już są w skojarzeniu**, kierujemy z $V_2$ do $V_1$.
4. Jeśli znajdziemy ścieżkę powiększającą, wykonujemy operację **różnicy symetrycznej** ($M \oplus p$). Oznacza to, że odwracamy stan krawędzi na ścieżce: te, które były w skojarzeniu, z niego wylatują, a te, których w nim nie było, do niego wchodzą. Ponieważ ścieżka zaczyna się i kończy krawędzią spoza skojarzenia, ogólna liczba krawędzi w skojarzeniu zawsze rośnie o 1.
5. Powtarzamy proces, aż nie da się znaleźć żadnej nowej ścieżki powiększającej (zgodnie z Twierdzeniem Berge'a mamy wtedy pewność, że skojarzenie jest maksymalne).

## Kiedy stosować

- Przydziały zadań do maszyn / pracowników do projektów (gdzie jeden pracownik robi jeden projekt).
- Dopasowywanie elementów w systemach (np. rekrutacja: kandydat -> wolne stanowisko).
- Jako podprogram w bardziej złożonych problemach grafowych (np. maksymalny przepływ w prostych sieciach).

## Pseudokod

```csharp
public HashSet<Edge> BipartiteMatching(Graph G) 
{
    HashSet<Edge> M = new HashSet<Edge>(); // Początkowo puste skojarzenie
    List<Edge> p;

    do 
    {
        p = FindAugmentingPath(G, M);
        
        if (p.Count > 0) 
        {
            // M = M ⊕ p (Różnica symetryczna)
            // Krawędzie z 'p' obecne w 'M' są usuwane, a te nieobecne są dodawane
            M.SymmetricExceptWith(p); 
        }
        
    } while (p.Count > 0);

    return M;
}

private List<Edge> FindAugmentingPath(Graph G, HashSet<Edge> M) 
{
    // 1. Znajdź wolne (nieskojarzone) wierzchołki
    var freeV1 = G.V1.Where(v => !M.Any(e => e.Contains(v))).ToList();
    var freeV2 = G.V2.Where(v => !M.Any(e => e.Contains(v))).ToList();

    // 2. Skonstruuj graf skierowany G_M
    DirectedGraph GM = new DirectedGraph();
    foreach (var edge in G.Edges) 
    {
        if (M.Contains(edge)) 
            GM.AddDirectedEdge(edge.V2, edge.V1); // Ze skojarzenia: V2 -> V1
        else 
            GM.AddDirectedEdge(edge.V1, edge.V2); // Spoza skojarzenia: V1 -> V2
    }

    // 3. Znajdź ścieżkę z DOWOLNEGO wolnego wierzchołka w V1 do DOWOLNEGO wolnego w V2
    // Używamy np. przeszukiwania wszerz (BFS)
    List<Edge> path = BFS_FindPath(GM, freeV1, freeV2);

    if (path == null) return new List<Edge>();

    // 4. Upewnij się, że to prosta ścieżka (BFS gwarantuje brak cykli, ale wg skryptu: usuń cykle)
    return RemoveCycles(path); 
}

```

## Przebieg na przykładzie

> [!example] Najważniejsza część notatki
> Ten przykład pokazuje największą moc algorytmu: potrafi on "zepsuć" część obecnego rozwiązania (usunąć krawędź ze skojarzenia), aby ostatecznie zyskać więcej połączeń.

**Dane wejściowe:** Zbiór $V_1$ = {1, 2, 3} (Pracownicy)

Zbiór $V_2$ = {A, B, C} (Zadania)

Dostępne krawędzie (kto może wykonać jakie zadanie):

* (1, A)
* (1, C)
* (2, A)
* (2, B)
* (3, B)

Początkowo skojarzenie $M = \emptyset$.

**Kroki:**

**Iteracja 1:**

* **Wolne $V_1$**: {1, 2, 3}, **Wolne $V_2$**: {A, B, C}
* Budujemy skierowany graf $G_M$. Ponieważ $M$ jest puste, wszystkie krawędzie idą z $V_1$ do $V_2$: `1->A`, `1->C`, `2->A`, `2->B`, `3->B`.
* Znajdujemy ścieżkę z wolnego $V_1$ do wolnego $V_2$. Np. prostą ścieżkę z 1 do A: `p = {(1, A)}`.
* Różnica symetryczna: dodajemy krawędź do $M$.
* **Obecne skojarzenie $M$:** `{(1, A)}`

**Iteracja 2:**

* **Wolne $V_1$**: {2, 3}, **Wolne $V_2$**: {B, C}
* Budujemy graf $G_M$. Krawędź `(1, A)` jest w $M$, więc idzie z powrotem: `A->1`. Reszta z $V_1$ do $V_2$: `1->C`, `2->A`, `2->B`, `3->B`.
* Szukamy ścieżki z {2, 3} do {B, C}. Np. od razu widzimy ścieżkę z 2 do B: `p = {(2, B)}`.
* Różnica symetryczna: dodajemy krawędź do $M$.
* **Obecne skojarzenie $M$:** `{(1, A), (2, B)}`

**Iteracja 3 (TU DZIEJE SIĘ MAGIA!):**

* **Wolne $V_1$**: {3}, **Wolne $V_2$**: {C}  *(Pracownik 3 nie ma zadania, zadanie C leży odłogiem).*
* Pracownik 3 potrafi zrobić TYLKO zadanie B. Ale B jest już przypisane do 2! W "chciwym" algorytmie tu byłby koniec. Zobaczmy jak działa nasza ścieżka powiększająca.
* Budujemy $G_M$:
* Krawędzie w $M$ ($V_2 \to V_1$): `A->1`, `B->2`
* Krawędzie poza $M$ ($V_1 \to V_2$): `1->C`, `2->A`, `3->B`


* Szukamy ścieżki z wolnego wierzchołka `3` do wolnego wierzchołka `C`.
1. Zaczynamy w `3`. Jedyna droga to `3->B` (krawędź poza $M$).
2. Jesteśmy w `B`. Jedyna droga (bo to krawędź ze skojarzenia) to `B->2`.
3. Jesteśmy w `2`. Gdzie możemy pójść? `2->A` (poza $M$).
4. Jesteśmy w `A`. Jedyna droga (ze skojarzenia) to `A->1`.
5. Jesteśmy w `1`. Idziemy po krawędzi wolnej `1->C`.
6. Jesteśmy w `C`. Sukces! To wierzchołek docelowy.


* **Znaleziona ścieżka powiększająca $p$:** `(3, B) -> (B, 2) -> (2, A) -> (A, 1) -> (1, C)`. Zauważ naprzemienność: `Nowa -> Stara -> Nowa -> Stara -> Nowa`.
* **Różnica symetryczna ($M \oplus p$):**
* Wywalamy stare (te co prowadziły wstecz): usuwamy `(2, B)` oraz `(1, A)`.
* Dodajemy nowe (te co prowadziły w przód): wstawiamy `(3, B)`, `(2, A)` oraz `(1, C)`.


* **Obecne skojarzenie $M$:** `{(3, B), (2, A), (1, C)}`

**Iteracja 4:**

* Brak wolnych wierzchołków. Algorytm kończy działanie.

**Wynik:** Maksymalne skojarzenie o rozmiarze 3: `{(1, C), (2, A), (3, B)}`. Każdy pracownik dostał zadanie!

## Złożoność

| Rodzaj     | Złożoność      | Skąd się bierze |
| ---------- | -------------- | --------------- |
| Czasowa    | $O(E\sqrt(V))$ |                 |
| Pamięciowa | $O(E)$         |                 |

> [!warning] Typowe pułapki
> * Zapominanie o odwracaniu kierunku krawędzi ze skojarzenia w grafie pomocniczym $G_M$. To absolutnie kluczowe, bo bez tego nie powstanie długa, odkręcająca ścieżka.
> * Błędne wykonywanie różnicy symetrycznej — pamiętaj, że krawędzie wspóldzielone przez $M$ i ścieżkę $p$ wylatują z ostatecznego rozwiązania.
> * Próba znalezienia ścieżki powiększającej pomiędzy dowolnymi wierzchołkami — ścieżka MUSI startować w wierzchołku **wolnym** z $V_1$ i kończyć w **wolnym** z $V_2$.
> * Po znalezieniu ścieżki $p$ jeżeli jest ona cyklem musimy zamienić go na ścieżkę prostą.

## Checklista egzaminacyjna

* [ ] podać problem, wejście i wyjście
* [ ] wyjaśnić ideę własnymi słowami
* [ ] zapisać lub odtworzyć pseudokod
* [ ] przejść algorytm na konkretnych danych
* [ ] podać złożoność czasową i pamięciową
* [ ] wskazać typowe pułapki

## Mini-fiszki

**Q:** Co rozwiązuje ten algorytm?

**A:** Znajduje maksymalne skojarzenie (największy zbiór rozłącznych krawędzi) w grafie dwudzielnym.

**Q:** Jaka jest główna idea?

**A:** Budowanie grafu skierowanego (krawędzie ze skojarzenia idą w tył, spoza skojarzenia w przód) i szukanie ścieżek powiększających, a następnie używanie na nich różnicy symetrycznej.

**Q:** Jaka jest złożoność czasowa i dlaczego?

**A:** $O(|V| \cdot |E|)$, ponieważ algorytm powiększa skojarzenie co najwyżej $O(|V|)$ razy, a każde znalezienie ścieżki za pomocą BFS/DFS kosztuje $O(|E|)$.

**Q:** Jak wygląda pierwszy nietrywialny krok na przykładzie?

**A:** Gdy dodanie nowej krawędzi bezpośrednio jest niemożliwe, algorytm idzie "pod prąd" po krawędzi już będącej w skojarzeniu, aby przenieść przypisanie na inny wierzchołek i zwolnić miejsce (robi tzw. ścieżkę naprzemienną, u nas Iteracja 3).

## Powiązania i źródła

**Źródła:**

* [[AZ.pdf]] (Algorytmy grafowe znajdowania skojarzenia, Algorytmy 14 i 15)

**Powiązane twierdzenia / pojęcia:**

* [[twierdzenie Berge’a o skojarzeniu maksymalnym i ścieżce powiększającej]]
* Różnica symetryczna
* Graf dwudzielny
