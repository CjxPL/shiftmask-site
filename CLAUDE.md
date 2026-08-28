# ShiftMask — kontekst projektu

Repozytorium strony marketingowej `shiftmask.com`. Statyczny HTML na GitHub Pages, bez frameworka i bez build stepu.

**Przed jakąkolwiek pracą nad designem przeczytaj `DESIGN-BRIEF.md`.** Opisuje obowiązujący kierunek wizualny, tokeny i kill listę. Strona została przepisana od zera 21.08.2026 na ciemną, typograficzną kompozycję — `index.html` jest teraz wzorcem, nie materiałem do poprawy.

## Produkt

ShiftMask to aplikacja desktopowa (na start: Windows; macOS to ewentualny drugi etap), która buduje bezpieczną **lokalną** kopię danych z Excela i CSV (SQL jako źródło i eksport do DuckDB to Faza 1 / Pro): wykrywa relacje między tabelami, przesuwa wszystkie daty o jeden wspólny offset i maskuje wartości deterministycznie. Kopię można oddać ChatGPT, Claude'owi czy Gemini, odebrać kod raportu lub aplikacji i offline podmienić dane na prawdziwe. Prawdziwe rekordy nigdy nie opuszczają komputera. Silnik lokalny: DuckDB.

Model cenowy: **Core License — 39 USD jednorazowo, na urządzenie, dożywotnio (cena founderska dla pierwszych 150 licencji; docelowo 59–69 USD).** Rok aktualizacji w cenie, odnowienie opcjonalne za 60% ceny zakupu. Bez subskrypcji na tym poziomie, świadomie. *(Zmienione 2026-08-28 — poprzedni model "72h/49 USD" jawnie odrzucony, patrz claude.ai Project "APP: ShiftMask" → pricing-strategy.md.)*

## Słownik

| Termin | Znaczenie w tym projekcie |
| --- | --- |
| **date shifting** | Przesunięcie wszystkich dat o ten sam offset, żeby odstępy między zdarzeniami zostały nienaruszone |
| **referential integrity** | Klucze maskowane spójnie między tabelami, więc joiny nadal działają |
| **time intelligence** | Miary czasowe w Power BI (YTD, YoY, średnie kroczące), które psuje losowa podmiana dat |
| **Core License** | Dożywotnia licencja na urządzenie za 39 USD (cena founderska), z rokiem aktualizacji w cenie |
| **Vault Ink / Coral / Cobalt** | Kolory marki, patrz sekcja 5 briefu |

## Twarde ograniczenia

- Jeden plik `index.html`, cały CSS inline. Google Fonts to jedyny dozwolony zewnętrzny host.
- Strona jest **wyłącznie ciemna**, bez wariantu jasnego. Wszystkie kolory malowane jawnie. Musi przechodzić WCAG AA — obecna wersja przechodzi przy 1440, 768 i 390 px, nie regresować.
- `CNAME` zawiera `shiftmask.com` i nie wolno go usuwać.
- Zero fałszywego dowodu społecznego: żadnych klientów, opinii, liczb pobrań ani logotypów, dopóki nie są prawdziwe.
- Pięć `TODO` w `index.html` (link do pobrania ×2, płatność, prywatność, kontakt) czeka na prawdziwe adresy.
- Uwaga na kolizje nazw klas w CSS — dwa błędy w tej wersji wzięły się dokładnie stąd. Po zmianach zrób zrzut ekranu, nie ufaj samemu kodowi.

## Głos

Deweloperowi BI mów mechanizmem — konkretnie, nazywając rzeczy po imieniu. Menedżerowi mów konsekwencją — jedno zdanie, zero żargonu. Ta sama prawda na dwóch poziomach szczegółu, nigdy dwie różne obietnice.

Zakazane: „ochrona", „zbroja", „shield", „sandbox", „piaskownica", „gwarantuje zgodność z RODO", sprzedaż strachem.

## Decyzje, które już zapadły

Nie otwieraj ich ponownie bez wyraźnej prośby:

- **Nazwa: ShiftMask.** Wybrana po audycie nazewniczym — `Sanitiz`, `DataSandbox` i `DataArmor` odpadły przez kolizje rynkowe i zajęte domeny.
- **Domeny:** `shiftmask.com` jest kanoniczna, `shiftmask.eu` przekierowuje na nią przez 301.
- **Meta title:** `ShiftMask — Anonymize Excel & SQL Data Before Using AI` (54 znaki). Nie skracać ani nie „ulepszać" bez powodu SEO.
- **Strategia pozyskania:** budżet 0 USD, wyłącznie organiczny SEO/SGE, Reddit i LinkedIn. Docelowe frazy to długi ogon pytaniowy, nie „data masking".
