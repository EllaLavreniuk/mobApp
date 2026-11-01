# ADR-001: Wybór frameworka

## Kontekst i wymagania
Projekt (MOB-003 – GoalPlanner) wymaga stworzenia mobilnej aplikacji do zarządzania celami i kamieniami milowymi. Główne wymagania biznesowe wpływające na wybór technologii to:
1. **Trwały zapis lokalny (Offline-first):** Aplikacja musi bezpiecznie przechowywać relacyjne dane (Cel → Kamienie milowe) lokalnie na urządzeniu (bez użycia zewnętrznego backendu) i pamiętać je po restarcie.
2. **Reaktywne obliczenia i aktualizacje:** Konieczność bieżącego wyliczania i prezentowania na ekranie procentu ukończonych kamieni milowych (MOB-003-BR-02).
3. **Złożona walidacja formularzy i relacji:** Aplikacja musi pilnować poprawności dat (termin kamienia nie może przekraczać terminu celu - MOB-003-BR-01) oraz blokować usunięcie celu, jeśli ma on przypisane zadania.

## Rozważone alternatywy
* React Native
* Flutter
* NativeScript

## Decyzja
Wybrano **React Native**.

## Uzasadnienie
1. **Zarządzanie stanem (State Management):** Ekosystem Reacta (Context API, Redux lub Zustand) idealnie sprawdza się w reaktywnym przeliczaniu danych. Dzięki temu każda zmiana statusu kamienia milowego automatycznie zaktualizuje wynik procentowy widoczny w głównym widoku (wymóg MOB-003-FR-10).
2. **Zaawansowane biblioteki do danych lokalnych:** React Native posiada wysoce zoptymalizowane rozwiązania offline, takie jak WatermelonDB, Realm czy MMKV. Pozwolą one w prosty sposób obsłużyć relacje na kluczach UUID i wdrożyć blokady kaskadowego usuwania, których wymaga specyfikacja.
3. **Obsługa skomplikowanych formularzy:** Integracja bibliotek takich jak `React Hook Form` z walidatorami `Yup` lub `Zod` pozwoli szybko i bezbłędnie zaimplementować wymaganą walidację logiki domenowej (np. kontrola zakresów dat).

## Konsekwencje i ryzyka
1. **Ryzyko niespójności wizualnej (Fragmentacja UI):** Ponieważ React Native wykorzystuje natywne komponenty, wygląd aplikacji na Androidzie i iOS może się nieznacznie różnić. Będzie to wymagało od dewelopera dodatkowego testowania stylów na obu platformach.
2. **Narzut komunikacyjny w relacjach:** Przy bardzo dużej liczbie rekordów w lokalnej bazie, przesyłanie dużej ilości danych przez mostek komunikacyjny (Bridge) do wątku JavaScript może powodować drobne spadki wydajności.

## Warunki ponownego rozpatrzenia decyzji
Decyzja mogłaby zostać zmieniona na **Flutter**, gdyby aplikacja w przyszłości wymagała implementacji zaawansowanych, spersonalizowanych animacji (np. skomplikowanych wykresów analitycznych obrazujących postęp celów) lub gdyby 100-procentowa spójność interfejsu (co do piksela na każdym urządzeniu) stała się krytycznym wymogiem biznesowym.