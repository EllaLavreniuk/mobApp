# Sprawozdanie — Laboratorium 1

**Przedmiot:** Budowa aplikacji mobilnych z użyciem technologii frontendowych  
**Student / identyfikator:** [uzupełnij]  
**Projekt biznesowy:** MOB-003 – GoalPlanner  
**Framework:** React Native  
**Data zajęć:** [2026-10-22]
**Repozytorium:** https://github.com/EllaLavreniuk/MOB-003-GoalPlanner.git
**Commit / tag odpowiadający oddaniu:** [hash / tag]

> Wypełnij na podstawie własnych działań. Odpowiedzi powinny zawierać dowody (pliki, commity, PR, wyniki uruchomienia), nie same deklaracje.

## 1. Cel laboratorium

Celem laboratorium było zapoznanie się z różnicami między najpopularniejszymi frameworkami mobilnymi (React Native, Flutter, NativeScript) i dokonanie świadomego wyboru technologii dla własnego projektu GoalPlanner (MOB-003). Praktyczne przygotowanie warsztatu pracy: skonfigurowanie środowiska programistycznego, pomyślne uruchomienie startowego szkieletu aplikacji na emulatorze, a także opanowanie poprawnego przepływu pracy z systemem Git (repozytorium, Issues, gałęzie funkcyjne i Pull Requesty).

## 2. Analiza technologii

**Dokument:** `docs/technology-comparison.md`  
**Najważniejsze różnice:** React Native wykorzystuje ekosystem JavaScript/TypeScript i renderuje interfejs przy użyciu natywnych komponentów systemu (UI), łącząc się z nimi przez asynchroniczny mostek. Flutter używa języka Dart i posiada własny silnik renderujący (Skia/Impeller), co uniezależnia go od natywnych widoków platformy i zapewnia maksymalną spójność wizualną. Z kolei NativeScript, choć również opiera się na JS/TS, wyróżnia się bezpośrednim, synchronicznym dostępem do natywnych API systemu, co eliminuje konieczność pisania dodatkowych "mostów" dla specyficznych funkcji sprzętowych.  
**Źródła:** Oficjalna dokumentacja React Native (reactnative.dev/docs), Flutter (docs.flutter.dev) oraz NativeScript (docs.nativescript.org).

## 3. Decyzja technologiczna

**Dokument:** `docs/technology-decision.md`  
**Wymagania karty MOB-003 wpływające na wybór:**

1. **Trwały zapis lokalny (Offline-first):** Konieczność bezpiecznego przechowywania relacyjnych danych (Cel → Kamienie milowe) lokalnie na urządzeniu, co wymaga dostępu do sprawdzonych, asynchronicznych bibliotek bazodanowych.
2. **Reaktywne obliczenia (Procent ukończonych celów):** Wymóg ciągłego przeliczania statystyk wymusza użycie frameworka z wydajnym systemem zarządzania stanem (State Management), aby interfejs odświeżał się automatycznie po zmianie statusu zadania.
3. **Zaawansowana walidacja reguł domenowych:** Konieczność pilnowania relacji czasowych (termin kamienia nie przekracza terminu celu) wymaga ekosystemu bogatego w narzędzia do obsługi formularzy i schematów weryfikacji danych.

**Dlaczego wybrano framework:** Wybrano **React Native**, ponieważ opiera się na znanych technologiach webowych (JavaScript/TypeScript, React). Posiada niezwykle dojrzały ekosystem bibliotek (np. Zustand do stanu, React Hook Form do formularzy, WatermelonDB/MMKV do zapisu lokalnego), które pokrywają wszystkie biznesowe wymagania projektu MOB-003.

**Rozważona alternatywa:** Rozważano **Fluttera**. Kompromis polegał na tym, że Flutter zapewniłby absolutną spójność wizualną interfejsu na każdej platformie (dzięki własnemu silnikowi renderującemu), ale wymagałby czasochłonnej nauki nowego języka programowania (Dart).

**Ryzyka:**

1. Fragmentacja UI: Ponieważ React Native używa natywnych komponentów platformy, interfejs może wyglądać nieco inaczej na systemach Android i iOS, co wymusi dodatkowe testy stylów.
2. Narzut wydajnościowy (Bridge): W przypadku składowania i filtrowania ogromnej liczby kamieni milowych w lokalnej bazie, komunikacja między wątkiem JavaScript a wątkiem natywnym może powodować niewielkie spadki płynności, jeśli nie zostanie odpowiednio zoptymalizowana.

## 4. Konfiguracja środowiska

| Narzędzie                   | Wersja                | Rola                                                 |
| --------------------------- | --------------------- | ---------------------------------------------------- |
| System operacyjny           | Windows               | Główne środowisko deweloperskie                      |
| Framework / SDK             | React Native / SDK 57 | Baza i szkielet aplikacji (środowisko Expo)          |
| Runtime / menedżer pakietów | Node.js / npm 11.x    | Środowisko uruchomieniowe JS i pobieranie zależności |
| Emulator / urządzenie       | Fizyczny smartfon     | Uruchomienie kodu za pomocą aplikacji Expo Go        |
| Edytor / IDE                | Visual Studio Code    | Edytor kodu źródłowego i obsługa terminala           |

**Polecenia uruchomienia:**

```text
cd GoalPlanner
npx expo start
(Pełna instrukcja instalacji znajduje się w głównym pliku README.md w repozytorium projektu)
```

**Wynik uruchomienia:** Aplikacja pomyślnie uruchomiła się na fizycznym urządzeniu mobilnym przy użyciu aplikacji Expo Go. Po aktualizacji zależności do SDK 58 rozwiązano problem niekompatybilności. Zrzut ekranu przedstawia działającą aplikację:
![Ekran startowy](../docs/images/screen_start.jpg)

**Weryfikacja po zmianie ekranu:** W pliku źródłowym zmieniono domyślny tekst powitalny na `MOB-003 – GoalPlanner`. Dzięki mechanizmowi Fast Refresh w środowisku Expo, po zapisaniu pliku zmiana natychmiast odświeżyła się na ekranie telefonu bez konieczności ręcznego restartu serwera: ![Ekran po zmianie](../docs/images/screen_changeName.jpg)

## 5. Praca z Git

- **Issue:** (https://github.com/EllaLavreniuk/MOB-003-GoalPlanner/issues/1#issue-6152022349)
- **Gałąź:** `feature/initial-screen`
- **Pull Request:** (https://github.com/EllaLavreniuk/MOB-003-GoalPlanner/pull/2)
- **Commit(y):** (https://github.com/EllaLavreniuk/MOB-003-GoalPlanner/commits/main/)
- **Samoocena PR:** Zgodnie z wymaganiami zweryfikowano, czy aplikacja uruchamia się lokalnie po aktualizacji wersji SDK do 58. Sprawdzono, czy zmieniony tekst (`MOB-003 – GoalPlanner`) wyświetla się prawidłowo i czy kod nie zawiera ukrytych danych wrażliwych ani zbędnych plików (poprawny `.gitignore`).
- **Stan `main` po scaleniu:** Kod został pomyślnie zintegrowany z gałęzią główną `main`. Aplikacja po scaleniu kompiluje się bez błędów, a historia repozytorium jest spójna i zawiera udokumentowany proces zmiany ekranu startowego.

## 6. Dyskusja

**Wybór technologii dla scenariusza zespołu:** `React Native`
**Dwa argumenty:** Brak bariery wejścia i optymalizacja budżetu – zespół doskonale zna już TypeScript i React, co przy krótkim terminie (6 miesięcy) pozwala na natychmiastowe rozpoczęcie prac bez konieczności nauki nowego języka. Dojrzały ekosystem dla wymaganych funkcji – React Native dysponuje sprawdzonymi bibliotekami do realizacji wszystkich kluczowych wymagań scenariusza: aparatu, geolokalizacji oraz lokalnego trybu offline.
**Największe ryzyko:** Zależność od bibliotek trzecich przy dostępie do sprzętu. Ponieważ funkcje takie jak aparat czy GPS bazują na zewnętrznych pakietach open-source, istnieje ryzyko, że w perspektywie dwuletniego utrzymania przestaną być one aktualizowane, a zespół bez znajomości języków natywnych (Java/Swift) będzie miał trudności z ich naprawą po aktualizacjach systemów.  
**Co mogłoby zmienić decyzję:** Zmienił(a)bym decyzję na Flutter, gdyby aplikacja miała opierać się na wysoce niestandardowym interfejsie pełnym złożonych animacji, który musi wyglądać w 100% identycznie na każdym urządzeniu.

## 7. Problemy i rozwiązania

| Problem / objaw| Hipoteza przyczyny| Działanie | Wynik |
| Błąd `Project is incompatible with this version of Expo Go` na telefonie. | Wersja aplikacji Expo Go (SDK 58) jest nowsza niż szablon wygenerowany na komputerze (SDK 57). | Aktualizacja środowiska za pomocą `npm install expo@latest` i wyrównanie pakietów przez `npx expo install --fix`. | Aplikacja na telefonie uruchomiła się pomyślnie. |
| Błąd `ERESOLVE could not resolve` podczas aktualizacji pakietów. | Konflikt zależności wewnątrz paczek przy przeskoku z SDK 57 na SDK 58. | Wywołanie polecenia naprawczego z flagą wymuszającą zignorowanie ścisłych konfliktów: `--legacy-peer-deps`. | Wymagane zależności zainstalowały się poprawnie. |
| Błąd sieciowy `ECONNRESET` w trakcie pobierania pakietów npm. | Zrywanie połączenia z rejestrem npm przez lokalną sieć Wi-Fi lub blokada TLS. | Zmiana dostawcy internetu (hotspot mobilny) oraz wyczyszczenie pamięci podręcznej przez `npm cache clean --force`. | Pakiety pobrane i dodane do `node_modules` bez przerw. |

## 8. Wnioski

1. Ekosystem React Native przy użyciu Expo wymaga bardzo ścisłej kontroli wersji między środowiskiem uruchomieniowym (aplikacją na urządzeniu) a kodem źródłowym. Narzędzia takie jak `npx expo install --fix` są kluczowe w zarządzaniu tymi zależnościami.
2. Założenie, że nowo wygenerowany projekt (przez `npx create-expo-app`) będzie automatycznie w 100% kompatybilny z najnowszą wersją aplikacji na telefonie, okazało się nietrafne. Zmusiło to do przeprowadzenia głębszej aktualizacji zaraz po inicjalizacji.
3. Przed laboratorium 2 należy zaplanować wstępną strukturę katalogów aplikacji oraz przeanalizować mechanizmy nawigacji (np. Expo Router), aby przygotować grunt pod implementację modeli danych `Cel` i `Kamień milowy`.

## 9. Użycie narzędzi AI (jeżeli dotyczy)

**Narzędzie i zakres wsparcia:** Wykorzystano model językowy (AI) w roli asystenta do diagnozy i rozwiązywania błędów konfiguracyjnych środowiska (niezgodność wersji Expo SDK 57 i 58), omijania problemów sieciowych podczas pobierania pakietów npm (`ECONNRESET`, konflikty `ERESOLVE`) oraz wsparcia w zakresie poprawnej składni poleceń Git.  
**Jak zweryfikowano wynik:** Wygenerowane podpowiedzi i komendy były na bieżąco weryfikowane poprzez ich uruchomienie w terminalu VS Code, co doprowadziło do udanej kompilacji i uruchomienia aplikacji na fizycznym urządzeniu (Expo Go). Weryfikacja Git odbyła się poprzez sprawdzenie statusu repozytorium, zgłoszeń (Issues) i Pull Requestów bezpośrednio na platformie GitHub.  
**Elementy wykonane samodzielnie:** Samodzielnie przeanalizowano specyfikację biznesową projektu (MOB-003 – GoalPlanner), zainicjowano projekt, zmodyfikowano kod źródłowy ekranu startowego (`index.tsx`), wykonano zrzuty ekranu.
