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

**Wynik uruchomienia:** [opis i link do zrzutu ekranu]  
**Weryfikacja po zmianie ekranu:** [co zmieniono i co zaobserwowano]

## 5. Praca z Git

- **Issue:** [link]
- **Gałąź:** [nazwa]
- **Pull Request:** [link]
- **Commit(y):** [hash/link]
- **Samoocena PR:** [co zostało sprawdzone]
- **Stan `main` po scaleniu:** [wynik]

## 6. Dyskusja

**Wybór technologii dla scenariusza zespołu:** [framework]  
**Dwa argumenty:** [1], [2]  
**Największe ryzyko:** [opis]  
**Co mogłoby zmienić decyzję:** [warunek]

## 7. Problemy i rozwiązania

| Problem / objaw            | Hipoteza przyczyny | Działanie | Wynik |
| -------------------------- | ------------------ | --------- | ----- |
| [opis lub „nie wystąpiły”] |                    |           |       |

## 8. Wnioski

1. [Czego dowiedziałem(-am) się o technologii?]
2. [Które założenie okazało się nietrafne lub wymaga sprawdzenia?]
3. [Co należy zrobić przed laboratorium 2?]

## 9. Użycie narzędzi AI (jeżeli dotyczy)

**Narzędzie i zakres wsparcia:** [np. wyjaśnienie błędu konfiguracji / propozycja porównania]  
**Jak zweryfikowano wynik:** [dokumentacja, uruchomienie, test]  
**Elementy wykonane samodzielnie:** [opis]

## 10. Checklista oddania

- [ ] Porównanie trzech frameworków.
- [ ] ADR wyboru technologii.
- [ ] Uruchomiona aplikacja i instrukcja w README.
- [ ] Issue, gałąź i scalony PR.
- [ ] Linki do dowodów i historia pracy.
- [ ] Problemy, wnioski i deklaracja AI (jeżeli dotyczy).
