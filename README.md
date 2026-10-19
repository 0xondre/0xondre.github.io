# Notatki techniczne

Prosty blog po polsku oparty na Jekyllu. GitHub Pages buduje stronę automatycznie z plików Markdown.

## Publikacja na GitHub Pages

1. Utwórz publiczne repozytorium `0xondre.github.io` na GitHubie.
2. Skopiuj zawartość tego folderu do głównego katalogu repozytorium i wypchnij ją na gałąź `main`.
3. W **Settings → Pages → Build and deployment** wybierz **Deploy from a branch**, gałąź `main` i folder **/(root)**.
4. Konfiguracja `_config.yml` jest już przygotowana dla adresu `https://0xondre.github.io`.

## Dodawanie wpisów

Dodaj plik `_posts/RRRR-MM-DD-tytul-wpisu.md`:

```markdown
---
title: "Tytuł wpisu"
description: "Jedno zdanie o treści wpisu."
date: 2026-10-19 10:00:00 +0200
tags: [Temat, Narzędzia]
read_time: 4
---

Treść wpisu w Markdown.
```

Data w nazwie pliku i polu `date` powinna być taka sama. GitHub Pages może ukryć wpisy z datą w przyszłości. Przykładowy artykuł znajduje się w `_posts/`; możesz go usunąć lub zastąpić własnym.

## Edycja wyglądu i treści

- Nazwa bloga, opis, adres: `_config.yml`.
- Strona główna: `index.html`.
- O blogu: `o-blogu.html`.
- Kolory, typografia i układ: `assets/style.css`.
- Szablon artykułu: `_layouts/post.html`.

## Podgląd lokalny

Jeśli masz Ruby i Bundler, uruchom:

```sh
bundle install
bundle exec jekyll serve
```

Otwórz adres podany przez Jekylla, zwykle `http://127.0.0.1:4000`. Przy `baseurl` ustawionym dla repozytorium projektu dodaj tę ścieżkę do adresu.
