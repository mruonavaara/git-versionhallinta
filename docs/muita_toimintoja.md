# Muita toimintoja

## Tiedostojen jättäminen versionhallinnan ulkopuolelle

Kaikkia projektin tiedostoja ei kannata viedä versionhallintaan.

Yleissääntönä pois jätetään 

- kaikki tiedostot, joita projektissa ei tarvita,  
- käännöstuotokset ja build-hakemistot,
- generoidut tiedostot, 
- työkalujen tuottamat loki- ja väliaikaistiedostot,
- pakettienhallinnan lataamat tiedostot ja
- henkilökohtaiset konfiguraatiotiedostot.

Repositorioon pitää viedä kaikki sellaiset tiedostot, joita tarvitaan kehittämiseen. Jos uusi kehittäjä kloonaa repositorion, hänen pitäisi pystyä jatkamaan kehitystä siitä.

### Luottamuksellinen tieto
Versionhallintaan ei pitäisi viedä luottamuksellisia tietoja kuten käyttäjätunnuksia, salasanoja ja järjestelmäkonfiguraatioita. Jos ne ovat versionhallinnassa ja viedään etärepositoryyn, ne ovat kaikkien niiden nähtävissä, joilla on repositoriaan lukuoikeus.

Luottamuksellisia tietoja kuitenkin tarvitaan järjestelmien kehittämisessä esimerkiksi tietokantayhteyden muodostamiseen. Tällöin on tehtävä jokin ratkaisu, jolla luottamukselliset tiedot tuodaan järjestelmään jotenkin toisin. 

Ratkaisu voi olla esim.
- Luottamukselliset tiedot ovat konfiguraatiotiedostossa, jota ei viedä versionhallintaan
- Luottamukselliset tiedot luetaan ympäristömuuttujista

Tällöin kehittäjä antaa paikallisesti luottamukselliset tiedot.


### Ignore-säännöt

Git:lle voi määrittää sääntöjä, mitkä tiedostot se jättää huomioimatta. Säännöt määritetään `.gitignore`-tiedostoon

Yleensä projektilla on yksi `.gitignore`-tiedosto projektin juurihakemistossa. Se vaikuttaa siihen hakemistoon, jossa se on sekä rekursiivisesti kaikkiin alihakemistoihin.

### Esimerkkejä .gitignore-sääntöjen laatimisesta

Kommenttirivit alkavat `#`-merkillä. Tyhjät rivit jätetään huomiotta. Normaalit korvaus-patternit (esim. `*`) toimivat. 

Esimerkkejä:

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

GitHubilla on laaja valikoima .gitignore-malleja erilaisille projekteille. Niistä saat hyvän lähtökohdan oman projektisi konfigurointiin ([https://github.com/github/gitignore](https://github.com/github/gitignore)).

### Huomiotta jätetyn tiedoston poistaminen

Joskus repositorioon lipsahtaa jotain sellaista, jonka ei sinne olisi pitänyt mennä, koska `.gitignore`-tiedostosta puuttuu sääntö, joka olisi pitänyt sinne laatia.

Tällöin voidaan poistaa tiedosto Git-hallinnasta:
```bash
git rm --cached tiedostonimi
```
Tiedosto merkitään poistettavaksi hakemistosta seuraavassa commitissa, valitsin `--cached` kuitenkin säilyttää sen työtilassa. Tiedosto on nyt työhakemistossasi untracked-tilassa, voit nyt lisätä .gitignore-säännön ja tehdä commitin, jossa tiedoston poisto talletetaan.

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

## Tagit

Versiohistoriaan voidaan kirjata muistiin tiettyjä nimettyjä versioita. Tällaisia ovat tyypillisesti järjestelmän julkaisuversiot (esim _v1.0.3_).

Git-järjestelmässä tämä tehdään toiminnolla `tag`. Tagit ovat viittauksia tiettyihin talletuksiin, ja niihin voidaan kirjata metatietoa kuten talletukseen (_annotated tag_):

```bash
git tag –a v.1.0.3 –m "v1.0.3"   # -a tarkoittaa "annotated"
```

Tagit voi listata komennolla `tag`. Tagin tiedot voi listat komennolla `show`:

```bash
git tag
git show v1.0.3
```

Tagin voi asettaa mihin tahansa talletukseen myöhemminkin:

```bash
git tag -a v1.2 9fceb02
```

### Tagit etärepositorioissa

Tageja ei viedä etärepositoryyn push-operaatiolla automaattisesti vaan ne pitää viedä erikseen. Se tapahtuu samalla tavalla kuin haarojen vienti:

```bash
git push origin v1.0.3	    # "origin" on etärepositorio, "v1.0.3" on tag
```

Kaikki tagit saa vietyä kerralla laajentimella `--tags`:

```bash
git push origin --tags
```

Tagi voidaan poistaa laajentimella `-d`:

```bash
git tag -d v1.0.3
```

Koska tagit ovat viittauksia talletuksiin siinä kuin muutkin viittaukset, niitä voi käyttää samalla tapaa, esim.
```bash
git checkout v1.2
```
