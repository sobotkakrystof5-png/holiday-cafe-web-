# Holiday CAFE — web

Jednostránkový web kavárny Holiday CAFE (Dolní Bousov). Jeden statický `index.html`, Tailwind CDN, vanilla JS — bez build kroku. Pravidla projektu viz `Claude.md`.

Nasazeno na Vercelu (projekt `holiday-cafe`).

## SEO TODO — akce mimo kód (pro klienta / správce)

### 1. Doména (blokuje vše ostatní!)
- [ ] `holidaycafe.cz` dnes míří na **starý hosting** (185.82.212.80, starý web, jen HTTP bez SSL). Nový web běží zatím jen na `holiday-cafe.vercel.app`.
- [ ] Ve Vercelu přidat domény `holidaycafe.cz` **i** `www.holidaycafe.cz` (Project → Settings → Domains) a u registrátora (Gransy / subreg) přesměrovat DNS: apex `A 76.76.21.21`, `www` `CNAME cname.vercel-dns.com` (přesné hodnoty ukáže Vercel).
- [ ] Canonical, sitemap i JSON-LD používají `https://www.holidaycafe.cz/` — Vercel nastavit tak, aby apex přesměrovával na www (301).

### 2. Google Search Console
- [ ] Ověřit vlastnictví domény (DNS TXT záznam) na https://search.google.com/search-console
- [ ] Odeslat `sitemap.xml`.

### 3. Seznam.cz Webmaster (klíčové pro český trh)
- [ ] Zaregistrovat web na https://reporter.seznam.cz (Seznam Webmaster) — jde o **jiný nástroj než Google Search Console**, bez něj Seznam web indexuje pomalu/neúplně.
- [ ] Ověřit, že zápis na Firmy.cz (https://www.firmy.cz/detail/13264481-holiday-cafe-dolni-bousov.html) odkazuje na novou URL webu.

### 4. Google Business Profile
- [ ] Převzít/založit profil na https://business.google.com — název **Holiday CAFE**, adresa **nám. T. G. Masaryka 270, 294 04 Dolní Bousov**, telefon **+420 733 666 194** (přesně v tomto formátu, stejně jako na webu a Firmy.cz — NAP shoda).
- [ ] Doplnit otevírací dobu Út–Ne 11:30–17:30, Po zavřeno; nahrát fotky; přidat odkaz na web.
- [ ] Průběžně sbírat recenze i na Googlu (web na ně již odkazuje).

### 5. Po nasazení zkontrolovat
- [ ] https://search.google.com/test/rich-results — validace JSON-LD (kavárna, menu, FAQ, drobečky).
- [ ] https://developers.facebook.com/tools/debug/ — náhled sdílení (og-image).
- [ ] https://pagespeed.web.dev — Core Web Vitals (LCP by mělo být zelené díky WebP + preload hero).
