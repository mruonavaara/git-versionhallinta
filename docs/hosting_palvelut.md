# Git-hosting-palvelut

Git-hosting tarkoittaa repositorytilan ja Git-palvelujen tarjoamista verkossa käytettäväksi. 

Git-hosting voidaan tehdä yrityksen omilla palvelimilla (_self hosting_) tai internet-palveluntarjoajan palvelimilla (_cloud hosting_). 

Käytetyimmät palvelut ovat
- GitHub (https://github.com/)
- Bitbucket (https://bitbucket.org/)
- GitLab (https://gitlab.com/)

# Palvelujen käyttö

Kuten muissakin online-palveluissa, käyttäjien on avattava tili palvelussa. 
Tilille voi perustaa useita repositorioita (projekteja).

Palvelussa oleva reposiotorio toimii kehittäjän etärepositoriona. Palvelussa olevan etärepositorion kautta kehittäjä voi jakaa oman työnsä  muille, ja vastaavasti saada muiden kehittäjien tekemiä muutoksia omaan paikalliseen repositorioonsa.

Kirjautumisten helpottamiseksi palveluihin voi tallettaa SSH-salausavaimen, jolloin liikennöinti repositoryjen kanssa tapahtuu SSH-protokollalla ilman erillistä kirjautumista.

Palvelut tarjoavat Git-toiminnallisuuden ja talletustilan lisäksi mm.
- Projektin jäsenten käsittelyn (_collaborators_)
- Vikaraportoinnin (_issue and bug tracking_)
- Projektinhallintatoiminnallisuutta (_agile boards_)

Ilmaisella tilillä on mahdollista toteuttaa pieniä projekteja. Maksullisilla tilauksilla saadaan suurempien projektien toteuttamiseen tarvittavia palveluja.

## Repositoryjen luominen palveluun

Repositorioita voi luoda palvelun web-käyttöliittymässä. Osa palveluista tukee myös repositoryn perustamista suoraan push-operaatiolla

Repositorioihin voidaan lisätä jäseniä (collaborator), ja heille voidaan antaa erilaisia oikeuksia, esim. guest, reporter, developer, maintainer

Erilaisia toimintoja ja asetuksia on runsaasti, esim. notifikaatioita, automaattisia toimintoja (hooks)

Perehdy palveluntarjoajasi ohjeisiin. Kaikilla suurilla palveluilla on erinomainen dokumentaatio.

## README ja Markdown

Palvelut esittävät README-nimisen tiedoston repositoryn etusivulla. Yleensä siitä tehdään projektin kotisivu. README kirjoitetaan Markdown-kielellä. 

Markdown on yksinkertainen merkkauskieli, katso esim. https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet

Koodieditoreihin on saatavana Markdown tukilaajennuksia, esim. esikatselu

Markdownia käytetään usein projektien dokumentointiin, sillä siten saadaan dokumentaatiollekin samanlainen versionhallinta kuin koodille.

![](./assets/vscode_md_preview.png)

