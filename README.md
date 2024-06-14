# Rozpoznawanie poleceń głosowych

Celem projektu było napisanie modelu klasyfikacyjnego, który przypisuje 1-sekundowym nagraniom audio wypowiedziane słowo kluczowe spośród:

1. down
2. go
3. left
4. no
5. off
6. on
7. right
8. stop
9. up
10. yes

lub stwierdzić, że zachodzi jeden z dwóch stanów specjalnych: w nagraniu jest cisza lub padło nieznane słowo. Łącznie przekłada się to na 12 klas.  

Model działa on w oparciu o sieci konwolucyjne. Najpierw klip audio przekształcany jest na spektrogram, który jest dwuwymiarową tablicą liczb. Następnie jest on normalizowany i poddawany działaniu następujących warstw:  

1. Conv2D: 32 filtry, kernel [11, 41], stride [2, 2]
2. Conv2D: 32 filtry, kernel [11, 21], stride [1, 2]
3. Conv2D: 32 filtry, kernel [11, 21], stride [1, 2]
4. MaxPool2D
5. Dense: 128 jednostek
6. Dense: 12 jednostek

Do aktywacji używana jest ReLU. Do regularyzacji wykorzystywane są Dropout i BatchNormalization. Funkcją straty jest entropia krzyżowa.

Zbiorem danych używanym do nauki jest [*speech\_commands*](https://www.tensorflow.org/datasets/catalog/speech_commands). Zbiory *train*, *validation*, *test* są w proporcji 85:10:5

W notebooku "psi-project.ipynb" znajdują się definicja modelu oraz jego trening. Zawarte są również przykładowe dane ze zbioru oraz zilustrowane kolejne kroki w preprocessingu danych.  

W notebooku "interactive-test.ipynb" przygotowane są skrypty do użytkowania modelu:

1. Zbadanie klasy audio nagranego mikrofonem użytkownika
2. Zbadanie klasy audio z pliku
3. Obliczenie metryk na zbiorach treningowym, walidacyjnym oraz testowym

Aby skrypty działały poprawnie należy wykonać kod we wszystkich komórkach w *Setup*, a następnie wykonać kod w interesującej nas komórce. Funkcje wyliczające metryki nie potrzebują żadnego dodatkowego przygotowania. W funkcji wyznaczającej klasę z pliku należy ustawić "path" na scieżkę do pliku. Funkcję wyznaczającą klasę z nagrania poprzedza 3 sekundowe odliczanie. Następnie audio nagrywane jest przez jedną sekundę.

