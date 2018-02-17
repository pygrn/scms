# sCMS Workshop

Que farem?
- Crearem un nou projecte basat en Pelican
- Generarem una mica de contingut
- El tunejarem una mica
- El publicarem


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

L'assistent demanarà confirmació per desplegar-hi les eines per defecte de desenvolupament i publicació, deixeu-ho tot per defecte. Ho modificarem després depenent d'on ho vulguem desplegar.


#### Estructura del projecte

Pelican ens haurà desplegat tot lo necessari per poder començar a generar contingut.

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

