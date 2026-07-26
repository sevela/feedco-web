# feedco.cz — pravidla pro práci v tomhle repu

Statický web, žádný build. Hostuje GitHub Pages z branch `main`, root. Doména je v `CNAME`.

Feedco = modulární e-commerce konektor pro Helios iNuvio. Samostatný web (spoke),
prolinkovaný s [jakubsevela.cz](https://jakubsevela.cz), nikoli pod ním.

## Stav

Web odchází z Carrdu. `index.html` je **replika původní Carrd stránky** — tmavý design
(`#171A1C`), mintový akcent `#00FFC2`, Inter, pilulková tlačítka. Neodpovídá brand systému
(jantar/limetka, Lora + DM Sans, tónované buttony). Je tu proto, aby přechod na Pages
nezměnil nic navenek. Redesign do brandu přijde jako druhý krok.

Markup je přepsaný do sémantického HTML, ne kopie Carrd soup. Vizuální hodnoty
(barvy, velikosti, rádiusy, pozadí, oddělovače) odpovídají originálu 1:1.

Pořadí dotahování webů je hub → feedco → ethel. Feedco je tedy druhé v řadě.

## Vizuální systém (pro redesign, ne pro současnou repliku)

Tokeny jsou v **`/brand/tokens.css`**, kompletní manuál na `/brand/`.
Nikdy nepiš hexy natvrdo.

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

### Když měníš tokeny

`brand/tokens.css` je shodný ve všech třech repech (`jakubsevela-web`, `feedco-web`,
`ethel-web`) — mění se jen accent blok. Změnu **propiš do ostatních dvou** a do manuálu
na `/brand/`.

## Ceny — pozor

Ceny na současné stránce (LITE 490 / BASIC 2 490 / PROFI 4 490 Kč měsíčně) jsou z Carrdu
a **neodpovídají** rozpracovanému cenovému modelu (4 moduly × tarify, sleva za kombinaci,
implementační fee). Ten model má čtyři nevalidované domněnky a dokud nejsou uzavřené,
**ceny na webu neměň a nové nepřidávej.** Cenová rozhodnutí patří do projektu Feedco,
ne do brand projektu.

## Texty

Česky, vykaná forma. Konkrétnost před přísliby — jména klientů, čísla, měřitelné výsledky.
Reference na webu: VERKON, Younger Optics Europe, MIRA MAR, ZLKL.
Disclaimer „není produktem Asseco Solutions" na produktovém webu zůstává.

## Co nedělat

- Nepřidávat build krok ani závislosti, dokud to nepůjde jinak.
- Nepřidávat PHP ani nic serverového — Pages umí jen statické soubory.
  Formuláře jdou přes Formspree.
- Neměnit `CNAME`, nemazat `.nojekyll`.
- Nepoužívat `localStorage`/`sessionStorage`.

## Známý technický dluh

- Současný `index.html` je replika Carrdu, mimo brand systém — čeká na redesign.
- Kontaktní formulář: Carrd ho obsluhoval na svojí straně (AJAX na `/post/contact`).
  V replice je nahrazený Formspree, protože Pages nic serverového neumí. **Používá zatím
  stejný endpoint jako hub (`xkgnqpnz`)** — odlišen jen skrytým polem `_subject`.
  Až bude čas, založit Feedcu vlastní formulář. Honeypot `input[name="mail"]` z originálu
  je zachovaný.
- **Google Ads konverze `AW-986763051` z originálu nebyla přenesena** — v Carrdu byla
  vložená *před* definicí `gtag()`, takže vyhazovala chybu a nikdy nefungovala. GA4
  (`G-ZK1160VT0P`) přenesené je a funguje. Jestli má konverze fungovat, musí se vložit
  až za GA4 snippet a navázat na odeslání formuláře, ne na načtení stránky.
- Chybí `og-image.jpg` (meta tagy na něj odkazují) a favicony.
  `ethel-web` má generátor v `scripts/generate-og.js`.
- Obrázky v `/images/` (`image01.png` hero, `image02`–`05.jpg` fotky referencí,
  `image06.jpg` v patičce) se stahují z Carrdu ručně. Když fotka chybí, `onerror` ji
  odstraní a u referencí se ukáže iniciála z `data-initials`; hero obrázek se skryje celý.
- Fonty jdou z Google Fonts CDN; `ethel-web` je má self-hostované.
  Sjednotit přes `node scripts/build-fonts.js`.
- Kalkulačka (`feedco-kalkulacka-v2.html`) žije mimo repo a čeká na rozhodnutí,
  jestli půjde na web veřejně, nebo zůstane interním nástrojem.
