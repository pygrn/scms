# sCMS Workshop

Que farem?
- [Crearem un nou projecte basat en Pelican](#creació-del-projecte)
- [Generarem una mica de contingut](#creeu-nou-contingut)
- [El tunejarem una mica](#És-hora-de-personalitzar-lo)
- [El publicarem](#publicació)


## Creació del projecte

### 1) Entrem al nostre entorn virtual i instal·lem els requeriments per al taller

```bash
$ workon $venv
$ pip intall -r requirements.txt
$ cat requirements.txt
pelican
markdown
```

Si no teniu cap entorn virtual, creueu-ne un de nou! Python3 plz :)



### 2) Crearem el projecte

Executarem l'eina de `quickstart`:

```bash
$ pelican-quickstart

Welcome to pelican-quickstart v3.7.1.

This script will help you create a new Pelican-based website.

Please answer the following questions so this script can generate the files
needed by Pelican.

...
```

, i anirem seguint l'assistent pas per pas:

#### Títol del nostre site

```bash
...

> What will be the title of this web site? Site de prova
```

#### Autor

```bash
> Who will be the author of this web site? Xavi Torelló
```

#### Idioma per defecte

```bash
> What will be the default language of this web site? [en] ca
```

#### URL

Si volem definir-lo, premem 'y', i introduim la url per defecte del nostre site:

```bash
> Do you want to specify a URL prefix? e.g., http://example.com   (Y/n) y
> What is your URL prefix? (see above example; no trailing slash) http://sitedeprova.com
```

#### Paginació

```bash
> How many articles per page do you want? [10] 5
```

#### Zona horària

```bash
> What is your time zone? [Europe/Paris] Europe/Andorra
```

L'assistent demanarà confirmació per desplegar-hi les eines per defecte de desenvolupament i publicació, deixeu-ho tot per defecte.

Ho modificarem després depenent d'on ho vulguem publicar.

Ens haurà creat la nostra configuració i haurà preparat l'esquelet base del nostre projecte.


#### Estructura del projecte

Pelican ens haurà creat tot lo necessari per poder començar a generar contingut.

L'estructura és la següent:

```bash
$ tree .
.
├── content                 <--- Aquí hi desarem tot el nostre contingut
├── develop_server.sh
├── fabfile.py
├── Makefile
├── output                  <--- Quan generem el site, els fitxers estàtics es desaran aqui
├── pelicanconf.py          <--- Configuració del projecte
└── publishconf.py          <--- Configuració de la publicació

2 directories, 5 files
```


### 3) Afegim contingut

#### Preparem una nova entrada

Escolliu el vostre editor de texte preferit, i creeu un nou fitxer dins del directori `content`:

```bash
$ cat <<EOF > content/primera_entrada.md
Title: La nostra primera entrada!
Date: 2018-02-21 19:36
Category: Posts

Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. Donec pede justo, fringilla vel, aliquet nec, vulputate eget, arcu.

In enim justo, rhoncus ut, imperdiet a, venenatis vitae, justo. Nullam dictum felis eu pede mollis pretium. Integer tincidunt. Cras dapibus. Vivamus elementum semper nisi. Aenean vulputate eleifend tellus. Aenean leo ligula, porttitor eu, consequat vitae, eleifend ac, enim. Aliquam lorem ante, dapibus in, viverra quis, feugiat a, tellus. Phasellus viverra nulla ut metus varius laoreet. Quisque rutrum. Aenean imperdiet. Etiam ultricies nisi vel augue. Curabitur ullamcorper ultricies nisi. Nam eget dui. Etiam rhoncus. Maecenas tempus, tellus eget condimentum rhoncus, sem quam semper libero, sit amet adipiscing sem neque sed ipsum. Nam quam nunc, blandit vel, luctus pulvinar, hendrerit id, lorem. Maecenas nec odio et ante tincidunt tempus. Donec vitae sapien ut libero venenatis faucibus. Nullam quis ante. Etiam sit amet orci eget eros faucibus tincidunt. Duis leo. Sed fringilla mauris sit amet nibh. Donec sodales sagittis magna. Sed consequat, leo eget bibendum sodales, augue velit cursus nunc,

EOF
```

Compilem el nostre site

```bash
$ pelican content
Done: Processed 1 article, 0 drafts, 0 pages and 0 hidden pages in 0.11 seconds.
```

Veureu que dins ha generat tots els fitxers estàtics dins d'`output`
```bash
$ tree
.
├── content
│   └── primera_entrada.md
├── develop_server.sh
├── fabfile.py
├── Makefile
├── output
│   ├── archives.html
│   ├── author
│   │   └── xavi-torello.html
│   ├── authors.html
│   ├── categories.html
│   ├── category
│   │   └── posts.html
│   ├── index.html
│   ├── la-nostra-primera-entrada.html
│   ├── tags.html
│   └── theme
│       ├── css
│       │   ├── main.css
│       │   ├── pygment.css
│       │   ├── reset.css
│       │   ├── typogrify.css
│       │   └── wide.css
│       └── images
│           └── icons
│               ├── aboutme.png
│               ├── bitbucket.png
│               ├── delicious.png
│               ├── facebook.png
│               ├── github.png
│               ├── gitorious.png
│               ├── gittip.png
│               ├── google-groups.png
│               ├── google-plus.png
│               ├── hackernews.png
│               ├── lastfm.png
│               ├── linkedin.png
│               ├── reddit.png
│               ├── rss.png
│               ├── slideshare.png
│               ├── speakerdeck.png
│               ├── stackoverflow.png
│               ├── twitter.png
│               ├── vimeo.png
│               └── youtube.png
├── pelicanconf.py
├── publishconf.py
```

Obrirem l'index del nostre nou site

```bash
$ firefox output/index.html
```

#### WTF? No tenim estils?

Estem obrint un html des del file:///, tots els requeriments relatius carregats (estils, JS, ...) no es poden satisfer.

La solució? Aixecar "el servidor" de desenvolupament que Pelican integra:

```bash
$ bash develop_server.sh start 8000
Starting up Pelican and HTTP server
DEBUG: Pelican version: 3.7.1
DEBUG: Python version: 3.6.4
...
...
Done: Processed 1 article, 0 drafts, 0 pages and 0 hidden pages in 0.11 seconds.
Pelican and HTTP server processes now running in background.
```

A partir d'aquest moment podem atacar la nostra web a `localhost:8000`

```bash
$ firefox "http://localhost:8000"
```

Qualsevol canvi que realitzem serà detectat automàticament, i Pelican "re-compilarà" el nostre site. Només cal que refresquem FF per veure els canvis

Per aturar-lo només caldrà fer:
```bash
$ bash develop_server.sh stop
```

## Creeu nou contingut

Hem vist que tot el contingut sota content és interpretat per Pelican com contingut temporal (cronològicament ordenable), el que permet implementar la lògica d'articles, posts, ...

Pelican permet crear una jerarquia de categories basada en la organització del directori `content`, de manera que podeu crear subdirectoris per cada categoria, i fer-hi penjar d'allà els fitxers de contingut.


### Pàgines

També permet definir pàgines sense cap relació temporal, per exemple per crear una landing page específica, una pàgina tipus "Sobre nosaltres" o fins i tot una de contacte.

Per fer-ho només cal crear nous fitxers de contingut sota el directori `content/pages`.


### Metadades

Pelican permet integrar metadades HTML en funció de les variables del contingut, les principals són:

- Title: El títol del contingut
- Date: Data de publicació
  - format `YYYY-MM-DD HH:MM`
- Modified: Data de modificació
  - format `YYYY-MM-DD HH:MM`
- Category: Categoria sota la qual agrupar el contingut
- Tags: Llista de tags `tag1, tag2, ...`
  - llista separada per comes
- Slug: `la-meva-url-personalitzada`
- Authors: `Author1, Author2, ...`
  - llista separada per comes
- Summary: Resum del contingut
- Status: identifica l'estat del contingut
  - hidden, draft, published


### Resum

Tenim dos tipus de contiguts:
- les entrades
- les pàgines

A `content` hi podem estructurar el contingut en subdirectoris per cada una de les categories, de forma que tot quedi un pel més ordenat:

```
content/
├── categoria1                  <--- entrades amb categoria1
│   └── una_altra_entrada.md
│   └── una_altra_entrada2.md
├── categoria2                  <--- entrades amb categoria1
│   └── una_entrada.md
│   └── una_entrada2.md
├── pages                       <--- pàgines
│   └── una_pagina.md
│   └── contacte.md
│   └── about.md
├── primera_entrada.md             
├── segona_entrada.md
└── wtf.md

```

Tot i això, dins del fitxer de contingut, podem definir-hi la categoria emprant la metadada `Category`. Si la definim, aquesta manarà sobre l'organització dels directoris.


### A jugar!

Creeu més continguts, i visualitzeu com Pelican els va afegint al nostre site.

Sigueu originals,
- jugueu una mica amb les possiblitats de _markdown_ o de _rst_
- creeu noves categories i reviseu com Pelican modifica la organització del site
- afegiu-hi metadades
- creeu contingut atemporal

```bash
$ vi content/segona_entrada.md
$ vi content/tercera_entrada.md
$ vi content/quarta_entrada.md
...
```



## És hora de personalitzar-lo!

Anem a 'tunejar' una mica el nostre site.

### Temes

Els temes oficials els trobareu a https://github.com/getpelican/pelican-themes. Podeu veure una captura de pantalla dels temes a http://www.pelicanthemes.com.

Escolliu-ne un, i el descarregarem:

```
$ git clone git@github.com:alexandrevicenzi/Flex.git ~/pelican-themes/Flex
```

#### L'instal·lem

Podem copiar-lo o directament linkar-lo.

El linkarem amb:
```
$ pelican-themes -s ~/pelican-themes/Flex --verbose
Linking themes...
Linking `/home/k/pelican-themes/Flex' to `$VIRTUAL_ENV/pygrn_scms_test/lib/python3.6/site-packages/pelican/themes/Flex' ...
```

El copiarem amb:
```
$ pelican-themes --install ~/pelican-themes/Flex --verbose
Installing themes...
Copying '/home/k/pelican-themes/Flex' to '$VIRTUAL_ENV/pygrn_scms_test/lib/python3.6/site-packages/pelican/themes/Flex' ...
```

Un cop instal·lat, validem que tot hagi anat bé:
```
$ pelican-themes -l
simple
notmyidea
Flex@               <--- aquí el tenim!
```





### Plugins

https://github.com/getpelican/pelican-plugins


### Traduccions



## Publicació!

Un cop tenim el nostre site llest, podem fer varies coses per publicar-lo, des d'accions manuals, scripts o integrar el procés de publicació dins del propi Pelican.

La gràcia de tot plegat és que Pelican integra diferents mecanismes típics de publicació:
- FTP
- SSH
- Github pages
- Amazon S3
- Rackspace Cloud Files
- Dropbox

En el taller veurem els tres primers.

### Handmade

Sempre tenim la opció de copiar el contingut generat cap al servidor destinació de forma manual.

Rudimentari, però funciona xD:
```bash
$ scp -r output/* $user@$host:$vhost
```

### Via Pelican-FTP

Tenim la opció de demanar-li a Pelican que s'encarregui de publicar els canvis via FTP. No cal que ho fem manualment, només cal definir certs paràmetres de configuració:

### Via Pelican-SSH

### Via Pelican-GithubPages
