# Uruchomienie shiftmask.com — krok po kroku

Wszystko poniżej robi się raz. Licz około 30 minut plus czas na propagację DNS.

---

## 1. Repozytorium na GitHubie

Zalecam założyć **organizację** o nazwie `shiftmask` (darmowa), a nie zwykłe repo na koncie prywatnym. Dwa powody: blokujesz nazwę na GitHubie zanim zrobi to ktoś inny, a adresy wyglądają wtedy jak `github.com/shiftmask/…` zamiast `github.com/twojlogin/…`, co przy sprzedaży narzędzia deweloperskiego robi różnicę.

1. `github.com/organizations/plan` → wybierz **Free** → nazwa organizacji: `shiftmask`.
2. W organizacji utwórz repozytorium **publiczne** o nazwie `shiftmask.github.io`.
   Publiczne, bo GitHub Pages dla kont darmowych działa tylko w repozytoriach publicznych.
3. Repozytorium na samą aplikację nazwij później po prostu `shiftmask` — nie mieszaj kodu produktu ze stroną.

Jeśli wolisz zostać na koncie prywatnym: utwórz repo `shiftmask-web`, reszta instrukcji jest identyczna, tylko w punkcie 4 wpiszesz `twojlogin.github.io` zamiast `shiftmask.github.io`.

## 2. Wypchnięcie plików

Rozpakuj paczkę, wejdź do katalogu i:

```bash
git init
git add .
git commit -m "Landing page"
git branch -M main
git remote add origin git@github.com:shiftmask/shiftmask.github.io.git
git push -u origin main
```

Plik `CNAME` już zawiera `shiftmask.com` — nie usuwaj go, GitHub czyta z niego domenę.

## 3. Włączenie GitHub Pages

W repozytorium: **Settings → Pages**.

- Source: **Deploy from a branch**
- Branch: `main`, katalog `/ (root)` → **Save**

Po minucie strona działa pod `shiftmask.github.io`. Custom domain podepniesz po ustawieniu DNS.

## 4. DNS w az.pl

Twoje nameservery to `ns6/ns7/ns8.az.pl`, więc rekordy ustawiasz w panelu az.pl (Domeny → shiftmask.com → Edycja DNS).

**Cztery rekordy A dla domeny głównej** (host pusty albo `@`):

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**Cztery rekordy AAAA** (opcjonalne, ale warto — IPv6):

```
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```

**Jeden CNAME dla `www`:**

```
www  →  shiftmask.github.io.
```

Kropka na końcu jest istotna, jeśli panel jej nie dokleja sam.

Usuń wszystkie rekordy A i CNAME, które az.pl założył domyślnie na stronę parkingową — inaczej będą walczyć z Twoimi.

## 5. Domena i HTTPS w GitHubie

Wróć do **Settings → Pages**:

1. **Custom domain**: `shiftmask.com` → Save. GitHub sprawdzi DNS; przy świeżych rekordach może przez chwilę pokazywać błąd — poczekaj i odśwież.
2. Gdy pojawi się zielony komunikat, zaznacz **Enforce HTTPS**. Certyfikat Let's Encrypt wystawia się automatycznie, ale opcja bywa dostępna dopiero po kilku godzinach, maksymalnie po dobie.

Nie ogłaszaj strony, dopóki HTTPS nie jest wymuszony.

## 6. Przekierowanie z .eu na .com

GitHub Pages obsługuje tylko jedną domenę na repozytorium, więc przekierowania nie zrobisz po jego stronie. Najczystsze rozwiązanie to Cloudflare — darmowe, z certyfikatem i prawdziwym kodem 301.

1. Załóż konto na Cloudflare i dodaj **tylko** `shiftmask.eu` (nie ruszaj `.com`).
2. Cloudflare da Ci dwa swoje nameservery — wpisz je w az.pl dla domeny `.eu`.
3. W Cloudflare: **Rules → Redirect Rules → Create rule**
   - Nazwa: `eu to com`
   - When: `Hostname` `equals` `shiftmask.eu` (dodaj drugi warunek OR dla `www.shiftmask.eu`)
   - Then: **Dynamic redirect**, wyrażenie: `concat("https://shiftmask.com", http.request.uri.path)`
   - Status: **301**, zaznacz **Preserve query string**
4. W **SSL/TLS** ustaw tryb **Full**.

Alternatywa bez Cloudflare: az.pl ma w panelu „przekierowanie domeny". Zadziała, ale sprawdź dwie rzeczy — czy przekierowanie jest **301**, a nie 302, i czy obsługuje HTTPS. Jeśli któregoś brakuje, wróć do Cloudflare.

## 7. Po uruchomieniu

- **Google Search Console**: dodaj `https://shiftmask.com`, potwierdź własność rekordem TXT w az.pl, wyślij `sitemap.xml`. Nie dodawaj `.eu` jako osobnej właściwości — ma tylko przekierowywać.
- **Bing Webmaster Tools**: zaimportuj z Search Console jednym kliknięciem. Warto, bo z indeksu Binga korzysta ChatGPT Search.
- **Sprawdź kartę społecznościową**: wklej adres w podgląd linków na LinkedInie albo w dowolny debugger OG. Powinien pojawić się `og.png`.
- **Uzupełnij cztery TODO** z README, zanim wrzucisz link gdziekolwiek.

## 8. Weryfikacja, że wszystko gra

```bash
curl -sI https://shiftmask.com            # oczekiwane: HTTP/2 200
curl -sI http://shiftmask.com             # oczekiwane: 301 na https
curl -sI https://www.shiftmask.com        # oczekiwane: 301 na apex
curl -sI https://shiftmask.eu             # oczekiwane: 301 na https://shiftmask.com
```

Jeśli któryś zwróci 404 z GitHuba, sprawdź czy plik `CNAME` faktycznie jest w repozytorium — najczęstsza przyczyna.
