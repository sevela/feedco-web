# feedco.cz

Modulární e-commerce konektor pro Helios Inuvio. Samostatný web (spoke) v architektuře
hub-and-spoke; hub je [jakubsevela.cz](https://jakubsevela.cz).

Statický web bez buildu. Nasazuje GitHub Pages z branch `main`, root.
Web odchází z Carrdu — `index.html` je zatím replika původní stránky, redesign přijde potom.

## Struktura

```
index.html            replika původní Carrd stránky (světlý design, mimo brand systém)
images/               obrázky a loga
brand/
  tokens.css          zdroj pravdy pro barvy, typografii, radiusy — accent limetková
  index.html          grafický manuál v1.1
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

`/brand/` — živý dokument, shodný napříč všemi třemi weby. Při změně palety nebo komponent
ho aktualizuj a propiš `tokens.css` do `jakubsevela-web` a `ethel-web`.
