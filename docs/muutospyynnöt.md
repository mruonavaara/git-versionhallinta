# Yhdistämispyynnöt

## Johdanto

Git-palvelut tarjoavat toiminnallisuutta, jossa Git-repositorihin voi tehdä __yhdistämispyyntöjä__ (_pull request_, _merge request_). Yhdistämispyyntö on ehdotus repositorion ylläpitäjille yhdistää pyynnön tekijän laatimat muutokset repositorion johonkin haaraan.

Yhdistämispyyntöihin voidaan liittää tietoja muutoksesta, kehittäjät voivat keskustella siitä, yhdistämispyyntöä voidaan jatkokehittää, ja muutospyynnöille voidaan määrittää katselmointityönkulkuja. 

Kaikki Git-palvelut tarjoavat samanlaisen toiminnallisuuden. Tässä materiaalissa eismerkkinä käytetään GitHub-palvelun yhdistämispyyntöjä.

## Yhdistämispyynnön tekeminen  

Pyynnön oleelliset tiedot ovat:

- mistä repositoriosta ja haarasta muutoksia ehdotetaan 
- mihin repositorioon ja haaraan ne haluttaisiin mukaan
- muutoksen otsikko ja kuvaus

Kun yhdistämispyyntöjä tehdään repositorion sisällä, tavallisin tapa on tehdä ehdotettu muutos omaan ominaisuushaaraansa. Kohdehaara on jokin projektissa sovittu yhteinen haara.  Muutospyynnölle annetaan otsikko, jolla se esitetään listauksissa, ja sille annetaan pyynnön käsittelijöitä varten kuvaus, mikä muutos on ja miksi sitä ehdotetaan.

Seuraavassa esimerkissä tehdään yhdistämispyyntö GitHub-palvelussa:

Ensin ehdotettava muutos on tehtävä paikallisesti. Sille tehdään ominaisuushaara ja viedään muutokset siihen. Ominaisuushaara viedään etärepositorioon GitHub-palvelussa, jotta sille voidaan tehdä yhdistämispyyntö.

```
git switch -c muutospyynnot
git add .
git commit -m "Lisää luku muutospyynnöistä"
git push -u origin muutospyynnot
```

Kun haara näkyy etärepositoriossa, yhdistämispyyntö voidaan tehdä GitHubin web-käyttöliittymässä.



## Forking

Yhdistämispyyntöjä voidaan tehdä yhden repositorion sisällä tai eri repositorioiden kesken. 
