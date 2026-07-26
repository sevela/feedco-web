# feedco.cz

Modulární e-commerce konektor pro Helios Inuvio. Samostatný web (spoke) v architektuře
hub-and-spoke; hub je [jakubsevela.cz](https://jakubsevela.cz).

Statický web bez buildu. Nasazuje GitHub Pages z branch `main`, root.
Web odchází z Carrdu — `index.html` je zatím replika původní stránky, redesign přijde potom.

## Struktura

```
index.html            web v brand systému (dark-first, limetkový akcent), texty z původní Carrd stránky
images/               obrázky a loga
brand/
  tokens.css          barvy, typografie, radiusy — accent limetková; kopie z jakubsevela-web
scripts/
  build-fonts.js      self-hosting Google Fonts do /fonts/
CNAME                 feedco.cz
.nojekyll             vypíná Jekyll — bez toho Pages ignoruje soubory s podtržítkem
robots.txt            zakazuje /brand/
sitemap.xml
CLAUDE.md             pravidla pro práci v repu — přečti dřív než začneš
```

## Lokální náhled

```bash
python3 -m http.server 8000
# http://localhost:8000
```

Absolutní cesty (`/brand/tokens.css`) fungují jen přes server, ne přes `file://`.

## Nasazení

Push do `main`. Pages vystaví do minuty.

## Grafický manuál

Manuál žije na **jednom místě**: <https://jakubsevela.cz/brand/> (zdroj `sevela/jakubsevela-web`,
soubor `brand/index.html`). V tomhle repu je jen `tokens.css`, protože ho web načítá.

Při změně palety nebo komponent aktualizuj manuál tam a `tokens.css` propiš sem
a do `ethel-web`.
