# 🎓 Index: Egzamin z Algorytmów Zaawansowanych

> [!abstract] Cel
> Jedno miejsce do kontroli zakresu, postępu i powtórek przed egzaminem.

## Jak używać

1. Tworzę brakujące notatki z szablonów w `101_Templates`.
2. W każdej notatce ustawiam `status`, np. `do_nauczenia`, `w_trakcie`, `do_powtorki`, `opanowane`.
3. W indeksie odhaczam zakres ręcznie, a tabele Dataview pokazują postęp z notatek.

## Statusy

| Status | Znaczenie |
| :--- | :--- |
| `do_nauczenia` | notatka istnieje, ale materiał nie jest opanowany |
| `w_trakcie` | materiał jest częściowo przerobiony |
| `do_powtorki` | materiał był przerobiony, ale wymaga powtórki |
| `opanowane` | umiem odtworzyć bez patrzenia |

## 🚀 Algorytmy

- [ ] [[znajdujący najbliższe dwa punkty na płaszczyźnie]]
- [ ] [[Matrix-Multiply, Matrix-Chain-Order]]
- [ ] [[Longest-Common-Subsequence]]
- [ ] [[zachłanny wyboru zajęć]]
- [ ] [[Huffmana]]
- [ ] [[szeregowania zadań]]
- [ ] [[Greedy-Set-Cover]]
- [ ] [[Approx-Vertex-Cover]]
- [ ] [[Exact-Subset-Sum]]
- [ ] [[Approx-Subset-Sum]]
- [ ] [[MM znajdujący maksymalne skojarzenie w grafie dwudzielnym (Hopcroft-Karp)]]

### Dashboard algorytmów

```dataview
TABLE
  status AS "Status",
  trudnosc AS "Trudność",
  zlozonosc_czasowa AS "Czas",
  zlozonosc_pamieciowa AS "Pamięć"
FROM "01_Algorithms"
SORT status ASC, file.name ASC
```

## 📜 Twierdzenia i dowody

- [ ] [[o strukturze problemu szeregowania zadań]]
- [ ] [[o poprawności algorytmu znajdującego parę najbliższych punktów]]
- [ ] [[o współczynniku jakości Approx-Vertex-Cover]]
- [ ] [[o współczynniku jakości Greedy-Set-Cover]]
- [ ] [[twierdzenie Berge’a o skojarzeniu maksymalnym i ścieżce powiększającej]]

### Dashboard twierdzeń

```dataview
TABLE
  status AS "Status",
  trudnosc AS "Trudność"
FROM "02_Theorems_and_Proofs"
SORT status ASC, file.name ASC
```

## Zadania z indeksu

```tasks
not done
path includes 00_Mind_Maps/Index_Egzamin.md
hide backlink
```

## Widok powtórek

### Do powtórki

```dataview
TABLE
  typ AS "Typ",
  trudnosc AS "Trudność"
FROM "01_Algorithms" OR "02_Theorems_and_Proofs"
WHERE status = "do_powtorki"
SORT file.name ASC
```

### Opanowane

```dataview
TABLE
  typ AS "Typ",
  trudnosc AS "Trudność"
FROM "01_Algorithms" OR "02_Theorems_and_Proofs"
WHERE status = "opanowane"
SORT file.name ASC
```
