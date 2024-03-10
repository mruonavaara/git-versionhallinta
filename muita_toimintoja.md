# Muita toimintoja

## Tiedostojen jättäminen versionhallinnan ulkopuolelle

Kaikkia projektin tiedostoja ei kannata viedä versionhallintaan, esim.
- Paketinhallinnan asentamat kirjastot (esim. /node_modules)
- Käännöstuotokset ja build-hakemistot (esim.  /target, .o, .class, .exe)
- Työkalujen tuottamat loki- yms. tiedostot
- Omat IDE-konfiguraatiotiedostot

Git:lle voi määrittää sääntöjä, mitkä tiedostot se jättää huomioimatta. Säännöt määritetään `.gitignore`-tiedostoon

Yleensä projektilla on yksi `.gitignore`-tiedosto projektin juurihakemistossa. Se vaikuttaa siihen hakemistoon, jossa se on sekä rekursiivisesti kaikkiin alihakemistoihin.

### Esimerkkejä .gitignore-sääntöjen laatimisesta

Kommenttirivit alkavat #-merkillä. Tyhjät rivit jätetään huomiotta. Normaalit korvaus-patternit (esim. *) toimivat. Esimerkkejä:

```
# Jätä huomiotta kaikki tiedostot, jotka päättyvät tilde-merkkiin (~)
*~

# Jätä huomiotta kaikki .log-tiedostot
*.log

# Jätä huomiotta kaikki .o- ja .a-tiedostot
*.[oa]

# Jätä huomiotta kaikki build-hakemistot missä tahansa hakemistossa
build/

# Jos sääntö alkaa /-merkille, sitä ei sovelleta alihakemistoihin:
# Jätä huomiotta vain tässä hakemistossa oleva temp-hakemisto
/temp

# Sääntöön voi tehdä poikkeuksen !-merkillä:
# Jätä huomiotta kaikki .log-tiedostot paitsi change.log
*.log
!change.log
```

### Mitä pitäisi ottaa, mitä jättää huomiotta?

Repositoryyn pitää viedä kaikki sellaiset tiedostot, joita tarvitaan kehittämiseen. Jos uusi kehittäjä kloonaa repositoryn, hänen pitäisi pystyä jatkamaan siitä.

Yleissääntönä pois jätetään 
- kaikki tiedostot, joita projektissa ei tarvita,  
- generoidut tiedostot, 
- pakettienhallinnan lataamat tiedostot ja 
- henkilökohtaiset konfiguraatiotiedostot. 

GitHubilla on laaja valikoima .gitignore-malleja erilaisille projekteille. Niistä saat hyvän lähtökohdan oman projektisi konfigurointiin (https://github.com/github/gitignore).

### Huomiotta jätetyn tiedoston poistaminen

Joskus repositoryyn lipsahtaa jotain sellaista, jonka ei sinne olisi pitänyt mennä, koska .gitignoresta puuttuu sääntö, joka olisi pitänyt sinne laatia.

Tällöin voidaan poistaa tiedosto Git-hallinnasta:
```bash
git rm --cached tiedostonimi
```
Tiedosto merkitään poistettavaksi hakemistosta seuraavassa commitissa, optio `--cached` kuitenkin säilyttää sen työtilassa. Tiedosto on nyt työhakemistossasi untracked-tilassa, voit nyt lisätä .gitignore-säännön ja tehdä commitin, jossa tiedoston poisto talletetaan.

__Huom!__ Tiedoston vanhat versiot kuitenkin jäävät historiaan. Jos haluat poistaa ne sieltäkin, on muutettava historiaa, mikä on aina riskialtista. Perehdy huolellisesti dokumentaatioon, jos lähdet sitä tekemään.

## Tarpeettomien tiedostojen poistaminen työtilasta

Komento `clean` poistaa kaikki `untracked`-tiedostot, joita ei ole erikseen mainittu .gitignoressa. Sillä voit puhdistaa työhakemiston turhista tiedostoista, joita ei tarvita repositoryssä eikä muutenkaan.

Koska tämä komento poistaa tiedostoja, on hyvä ensin tarkistaa, mitä clean tekisi:

```bash
git clean –d –-dry-run            # -d poistaa myös hakemistot
```

Kun olet varma, että poistettavat tiedostot todella ovat turhia, voit ajaa komennon

```bash
git clean -d
```

Komennolla on myös interaktiivinen moodi, jossa aina kysytään, mitä tehdään:

```bash
git clean -i -d
```
## Muutosten peruuttaminen

### Talletetun commitin peruuttaminen

revert

### Työtilan muutosten peruuttaminen

reset
