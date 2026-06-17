---
typ: twierdzenie
egzamin: true
status: do_powtorki
trudnosc: 4
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
  
Twierdzenie to dowodzi, że problem optymalnego szeregowania zadań o jednostkowym czasie trwania posiada strukturę matroidu. Jest to kluczowa informacja z punktu widzenia projektowania algorytmów, ponieważ dla struktur będących matroidami algorytmy zachłanne gwarantują znalezienie rozwiązania optymalnego.  
  
Własność wymiany mówi intuicyjnie tyle, że jeśli mamy większy poprawny zestaw zadań $B$ oraz mniejszy poprawny zestaw zadań $A$, to w tym większym zestawie znajdziemy co najmniej jedno zadanie, które można bezpiecznie dodać do mniejszego zestawu.  
  
Funkcja $N_t(A)$ służy do kontrolowania, czy do czasu $t$ nie mamy zbyt wielu zadań z terminem wykonania najpóźniej $t$. Ponieważ każde zadanie trwa jedną jednostkę czasu, do czasu $t$ da się wykonać najwyżej $t$ zadań. Dlatego warunek:  
$$N_t(A)\le t$$  
oznacza, że zbiór $A$ nie przeciąża żadnego przedziału czasowego.  
  
W dowodzie własności wymiany szukamy ostatniego momentu $k$, w którym zbiór $B$ jeszcze nie ma przewagi nad zbiorem $A$ pod względem liczby zadań z terminami do tego czasu. Skoro na końcu $B$ ma więcej zadań niż $A$, to po momencie $k$ musi już mieć przewagę. Dzięki temu można znaleźć zadanie z $B\setminus A$, które da się dodać do $A$ bez naruszenia niezależności.  
  
## Szkielet dowodu  
  
> [!tip] Plan dowodu  
> 1. Wykazanie dziedziczności jako cechy oczywistej dla podzbiorów zadań.  
> 2. Założenie niezależności zbiorów $A$ i $B$ oraz relacji rozmiarów $|B| > |A|$ w celu wykazania własności wymiany.  
> 3. Zdefiniowanie funkcji $N_t(A)$ jako liczby zadań ze zbioru $A$ z terminem wykonania nie większym niż $t$.  
> 4. Zdefiniowanie parametru $k$ jako największego punktu czasowego $t$, dla którego zachodzi $N_t(B)\le N_t(A)$.  
> 5. Uzasadnienie, że $k<n$, ponieważ dla $t=n$ mamy $N_n(B)=|B|>|A|=N_n(A)$.  
> 6. Wykazanie, że dla każdego $t>k$ zachodzi $N_t(B)>N_t(A)$.  
> 7. Wybranie zadania $x\in B\setminus A$ o dopuszczalnym terminie wykonania równym $k+1$.  
> 8. Konstrukcja nowego zbioru $A'=A\cup\{x\}$.  
> 9. Weryfikacja niezależności $A'$ przez sprawdzenie nierówności $N_t(A')\le t$ osobno dla $t\le k$ oraz dla $t>k$.  
  
## Pełny dowód  
  
Każdy podzbiór niezależnego zbioru zadań jest również niezależny. Jeżeli pewien zbiór zadań można wykonać tak, aby żadne zadanie się nie spóźniło, to po usunięciu części zadań również można wykonać pozostałe zadania bez spóźnień.  

Aby wykazać własność wymiany, załóżmy, że $A$ i $B$ są zbiorami niezależnymi oraz że:  
$$|B|>|A|.$$
Niech $N_t(A)$ oznacza liczbę zadań ze zbioru $A$, których dopuszczalny termin wykonania jest nie większy niż $t$:  
$$N_t(A)=|\{x\in A : d_x\le t\}|.$$
Przyjmujemy również:  
$$N_0(A)=N_0(B)=0.$$
Niech:  
$$k=\max\{t: N_t(B)\le N_t(A)\}.$$
Ponieważ:  
$$N_n(B)=|B|>|A|=N_n(A),$$
mamy:  
$$k<n.$$
Z maksymalności $k$ wynika, że dla każdego $t>k$ zachodzi:  
$$N_t(B)>N_t(A).$$
W szczególności:  
$$N_{k+1}(B)>N_{k+1}(A).$$
Jednocześnie z definicji $k$ mamy:  
$$N_k(B)\le N_k(A).$$
Oznacza to, że przy przejściu od czasu $k$ do czasu $k+1$ zbiór $B$ uzyskuje przewagę nad zbiorem $A$. Musi więc istnieć zadanie:  
$$x\in B\setminus A$$
o dopuszczalnym terminie wykonania równym:  
$$d_x=k+1.$$
Niech:  
$$A'=A\cup\{x\}.$$
Korzystając z własności z Lematu 1, wykażemy teraz, że zbiór $A'$ jest niezależny. Musimy pokazać, że dla każdego $t$ zachodzi:  
$$N_t(A')\le t.$$
Dla $1\le t\le k$ zadanie $x$ nie jest liczone w $N_t(A')$, ponieważ jego termin wykonania wynosi $k+1$. Zatem:  
$$N_t(A')=N_t(A)\le t,$$
ponieważ $A$ jest zbiorem niezależnym.
Dla pozostałego przedziału czasowego, czyli dla $t>k$, zadanie $x$ jest już liczone, więc:  
$$N_t(A')=N_t(A)+1.$$
Ponieważ dla każdego $t>k$ zachodzi:
$$N_t(B)>N_t(A),$$
a wartości $N_t(A)$ i $N_t(B)$ są całkowite, dostajemy:
$$N_t(A)+1\le N_t(B).$$
W konsekwencji: 
$$N_t(A')=N_t(A)+1\le N_t(B)\le t,$$
ponieważ zbiór $B$ jest niezależny. 
W obu przypadkach otrzymaliśmy:  $N_t(A')\le t.$ 
Zatem zbiór $A'$ jest niezależny. Istnieje więc zadanie $x\in B\setminus A$, które można dodać do $A$, zachowując niezależność. Własność wymiany jest spełniona.  
  
Skoro spełniona jest dziedziczność oraz własność wymiany, struktura $(S,\mathcal{C})$ jest matroidem.
## Wersja do powiedzenia na głos

Musimy udowodnić, że zadania o jednostkowym czasie wykonania z określonymi terminami tworzą matroid. Warunek dziedziczności jest oczywisty: jeśli jakiś zbiór zadań da się wykonać bez spóźnień, to każdy jego podzbiór też da się wykonać bez spóźnień.
Żeby pokazać własność wymiany, bierzemy dwa niezależne zbiory zadań: mniejszy $A$ i większy $B$, czyli $|B|>|A|$. Dla każdego czasu $t$ patrzymy na $N_t(A)$, czyli liczbę zadań ze zbioru $A$, których termin wykonania jest nie większy niż $t$.
Szukamy ostatniego momentu $k$, w którym zbiór $B$ jeszcze nie ma więcej takich zadań niż zbiór $A$, czyli $N_k(B)\le N_k(A)$. Ponieważ na końcu $B$ ma więcej zadań niż $A$, od momentu $k+1$ zbiór $B$ musi już mieć przewagę. W szczególności istnieje zadanie $x\in B\setminus A$, którego termin wykonania wynosi $k+1$.
Dodajemy to zadanie do $A$, tworząc $A'=A\cup\{x\}$. Teraz sprawdzamy niezależność. Dla czasów $t\le k$ nowe zadanie jeszcze się nie liczy, więc $N_t(A')=N_t(A)\le t$. Dla czasów $t>k$ nowe zadanie już się liczy, ale wtedy mamy $N_t(A')=N_t(A)+1\le N_t(B)\le t$. Pierwsza nierówność wynika z tego, że po $k$ zbiór $B$ ma więcej zadań niż $A$, a druga z niezależności $B$.
Zatem dla każdego $t$ zachodzi $N_t(A')\le t$, więc $A'$ jest niezależny. To pokazuje własność wymiany, a razem z dziedzicznością oznacza, że $(S,\mathcal C)$ jest matroidem.
## Typowe pułapki

> [!warning] Uważaj na
>- Dokładne rozumienie definicji funkcji $N_t(A)$ — reprezentuje ona liczbę zadań należących do zbioru $A$, których dopuszczalny termin wykonania wynosi maksymalnie $t$.  
> - Parametr $k$ nie oznacza ostatniego momentu, w którym $B$ przewyższa $A$. Poprawnie: $k$ to ostatni moment, w którym $B$ jeszcze nie przewyższa $A$, czyli $N_k(B)\le N_k(A)$.  
> - Z faktu $N_n(B)=|B|>|A|=N_n(A)$ wynika, że $k<n$.  
> - Dla każdego $t>k$ zachodzi $N_t(B)>N_t(A)$.  
> - Przy przejściu z $N_t(B)>N_t(A)$ do $N_t(A)+1\le N_t(B)$ korzystamy z tego, że są to liczby całkowite.  
> - Sprawdzanie niezależności $A'$ wymaga rozpatrzenia dwóch przypadków: $t\le k$ oraz $t>k$.  
> - Prawidłowe powołanie się na Lemat 1 polega na wykazaniu nierówności $N_t(A')\le t$ dla każdego $t$.

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
- [[Matroid]]
- [[szeregowania zadań]]