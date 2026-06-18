---
typ: algorytm
egzamin: true
status: do_nauczenia
trudnosc:
utworzono: 2026-06-18
powiazania:
  - "[[Index_Egzamin]]"
---

# Algorytmy Mnożenia Macierzy (Matrix-Multiply, Matrix-Chain-Order)

> [!abstract] Cel egzaminacyjny
> Umiem wyjaśnić działanie algorytmu i przejść go krok po kroku na konkretnych danych.

## Problem

**Wejście:** Ciąg (łańcuch) $n$ macierzy $A_1, A_2, \dots, A_n$, które chcemy przez siebie pomnożyć. Ponieważ wymiary sąsiadujących macierzy muszą się zgadzać, wymiary podajemy jako pojedynczą tablicę $p$, gdzie macierz $A_i$ ma wymiary $p_{i-1} \times p_i$.
**Wyjście:** Tabela minimalnych kosztów mnożenia ($m$), tabela optymalnych podziałów ($s$) oraz ostatecznie wynikowa macierz.
**Co algorytm ma znaleźć / policzyć / skonstruować:** Mnożenie macierzy jest łączne, więc możemy stawiać nawiasy w różnej kolejności (np. $(A_1 A_2)A_3$ albo $A_1(A_2 A_3)$). Różne nawiasowanie drastycznie zmienia liczbę wykonywanych mnożeń skalarnych. Algorytm `Matrix-Chain-Order` korzysta z programowania dynamicznego, aby wyznaczyć optymalne nawiasowanie minimalizujące liczbę mnożeń. Następnie `Matrix-Chain-Multiply` faktycznie mnoży te macierze według znalezionego optymalnego planu.

## Idea

1. Zamiast sprawdzać zawiłe permutacje nawiasów, używamy **Programowania Dynamicznego**.
2. Definiujemy podproblem: niech $m[i, j]$ oznacza minimalny koszt pomnożenia łańcucha macierzy od $A_i$ do $A_j$.
3. Koszt pomnożenia pojedynczej macierzy to zero ($m[i, i] = 0$).
4. Dla dłuższego łańcucha (od $i$ do $j$) sprawdzamy każde możliwe miejsce rozcięcia (punkt $k$, gdzie $i \le k < j$). Obliczamy koszt pomnożenia lewej części ($A_i \dots A_k$), prawej części ($A_{k+1} \dots A_j$) oraz koszt połączenia tych dwóch wynikowych macierzy (wynosi on $p_{i-1} \cdot p_k \cdot p_j$).
5. Wybieramy takie $k$, dla którego suma tych trzech kosztów jest najmniejsza, i zapisujemy ten optymalny punkt rozcięcia w tabeli $s[i, j]$.
6. Obliczenia prowadzimy rosnąco według długości łańcucha $l$ (najpierw pary, potem trójki macierzy itd.).

## Kiedy stosować

- Grafika komputerowa (np. transformacje 3D polegają na potężnych łańcuchach mnożeń macierzy przekształceń).
- Optymalizacja kompilatorów i bibliotek matematycznych (kalkulatory tensorowe, sieci neuronowe), gdzie zaplanowanie kolejności operacji przyspiesza wykonanie programu tysiące razy.

## Pseudokod

```csharp
// 1. ZWYKŁE MNOŻENIE DWÓCH MACIERZY
public Matrix MatrixMultiply(Matrix A, Matrix B) 
{
    if (A.Columns != B.Rows) throw new Exception("Niezgodne rozmiary");
    
    Matrix C = new Matrix(A.Rows, B.Columns);
    for (int i = 1; i <= A.Rows; i++) 
    {
        for (int j = 1; j <= B.Columns; j++) 
        {
            C[i, j] = 0;
            for (int k = 1; k <= A.Columns; k++) 
            {
                C[i, j] += A[i, k] * B[k, j];
            }
        }
    }
    return C;
}

// 2. SZUKANIE OPTYMALNEGO NAWIASOWANIA (Programowanie Dynamiczne)
public (int[,], int[,]) MatrixChainOrder(int[] p) 
{
    int n = p.Length - 1; // Liczba macierzy
    int[,] m = new int[n + 1, n + 1]; // Tabela kosztów
    int[,] s = new int[n + 1, n + 1]; // Tabela punktów podziału k

    // Koszt mnożenia jednej macierzy to 0
    for (int i = 1; i <= n; i++) m[i, i] = 0;

    // l to długość rozpatrywanego łańcucha macierzy
    for (int l = 2; l <= n; l++) 
    {
        for (int i = 1; i <= n - l + 1; i++) 
        {
            int j = i + l - 1;
            m[i, j] = int.MaxValue;

            // Sprawdzamy każde możliwe miejsce rozcięcia k
            for (int k = i; k <= j - 1; k++) 
            {
                int q = m[i, k] + m[k + 1, j] + (p[i - 1] * p[k] * p[j]);
                
                if (q < m[i, j]) 
                {
                    m[i, j] = q; // Nowy minimalny koszt
                    s[i, j] = k; // Zapamiętujemy, w którym miejscu przecięliśmy
                }
            }
        }
    }
    return (m, s);
}

// 3. FAKTYCZNE MNOŻENIE NA BAZIE OPTYMALNEGO NAWIASOWANIA
public Matrix MatrixChainMultiply(Matrix[] A, int[,] s, int i, int j) 
{
    if (j > i) 
    {
        // Wywołujemy rekurencyjnie dla optymalnego punktu podziału k = s[i, j]
        Matrix X = MatrixChainMultiply(A, s, i, s[i, j]);
        Matrix Y = MatrixChainMultiply(A, s, s[i, j] + 1, j);
        return MatrixMultiply(X, Y);
    } 
    else 
    {
        return A[i]; // Baza rekursji: pojedyncza macierz
    }
}

```

## Przebieg na przykładzie

> [!example] Najważniejsza część notatki
> Ten przykład pozwoli Ci odtworzyć kolejność wypełniania komórek. Wypełniamy tabelę $m$ zawsze po przekątnych – od najkrótszych łańcuchów do najdłuższych.

**Dane wejściowe:** Mamy 4 macierze ($n=4$). Tablica wymiarów: $p = (10, 20, 30, 40, 30)$.
Wymiary konkretnych macierzy:

* $A_1$: $10 \times 20$
* $A_2$: $20 \times 30$
* $A_3$: $30 \times 40$
* $A_4$: $40 \times 30$

**Kroki algorytmu (MatrixChainOrder):**

**Krok 1 (Łańcuchy o długości $l=1$):**
Wypełniamy główną przekątną zerami. Nie kosztuje nas nic pomnożenie macierzy samej przez siebie (bo nie ma mnożenia).
$m[1,1] = m[2,2] = m[3,3] = m[4,4] = 0$.

**Krok 2 (Łańcuchy o długości $l=2$):**
Mamy tylko jedno możliwe cięcie dla pary, więc to proste mnożenie wymiarów $p_{i-1} \cdot p_k \cdot p_j$.

* $m[1,2]$ (cięcie $k=1$): $m[1,1] + m[2,2] + 10 \cdot 20 \cdot 30 = 0 + 0 + 6000 = \mathbf{6000}$. ($s[1,2] = 1$)
* $m[2,3]$ (cięcie $k=2$): $m[2,2] + m[3,3] + 20 \cdot 30 \cdot 40 = 0 + 0 + 24000 = \mathbf{24000}$. ($s[2,3] = 2$)
* $m[3,4]$ (cięcie $k=3$): $m[3,3] + m[4,4] + 30 \cdot 40 \cdot 30 = 0 + 0 + 36000 = \mathbf{36000}$. ($s[3,4] = 3$)

**Krok 3 (Łańcuchy o długości $l=3$):**
Tu już mamy wybór.

* Dla $m[1,3]$ możemy przeciąć w $k=1$ (czyli $A_1(A_2 A_3)$) lub w $k=2$ (czyli $(A_1 A_2)A_3$).
* Jeśli $k=1$: $m[1,1] + m[2,3] + 10 \cdot 20 \cdot 40 = 0 + 24000 + 8000 = 32000$.
* Jeśli $k=2$: $m[1,2] + m[3,3] + 10 \cdot 30 \cdot 40 = 6000 + 0 + 12000 = 18000$.
* Mniejsze jest 18000, więc $\mathbf{m[1,3] = 18000}$ oraz $s[1,3] = 2$.


* Dla $m[2,4]$ tniemy w $k=2$ lub $k=3$.
* Jeśli $k=2$: $m[2,2] + m[3,4] + 20 \cdot 30 \cdot 30 = 0 + 36000 + 18000 = 54000$.
* Jeśli $k=3$: $m[2,3] + m[4,4] + 20 \cdot 40 \cdot 30 = 24000 + 0 + 24000 = 48000$.
* Mniejsze to 48000, więc $\mathbf{m[2,4] = 48000}$ oraz $s[2,4] = 3$.



**Krok 4 (Cały łańcuch o długości $l=4$):**
Obliczamy ostateczne $m[1,4]$. Możemy ciąć w $k=1, 2$ lub $3$.

* $k=1$: $m[1,1] + m[2,4] + 10 \cdot 20 \cdot 30 = 0 + 48000 + 6000 = 54000$.
* $k=2$: $m[1,2] + m[3,4] + 10 \cdot 30 \cdot 30 = 6000 + 36000 + 9000 = 51000$.
* $k=3$: $m[1,3] + m[4,4] + 10 \cdot 40 \cdot 30 = 18000 + 0 + 12000 = 30000$.
Mniejsze jest 30000. $\mathbf{m[1,4] = 30000}$ oraz $s[1,4] = 3$.

**Wynik i rekonstrukcja:**
Wiemy, że optymalny koszt to 30000. Odczytujemy nawiasowanie z tablicy $s$:

* Główny podział to $s[1,4] = 3$. Mamy więc $(A_1 \dots A_3) (A_4)$.
* Podział lewej części to $s[1,3] = 2$. Mamy więc $((A_1 A_2) A_3)$.
* Prawa część to tylko jedna macierz.
**Ostateczny, optymalny plan mnożenia to:** $(((A_1 A_2) A_3) A_4)$.

```mermaid
graph TD
    Root["A1..A4"] -->|s[1,4]=3| Left1["(A1..A3)"]
    Root --> Right1["A4"]
    
    Left1 -->|s[1,3]=2| Left2["(A1..A2)"]
    Left1 --> Right2["A3"]
    
    Left2 -->|s[1,2]=1| Leaf1["A1"]
    Left2 --> Leaf2["A2"]

    style Root fill:#bbdefb,stroke:#1565c0,stroke-width:2px
    style Left1 fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px
    style Left2 fill:#fff9c4,stroke:#fbc02d,stroke-width:2px

```

## Złożoność

| Rodzaj | Złożoność | Skąd się bierze |
| --- | --- | --- |
| Czasowa | `O(n^3)` | Dla algorytmu `MatrixChainOrder` mamy 3 zagnieżdżone pętle: po długości $l$, punkcie startowym $i$ oraz punkcie cięcia $k$. Czas samego mnożenia zależy już od wymiarów konkretnych macierzy, ale optymalizacja drastycznie go skraca. |
| Pamięciowa | `O(n^2)` | Musimy przechowywać w pamięci dwuwymiarowe tabele $m$ oraz $s$ o wymiarach $(n+1) \times (n+1)$. |

> [!warning] Typowe pułapki
> * Mylenie indeksów w rozmiarach wymiarów ($p$) — pamiętaj, że macierz $A_k$ ma wymiary $p_{k-1} \times p_k$. Dlatego wzór na łączenie macierzy to zawsze $p_{i-1} \cdot p_k \cdot p_j$.
> * Wypełnianie tabeli po wierszach / kolumnach zamiast po przekątnych — to najczęstszy błąd! Algorytm buduje rozwiązanie od najkrótszych łańcuchów (długość $l=2, 3, 4\dots$). Jeśli spróbujesz policzyć $m[1,3]$ nie mając jeszcze $m[2,3]$, cały proces się posypie.
> * Błędne odczytanie tabeli $s$ — wartość w $s[i, j] = k$ oznacza, że lewa podgrupa kończy się DOKŁADNIE na macierzy $A_k$, a prawa zaczyna się od $A_{k+1}$.
> 
> 

## Checklista egzaminacyjna

* [ ] podać problem, wejście i wyjście
* [ ] wyjaśnić ideę własnymi słowami
* [ ] zapisać lub odtworzyć pseudokod
* [ ] przejść algorytm na konkretnych danych
* [ ] podać złożoność czasową i pamięciową
* [ ] wskazać typowe pułapki

## Mini-fiszki

**Q:** Co rozwiązuje Matrix-Chain-Order?

**A:** Szuka takiego rozmieszczenia nawiasów w ciągu mnożonych macierzy, które minimalizuje sumaryczną liczbę wykonywanych operacji skalarnych (mnożeń).

**Q:** Czym są tablice $m$ oraz $s$ w tym algorytmie?

**A:** Tablica $m$ przechowuje minimalne koszty pomnożenia danego podłańcucha, a tablica $s$ zapamiętuje "punkt cięcia" $k$, w którym należy podzielić ten łańcuch na nawiasy.

**Q:** W jakiej kolejności wypełniana jest tabela w programowaniu dynamicznym?

**A:** Zawsze od najkrótszych łańcuchów macierzy ($l=2$) do najdłuższego ($l=n$), czyli po kolejnych przekątnych tabeli w górę i w prawo.

**Q:** Jaki jest koszt pomnożenia dwóch fragmentów $A_{i \dots k}$ oraz $A_{k+1 \dots j}$?

**A:** Ich koszt to koszt własny obu fragmentów powiększony o koszt ich połączenia: $m[i,k] + m[k+1,j] + p_{i-1} \cdot p_k \cdot p_j$.

## Powiązania i źródła

**Źródła:**

* [[AZ.pdf]] (Programowanie dynamiczne - Algorytmy 4, 5, 6)

**Powiązane twierdzenia / pojęcia:**

* Programowanie dynamiczne.
* Drzewo binarne (jak widać na diagramie, rozbiór na optymalne nawiasy tworzy strukturę odwróconego drzewa wywołań).
