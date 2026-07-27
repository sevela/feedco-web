# feedco.cz — pravidla pro práci v tomhle repu

Statický web, žádný build. Hostuje GitHub Pages z branch `main`, root. Doména je v `CNAME`.

Feedco = modulární e-commerce konektor pro Helios Inuvio. Samostatný web (spoke),
prolinkovaný s [jakubsevela.cz](https://jakubsevela.cz), nikoli pod ním.

## Stav

Web odešel z Carrdu na GitHub Pages a **je přestylovaný podle grafického manuálu**
(dark-first paleta, limetkový akcent, Lora + DM Sans + DM Mono, tónovaná tlačítka,
radius 8/12, kontejner `--content-max`, fonty self-hostované). Naposledy sjednoceno
s manuálem **v1.6** (26. 7. 2026): hero má jednotnou stavbu z hubu (chip label, velké H1,
dvě CTA, ~84vh) a tarify jsou tři price-cards podle sekce 09 manuálu.
Tokeny se berou z `/brand/tokens.css`, žádné hexy natvrdo.

**Texty jsou z původní Carrd stránky** s dvěma výjimkami: wordmark `FEEDCO` → `feedco.`
podle pravidla z manuálu a **hero text nový od Jakuba (26. 7. 2026)** — label „Integrace
pro Helios Inuvio", H1 „Propojte Helios se světem e-commerce", nový perex; meta a og
description s ním sjednocené. Obsahová revize zbytku stránky (strukura, argumentace,
ceny) je samostatný krok, který ještě nenastal.

Pořadí dotahování webů je hub → feedco → ethel.

## Vizuální systém

Tokeny jsou v **`/brand/tokens.css`**. Kompletní manuál v tomhle repu **není** —
žije na jednom místě: <https://jakubsevela.cz/brand/> (zdroj `sevela/jakubsevela-web`, `brand/index.html`).
Tady je jen `tokens.css`, protože ho web reálně načítá.
Nikdy nepiš hexy natvrdo — `index.html` už je na tokenech postavený.

- **Dark-first.** Pozadí `--bg` / `--bg-alt`, karty `--card`.
- **Accent = limetková `#9ed455`.** Barva jen v akcentech (tečka, CTA, odkazy, ikony stavu),
  nikdy jako plocha na pozadí.
- **Buttony tónované:** 12 % podklad + 35 % border, text v light odstínu. Hover 18 % / 50 %.
  Plné barevné plochy jsou zakázané.
- **Typografie:** Lora (nadpisy) / DM Sans (text a UI) / DM Mono (detaily) /
  Space Grotesk **jen** pro wordmark a monogram.
- **Wordmark:** `feedco<span class="dot">.</span>` — tečka na konci, bold 700,
  `font-size: 1.25em`. Monogram pro čtvercové formáty: `f.`
- **Radius:** tlačítka 8 px, karty 12 px.
- **Kontrast:** text na tónované ploše vždy v `--accent-l`. `--text-2` nepoužívat pod 14 px.

### Sdílená patička

Blok `<footer>` je označený komentářem a má být **shodný na všech třech webech**. Mění se
jen wordmark, věta pod ním, prolinky na zbylé dva weby a disclaimer. Struktura, CSS,
kontaktní blok (e-mail na dané doméně, +420 774 267 301, LinkedIn) a právní blok
(Mgr. Jakub Ševela, Lidická 700/19, 602 00 Brno, IČ, DIČ) jsou stejné.
Když patičku měníš, propiš to do `jakubsevela-web` a `ethel-web`.

**Wordmark patří do vlastního pásu nad sloupci, ne do prvního sloupce.** Když stál jako
první prvek jednoho sloupce, jeho velikost a `line-height` rozhodily horní hranu proti
ostatním sloupcům a patička vypadala rozsypaně. Všechny tři sloupce pod ním začínají
textem **stejné velikosti a line-heightu** (15 px / 1.5) — tagline i první odkaz v obou
seznamech. Když sem přidáváš sloupec, drž tuhle metriku, jinak se to rozjede znovu.
Mono label nad sloupcem byl další takový rozdíl a proto zmizel; e-mail a telefon
nadpis „Kontakt" nepotřebují.

**Prolinky nemají zastřešující nadpis.** Osobní web a produktový web nepatří pod jednu
hlavičku, protože k Feedcu mají různý vztah — proto každý odkaz nese vlastní jednořádkový
popis, co to je. Zkoušeli jsme „Další weby" (mdlé) i „Od stejného autora" (spojuje
nespojitelné) a obojí zahodili. Odkazy odděluje vlasová linka vlevo, která na hover
zezelená.

Ikony v patičce (LinkedIn) jsou **monochromatické** — `fill: currentColor`, takže dědí
barvu textu i hover. Značkové barvy třetích stran do palety nepatří.

Odkaz na `docs.feedco.cz` byl v patičce zkoušený a zahozený.

**Newsletter v patičce zatím není.** Podle roadmapy nemá platformu ani frekvenci a hub
kvůli tomu záměrně nemá signup. Odkaz na neexistující odběr je horší než žádný. Až
newsletter vznikne, přidat sem i na ostatní dva weby.

Kontaktní e-mail se řídí doménou webu: `kontakt@feedco.cz` zde, na ethel.cz `info@ethel.cz`.
Telefon a LinkedIn jsou společné.

### Wordmark v hlavičce

Wordmark je **jen v hlavičce**, ne v heru — H1 je propozice stránky, ne logo.
Pozor na specificitu: `.topnav ul a` (ne `.topnav a`), jinak mono a uppercase styl
navigačních odkazů přebije wordmark a ten se vykreslí velkými písmeny v DM Mono.

### Když měníš tokeny

`brand/tokens.css` je shodný ve všech třech repech (`jakubsevela-web`, `feedco-web`,
`ethel-web`) — mění se jen accent blok. Změnu **propiš do ostatních dvou** a do manuálu
v `jakubsevela-web/brand/index.html`, který je jediná verze.

## Ceny — kalkulačka (od 27. 7. 2026)

Statické tarify z Carrdu (LITE 490 / BASIC 2 490 / PROFI 4 490) jsou **nahrazené
interaktivní kalkulačkou** v sekci `#tarify` (v navigaci „Ceník"). Ceny nese modulární
model: 5 modulů (E-shop konektor, Feed konektor, Přijaté objednávky, Vydané objednávky,
Feedco API) × tarify Start/Standard/Profi, jednotný příplatek 990 Kč/měs (další e-shop /
+5 feedů / další API dodavatel), sleva za kombinaci (2 moduly −10 %, 3+ −15 %)
a jednorázové nasazení (u Profi a Feedco API „od"). Data a přepočty žijí v `index.html`
ve skriptu s `const MODULES` — kalkulačku dodal Jakub, ceny se mění jen tam.
CTA souhrnu předvyplní sestavu do kontaktního formuláře (`#kf-message`) — lead jde
přes `web-lead` do DB, žádné mailto. Cenová rozhodnutí dál patří do projektu Feedco;
tady se řeší jen jejich podání.

## Texty

Česky, vykaná forma. Konkrétnost před přísliby — jména klientů, čísla, měřitelné výsledky.
Reference na webu: VERKON, Younger Optics Europe, MIRA MAR, ZLKL.
Disclaimer „není produktem Asseco Solutions" na produktovém webu zůstává.

## Co nedělat

- Nepřidávat build krok ani závislosti, dokud to nepůjde jinak.
- Nepřidávat PHP ani nic serverového — Pages umí jen statické soubory.
  Formulář jde přes Supabase edge funkci (viz níže), ne přes vlastní backend.
- Neměnit `CNAME`, nemazat `.nojekyll`.
- Nepoužívat `localStorage`/`sessionStorage`.

## Známý technický dluh

- Barva `#ff9999` z originálu (u „bez Feedca") v paletě není. Nahrazena `--text-3`, takže
  kontrast mezi „bez Feedca" (utlumené) a „s Feedcem" (akcent) drží bez cizí barvy.
- Vypuštěno z Carrdu jako neslučitelné s manuálem: mintový geometrický podklad na celé
  stránce (barva jako plocha), šachovnicový vzor v kartách, vlnkové oddělovače,
  pilulková tlačítka s 3px borderem.
- Navigace je teď sticky (v Carrdu nebyla) — stejně jako na hubu.
- Texty čekají na obsahovou revizi; zatím jsou to Carrd verze.
- **Kontaktní formulář (vyřešeno 26. 7. 2026):** Carrd ho obsluhoval na svojí straně
  (AJAX na `/post/contact`), replika mezitím jela přes sdílený Formspree endpoint
  hubu (`xkgnqpnz`). Teď posílá `POST` na vlastní Supabase edge funkci `web-lead`
  v projektu `ClientDB4AI` (`https://gygwfcattcunbikootbx.supabase.co/functions/v1/web-lead`) —
  ověří honeypot (`input[name="mail"]`, zachovaný z originálu) a rate limit (3× / 10 min
  na IP), uloží lead do `public.web_leads` (sloupec `site` pro budoucí sdílení
  s jakubsevela.cz / ethel.cz) a přes Resend pošle notifikaci na `kontakt@feedco.cz`
  i automatickou odpověď odesílateli. Odpovídá 303 redirectem zpět na
  `feedco.cz/?odeslano=1#kontakt` (nebo `?chyba=1` / `?chyba=limit`), inline skript
  v patičce `index.html` podle toho zobrazí `#kontakt-status` a schová formulář.
  Odesílací doména `feedco.cz` čeká na verifikaci u Resendu (DKIM/SPF DNS záznamy
  přidané do zóny na Webglobe) — dokud neproběhne, e-maily se neodešlou, ale lead
  se do DB uloží vždy.
- **Google Ads konverze `AW-986763051` z originálu nebyla přenesena** — v Carrdu byla
  vložená *před* definicí `gtag()`, takže vyhazovala chybu a nikdy nefungovala. GA4
  (`G-ZK1160VT0P`) přenesené je a funguje. Jestli má konverze fungovat, musí se vložit
  až za GA4 snippet a navázat na odeslání formuláře, ne na načtení stránky.
- Chybí `og-image.jpg` (meta tagy na něj odkazují). Favicony už jsou (monogram `f.`,
  26. 7.); generátor og-image má `jakubsevela-web` v `scripts/generate-og.js`.
- Fotky referencí (`image02`–`05.jpg`) se stahují z Carrdu ručně. Když fotka chybí,
  `onerror` ji nahradí iniciálami.
- ~~Kalkulačka žije mimo repo a čeká na rozhodnutí.~~ **Vyřešeno 27. 7. 2026** —
  kalkulačka je veřejně na webu v sekci `#tarify` a nahradila statické price-cards.
  Komponenta price-card z manuálu zůstává pro ethel.cz.
