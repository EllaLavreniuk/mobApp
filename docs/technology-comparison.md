# Zadanie 1: analiza trzech frameworków


## 1. Analiza kryteriów

### 1. Język programowania
*   **React Native**: Używa JavaScript lub TypeScript w połączeniu ze składnią JSX (React). 
    *   Zgodnie z [dokumentacją RN](https://reactnative.dev/docs/getting-started), framework opiera się na podstawach Reacta i technologiach webowych.
*   **Flutter**: Wykorzystuje język Dart (stworzony przez Google).
    *    Zgodnie z [dokumentacją Fluttera](https://docs.flutter.dev/), język ten kompiluje się do kodu maszynowego w trybie release (AOT).
*   **NativeScript**: Używa JavaScript lub TypeScript i może być zintegrowany z frameworkami takimi jak Angular, Vue.js lub Svelte.
    *    Zgodnie z [dokumentacją NativeScript](https://docs.nativescript.org/), środowisko pozwala na użycie czystego TS/JS lub wyżej wymienionych frameworków.
*   **[Ocena]**: React Native i NativeScript mają najniższy próg wejścia dla programistów webowych. Flutter wymaga nauki Darta, co na początku może spowolnić zespół, ale Dart jest bardzo intuicyjny dla osób znających Javę lub C#.

### 2. Sposób tworzenia/renderowania UI
*   **React Native**: Renderuje prawdziwe, natywne komponenty platformy (np. `UIView` na iOS, `View` na Androidzie) poprzez asynchroniczny mostek (lub nową architekturę JSI).
*   **Flutter**: Posiada własny silnik renderujący (Skia / Impeller), który samodzielnie rysuje każdy piksel interfejsu na płótnie dostarczonym przez system. Nie używa natywnych widoków OEM.
*   **NativeScript**: Podobnie jak React Native, mapuje kod UI (często pisany w XML) na natywne komponenty systemu, działając na jednym wątku z użyciem bezpośrednich wywołań.
*   **[Ocena]**: Podejście Fluttera uważam za najbardziej przewidywalne – interfejs wygląda identycznie na każdym urządzeniu. React Native i NativeScript zapewniają bardziej "natywne" odczucia, ale ryzykujemy niespójności graficzne między wersjami systemów.

### 3. Dostęp do natywnych API
*   **React Native**: Wymaga tworzenia modułów natywnych (Native Modules) w Javie/Kotlinie lub Swifcie/Objective-C, które komunikują się z JS. 
*   **Flutter**: Wykorzystuje tzw. Platform Channels do asynchronicznej komunikacji między kodem w Dart a natywnym kodem hosta. 
*   **NativeScript**: Wstrzykuje natywne klasy bezpośrednio do silnika JS (V8 / JavaScriptCore), pozwalając na wywoływanie natywnego kodu iOS/Androida bezpośrednio z poziomu TypeScriptu.
*   **[Ocena]**: NativeScript deklasuje tu konkurencję pod względem łatwości dostępu do specyficznych, niskopoziomowych funkcji bez znajomości języków natywnych.

### 4. Wsparcie Android / iOS
*   *[Fakt]* Cała trójka wspiera tworzenie aplikacji na systemy Android oraz iOS z jednej bazy kodu. Ponadto Flutter i React Native oferują stabilne wsparcie dla Web i wczesne dla aplikacji desktopowych (Windows, macOS).
*   **[Ocena]**: Flutter najlepiej radzi sobie z unifikacją – aplikacje po prostu działają niezależnie od nakładki systemowej Androida.

### 5. Narzędzia (Tooling)
*   **React Native**: Posiada potężny ekosystem Expo, który dramatycznie upraszcza budowanie, testowanie (Expo Go) i aktualizacje (OTA).
*   **Flutter**: Wyposażony w świetne, wbudowane narzędzia CLI, instalator i zestaw Flutter DevTools (profiler wydajności, inspektor widżetów).
*   **NativeScript**: Udostępnia CLI oraz integrację z Webpackiem; narzędzia są poprawne, ale rzadziej aktualizowane.
*   **[Ocena]**: Flutter DevTools to najbardziej kompletne i najstabilniejsze środowisko. Expo z RN jest świetne, ale bywa problematyczne przy ucieczce ("eject") do czystego kodu natywnego.

### 6. Testowanie
*   **React Native**: Silnie opiera się na narzędziach ze świata JS: Jest dla testów jednostkowych, Detox dla testów E2E.
*   **Flutter**: Posiada wbudowany, rewelacyjny mechanizm "Widget Testing", który pozwala testować komponenty interfejsu w izolacji bez odpalania emulatora, oraz pakiet `integration_test`.
*   **NativeScript**: Używa tradycyjnych runnerów, takich jak Karma, oraz frameworków Appium do testów E2E.
*   **[Ocena]**: Wbudowane testowanie we Flutterze (Widget Testing) jest znacznie szybsze i stabilniejsze niż opieranie się na rozwiązaniach firm trzecich, jak ma to miejsce w React Native.

### 7. Ekosystem
*   **React Native**: Gigantyczna liczba paczek na npm, ogromna społeczność (wsparcie Meta).
*   **Flutter**: Bardzo dynamicznie rosnący ekosystem paczek na `pub.dev` (wsparcie Google).
*   **NativeScript**: Niszowy ekosystem, mała społeczność, często oparta na wtyczkach utrzymywanych przez pojedyncze osoby.
*   **[Ocena]**: React Native to najbezpieczniejszy wybór komercyjny ze względu na podaż bibliotek. Wybór NativeScript wiąże się z wysokim ryzykiem, że napotkany problem nie został jeszcze przez nikogo na świecie rozwiązany na Stack Overflow.

### 8. Ograniczenia
*   **React Native**: Historyczny wąskim gardłem był asynchroniczny "Mostek" (Bridge) do UI; skomplikowany proces aktualizacji (upgrade) frameworka.
*   **Flutter**: Rozmiar pliku wynikowego aplikacji jest zazwyczaj większy niż u konkurencji (zawiera cały silnik Skia/Impeller); aplikacje nie używają natywnych ułatwień dostępu w taki sam naturalny sposób jak RN.
*   **NativeScript**: Stroma krzywa uczenia się, jeśli chcemy w pełni wykorzystać natywne API (wymaga znajomości struktury SDK Androida/iOS, choć piszemy w TS).

---

## 2. Odpowiedzi na pytania kontrolne

**1. Dlaczego React Native nie jest tym samym co aplikacja webowa w WebView?**
Aplikacje w WebView (np. Cordova, Ionic) wyświetlają interfejs za pomocą silnika przeglądarki internetowej, renderując znaczniki HTML i stylizując je w CSS (operacje na drzewie DOM). React Native nie używa HTML-a. Używa JavaScriptu jako zarządcy, który instruuje system operacyjny, aby ten narysował swoje wbudowane, natywne komponenty (np. autentyczny `android.widget.Button` zamiast `<button>`).

**2. Czym różni się podejście Fluttera do interfejsu od React Native?**
React Native zmusza system operacyjny do rysowania swoich własnych, natywnych elementów kontrolnych. Flutter ignoruje wbudowane widoki systemu. Zamiast tego komunikuje się bezpośrednio z układem graficznym (GPU) urządzenia (np. przez OpenGL, Vulkan, Metal) i samodzielnie renderuje każdy pojedynczy piksel na ekranie przy użyciu własnego silnika (Skia lub Impeller).

**3. Co oznacza dostęp do natywnego API w NativeScript?**
Oznacza to, że za pomocą mechanizmu refleksji i silników JavaScriptCore / V8, programista może w pliku TypeScript bezpośrednio odwołać się do klas z języka Java lub Swift bez konieczności pisania jakiegokolwiek pomostu w tych językach (tzw. wrappera). Przykład: `const context = android.content.Context;` napisane prosto w kodzie JS działa natychmiast na urządzeniu.

**4. Dlaczego liczba pobrań biblioteki nie wystarcza do oceny ryzyka technologicznego?**
Liczba pobrań na platformach typu `npm` bywa sztucznie zawyżona. Pakiety są pobierane automatycznie przy każdym uruchomieniu systemów CI/CD (Continuous Integration), przez boty monitorujące lub jako rzadko używane subzależności (dependency of a dependency) innych, większych pakietów. Lepszymi miernikami ryzyka są: data ostatniego commita, liczba rozwiązanych Issue / Pull Requestów oraz fakt wspierania paczki przez organizacje komercyjne, a nie pojedynczego hobbystę.

**Dyskusja: wybór technologii w warunkach ograniczeń:** React Native

**Dwa argumenty:** 
1. **Brak bariery wejścia i optymalizacja budżetu:** Zespół doskonale zna już TypeScript i React. Przy krótkim terminie (6 miesięcy) i ograniczonym budżecie pozwala to na natychmiastowe rozpoczęcie prac, eliminując czasochłonny etap nauki nowego języka (np. Darta).
2. **Dojrzały ekosystem dla wymaganych funkcji:** React Native dysponuje sprawdzonymi bibliotekami do realizacji wszystkich kluczowych wymagań: aparatu (`react-native-vision-camera`), geolokalizacji (`react-native-geolocation-service`) oraz lokalnego trybu offline (np. `WatermelonDB`).

**Największe ryzyko:** 
Zależność od bibliotek trzecich przy dostępie do sprzętu. Funkcje (aparat, GPS) bazują na zewnętrznych pakietach open-source. W perspektywie dwuletniego utrzymania istnieje ryzyko, że przestaną być one aktualizowane, a zespół webowy (bez znajomości Javy/Swifta) będzie miał trudności z naprawą natywnego kodu podczas aktualizacji systemów iOS/Android.

**Co mogłoby zmienić decyzję:** 
Zmienił(a)bym decyzję na **Flutter**, gdyby aplikacja miała opierać się na wysoce niestandardowym interfejsie pełnym złożonych animacji, który musi wyglądać w 100% identycznie na każdym urządzeniu (z pominięciem natywnych komponentów systemowych).