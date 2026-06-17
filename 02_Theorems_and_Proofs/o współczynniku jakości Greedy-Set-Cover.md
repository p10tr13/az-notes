---
typ: twierdzenie
egzamin: true
status: do_powtorki
trudnosc: "4"
utworzono: 2026-06-02
powiazania:
  - "[[Index_Egzamin]]"
---

# o współczynniku jakości Greedy-Set-Cover

> [!abstract] Cel egzaminacyjny
> Umiem podać treść twierdzenia i odtworzyć dowód bez patrzenia w notatkę.

## Treść twierdzenia

> [!quote] Twierdzenie
> Ograniczenie względne algorytmu (GreedySetCover) wynosi $H(\max\{|S| : S \in \mathcal{C}\})$. Z dalszej części dowodu wynika również, że ograniczenie to można zapisać jako $H(\max\{|S| : S \in \mathcal{F}\})$.

## Założenia

- $X$ to zbiór, dla którego szukamy pokrycia.
- $\mathcal{F}$ to rodzina podzbiorów zbioru $X$.
- Algorytm zachłannie wybiera zbiór $S \in \mathcal{F}$, który maksymalizuje liczbę niepokrytych dotąd elementów ($|S \cap U|$).
## Co trzeba pokazać

Należy wykazać, że rozmiar pokrycia znalezionego przez algorytm zachłanny ($|\mathcal{C}|$) jest nie większy niż rozmiar pokrycia optymalnego ($|\mathcal{C}^*|$) pomnożony przez $k$-tą liczbę harmoniczną $H(k)$, gdzie $k$ to maksymalny rozmiar zbioru w dostępnej rodzinie zbiorów.
## Intuicja

Dlaczego to twierdzenie jest prawdziwe i po co jest potrzebne? Dowód opiera się na sprytnym "księgowaniu" kosztów. Wybranie zbioru do pokrycia kosztuje "1", a ten koszt rozdzielamy po równo na wszystkie nowo pokryte elementy. Ponieważ algorytm w każdym kroku zachłannie wybiera zbiór pokrywający jak najwięcej nowych elementów, koszt przypisywany pojedynczemu elementowi maleje. Sumując te malejące ułamki, otrzymujemy sumę przypominającą szereg harmoniczny, co ostatecznie daje nam czynnik aproksymacji $H(|S|)$.
## Szkielet dowodu

> [!tip] Plan dowodu
> 1. Zdefiniuj jednostkowy koszt wybrania zbioru $S_i$ i rozdziel go równo między nowo pokryte elementy, definiując $c_x$.
> 2. Zapisz rozmiar otrzymanego pokrycia $|\mathcal{C}|$ jako sumę wszystkich $c_x$ i ogranicz ją przez sumę kosztów dla pokrycia optymalnego $\mathcal{C}^*$.
> 3. Sformułuj kluczową nierówność: dla dowolnego zbioru $S \in \mathcal{F}$ suma kosztów jego elementów to maksymalnie $H(|S|)$.
> 4. Zastosuj tę nierówność do sumy z kroku drugiego, uzyskując ostateczne oszacowanie $|\mathcal{C}| \le |\mathcal{C}^*| \cdot H(\max\{|S|\})$.
> 5. Przeprowadź techniczny dowód kluczowej nierówności, analizując ciąg $u_i$ (liczbę elementów $S$ wciąż niepokrytych po $i$ krokach).

## Pełny dowód

Dowód przeprowadzamy, wiążąc z każdym zbiorem wybieranym przez algorytm pewien koszt i rozdzielając go między elementy pokrywane po raz pierwszy. Niech $S_i$ oznacza $i$-ty podzbiór wybierany przez procedurę; dodanie go do $\mathcal{C}$ ma koszt jednostkowy. Koszt wybrania $S_i$ rozdzielamy równo między elementy pokrywane przez $S_i$ po raz pierwszy. Dla każdego $x \in X$ koszt z nim związany oznaczamy jako $c_x$. Jeśli $x$ jest pokryty po raz pierwszy przez $S_i$, to: $$c_x = \frac{1}{|S_i - (S_1 \cup S_2 \cup ... \cup S_{i-1})|}$$ Koszt optymalnego pokrycia $\mathcal{C}^*$ (które też pokrywa całe $X$) pozwala nam zapisać: $$|\mathcal{C}| = \sum_{x \in X} c_x \le \sum_{S \in \mathcal{C}^*} \sum_{x \in S} c_x$$
> [!note]
> * Lewa to po prostu koszt pokrycia tego uniwersum algorytmem
> * Prawa to suma kosztów dodania elementów w pierwszym ich momencie pokrycia, ale dla zbiorów wykorzystanych przez pokrycie optymalne. Przykład:
> 	* Pokrycie optymalne wykorzystuje {1, 2, 3}, {2, 4}
> 	* Koszt dla 2 jest liczony podwójnie $\frac{1}{3} \times 2$

Dalsza część dowodu opiera się na wykazaniu nierówności dla dowolnego $S \in \mathcal{F}$: $$\sum_{x \in S} c_x \le H(|S|)$$Z tej nierówności natychmiast wynika teza: $$|\mathcal{C}| \le \sum_{S \in \mathcal{C}^*} H(|S|) \le |\mathcal{C}^*| \cdot H(\max\{|S| : S \in \mathcal{F}\})$$**Dowód kluczowej nierówności:** Dla dowolnego $S \in \mathcal{F}$ niech $u_i = |S - (S_1 \cup S_2 \cup ... \cup S_i)|$ będzie liczbą elementów zbioru $S$ nadal niepokrytych po wybraniu $S_1, ..., S_i$. Definiujemy $u_0 = |S|$. Niech $k$ będzie najmniejszym indeksem takim, że $u_k = 0$. Wówczas dla $i=1,2,...,k$ zachodzi $u_{i-1} \ge u_i$, a zbiór $S_i$ pokrywa po raz pierwszy $u_{i-1} - u_i$ elementów z $S$. Suma kosztów dla elementów z $S$ to: $$\sum_{x \in S} c_x = \sum_{i=1}^k (u_{i-1} - u_i) \cdot \frac{1}{|S_i - (S_1 \cup ... \cup S_{i-1})|}$$
> [!note]
> * lewa strona to koszt pokrycia wszystkich elementów dowolnego zbioru $S$
> * prawa strona to suma po iteracjach, a w niej:
> 	* po lewej ilość elementów ze zbioru $S$ pokryta w iteracji $i$
> 	* po prawej koszt pokrycia każdego z tych elementów, czyli 1 przez ilość nowych elementów całego uniwersum pokrywanych przez $S_i$

Z własności wyboru zachłannego wiemy, że $S_i$ pokrywa co najmniej tyle samo nowych elementów co zbiór $S$, zatem: $|S_i - (S_1 \cup ... \cup S_{i-1})| \ge |S - (S_1 \cup ... \cup S_{i-1})| = u_{i-1}$. Otrzymujemy: $$\sum_{x \in S} c_x \le \sum_{i=1}^k (u_{i-1} - u_i) \cdot \frac{1}{u_{i-1}}$$Oszacowanie sumy (korzystając z definicji liczb harmonicznych):$$\sum_{i=1}^k (u_{i-1} - u_i) \cdot \frac{1}{u_{i-1}} \le \sum_{i=1}^k \sum_{j=u_i + 1}^{u_{i-1}} \frac{1}{j} = \sum_{i=1}^k \left( H(u_{i-1}) - H(u_i) \right)$$$$= H(u_0) - H(u_k) = H(|S|) - H(0) = H(|S|)$$Co kończy dowód.
## Wersja do powiedzenia na głos

Zasada jest taka: każdy wybrany podzbiór kosztuje 1. Ten koszt dzielimy na nowo pokryte w danym kroku elementy. Ponieważ zawsze bierzemy zbiór, który pokrywa najwięcej nowych elementów, to te jednostkowe koszty przypadające na element są małe i z każdym krokiem algorytmu przypominają wyrazy szeregu harmonicznego. Całkowity koszt naszego pokrycia to suma tych małych ułamków. Jeśli weźmiemy optymalne pokrycie, suma kosztów wewnątrz jego zbiorów nie przekroczy liczby harmonicznej z rozmiaru tych zbiorów. Stąd nasz wynik jest gorszy co najwyżej o czynnik $H(|S_{max}|)$.
## Typowe pułapki

> [!warning] Uważaj na
> - Zrozumienie, czym jest $c_x$ – jest to koszt zdefiniowany w momencie **pierwszego** pokrycia elementu $x$ przez algorytm.
> - Poprawne uzasadnienie przejścia $|S_i - \dots| \ge u_{i-1}$. Wynika ono bezpośrednio z tego, że algorytm jest zachłanny i w kroku $i$-tym wolał wybrać $S_i$ niż $S$.
> - Poprawne przejście z teleskopowej sumy liczb harmonicznych.

## Checklista egzaminacyjna

- [ ] podać pełną treść twierdzenia
- [ ] wymienić założenia
- [ ] powiedzieć, co dokładnie trzeba udowodnić
- [ ] odtworzyć szkielet dowodu
- [ ] odtworzyć pełny dowód
- [ ] wyjaśnić intuicję dowodu własnymi słowami
- [ ] wskazać typowe pułapki

## Mini-fiszki

**Q:** Jaka jest treść twierdzenia o pokryciu zbiorowym?
**A:** Algorytm zachłanny ma współczynnik aproksymacji równy $H(\max|S|)$, czyli $k$-tej liczbie harmonicznej maksymalnego rozmiaru zbioru.

**Q:** Jak przypisuje się koszty poszczególnym elementom?
**A:** Element pokryty po raz pierwszy w kroku $i$ przez zbiór $S_i$ otrzymuje koszt odwrotnie proporcjonalny do liczby *nowych* elementów pokrytych przez ten zbiór.

**Q:** Co to jest $u_i$ w dowodzie?
**A:** Jest to liczba elementów dowolnego, ustalonego zbioru $S$, które wciąż pozostają niepokryte po $i$-tym kroku algorytmu.

**Q:** Na jakiej podstawie szacujemy wielkość mianownika w dowodzie nierówności na sumę kosztów?
**A:** Na podstawie własności wyboru zachłannego – algorytm w kroku $i$-tym wybrał $S_i$, a nie $S$, co oznacza, że $S_i$ dostarczył co najmniej tyle samo nowych elementów co $S$ (czyli co najmniej $u_{i-1}$).

**Q:** Gdzie najłatwiej popełnić błąd w wyprowadzeniu wzoru?
**A:** Na etapie oszacowania $\frac{u_{i-1} - u_i}{u_{i-1}} \le H(u_{i-1}) - H(u_i)$ wykorzystującego sumy częściowe szeregu harmonicznego.

## Powiązania i źródła

**Źródła:**
- [[AZ.pdf]] (Algorytmy aproksymacyjne)

**Powiązane algorytmy / pojęcia:**
- Algorytm [[Greedy-Set-Cover]]
- Liczby harmoniczne
