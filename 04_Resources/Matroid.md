## Definicja

Matroid jest parą

$$
M = (E,\mathcal{I})
$$

gdzie:

- $E$ — skończony zbiór elementów,
- $\mathcal{I}$ — rodzina podzbiorów $E$, zwanych **zbiorami niezależnymi**.

Rodzina $\mathcal{I}$ musi spełniać następujące aksjomaty.

### 1. Pusty zbiór

$$
\emptyset \in \mathcal{I}
$$

### 2. Dziedziczność

Jeżeli

$$
A \in \mathcal{I}
$$

oraz

$$
B \subseteq A,
$$

to

$$
B \in \mathcal{I}.
$$

Każdy podzbiór zbioru niezależnego jest niezależny.

### 3. Własność wymiany

Jeżeli

$$
A,B \in \mathcal{I}
$$

oraz

$$
|A| < |B|,
$$

to istnieje element

$$
x \in B \setminus A
$$

taki, że

$$
A \cup \{x\} \in \mathcal{I}.
$$

Mniejszy zbiór niezależny można zawsze powiększyć elementem z większego zbioru niezależnego.

# Intuicja

Matroid formalizuje pojęcie **niezależności**.

Uogólnia wiele struktur matematycznych:

- niezależność liniową wektorów,
- zbiory krawędzi niezawierające cykli w grafach,
- ograniczenia typu „można wybrać najwyżej $k$ elementów z danej grupy”.

Matroid pozwala analizować wszystkie te przypadki przy pomocy jednego aparatu matematycznego.

# Znaczenie w algorytmach

Najważniejszym powodem stosowania matroidów jest następujące twierdzenie.

## Twierdzenie o algorytmie zachłannym

Dany jest matroid

$$
M=(E,\mathcal I)
$$

oraz funkcja wag

$$
w:E\rightarrow \mathbb R.
$$

Algorytm:

1. sortuje elementy malejąco według wag,
2. dodaje kolejny element, jeśli zachowuje niezależność,

znajduje zbiór niezależny o maksymalnej sumie wag.

## Znaczenie praktyczne

Jeżeli w zadaniu uda się wykazać, że zbiór rozwiązań dopuszczalnych tworzy matroid, to poprawność algorytmu zachłannego wynika automatycznie z teorii matroidów.

Typowy schemat dowodu:

1. Definicja zbiorów niezależnych.
2. Weryfikacja aksjomatów matroidu.
3. Zastosowanie twierdzenia o optymalności algorytmu zachłannego.

# Przykłady

## Matroid liniowy

### Elementy

Wektory.

### Zbiory niezależne

Zbiory liniowo niezależnych wektorów.

Przykład:

$$
(1,0), (0,1)
$$

są niezależne.

Natomiast

$$
(1,0), (0,1), (1,1)
$$

są zależne, ponieważ

$$
(1,1) = (1,0) + (0,1).
$$

## Matroid grafowy

### Elementy

Krawędzie grafu.

### Zbiory niezależne

Zbiory krawędzi niezawierające cykli.

Niezależnymi zbiorami są lasy.

Maksymalne zbiory niezależne odpowiadają drzewom rozpinającym.

## Matroid partycyjny

Zbiór elementów podzielony jest na klasy:

$$
E_1,E_2,\ldots,E_m.
$$

Dla każdej klasy określony jest limit

$$
k_i.
$$

Zbiór jest niezależny, jeśli zawiera co najwyżej $k_i$ elementów z klasy $E_i$.

Ten typ matroidu często pojawia się w zadaniach optymalizacyjnych.

# Matroidy w harmonogramowaniu zadań

W klasycznym problemie harmonogramowania z terminami:

- elementami są zadania,
- zbiór niezależny to zbiór zadań możliwy do wykonania przed ich terminami.

Dowód poprawności algorytmu zachłannego zwykle przebiega następująco:

1. Definiuje się rodzinę zbiorów niezależnych.
2. Udowadnia się:
   - aksjomat pustego zbioru,
   - dziedziczność,
   - własność wymiany.
3. Wnioskuje się, że otrzymana struktura jest matroidem.
4. Stosuje się twierdzenie o optymalności algorytmu zachłannego dla matroidów.

# Jak rozpoznać matroid na egzaminie

Jeżeli rozwiązania dopuszczalne:

- pozostają dopuszczalne po usunięciu elementów,
- oraz spełniają własność wymiany,

to warto sprawdzić, czy nie tworzą matroidu.

Pojawienie się matroidu jest bardzo silną wskazówką, że istnieje poprawny algorytm zachłanny.

# Najważniejsze fakty do zapamiętania

## Definicja

Matroid:

$$
M=(E,\mathcal I)
$$

spełniający:

1. pusty zbiór,
2. dziedziczność,
3. własność wymiany.

## Intuicja

Matroid = abstrakcyjny model niezależności.

## Najważniejsze twierdzenie

Dla matroidów algorytm zachłanny wybierający elementy w kolejności malejących wag znajduje rozwiązanie optymalne.

## Typowe przykłady

- niezależność liniowa wektorów,
- zbiory krawędzi bez cykli,
- ograniczenia partycyjne,
- harmonogramowanie zadań z terminami.