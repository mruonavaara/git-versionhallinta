# Peruskäyttö

## Repositorion perustaminen

Voit perustaa repositorion hakemistoon, joka ei ole vielä versionhallinnassa, komennolla `init`.

```bash
mkdir demo 		# luodaan hakemisto
cd demo		    # vaihdetaan uusi hakemisto oletushakemistoksi
git init
```

Komento luo tyhjän repositorion, johon voit tallettaa versioita. Tiedot tallentuvat alihakemistoon `.git`-nimiseen alihakemistoon. 
`.git`-hakemistosta tunnistat, onko hakemisto Git-versionhallinnassa.

Tiedostot ja hakemistot, joiden nimi alkaa pisteellä, ovat piilotettuja, niitä ei oletusarvoisesti näytetä. Saat piilotetut hakemistot näkyviin `ls`-komennon laajentimella `-a`. Laajentimella `-l` näytetään tiedostojen ja hakemistojen kaikki tiedot.

``` bash
$ ls -l -a
total 31
drwxr-xr-x 1 h01975 1049089    0 Feb 15 15:04 ./
drwxr-xr-x 1 h01975 1049089    0 Feb 22 15:08 ../
drwxr-xr-x 1 h01975 1049089    0 Feb 15 15:04 .git/
-rw-r--r-- 1 h01975 1049089   81 Feb 15 12:36 .gitattributes
drwxr-xr-x 1 h01975 1049089    0 Feb 15 12:36 .github/
-rw-r--r-- 1 h01975 1049089  490 Feb 15 12:36 .gitignore
-rw-r--r-- 1 h01975 1049089   13 Feb 15 13:42 hello.txt
-rw-r--r-- 1 h01975 1049089 9305 Feb 15 12:36 readme.md
-rw-r--r-- 1 h01975 1049089   29 Feb 15 15:04 time.txt
```

Jotta piilotetut tiedostot näkyisivät Windowsin tiedostojenhallinnassa, on tiedostojenhallinan asetuksissa määritettävä piilotetut tiedostot näkyviin.

- [View hidden files and folders in Windows](https://support.microsoft.com/en-us/windows/view-hidden-files-and-folders-in-windows-97fbc472-c603-9d90-91d0-1166d1d9f4b5)

### Repositorion perustaminen toisesta repositoriosta

Usein haluat kopioida olemassa olevan repositoryn ja jatkaa työskentelyä siitä. Tämä tapahtuu komennolla `clone`, esim.

```
git clone https://github.com/libgit2/libgit2
```

Komento lisää nykyiseen hakemistoon alihakemiston libgit2, joka sisältää alkuperäisen repositoryn datan kopion (`.git`) sekä uusimman version tiedostot. Se myös konfiguroi alkuperäisen repositoryn uuden repositoryn etärepositoryksi. 

Täsä aihetta käsitellään myöhemmin osiossa _Hajautettu Git_.

## Tiedostot Git-hakemistossa

Hakemisto, johon on perustettu Git-repositorio, on Git:n __työhakemisto__ (_working set_). 

Työhakemistossa olevat tiedostot ja alihakemistot ovat otettavissa Git-hallintaan. Tiedostot pitää viedä erikseen Git-hallintaan, jos niiden versioita halutaan hallinnoida.

Git:n näkökulmasta hakemistossa olevat tiedostot voivat Git-termein olla joko 

-  _Tracked_ (Otettu Git:n hallintaan) tai 
-  _Untracked_ (Ei Git-hallinnassa).

Git:n hallinnassa oleva työhakemiston tiedosto voi olla

- _Unmodified_ - muuttumaton sama kuin talletettu uusin versio 
- _Modified_ – muuttunut, erilainen kuin talletettu uusin versio
- _Staged_ – merkitty otettavaksi seuraavaan talletukseen

Oheinen kuva kuvaa eri tiloja ja niiden välisiä siirtymiä.

- Jos hakemistoon lisätään uusi tiedosto, se on `untracked`.
- Jos hakemistossa oleva Git-hallinnassa oleva tiedosto muuttuu, sen tilaksi tulee `modified`.
- Uudet ja muuttuneet tiedostot voidaan merkitä otettavaksi seuraavaan talletukseen toiminnolla `add` (_stage the file_). 
- Kun talletus  (_commit_) tehdään, kaikki mukaan otettavaksi merkityt tiedostoversiot talletetaan, ja niiden tilaksi tulee `unmodified`.

![](assets/git_file_states.png)

Työhakemiston tiedostojen Git-tilaa voi tarkastella komennolla status.

```bash
git status
```

!!! tip "Vinkki"
    
    Työhakemiston git-tilaa (komento `status`) kannattaa tarkastella ennen Git-operaatioita ja niiden jälkeen, niin pysyt aina tilanteen tasalla, mitä repositoriossasi tapahtuu. 

## Muutosten tallettaminen, vaihe 1: add

Tiedostoversioiden tallettaminen on kaksivaiheinen operaatio. 

Kun tiedosto on valmis talletettavaksi versionhallintaan, uusi tai muutettu tiedosto on merkittävä otettavaksi mukaan seuraavaan talletukseen (_commit_). Tätä toimintoa kutsutaan Git-terminologiassa nimellä _staging_, ja se tehdään komennolla `add`. 

Tiedostot voidaan lisätä seuraavaan talletukseen yksittäin.

```bash
git add hello.html   # tiedosto hello.html otetaan mukaan seuraavaan talletukseen
```

Voit myös lisätä koko hakemiston, jolloin kaikki hakemiston tiedostot ja alihakemistot sisältöineen lisätään kerralla. Hakemistot ovat myös tiedostoja, nekin versioituvat.

```bash
git add .		# . viittaa nykyiseen hakemistoon, kaikki uudet ja muuttuneet tiedostot otetaan mukaan
```

Nyt muuttuneet tiedostot ovat valmiita talletettavaksi versionhallintaan. Kuten huomasit, uuden tiedoston tuominen on muutos siinä kuin olemassa olevankin muuttaminen.

Nyt Git on tietoinen, mitä pitää tallentaa, ja ollaan valmiita `commit`-toimintoa varten.

## Muutosten tallettaminen, vaihe 2: commit

Varsinainen talletus tapahtuu komennolla `commit`.

```bash
git commit
```

Komento käynnistää editorin, jolla voit kirjoittaa muutokseen talletettavan kommentin. Kun talletat ja suljet, muutos viedään tietovarastoon.

Kirjaa kommenttiin muutoksen aihe selkeästi, ne ovat tärkeää kommunikaatiota itsellesi ja projektiryhmällesi.

Voit myös kirjata kommentin komentorivillä ilman editoria:

```bash
git commit –m "Lisätty logout-toiminnallisuus"
```

## Talletusten tarkastelu

Työtilan muutoksia verrattuna talletettuihin voit tarkastella tutulla komennolla `status`. Sitä kannattaa käyttää ahkerasti, jotta pysyt selvillä, mikä on hakemiston ja sen muutosten Git-tila:

```bash
git status
```

Näet commit-talletusten historian komennolla `log`.

```bash
git log
```

Komento listaa kaikki talletukset käänteisessä aikajärjestyksessä. Laajentimella `--stat` Git lisää tulostukseen lyhyen yhteenvedon talletusten muutoksista:

```
git log --stat
```

Työhakemistossa olevan tiedoston muutoksia verrattuna viimeksi talletettuun versioon voi tarkastella komennolla `diff`.

```bash
git diff hello.html
```

## Tiedostojen poistaminen ja siirtäminen

Kuten aiemmin todettiin, hakemistot versioituvat myös. Jos haluat poistaa tiedoston repositoriosta tai siirtää tiedoston toiseen hakemistoon, olet tekemässä uutta versiota hakemistoista. 

Git-komento `rm` poistaa tiedoston paitsi työhakemistosta myös Git-hallinnasta. Muutos on sen lisäksi talletettava versionhallintaan.

```bash
git rm test.txt
git commit -m "Poistettu tarpeeton tiedosto"
```

Huomaa, että vanhat talletetut versiot säilyvät versionhallinnassa! Se, mikä on versionhallintaan talletettu, säilyy siellä.

Git-komennolla `mv` voi nimeätä tiedoston uudelleen tai siirtää toiseen hakemistoon. 

``` bash
git mv oldname.txt newname.txt
mkdir newdir
git mv newname.txt newdir
git add .
git commit -m "Uudelleenjärjestelty tiedostoja"
```

Tiedostoja voi poistaa ja siirtää repositorion sisällä käyttöjärjestelmän komennoilla (esim. `rm` tai `mv`). Muutokset talletetaan Git-hallintaan samalla tapaa kuin mikä tahansa muutos: ensin `add`, sitten `commit`. Vastaavilla Git-komennoilla ei `add`-vaihetta tarvita.

## Harjoitus 2
Harjoitellaan perustoimintoja. 

Tarkista repositorion tilanne joka välissä komennolla `status`. Muista laatia talletuksillesi kuvaava kommenttiviesti!

1. Tee koneellesi kurssin harjoituksia varten hakemisto ja perusta sinne Git-repositorio.
2. Tee repositorioon tiedosto (esim. `test.txt`) ja kirjoita tiedostoon jotain. Talleta tiedosto Git-hallintaan. 
4. Tee repositorioon hakemisto `hello` ja sinne tiedosto `hello.html`. Tiedoston sisältö voi olla esim.

    ``` html
    Hei maailma!
    ```

    Vie nämä muutokset Git-hallintaan.

5. `hello.html`-tiedoston sisältö ei vielä ole HTML-koodia. Lisää tekstiin h1-merkkaus, jolloin siitä tulee HTML-elementti:

    ``` html
    <h1>Hei maailma!</h1>
    ```

    Vie muutos versionhallintaan. 

6. Muuta `hello.html`-tiedoston nimeksi `index.html` ja talleta muutos.
7. Ensimmäisenä luotu test.txt-tiedosto on nyt käynyt tarpeettomaksi. Poista se versionhallinnasta ja talleta muutos. Laadi talletuksellesi kuvaava kommenttiviesti.
8. Lisää vielä joitakin tiedostoja ja talleta ne versionhallintaan. 
9. Tarkastele tekemiäsi talletuksia komennolla `git log`. Kokeile myös komentoa laajentimella `--stat`. Mitä lisätietoa saat?


## Paluu menneisyyteen

Johdanto-osiossa väitettiin, että versionhallinnan avulla on mahdollista palauttaa ohjelmiston aiempia versioita. Kokeillaan sitä seuraavassa.

Tarkastellaan Git-komennon `log` tulostusta:
```
commit 6fa5fd1b94a163464aaf56a7b69b6f7f4cca429b
Author: Ruonavaara Markku <markku.ruonavaara@haaga-helia.fi>
Date:   Sun Mar 10 15:16:39 2024 +0200

    Lisätty toinen tiedosto

commit 77d8790ada4aa9ce8e438a360e44657334eeb7d3
Author: Ruonavaara Markku <markku.ruonavaara@haaga-helia.fi>
Date:   Sun Mar 10 15:14:41 2024 +0200

    Uudelleenjärjestelty tiedostoja

commit 5d565f66349cb8eb1b3550855d89d12496f23a1b
Author: Ruonavaara Markku <markku.ruonavaara@haaga-helia.fi>
Date:   Sun Mar 10 15:13:46 2024 +0200

    Lisätty tiedosto

commit f78c0a4d638b3c3f3cfb85a2c5e7eba38023d8b3
Author: Ruonavaara Markku <markku.ruonavaara@haaga-helia.fi>
Date:   Sun Mar 10 14:57:53 2024 +0200

    Ensimmäinen commit

```
Git antaa jokaiselle talletukselle (_commit_) yksikäsitteisen tunnistemerkkijonon (esim. _6fa5fd1b94a163464aaf56a7b69b6f7f4cca429b_). Tätä tunnistetta kutsutaan Git-terminologiassa nimellä _hash_.

Kun tiedämme tallennuksen tunnisteen, voimme palata sen tilanteeseen komennolla `checkout`. Palataan ensimmäisen tallennuksen _Ensimmäinen commit_ tilanteeseen: 
```bash
$ git checkout f78c0a4
Note: switching to 'f78c0a4'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at f78c0a4 Ensimmäinen commit
```
Koko tunnistetta ei tarvitse antaa, seitsemän ensimmäistä merkkiä riittää.

Nyt työhakemisto on päivittynyt ensimmäisen talltuksen tilanteeseen, ja hakemistossa on vain sinne ensimmäisenä tehty tiedosto `text.txt`.

```
$ ls -l -a
total 13
drwxr-xr-x 1 h01975 1049089  0 Mar 10 16:17 ./
drwxr-xr-x 1 h01975 1049089  0 Mar 10 13:49 ../
drwxr-xr-x 1 h01975 1049089  0 Mar 10 16:20 .git/
-rw-r--r-- 1 h01975 1049089 17 Mar 10 15:00 test.txt

```

Komennon ilmoitus kertoo, että olemme _detached HEAD_-tilassa. Se tarkoittaa, että jos teemme muutoksia, ne eivät tule tallettumaan mihinkään _haaraan_, jolloin ne eivät näkyisi versiohistoriassa. Käytännössä tässä tilassa ei kannata tallettaa muutoksia. 

Takaisin nykytilaan päästään esimerkiksi Git:n antaman neuvon mukaisesti:

```bash
git switch -     # palataan siihen haaraan, josta checkout tehtiin
```

Siihen, mistä tässä on kyse ja miten kannattaa toimia, palataan myöhemmin osiossa _Haarat_. 

!!! tip "Vinkki"
    Git neuvoo sinua aina, kun teet jonkin toimenpiteen. 
    
    Ilmoituksia kannattaa lukea ja yrittää tulkita. Ongelmatilanteissa sen ehdotukset usein ohjaavat oikeaan suuntaan.


## Oho! Eiku…

Versionhallintatoimintojen kanssa voi helposti tulla erehdyksiä. Hätä ei kuitenkaan ole tämännäköinen, kaikki on oikaistavissa. Tässä joitakin peruutusohjeita.

### `add`-komennon peruuttaminen

Jos lisäsit seuraavaan talletukseen tiedoston, joka ei sinne kuuluisi, voit peruuttaa lisäyksen komennolla `reset`.

```bash
git reset temp.log
```

Jos et anna parametria, kaikki lisätyt tiedostot poistetaan seuraavasta tallennuksesta.

Komento ei poista tai muuta tiedostoja, vain muuttaa tiedostojen tilan talletuksen suhteen.

### Työtilaan tehtyjen muutosten peruuttaminen ennen talletusta

Jos haluat peruuttaa työtilassa tekemäsi muutokset, __joita ei vielä ole talletettu versionhallintaan__, voit palauttaa tiedoston versionhallinnan tuoreimman version tasalle komennolla `restore`:

```bash
git restore hello.html
```
!!! danger "Varoitus"
    Huomaa, että tässä tapauksessa __tekemästi muutokset häviävät eivätkä ne ole palautettavissa__. Vain talletetut versiot voidaan palautettaa.

Jos haluat peruuttaa kaikki työtilaan tekemäsi muutokset, se onnistuu komennolla `git reset --hard`. Käytä sitä vain, kun olet varma, että haluat hylätä kaikki tekemästi muutoksiet

### Talletettujen muutosten peruminen

Jos olet tallettanut muutoksen versionhallintaan, muutokselle on jo luotu tunniste ja siitä on talletettu kaikki tiedot. Jos sitä muutettaisiin, jouduttaisin peukaloimaan repositorion versiohistoriaa.

Talletetun muutoksen poistaminen ei oikeastaan edes ole järkevää. Sen sijaan että yrittäisit muuttaa historiaa, voit tehdä uuden muutoksen, jossa väärä muutos korjataan. 

Yksi ylimääräinen talletus ei haittaa, ja korjaus on täysin riskitön. Historian muuttaminen sen sijaan olisi riskialtista, se voisi aiheuttaa monin verroin suurempia ongelmia kuin ylimääräinen talletus.

Voit peruuttaa kokonaisen talletuksen tekemällä "anti-talletuksen" Git-komennolla `revert`. Komento tekee muutoksen, joka peruuttaa sille parametrina annetun talletuksen kokonaan.

```bash
$ git log -2      # näyttää kaksi viimeisintä talletusta
commit 4a731586b83b6c1469416a489e5da1a4560707d4 (HEAD -> master)
Author: Ruonavaara Markku <markku.ruonavaara@haaga-helia.fi>
Date:   Sun Mar 10 16:58:47 2024 +0200

    Lisätty log-tiedosto

commit 21f29c9814e6f101319edc51a199b2d62eb97fae
Author: Ruonavaara Markku <markku.ruonavaara@haaga-helia.fi>
Date:   Sun Mar 10 15:19:32 2024 +0200

    Siirrelty taas tiedostoja

$ git revert 4a73158
[master 83e809b] Revert "Lisätty log-tiedosto"
 1 file changed, 53 deletions(-)
 delete mode 100644 log.txt

$ git log -2
commit 83e809b0dd28076a423d916229567e61f8f44043 (HEAD -> master)
Author: Ruonavaara Markku <markku.ruonavaara@haaga-helia.fi>
Date:   Sun Mar 10 16:59:26 2024 +0200

    Revert "Lisätty log-tiedosto"

    This reverts commit 4a731586b83b6c1469416a489e5da1a4560707d4.

commit 4a731586b83b6c1469416a489e5da1a4560707d4
Author: Ruonavaara Markku <markku.ruonavaara@haaga-helia.fi>
Date:   Sun Mar 10 16:58:47 2024 +0200

    Lisätty log-tiedosto

```
Komento `revert` peruuttaa yhden talletuksen kerrallaan. Jos haluat peruuttaa useampia talletuksia, jokainen pitää peruuttaa yksi kerrallaan.

Muista, että __kaikki, mikä on versionhallintaan talletettu, on palautettavissa__. Siksi `commit`-talletuksia kannattaa tehdä usein.

## Harjoitus 3

Harjoitellaan peruuttelua.

1. Tee repositorioosi useita muutoksia: muuta talletettuja tiedostoja ja lisää uusia tiedostoja.  Älä talleta!

2. Kokeile `add`-toiminnon peruuttamista. 
     - Lisää muutokset seuraavaan talletukseen (`add`).
     - Poista muutoksia yksittäin seuraavasta talletuksesta.
     - Poista kaikki loput muutokset seuraavasta talletuksesta. 
     - Sinulla pitäisi nyt olla työtilassa useita tallettamattomia muutoksia, joista mikään ei ole menossa seuraavaan talletukseen. 

3. Kokeile työtilaan tehtyjen muutosten peruuttamista. Tarkista tilanne joka välissä komennolla `status`.
     - Peruuta jonkin talletetun tiedoston muutokset työtilasta.
     - Poista kaikki loput muutokset työtilasta. 
     - Mitä tapahtui uusille _untracked_-tilassa oleville tiedostoille?

4. Kokeile talletuksen peruuttamista
     - Talleta nyt kaikki muutokset. 
     - Peruuta talletus komennolla `revert`. 
     - Mitä näyttää komento `log`?

