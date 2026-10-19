---
title: "Co naprawdę robi cache HTTP?"
description: "Kilka nagłówków, które pomagają przeglądarce zdecydować, czy pobrać zasób ponownie."
date: 2026-10-19 10:00:00 +0200
tags: [HTTP, Web]
read_time: 5
---

Cache HTTP często kojarzy się z prostym przełącznikiem: zasób jest albo zapamiętany, albo nie. W praktyce przeglądarka podejmuje dwie osobne decyzje: **czy może użyć zapisanej odpowiedzi bez kontaktu z serwerem** oraz **czy może sprawdzić, czy ta odpowiedź nadal jest aktualna**.

## Świeża odpowiedź

Serwer może określić czas, przez który odpowiedź pozostaje świeża:

```http
Cache-Control: public, max-age=3600
```

`max-age=3600` oznacza godzinę świeżości. W tym czasie cache może obsłużyć kolejne żądanie bez ponownego pobierania odpowiedzi. Dyrektywa `public` pozwala przechowywać ją także współdzielonym cache’om, na przykład pośredniczącym między użytkownikiem a serwerem. Nie ustawiaj jej bez namysłu dla treści zależnych od zalogowanego użytkownika.

## Nieaktualna nie znaczy bezużyteczna

Po upływie czasu świeżości przeglądarka może zweryfikować zapisaną kopię. Służą do tego między innymi `ETag` i `Last-Modified`.

```http
ETag: "article-v3"
```

Przy następnym żądaniu klient może wysłać:

```http
If-None-Match: "article-v3"
```

Jeżeli zasób się nie zmienił, serwer odpowiada `304 Not Modified`. Nie przesyła wtedy pełnej treści odpowiedzi, a klient korzysta z zapisanej kopii. To nadal wymaga kontaktu z serwerem, lecz zwykle oszczędza transfer.

## Dwie praktyczne strategie

**Zasoby z hashem w nazwie**, na przykład `app.4f2a9c.js`, mogą mieć długi czas świeżości. Zmiana zawartości zmienia nazwę pliku, więc nowa wersja dostaje nowy adres.

**Dokument HTML** często wymaga krótszego czasu świeżości lub ponownej walidacji, aby wskazywał na aktualne zasoby. Warto sprawdzić rzeczywiste nagłówki odpowiedzi w zakładce Network narzędzi deweloperskich, zamiast zakładać, że cache działa tak samo dla każdego pliku.

> Dobra reguła: najpierw ustal, czy adres zasobu zmienia się wraz z jego treścią. Dopiero potem wybierz czas przechowywania.

Cache nie jest jednym mechanizmem. To zestaw zasad dotyczących świeżości, przechowywania i walidacji. Rozdzielenie tych pojęć ułatwia diagnozowanie sytuacji, w których użytkownik widzi starą wersję strony.
