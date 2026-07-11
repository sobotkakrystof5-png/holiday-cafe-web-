# CLAUDE.md — Holiday CAFE (Dolní Bousov)

Projektový dokument pro vývoj jednostránkového webu kavárny **Holiday CAFE**. Tento soubor slouží jako jediný zdroj pravdy pro Claude (i lidské vývojáře) při generování, úpravách a rozšiřování webu. Vždy se jím řiď — má přednost před obecnými zvyklostmi.

---

## 1. O projektu

- **Klient:** Holiday CAFE, malá kavárna na rohu náměstí v Dolním Bousově (brána do Českého ráje).
- **Cíl:** Jednostránkový (one-page) prezentační web — teplý, lidský, lokální. Návštěvník má mít pocit „mini dovolené" od každodenního stresu.
- **Cílové publikum:** Místní, rodiny s dětmi, senioři, cyklisté, turisté a pejskaři — velká část přístupů bude z mobilu.

### Jádro značky a inkluze (KRITICKÉ pravidlo)
Kavárna zaměstnává lidi s handicapem. **Toto se na webu explicitně zmíní** — vřele, přirozeně a bez patosu. Není to PR tah, je to součást identity podniku. Správná slova: „lidé s handicapem", „naši lidé", „parta, která to myslí vážně". Zakázána jsou korporátní klišé jako „sociální odpovědnost", „dáváme šanci", „pomáháme", „chráněná dílna". Inkluze se komunikuje jako samozřejmost — s hrdostí, ne s lítostí.

---

## 2. Tón a jazyk (Tone of Voice)

- **Jazyk:** Čeština, 1. osoba množného čísla („my" — „vaříme", „těšíme se na vás").
- **Charakter:** Vřelý, lidský, autentický, lokální. Jako by mluvil kamarád, ne firma.
- **Zakázáno:** Korporátní fráze, marketingové buzzwordy, anglicismy bez důvodu, superlativní klišé („nejlepší zážitek", „prémiová kvalita", „unikátní koncept").
- **Povoleno a žádoucí:** Konkrétnost, drobné lidské detaily, humor s mírou, dovolenková/přímořská metaforika („zastavte se jako na dovolené").

---

## 3. Vizuální identita a design systém

### Barvy
| Použití | Hodnota | Poznámka |
|---|---|---|
| Bílé sekce — pozadí | `#FFFFFF` | |
| Hnědé sekce — pozadí | `#4A3525` (alt. `#5C4033`) | teplá kávová hnědá, definovat jako Tailwind custom color `cafe-brown` |
| Text na bílé | tmavý charcoal/černá (např. `#1F1B16`) | vysoký kontrast |
| Text na hnědé | krémová/slonovinová `#FDFBF7` | definovat jako `cafe-cream` |

**Pravidlo střídání:** Sekce se **striktně střídají** bílá ↔ hnědá v tomto pořadí:
Navbar (hnědá) → Hero (bílá) → O nás (hnědá) → Menu (bílá) → Naše parta (hnědá) → Kde nás najdete (bílá) → Footer (hnědá).

**KRITICKÉ pravidlo — Navbar:** `<header>` musí mít vždy pevně hnědé pozadí `#4A3525` bez ohledu na to, která sekce je pod ním při scrollu. **Nikdy nepoužívej opacity modifikátor** (`bg-cafe-brown/96` apod.) ani `backdrop-blur` — Tailwind CDN tyto kombinace s custom hex barvami neřeší spolehlivě. Správná implementace: CSS pravidlo `header { background-color: #4A3525 !important; }` + inline `style="background-color: #4A3525;"` na `<header>` elementu. Text nav-linků musí být vždy světlý (krémová `#EAE0D2` nebo bílá `#FDFBF7`) — nepoužívej opacity modifikátory na barvách textu v Tailwindu CDN.

### Styl
- Čistý, útulný, „high-end but accessible" — kavárenský, ne korporátní.
- Jemné přímořské/dovolenkové akcenty (inspirace logem: černobílá palma rostoucí z kokosu/šálku kávy). Akcenty decentně — ikonky, dekorace, ne kýč.
- Zaoblené rohy, měkké stíny, dostatek vzduchu (whitespace).
- Kontrast textu musí vždy splňovat čitelnost (cíl: WCAG AA).

### Obrázky (dočasné placeholdery)
Reálné fotky zatím nejsou. Používej:
- elegantní sémantické SVG placeholdery, **nebo**
- pečlivě stylované Unsplash bloky (`https://images.unsplash.com/...`) s kávovou/kavárenskou estetikou.
Vše připravit tak, aby šlo později snadno nahradit reálnými fotkami (jasné `alt` texty, jednotné poměry stran).

---

## 4. Technický stack a pravidla

- **Jeden soubor:** validní HTML5, vše v jednom `index.html`.
- **CSS:** Tailwind CSS přes CDN (standardní třídy; custom barvy přes `tailwind.config` inline skript).
- **JS:** Pouze Vanilla JavaScript. **Žádné externí UI knihovny** kromě Tailwindu (žádný jQuery, Alpine, Bootstrap…).
- **Responzivita:** Mobile-first. Mobilní UX má nejvyšší prioritu.
- **Sémantika a SEO:** `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`, správná hierarchie nadpisů (jeden `<h1>`), meta description, `lang="cs"`, Open Graph základ.
- **Scroll:** `scroll-behavior: smooth` (CSS) + kotvy na sekce.
- **Kvalita kódu:** Production-ready, čistě odsazené, komentované bloky sekcí, připravené na pozdější výměnu obsahu.

### Vanilla JS musí obsluhovat
1. **Mobilní hamburger menu** — otevření/zavření s plynulou animací, zavření po kliku na odkaz.
2. **Plynulý scroll** na kotvy.
3. **ScrollSpy** — dynamické zvýraznění aktivního odkazu v navigaci podle pozice scrollu.

---

## 5. Struktura stránky a obsah

### [NAVBAR] — hnědá
- Vlevo: logo placeholder + text „Holiday CAFE" (koncept loga: černobílá palma z kokosu/šálku).
- Vpravo (desktop): odkazy **O nás, Menu, Naše parta, Kde nás najdete, Kontakt**.
- Mobil: funkční čisté hamburger menu (Vanilla JS).
- Navbar fixní/sticky, dobře čitelný i při scrollu.

### [HERO] — bílá
- Titulek: **Holiday CAFE**
- Slogan: **„Zastavte se na chvíli. Jako na dovolené."**
- CTA tlačítko (hnědá/krémová) → `#kde-nas-najdete` nebo `#menu`.
- Úvodní text (použít doslova):
  > „Jsme malá kavárna na rohu bousovského náměstí. Vařit kafe nás baví a budeme rádi, když se u nás zastavíte – ať jdete kolem pěšky, na kole, s kočárkem nebo se psem."

### [O NÁS & PŘÍBĚH] — hnědá
- Vysvětlení filozofie „Holiday": místo, kde se čas zpomalí, vše připravujeme s úsměvem a láskou, vítán je každý (rodiny, senioři, cyklisté, psi).
- **Badge/karty (Tailwind, ikonky):**
  - 🚲 Certifikace **„Cyklisté vítáni"**
  - 🐕 **Dog-friendly**
  - 👨‍👩‍👧 **Family-friendly** (dětský koutek)

### [MENU — CO NABÍZÍME] — bílá
Čistý grid / moderní „café board". Položky s krátkým, chutným popisem:
- Výběrová káva (**Nordbeans** — espresso & Chemex filtr)
- Kvalitní sypané čaje
- Domácí dorty a dezerty
- Vyhlášená točená zmrzlina
- Domácí vafle & poháry
- Domácí limonády
- Zapečené bagety
- Doplňující věta: **„Vše si u nás můžete vzít také s sebou."**

### [NAŠE PARTA] — hnědá *(klíčová emoční sekce)*
- Titulek: **„Naše parta"** nebo **„Kdo se o vás postará"**.
- Grid karet členů týmu. Každá karta:
  - placeholder pro osobní fotku (zaoblené rohy),
  - jméno + role,
  - přátelské bio o 3 větách (odkud je, koníčky, oblíbená položka z menu).
- Zatím **3 realistické ukázkové profily** (smyšlené, ale uvěřitelné a lidské).
- Pod kartami širší placeholder pro **společnou fotku celého týmu**.
- Tón: osobní, kamarádský, nulový korporát. V bio členů týmu lze přirozeně zmínit handicap — pokud to dává smysl pro daný profil, vřele a bez patosu (viz sekce 1).

### [KDE NÁS NAJDETE & KONTAKT] — bílá
Dvousloupcový layout (informace × mapa/otevírací doba):
- **Adresa:** nám. T. G. Masaryka 270, 294 04 Dolní Bousov — zdůraznit rohovou polohu a „bránu do Českého ráje".
- **Otevírací doba:** Úterý–Neděle 11:30–17:30, Pondělí zavřeno. *(Aktualizováno 7/2026 dle reálného provozu — dřívější verze uváděla neděli zavřeno.)*
- **Vybavení:** prostorná venkovní zahrádka, Wi-Fi zdarma, platba kartou i QR.
- **Kontakty:** Tel. **+420 733 666 194**, e-mail **jaroslavajakubcova@email.cz**, odkaz na FB (Holiday CAFE).
- **Hodnocení:** decentní badge **4,9/5 na Firmy.cz** (chválí kávu, útulnou atmosféru a ochotný personál).
- **Mapa:** stylovaný Google Maps iframe placeholder nebo interaktivní prvek.

### [FOOTER] — hnědá, menší písmo
- Holiday CAFE © 2026. Všechna práva vyhrazena.
- **IČO: 08064237**
- Rychlé odkazy / odkaz „zpět nahoru".

---

## 6. Kontrolní checklist před odevzdáním

- [ ] Jediný HTML soubor, validní HTML5, `lang="cs"`.
- [ ] Striktní střídání bílá ↔ hnědá dle pořadí sekcí.
- [ ] Kontrast textu OK na obou pozadích (charcoal na bílé, `#FDFBF7` na hnědé).
- [ ] Mobile-first, hamburger menu funkční (otevřít/zavřít/zavřít po kliku).
- [ ] Smooth scroll + funkční ScrollSpy.
- [ ] Zmínka o lidech s handicapem je na webu přítomna — vřelá, přirozená, bez patosu ani korporátní rétoriky.
- [ ] Texty česky, v 1. os. mn. č., bez korporátních frází.
- [ ] Všechny kontaktní údaje, otevírací doba a IČO přesně dle sekce 5.
- [ ] Placeholdery snadno nahraditelné reálnými fotkami (alt texty, jednotné rozměry).
- [ ] Kód čistě odsazený, sekce komentované, bez externích knihoven mimo Tailwind CDN.

### SEO checklist (doplněno 7/2026)

- [ ] `meta description` 150–160 znaků s frázemi „kavárna Dolní Bousov", „Český ráj", „chráněná kavárna", „zmrzlina".
- [ ] `<link rel="canonical">`, `meta robots` (`index, follow, max-image-preview:large`), `theme-color`, geo tagy (`geo.region CZ-20`, `geo.placename`, `geo.position`).
- [ ] Open Graph i Twitter Card kompletní; `og:image` a `twitter:image` s **absolutní** URL (`assets/images/og-image.jpg`, 1200×630).
- [ ] JSON-LD: `CafeOrCoffeeShop` (sameAs, aggregateRating s reviewCount, hasMenu, openingHoursSpecification vč. explicitně zavřeného pondělí `00:00–00:00`), `Menu`, `BreadcrumbList`, `FAQPage`, `WebSite`.
- [ ] Všechny fotky ve WebP < 200 KB; `width`/`height` na každém `<img>`; `loading="lazy"` mimo hero; hero má `fetchpriority="high"` + `<link rel="preload">` + `srcset`.
- [ ] `robots.txt`, `sitemap.xml` a `manifest.json` v rootu; `apple-touch-icon.png` + ikony 192/512 v `assets/icons/`.
- [ ] NAP (název, adresa, telefon) identické na webu, Firmy.cz a Google Business Profile.
- [ ] Slovní spojení „chráněná dílna" smí být jen v meta datech / JSON-LD `keywords` (vyhledávaný termín) — **nikdy v textu stránky** (viz sekce 1).
- [ ] Interní kotvy (`#menu`, `#o-nas`, `#kde-nas-najdete`, `#nase-parta`…) existují a jsou unikátní.

## 7. Jak pracovat s tímto projektem (instrukce pro Claude)

- Při jakékoli úpravě webu zachovej barevné střídání sekcí, tón textů a pravidlo komunikace inkluze (viz sekce 1).
- Nové texty piš vždy česky, vřele a konkrétně; před přidáním copy zkontroluj zákazy ze sekce 2.
- Při výměně placeholderů za reálné fotky zachovej poměry stran a doplň smysluplné `alt` popisky.
- Nepřidávej závislosti ani build krok — projekt musí zůstat jeden statický HTML soubor.
- **Navbar je vždy hnědá** — viz kritické pravidlo v sekci 3. Nikdy neupravuj barvu `<header>` přes Tailwind opacity modifikátory; vždy použij CSS `header { background-color: #4A3525 !important; }` v `<style>` bloku.