# Budżet klubu — KOBREM 71

Prosty dashboard z budżetem klubu. Statyczna strona (jeden plik `index.html`),
działa lokalnie i na GitHub Pages, bez żadnej instalacji.

## Struktura

```
budzet-klubu/
├── index.html      ← cały dashboard + dane
├── faktury/        ← tu trafiają zdjęcia faktur
└── README.md
```

## Jak liczone są kwoty

- **Saldo na koncie** — realne pieniądze na koncie klubu (podane ręcznie).
- **Zaplanowane do zapłaty** — przyszłe wydatki (np. pensja trenera). Odejmowane od salda.
- **Prognozowane saldo** = saldo − zaplanowane do zapłaty.
- **Faktury** — rejestr wydatków ze zdjęciem. Domyślnie mają status „opłacony”
  (są już uwzględnione w saldzie), więc nie odejmują się drugi raz. Fakturę
  jeszcze nieopłaconą oznaczamy statusem `do_zaplaty` i wtedy wchodzi do prognozy.

## Jak dodać fakturę

1. Wrzuć zdjęcie do folderu `faktury/` (np. `2026-08-15-pilki.jpg`).
2. W `index.html`, w sekcji `const DANE`, dopisz wpis do listy `wydatki`:

```js
{ data:"2026-08-15", opis:"Piłki treningowe", kategoria:"Sprzęt",
  kwota:349.00, status:"oplacony", zdjecie:"2026-08-15-pilki.jpg" },
```

3. Zaktualizuj `saldo` i `aktualizacja` na górze `DANE`.

W praktyce wystarczy, że prześlesz mi zdjęcie + opis + kwotę — zrobię to za Ciebie
i oddam gotowe pliki do wgrania.

## Publikacja na GitHub Pages

```bash
cd budzet-klubu
git init
git add .
git commit -m "Budżet klubu — start"
git branch -M main
git remote add origin https://github.com/kobrem71/budzet-klubu.git
git push -u origin main
```

Następnie w repozytorium na GitHubie: **Settings → Pages → Source: `main` / `root`**.
Po chwili strona będzie pod adresem:

```
https://kobrem71.github.io/budzet-klubu/
```
