---
typ: twierdzenie
egzamin: true
status: do_nauczenia
trudnosc: 3
utworzono: 2026-06-03
powiazania:
  - "[[Index_Egzamin]]"
---

# Struktura problemu szeregowania zadań (Twierdzenie 1)

> [!abstract] Cel egzaminacyjny
> Umiem podać treść twierdzenia i odtworzyć dowód bez patrzenia w notatkę.

## Treść twierdzenia

> [!quote] Twierdzenie
> Jeśli $S$ jest zbiorem zadań o jednostkowych czasach wykonania, a $\mathcal{C}$ rodziną podzbiorów niezależnych zbioru $S$, to $(S,\mathcal{C})$ jest matroidem.

## Założenia

- $S$ stanowi zbiór zadań, z których każde charakteryzuje się jednostkowym czasem wykonania.
- $\mathcal{C}$ oznacza rodzinę podzbiorów niezależnych zbioru $S$.
- Zbiór zadań uznaje się za niezależny, jeżeli przy uporządkowaniu zadań niemalejąco według dopuszczalnego terminu wykonania żadne zadanie nie jest spóźnione (zgodnie z Lematem 1).

## Co trzeba pokazać

Należy udowodnić, że para $(S, \mathcal{C})$ spełnia dwa fundamentalne warunki definicyjne matroidu:
1. **Dziedziczność**: Każdy podzbiór niezależnego zbioru zadań jest również zbiorem niezależnym.
2. **Własność wymiany**: Dla dowolnych dwóch podzbiorów niezależnych $A, B \in \mathcal{C}$, gdzie $|B| > |A|$, istnieje takie zadanie $x \in B \setminus A$, że zbiór $A' = A \cup \{x\}$ pozostaje niezależny.

## Intuicja

Dlaczego to twierdzenie jest prawdziwe i po co jest potrzebne?
Twierdzenie to dowodzi, że problem optymalnego szeregowania zadań o jednostkowym czasie trwania posiada strukturę matroidu. Jest to kluczowa informacja z punktu widzenia projektowania algorytmów, ponieważ dla struktur będących matroidami algorytmy zachłanne (np. wybierające zadania w kolejności nierosnących wag/kar) gwarantują znalezienie rozwiązania całkowicie optymalnego. Własność wymiany mówi nam intuicyjnie tyle, że jeśli mamy większy poprawny zestaw zadań ($B$) oraz mniejszy ($A$), to w tym większym zawsze znajdziemy co najmniej jedno zadanie, które możemy bezpiecznie przenieść do mniejszego zestawu i tak zmodyfikować harmonogram, że żadne zadanie nadal nie przekroczy swojego terminu.

## Szkielet dowodu

> [!tip] Plan dowodu
> 1. Wykazanie dziedziczności jako cechy oczywistej dla podzbiorów zadań.
> 2. Założenie niezależności zbiorów $A$ i $B$ oraz relacji rozmiarów $|B| > |A|$ w celu wykazania własności wymiany.
> 3. Definicja parametru $k$ jako największego punktu czasowego $t$, dla którego skumulowana liczba zadań spełnia $N_t(B) > N_t(A)$.
> 4. Uzasadnienie istnienia zadania $x \in B \setminus A$ o dopuszczalnym terminie nie większym niż $k+1$.
> 5. Konstrukcja nowego zbioru $A' = A \cup \{x\}$ i weryfikacja jego niezależności przy użyciu kryteriów z Lematu 1 w rozbiciu na dwa przedziały czasowe.

## Pełny dowód

Każdy podzbiór niezależnego zbioru zadań jest też oczywiście niezależny.

Aby wykazać własność wymiany, załóżmy że $A$ i $B$ są zbiorami niezależnymi oraz że $|B|>|A|$. Niech $k$ będzie największym $t$ takim że zachodzi $N_{t}(B)>N_{t}(A)$. Wiadomo, że $N_{n}(B)=|B|$, $N_{n}(A)=|A|$ i $|B|>|A|$, więc $k<n$ oraz dla każdego $j$ z przedziału $k+1\le j<n$ zachodzi $N_{j}(B)>N_{j}(A)$.

Stąd $B$ zawiera więcej zadań niż $A$ o dopuszczalnym terminie wykonania nie większym od $k+1$. Niech $x$ będzie zadaniem w $B-A$ o dopuszczalnym terminie nie większym od $k+1$. Niech $A^{\prime}=A\cup\{x\}$.

Korzystając z własności z lematu 1, wykażemy teraz, że zbiór $A^{\prime}$ musi być niezależny.
Dla $1\le t\le k$ mamy $N_{t}(A^{\prime})\le N_{t}(A)\le t$, ponieważ $A$ jest zbiorem niezależnym.
Dla pozostałego przedziału czasowego ($t > k$) zachodzi relacja $N_{t}(A^{\prime})\le N_{t}(B)\le t$, ponieważ zbiór $B$ jest niezależny.

Stąd zbiór $A^{\prime}$ jest niezależny, co ostatecznie kończy dowód, że struktura $(S, \mathcal{C})$ jest matroidem.

## Wersja do powiedzenia na głos

Musimy udowodnić, że zadania o jednostkowym czasie z określonymi terminami tworzą matroid. Warunek podzbioru bierzemy za pewnik – skoro z większego zbioru zadań żadne się nie spóźnia, to z mniejszego tym bardziej. Żeby pokazać wymianę, bierzemy dwa bezbłędne zestawy zadań: mniejszy A i większy B. Szukamy ostatniego momentu w czasie (oznaczamy go jako $k$), w którym skumulowana liczba zadań z B przewyższa liczbę zadań z A. Skoro tam jest ich więcej, to w B musi istnieć jakieś zadanie $x$, którego brakuje w A, a którego termin upływa najpóźniej w momencie $k+1$. Tworzymy nowy zbiór dodając to zadanie do A. Sprawdzamy niezależność: przed i w momencie $k$ liczba zadań nowego zbioru jest bezpiecznie ograniczona przez zbiór A, a po momencie $k$ przez zbiór B. W żadnym przedziale nie przekraczamy limitu czasu, więc nowy zbiór też jest niezależny.

## Typowe pułapki

> [!warning] Uważaj na
> - Dokładne rozumienie definicji funkcji $N_t(A)$ — reprezentuje ona liczbę zadań należących do zbioru $A$, których dopuszczalny termin wykonania wynosi *maksymalnie* $t$.
> - Oryginalny zapis w skrypcie zawiera błędy powielenia indeksów w końcowej fazie dowodu — pamiętaj, że sprawdzanie niezależności $A'$ wymaga rozpatrzenia wartości dla $t \le k$ oraz wartości wyższych $t > k$.
> - Prawidłowe powołanie się na Lemat 1 przy uzasadnianiu niezależności poprzez nierówność $N_t(A') \le t$.

## Checklista egzaminacyjna

- [ ] podać pełną treść twierdzenia
- [ ] wymienić założenia
- [ ] powiedzieć, co dokładnie trzeba udowodnić
- [ ] odtworzyć szkielet dowodu
- [ ] odtworzyć pełny dowód
- [ ] wyjaśnić intuicję dowodu własnymi słowami
- [ ] wskazać typowe pułapki

## Mini-fiszki

**Q:** Jak brzmi treść twierdzenia o strukturze problemu szeregowania?  
**A:** Jeśli $S$ to zbiór zadań o jednostkowych czasach wykonania, a $\mathcal{C}$ to rodzina jego podzbiorów niezależnych, to para $(S, \mathcal{C})$ stanowi matroid.

**Q:** Kiedy zbiór zadań w tym problemie jest uznawany za niezależny?  
**A:** Gdy zadania da się ułożyć w takiej kolejności (według dopuszczalnych terminów), że żadne z nich nie zanotuje spóźnienia.

**Q:** Jak definiujemy moment $k$ w dowodzie własności wymiany?  
**A:** Jako największy indeks czasowy $t$, dla którego skumulowana liczba zadań w zbiorze $B$ jest ściśle większa niż w zbiorze $A$ ($N_t(B) > N_t(A)$).

**Q:** Na co pozwala nam wyznaczenie momentu $k$?  
**A:** Gwarantuje nam to, że w zbiorze $B \setminus A$ znajdziemy zadanie $x$ o terminie wykonania nie większym niż $k+1$, które można dołączyć do zbioru $A$.

**Q:** Jak dowodzimy niezależności nowo utworzonego zbioru $A'$?  
**A:** Wykorzystujemy Lemat 1, wykazując spełnienie nierówności $N_t(A') \le t$ oddzielnie dla kroków do momentu $k$ (szacowanie przez niezależny zbiór $A$) oraz po momencie $k$ (szacowanie przez niezależny zbiór $B$).

## Powiązania i źródła

**Źródła:**
- [[AZ.pdf]] (Algorytmy zachłanne - Algorytm szeregowania zadań) 

**Powiązane algorytmy / pojęcia:**
- Definicja matroidu (własność dziedziczności i wymiany) 
- Harmonogramowanie zadań z terminami i karami 