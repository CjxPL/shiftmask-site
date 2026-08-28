# shiftmask.com — kierunek projektowy

Strona została **przepisana od zera** 21.08.2026. Poprzednia wersja — jasna, oparta na siatkach zaokrąglonych kart — została odrzucona jako szablonowa. Ten dokument opisuje kierunek, który obowiązuje teraz.

---

## 1. Punkt odniesienia

Inspiracją była ciemna estetyka fintechowa (`finance.elementra.themerex.net`). Przeniesione zostały **zasady**, nie rozwiązania:

| Wzięte | Odrzucone jako niemożliwe albo nieuczciwe |
| --- | --- |
| Ciemna baza jako jedyny motyw | Logotypy partnerów — nie mamy partnerów |
| Ogromna typografia wyświetlająca | Opinie klientów — nie mamy klientów |
| Pełnoszerokościowe pasma koloru | Wymyślone statystyki firmy |
| Geometria i faktura w tle | Zdjęcia stockowe ludzi w biurze |
| Ruch przy scrollu | Wideo w tle |

## 2. Decyzje, które obowiązują

**Ciemny motyw jest jedyny.** Strona nie ma wariantu jasnego. Wszystkie kolory są malowane jawnie, więc trzyma się niezależnie od ustawień systemu. To świadoma decyzja, nie brak.

**Typografia niesie stronę.** Nagłówek pierwszego poziomu do 124 px, nagłówki sekcji do 72 px, oba w Chivo 900 z ciasnym trackingiem. Drugi wiersz nagłówka głównego jest **konturowy w kolorze Coral** — to najmocniejszy gest typograficzny na stronie i nie powtarza się nigdzie indziej.

**Jedno głośne miejsce.** Pełnoszerokościowe pasmo Coral z gigantycznym zerem („0 bajtów wysłanych na serwer"). To jedyna duża powierzchnia Coralu na całej stronie — świadome odstępstwo od zasady z księgi marki, wydane raz.

**Kompozycja pokazuje przesunięcie.** Trzy kroki metody są kolejno przesuwane w prawo. Nagłówki nie są wyśrodkowane. Sekcja „co przeżywa" ma przyklejony nagłówek po lewej i przewijające się wiersze po prawej.

**Faktura zamiast dekoracji.** Delikatna siatka arkusza kalkulacyjnego na całym tle, wygaszana maską radialną. Ciepła poświata Coral za obiektem transformacji. Para przesuniętych kwadratów wychodząca poza róg pasma.

**Ruch jest oszczędny.** Paski redakcji wjeżdżają raz przy wczytaniu, daty przeskakują na przesunięte. Sekcje pojawiają się przy scrollu. Wszystko wyłączone przy `prefers-reduced-motion`.

## 3. Kill list — nadal obowiązuje

```
- przyklejona nawigacja z backdrop-filter
- box-shadow jako domyślna powierzchnia
- siatka trzech kart pod nagłówkiem
- kafelki person
- powtarzany rytm: etykieta → nagłówek → akapit → siatka
- wyśrodkowane wszystko
- lorem ipsum, wymyśleni klienci, wymyślone liczby
```

## 4. Tokeny — wersja obowiązująca

```css
--void:#07090F;        /* tło strony */
--ink:#0E1320;         /* panele */
--surface:#141A28;     /* panel jaśniejszy */
--fog:#E6EAF3;         /* tekst główny, paski redakcji */
--muted:#8D96AD;       /* tekst drugorzędny */
--dim:#828CA6;         /* etykiety monospace — 5,9:1 na --void */
--rule:#222A3B;        /* kreski */
--rule-bright:#333D52;
--coral:#FF7B64;       /* Coral jako tekst na ciemnym */
--coral-solid:#FF5F45; /* wypełnienia, pasmo, kontur nagłówka */
--cobalt:#8FA3FF;      /* focus */
--verified:#3FCB98;    /* stan pozytywny */
```

Na paśmie Coral tekst wyłącznie w `--ink` (#0E1320).
`--dim` było wcześniej `#5E6880` i dawało 3,57:1 — za mało. Nie cofać.

## 5. Stan weryfikacji

Sprawdzone programowo przy 1440, 768 i 390 px:

- Brak poziomego przewijania strony na każdej z tych szerokości.
- Zero par tekst/tło poniżej WCAG AA (duży tekst liczony wg progu 3:1).
- Meta title 54 znaki, opis 147 znaków, JSON-LD parsuje się poprawnie.

Po każdej zmianie warto to powtórzyć — dwa błędy w tej wersji wynikły z kolizji nazw klas w CSS (`.bar` w nawigacji zderzone z `.bar` paska redakcji, `.band p` nadpisujące `.zero`), a takie rzeczy nie są widoczne w kodzie, tylko na zrzucie.

## 6. Czego nie wolno napisać

- Nie „ochrona", nie „zbroja", nie „shield". Produkt nie broni przed atakiem — sprawia, że nie ma czego atakować.
- Nie „gwarantuje zgodność z RODO". Wolno: „usuwa dane osobowe z kopii, którą udostępniasz".
- Nie „sandbox", nie „piaskownica".
- Statystyka o shadow AI to kontekst, nie groźba.
- Zero wymyślonych klientów, opinii i liczb.

## 7. Zostało do zrobienia

- Pięć znaczników `TODO` w `index.html`: link do pobrania (×2), płatność, prywatność, kontakt.
- Sekcja z ekranami aplikacji, kiedy interfejs będzie gotowy — dziś strona opisuje mechanizm, ale nie pokazuje produktu.
