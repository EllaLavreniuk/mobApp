# Specyfikacje biznesowa 3
**Przedmiot:** Budowa aplikacji mobilnych z użyciem technologii frontendowych  
**Poziom:** studia I stopnia, semestr 7  
**Data:** 2026-10-18

## Zasady wspólne i interpretacja
- Każda aplikacja realizuje pełny CRUD **głównej encji podrzędnej** (druga encja w karcie) oraz co najmniej tworzenie, odczyt i edycję encji nadrzędnej; usuwanie nadrzędnej encji musi mieć zdefiniowaną politykę dla istniejących rekordów zależnych (np. blokada usunięcia).
- Wymagane są: lista, szczegóły, formularz, wyszukiwanie po nazwie/tytule, filtr po atrybucie domenowym, sortowanie po dacie/nazwie oraz trwały zapis lokalny.
- Wszystkie identyfikatory są lokalnymi UUID; pola oznaczone `?` są opcjonalne. Wymagane są też pola techniczne `id` i klucz obcy encji podrzędnej. Kwoty przechowuje się jako wartości dziesiętne, a nie binarne float; daty i strefy czasowe obsługuje się spójnie.
- Minimum trzy walidacje domenowe: wymagane nazwy, ograniczenia typów/zakresów oraz reguła specyficzna z karty. Co najmniej jedna reguła biznesowa musi mieć automatyczny test pozytywny i negatywny.
- Zakres: jedna osoba, dane lokalne, bez backendu, logowania, płatności i integracji zewnętrznych. Dane demonstracyjne są fikcyjne. Dodatkowe rozszerzenia są przekazywane dopiero w późniejszym laboratorium i nie wchodzą do podstawowego zakresu.
- Kryteria akceptacji są przykładowymi scenariuszami obowiązkowymi; nie zastępują testów całego CRUD ani testów sytuacji pustych/błędnych.

## MOB-003 – GoalPlanner
**Kontekst i problem:** Planowanie i realizacja celów. Brak uporządkowanej ewidencji utrudnia przegląd informacji i podejmowanie decyzji.  
**Użytkownik docelowy:** osoba realizująca cele osobiste.  
**Cel biznesowy:** Umożliwić prowadzenie ewidencji „kamień milowy” w kontekście „cel”, kontrolę poprawności danych oraz uzyskanie użytecznego podsumowania.

### Model danych
- **Cel** (`id:uuid`; nazwa:text; termin:date; status:enum).
- **Kamień milowy** (`id:uuid`; `parentId:uuid`; nazwa:text; termin:date; ukończony:boolean).
- **Relacja:** `Cel (1) → (N) Kamień milowy`. Rekord podrzędny musi wskazywać istniejący rekord nadrzędny. Usunięcie nadrzędnego rekordu z powiązaniami jest blokowane z czytelnym komunikatem.

### Wymagania biznesowe
- **MOB-003-FR-01:** Dodawanie, wyświetlanie, edycja i usuwanie rekordów „kamień milowy”.
- **MOB-003-FR-02:** Tworzenie, przeglądanie i edycja rekordów „cel”.
- **MOB-003-FR-03:** Przypisywanie każdego rekordu „kamień milowy” do wybranego rekordu nadrzędnego.
- **MOB-003-FR-04:** Wyświetlanie listy rekordów wraz z widokiem szczegółów.
- **MOB-003-FR-05:** Wyszukiwanie po nazwie/tytule (dla encji bez takiego pola: po podstawowym polu tekstowym).
- **MOB-003-FR-06:** Filtrowanie po encji nadrzędnej oraz co najmniej jednym polu domenowym, jeżeli występuje; w przeciwnym razie po dacie.
- **MOB-003-FR-07:** Sortowanie według daty lub nazwy; określenie kierunku sortowania.
- **MOB-003-FR-08:** Walidacja pól obowiązkowych, zakresów liczbowych i reguł biznesowych.
- **MOB-003-FR-09:** Prezentowanie komunikatów błędów, pustej listy oraz potwierdzenia usunięcia.
- **MOB-003-FR-10:** Wyliczanie i prezentacja: Procent ukończonych kamieni milowych.
- **MOB-003-FR-11:** Zachowanie danych po ponownym uruchomieniu aplikacji.

### Reguły biznesowe
- **MOB-003-BR-01:** Termin kamienia milowego nie może przekraczać terminu celu.
- **MOB-003-BR-02:** Procent ukończonych kamieni milowych.
- **MOB-003-BR-03:** Puste nazwy/tytuły są niedozwolone; wartości liczbowe i daty muszą odpowiadać deklarowanym typom i zakresom.
- **MOB-003-BR-04:** Nie można zapisać rekordu podrzędnego bez istniejącego powiązania; usunięcie rekordu nadrzędnego z zależnościami jest blokowane.

### Kryteria akceptacji (Given–When–Then)
1. **CRUD:** **Mając** utworzony rekord „cel”, **gdy** użytkownik doda poprawny rekord „kamień milowy”, **wtedy** jest on widoczny na liście i w szczegółach; po edycji prezentuje nowe wartości, a po potwierdzonym usunięciu znika z listy.
2. **Walidacja:** **Mając** formularz „kamień milowy”, **gdy** użytkownik poda wartości sprzeczne z regułą `MOB-003-BR-01`, **wtedy** zapis zostaje zablokowany, a aplikacja pokazuje przyczynę.
3. **Logika domenowa:** **Mając** co najmniej dwa poprawne rekordy testowe, **gdy** użytkownik otworzy podsumowanie, **wtedy** aplikacja wyświetla wynik zgodny z zasadą: Procent ukończonych kamieni milowych.
4. **Relacje:** **Mając** rekord „cel” z powiązanym rekordem „kamień milowy”, **gdy** użytkownik spróbuje usunąć rekord nadrzędny, **wtedy** operacja zostaje zablokowana z informacją o istniejących zależnościach.
5. **Trwałość:** **Mając** zapisane dane, **gdy** użytkownik zamknie i uruchomi aplikację ponownie, **wtedy** rekordy oraz ich relacje pozostają dostępne.
