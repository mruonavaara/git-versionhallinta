# Git projektissa

## Työnkulut hajautetussa Git-ympäristössä

Git:n käyttö perustuu siihen, että kaikki tapahtuu paikallisessa repositoryssä. Kun projektissa on useita kehittäjiä, eri kehittäjien työ jaetaan toisille etärepositoryjen avulla.

Etä-repositoryt voidaan organisoida usein eri tavoin, ja niiden käyttöön voidaan laatia erilaisia työnkulkuja. Työnkulku vastaa kysymyksiin
- Miten organisoin oman työni omassa repositoryssani, jotta sen vieminen yhteiseen projektiin onnistuu
- Miten vien oman työni yhteiseen projektiin
- Miten saan muiden työt omaan repositoryyni

Seuraavassa esitellään esimerkinomaisesti kaksi erilaista tapaa organisoida versionhallinnan työnkulkuja projektissa.

### Keskitetty malli

Keskitetyssä mallissa projektilla on yksi yhteinen repositorio, jonka kanssa kaikki kehittäjät synkronoivat oman työnsä. 

![](./assets/centralized_workflow.png)

_Lähde: [Chacon S., Straub B, Pro Git, luku 5.](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell) [CC BY-NC-SA 3.0](https://creativecommons.org/licenses/by-nc-sa/3.0/)_

Kehittäjät hakevat muiden muutokset keskitetystä repositoriosta, liittävät ne omiin muutoksiinsa, ja vievät lopuksi omat muutoksensa yhteiseen repositorioon.

Mallin käyttäminen edellyttää, että kaikilla projektin kehittäjillä on oikeudet viedä muutoksia yhteiseen repositorioon (_push_).

### Integrointimanagerimalli

Julkisissa projekteissa (esim. avoimen lähdekoodin projekteissa) ei ole mahdollista antaa kaikille projektin jäsenille oikeuksia muuttaa yhteisen repositorion sisältöä. 

Tällöin Git-versionhallinnassa voidaan soveltaa mallia, jossa jokaisella kehittäjillä on oma julkinen repositorio ja lukuoikeudet toistensa repositorioihin.

Yksi repositorio on yhteinen ”virallinen”, johon kaikilla on lukuoikeus, mutta jonne vain projektin ylläpitäjällä (_integraatiomanageri_) on oikeus viedä muutoksia.

![](./assets/integration_manager_workflow.png)

_Lähde: [Chacon S., Straub B, Pro Git, luku 5.](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell) [CC BY-NC-SA 3.0](https://creativecommons.org/licenses/by-nc-sa/3.0/)_

Kukin kehittäjä julkaisee muutoksensa omaan julkiseen repositorioonsa ja lähettää ylläpitäjälle pyynnön yhdistää ne viralliseen repositorioon. 

Tätä työnkulkua tässä materiaalissa ei käsitellä tämän enempää.  

## Talletusten käytännöt

Tallennusten kommentit viestittävät projektin kehittäjille, mitä muutoksia toiset ovat projektiin tehneet. Talletusten kommentoinnin käytännöistä on syytä sopia projektissa yhteisesti.

Kommentointiin on vakiintuneita hyviä käytäntöjä, esim. [How to Write a Git Commit Message](https://cbea.ms/git-commit/). Niiden mukaan kommentteihin on hyvä kirjata
- Lyhyt (max 50 merkkiä), otsikkotyyppinen kuvaus ensimmäiselle riville.
- Tarvittaessa pidempi kuvaus muutoksesta ja se syistä rivinvaihdolla erotettuna.

Jokaisesta loogisesta kokonaisuudesta kannattaa tehdä erillinen talletus. Tällöin muutosten tarkastelu ja käsittely projektissa on mahdollisimman selkeää. Vaikka olisit kehittänyt useita ominaisuuksia kerralla, voit `add`-vaiheessa jakaa muutokset eri talletuksiin. 

Ylimääräinen white-space (välilyönnit, tabulaattorit, rivinvaihdot jne.) ei vaikuta suoritukseen mutta voi näkyä Git-talletuksissa muille turhina muutoksia. Voit tarkistaa sellaiset `diff`-komennolla:
```bash
$ git diff --check
```

Editoreissa on ominaisuuksia, jolla white-space-ongelmat voidaan poistaa automaattisesti.

## Yhteistyö keskitetyssä mallissa

Yksinkertaisin malli, jota useimmissa pienissä projekteissa käytetään, on keskitetty. Kaikilla kehittäjillä on tällöin kirjoitusoikeudet yhteiseen repositorioon.

Aluksi kaikki kloonaavat yhteisen repositoryn

```bash
$ git clone <repository-url>
```

Muutokset tehdään omassa repositoriossa ja talletetaan sinne, kukin kehittäjä omaan tahtiinsa.

```bash
$ git commit
```

Kun muutokset ovat valmiita, ne voidaan viedä yhteiseen repositorioon 

```bash
$ git push origin master
```
1. Tilanne komennon `fetch jälkeen`:

![](./assets/after_fetch.png)

2. Tilanne komennon `merge` jälkeen:
![](./assets/after_merge.png)

3. Tilanne komennon `push` jälkeen:
   
![](./assets/after_push.png)

_Lähde: [Chacon S., Straub B, Pro Git, luku 5.](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell) [CC BY-NC-SA 3.0](https://creativecommons.org/licenses/by-nc-sa/3.0/)_

Lopputilanteessa oma repositorio ja yhteinen repositorio ovat samalla tasalla, ja `origin/master`-haaran tuoreimmassa talletuksessa on versio, jossa on yhdistetty kaikkien kehittäjien tähänastiset muutokset.  

## Rinnakkaiset muutokset

Edellä kuvattu onnistuu noin suoraviivaisesti kuitenkin vain, jos kehittäjät tekevät muutokset vuorotellen. 

Toiset kehittäjät voivat  olla julkaisseet uusia muutoksia sillä aikaa kun kehität omiasi. Tällöin versiopolut erkanevat. 

Ennen kuin omat muutokset voidaan viedä yhteiseen repositorioon, on haettava sieltä muiden mahdollisesti tekemät uudet muutokset omaan repositorioon. 

Muiden muutokset on yhdistettävä omiin muutoksiin ja mahdolliset konfliktit ratkottava. Vasta sitten valmis ja testattu lopputulos voidaan viedä yhteiseen repositorioon.

Seuraavassa esimerkissä käydään oman ja muiden kehittäjien muutosten yhdistäminen läpi vaihe vaiheelta: 

```bash
$ git fetch origin          # 1, haetaan muiden tekemät muutokset
$ git merge origin/master   # 2. yhdistetään ne omiin muutoksiin
# ...ratkotaan mahdolliset konfliktit
$ git push origin master    # 3. viedään valmis lopputulos yhteiseen repositorioon
```

ToVaiheet 1 ja 2 (`fetch` ja `merge`) tehdään usein kerralla komennolla `pull`.

```bash
$ git pull origin master
```
Huomaa, että `pull` voi aiheuttaa konflikteja, sillä se tekee myös yhdistämisen. Jos tilanne näyttää liian sekavalta, keskeneräisen yhdistämisen voi peruuttaa komennolla `git merge --abort`. 

## Yhteenvetoa
Jokaisesta loogisesta kokonaisuudesta kannattaa tehdä erillinen talletus. Tällöin muutosten tarkastelu ja käsittely projektissa on mahdollisimman selkeää. 

Talletusten kommentointi on tärkeää projketin kehittäjien välisen kommunikoinnin kannalta. Noudata hyviä kommentointikäytäntöjä. 

Seuraava kuva summaa tyypillisen työnkulun projektissa, jossa noudatetaan keskitettyä mallia. 

![](./assets/centralized_workflow_example.png)

_Lähde: [Chacon S., Straub B, Pro Git, luku 5.](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell) [CC BY-NC-SA 3.0](https://creativecommons.org/licenses/by-nc-sa/3.0/)_

- Alussa kehittäjät kloonaavat yhteisen repositorion. Näin he saavat olemassaolevan koodin työtilaansa ja voivat jatkaa kehitystä.
- Kukin kehittäjä tekee oman työnsä omassa repositoriossaan.
- Ennen omien muutosten julkaisemista kunkin kehittäjän on tuotava omaan repositorioonsa se haara, johon uudet muutokset halutaan viedä.
- Etärepositoriosta saadut muutokset pitää yhdistää omiin muutoksiin. Tuloksena saadaan tallennus, jossa on kaikki tämänhetkiset muutokset.
- Uusi tallennus viedään yhteiseen repositorioon, josta muut kehittäjät puolestaan voivat hakea sen itselleen.

## Harjoitus 6

Harjoitellaan ohjelmiston kehittämistä ja muutosten synkronointia verkkopalvelussa sijaitsevan etärepositorion kanssa. 

_Täydennetään myöhemmin_






