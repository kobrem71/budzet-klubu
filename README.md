# Budżet klubu — KOBREM 71 (dostęp na hasło)

Prosty dashboard z budżetem klubu, hostowany na GitHub Pages, **chroniony hasłem**.

## Jak działa ochrona

GitHub Pages jest zawsze publiczny, więc strony nie da się „schować" po stronie
serwera. Zamiast tego **cała strona jest zaszyfrowana hasłem (AES, StatiCrypt)**:

- Kto wejdzie na adres, widzi ekran z prośbą o hasło.
- Bez hasła treść to nieczytelny szyfr — nawet w podglądzie źródła strony
  nie widać ani salda, ani kwot, ani opisów.
- Zdjęcia faktur są **wtapiane w zaszyfrowaną stronę** (base64), więc nie da się
  ich otworzyć osobnym linkiem z pominięciem hasła.

### Co warto wiedzieć (uczciwie)

- To **jedno wspólne hasło** dla całego zarządu (nie osobne konta). Żeby odebrać
  komuś dostęp — zmieniamy hasło i rozsyłamy nowe.
- Bezpieczeństwo = siła hasła. Ustaw długie, nieoczywiste hasło (najlepiej frazę).
- W repozytorium leży **tylko zaszyfrowany `index.html`**. Plik źródłowy z jawnymi
  danymi (`index.source.html`) nigdy nie trafia do gita (jest w `.gitignore`).
- Jeśli kiedyś zechcesz osobne loginy dla każdego członka zarządu (z możliwością
  odbierania dostępu), to darmowa opcja Cloudflare Access — ale to już poza gitem.

## Zmiana hasła

```bash
npx staticrypt index.source.html -p "TWOJE-NOWE-HASLO" --short -d _enc --remember 30 \
  --template-title "Budżet klubu — KOBREM 71" \
  --template-instructions "Dostęp tylko dla zarządu. Podaj hasło, aby zobaczyć budżet." \
  --template-button "Wejdź" --template-placeholder "Hasło" \
  --template-error "Nieprawidłowe hasło — spróbuj ponownie." \
  --template-remember "Zapamiętaj mnie na tym urządzeniu (30 dni)" \
  --template-color-primary "#1c6a47" --template-color-secondary "#e8ece6"
mv _enc/index.source.html index.html && rm -rf _enc
```

Potem `git add index.html && git commit -m "zmiana hasla" && git push`.

## Dodanie faktury

Prześlij mi zdjęcie + opis + kwotę. Ja wtopię zdjęcie w stronę, zaktualizuję
saldo, ponownie zaszyfruję i oddam gotowy `index.html` do wypchnięcia.

## Publikacja na GitHub Pages

```bash
cd budzet-klubu
git remote add origin https://github.com/kobrem71/budzet-klubu.git
git push -u origin main
```

Następnie **Settings → Pages → Source: main / root**. Adres strony:
`https://kobrem71.github.io/budzet-klubu/`

## Pliki

```
budzet-klubu/
├── index.html          ← ZASZYFROWANA strona (to idzie do repo)
├── README.md
├── .gitignore
├── index.source.html   ← JAWNE źródło, lokalne, NIE w repo
└── .staticrypt.json    ← konfiguracja szyfrowania, lokalne, NIE w repo
```
