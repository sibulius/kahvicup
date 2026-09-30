# Kahvicup

Kahvicup on [Obsidianilla](https://obsidian.md) luotu, markdown-tiedostoihin pohjautuva seuran hallintatyökalu. Projekti sisältää valmiit mallipohjat (templates) ja esimerkkitiedostot, joiden avulla seuran, joukkueiden, pelaajien, huoltajien, toimihenkilöiden ja sarjojen tiedot voi koota yhteen tietokantamaiseen kirjastoon (vaultiin).

Kaikki tieto on tavallisia tekstitiedostoja. Tiedot eivät ole sidottuina mihinkään tiettyyn palveluun, ja ne ovat luettavissa ja muokattavissa millä tahansa tekstieditorilla.

## Sisällys

1. [Ideana](#ideana)
2. [Ominaisuudet](#ominaisuudet)
3. [Aloitus](#aloitus)
4. [Kansiorakenne](#kansiorakenne)
5. [Tietotyypit ja kentät](#tietotyypit-ja-kentät)
6. [Tietotyyppien väliset linkit](#tietotyyppien-väliset-linkit)
7. [Uuden tiedon lisääminen](#uuden-tiedon-lisääminen)
8. [Tietojen hyödyntäminen](#tietojen-hyödyntäminen)
9. [Obsidian-asetukset](#obsidian-asetukset)
10. [Versionhallinta (Git)](#versionhallinta-git)
11. [Nimeämiskäytännöt](#nimeämiskäytännöt)
12. [Tunnetut huomiot ja jatkokehitys](#tunnetut-huomiot-ja-jatkokehitys)

## Ideana

Jokainen asia (pelaaja, joukkue, seura jne.) on oma markdown-tiedostonsa. Tiedoston alussa on **YAML frontmatter** eli rajattu tietoalue, joka sisältää asian rakenteiset tiedot:

```yaml
---
tyyppi: pelaaja
etunimi: Milla
sukunimi: Mallila
lempinimi: Maltsu
syntymäaika: 2014-01-01
joukkueet:
  - "[[Mallilan Pallo T13]]"
tags:
  - naiset
---
```

Tiedostot linkitetään toisiinsa Obsidianin `[[wikilinkeillä]]`. Näin pelaaja tietää joukkueensa, joukkue seuransa ja huoltaja lapsensa. Obsidian rakentaa linkeistä automaattisesti taustalinkit (backlinks) ja verkkonäkymän.

`tyyppi`-kenttä kertoo, minkä tyyppisestä tiedosta on kyse. Sen avulla tiedostot voi suodattaa ja listata esimerkiksi Bases-näkymissä.

## Ominaisuudet

- Valmiit mallipohjat kaikille keskeisille tietotyypeille.
- Esimerkkitiedostot, joista näkee, miten kentät täytetään ja linkitetään.
- Ominaisuuksien tyypit (päivämäärä, lista, valintaruutu) on määritelty valmiiksi, joten Obsidianin ominaisuuspaneeli näyttää kentät oikein.
- Toimii ilman ulkoisia lisäosia: käytössä vain Obsidianin omat ydinosat.
- Tietojen siirrettävyys: pelkkiä tekstitiedostoja, jotka sopivat Git-versionhallintaan.
- Toimii sekä tietokoneella että mobiilissa Obsidian-sovelluksessa.

## Aloitus

1. **Asenna Obsidian** osoitteesta <https://obsidian.md>.
2. **Hae projekti koneelle**:
   - lataa zip-tiedostona GitHubista (Code → Download ZIP) ja pura se, tai
   - kloonaa Gitillä: `git clone https://github.com/sibulius/kahvicup.git`
3. **Avaa kansio vaultina**: Obsidian → *Open folder as vault* → valitse `kahvicup`-kansio.
4. Jos Obsidian kysyy luottamusta vaultiin, valitse *Trust author and enable plugins*. Projekti ei vaadi yhteisölisäosia, joten valinta ei ole kriittinen.
5. Tutustu `01 Hallinta` -kansion esimerkkitiedostoihin ja kokeile luoda oma tiedosto pohjasta.
6. Kun olet valmis aloittamaan oikean käytön, korvaa tai poista mallitiedostot (esim. "Milla Mallila", "Mallilan Pallo Ry") ja lisää omat tietosi.

## Kansiorakenne

```
kahvicup/
├── .obsidian/             Obsidianin asetukset (osa versionhallinnassa)
├── 01 Hallinta/           Varsinaiset tiedot
│   ├── Joukkueet/
│   ├── Kaudet/
│   ├── Pelaajat/
│   ├── Sarjat/
│   ├── Seurat/
│   ├── Toimihenkilöt/
│   ├── Vanhemmat/
│   └── Yhteyshenkilöt/
├── 99 Pohjat/             Mallipohjat uusille tiedostoille
├── .gitignore
└── README.md
```

Kansioiden numerointi (`01`, `99`) pitää ne haluttussa järjestyksessä tiedostoselaimessa. Numeroiden väliin jää tilaa uusille kansioille, esimerkiksi `02 Turnaukset` tai `03 Raportit`.

## Tietotyypit ja kentät

Jokaisella tyypillä on oma pohja `99 Pohjat` -kansiossa (tiedostonimi alkaa alaviivalla). Alla olevissa taulukoissa on pohjien kentät.

### Seura (`tyyppi: seura`)

| Kenttä | Kuvaus | Esimerkki |
|---|---|---|
| `y_tunnus` | Y-tunnus | `1234567-8` |
| `nimi` | Seuran nimi | `Mallilan Pallo Ry` |
| `kotipaikka` | Kotipaikkakunta | `Mallila` |
| `katuosoite` | Katuosoite | `Mallipolku 1` |
| `postinumero` | Postinumero (lainausmerkeissä) | `"90100"` |
| `toimipaikka` | Postitoimipaikka | `Mallila` |
| `www` | Kotisivut | `http://www.mallilanps.fi` |
| `email` | Sähköposti | `info@mallilanps.fi` |
| `puhelin` | Puhelinnumero | `040-12345678` |
| `tags` | Tunnisteet, esim. laji | `jalkapallo` |

### Joukkue (`tyyppi: joukkue`)

| Kenttä | Kuvaus | Esimerkki |
|---|---|---|
| `nimi` | Joukkueen nimi | `Mallilan Pallo T13` |
| `seura` | Linkki seuraan | `"[[Mallilan Pallo Ry]]"` |
| `ikäluokka` | Syntymävuosi tai ikäluokka | `2014` |
| `tags` | Tunnisteet, esim. sukupuoli | `naiset` |

### Pelaaja (`tyyppi: pelaaja`)

| Kenttä | Kuvaus | Esimerkki |
|---|---|---|
| `etunimi` | Etunimi | `Milla` |
| `sukunimi` | Sukunimi | `Mallila` |
| `lempinimi` | Lempinimi | `Maltsu` |
| `syntymäaika` | Päivämäärä muodossa VVVV-KK-PP | `2014-01-01` |
| `joukkueet` | Lista linkkejä joukkueisiin | `- "[[Mallilan Pallo T13]]"` |
| `tags` | Tunnisteet | `naiset` |

### Vanhempi / huoltaja (`tyyppi: vanhempi`)

| Kenttä | Kuvaus | Esimerkki |
|---|---|---|
| `etunimi`, `sukunimi` | Nimi | `Minja`, `Mallila` |
| `puhelin` | Puhelinnumero | `040-3456789` |
| `email` | Sähköposti | `minja@mallila.fi` |
| `pelaajat` | Lista linkkejä pelaajiin | `- "[[Mallila Milla]]"` |
| `tags` | Tunnisteet | |

### Toimihenkilö (`tyyppi: toimihenkilö`)

| Kenttä | Kuvaus | Esimerkki |
|---|---|---|
| `etunimi`, `sukunimi` | Nimi | `Veikko`, `Vastuullinen` |
| `puhelin`, `email` | Yhteystiedot | |
| `roolit` | Lista rooleista | `Vastuuvalmentaja` |
| `joukkueet` | Lista linkkejä joukkueisiin | `- "[[Mallilan Pallo T13]]"` |
| `tags` | Esim. koulutus | `UEFA-C` |

### Yhteyshenkilö (`tyyppi: yhteyshenkilö`)

Ulkopuolinen yhteyshenkilö, esimerkiksi sarjan vastaava.

| Kenttä | Kuvaus | Esimerkki |
|---|---|---|
| `etunimi`, `sukunimi` | Nimi | `Tuukka`, `Turnee` |
| `puhelin`, `email` | Yhteystiedot | |
| `tags` | Rooli tai tehtävä | `sarjavastaava` |

### Sarja (`tyyppi: sarja`)

| Kenttä | Kuvaus | Esimerkki |
|---|---|---|
| `nimi` | Sarjan nimi | `Talviliiga` |
| `virallinen` | Onko virallinen sarja (`true`/`false`) | `false` |
| `www` | Sarjan kotisivut | |
| `yhteyshenkilöt` | Lista linkkejä yhteyshenkilöihin | `- "[[Turnee Tuukka]]"` |

### Kausi (`tyyppi: kausi`)

| Kenttä | Kuvaus | Esimerkki |
|---|---|---|
| `alkupäivä` | Kauden ensimmäinen päivä | `2026-11-01` |
| `loppupäivä` | Kauden viimeinen päivä | `2027-10-31` |

## Tietotyyppien väliset linkit

```
Seura ◄────── Joukkue ◄────── Pelaaja ◄────── Vanhempi
                  ▲
                  └────────── Toimihenkilö

Sarja ──────► Yhteyshenkilö

Kausi (erillinen)
```

- **Joukkue → Seura**: kentässä `seura`.
- **Pelaaja → Joukkue**: kentässä `joukkueet`. Pelaaja voi kuulua useaan joukkueeseen.
- **Toimihenkilö → Joukkue**: kentässä `joukkueet`.
- **Vanhempi → Pelaaja**: kentässä `pelaajat`. Samalla vanhemmalla voi olla useita lapsia.
- **Sarja → Yhteyshenkilö**: kentässä `yhteyshenkilöt`.

Linkit kirjoitetaan frontmatteriin aina lainausmerkeissä: `"[[Tiedoston nimi]]"`. Ilman lainausmerkkejä YAML tulkitsee hakasulkeet väärin.

## Uuden tiedon lisääminen

1. Luo uusi tyhjä muistio oikeaan alikansioon (esim. `01 Hallinta/Pelaajat`).
2. Anna tiedostolle nimi. Suositus: `Sukunimi Etunimi`, jolloin tiedostot menevät aakkosjärjestykseen sukunimen mukaan.
3. Lisää pohja: komentopaletti (`Ctrl/Cmd + P`) → **Templates: Insert template** → valitse esim. `_Pelaaja`.
4. Täytä kentät. Ominaisuuspaneelissa (Properties) kentät näkyvät lomakkeena, ja raakamuodossa ne voi muokata kirjoittamalla.
5. Linkitä toisiin tiedostoihin kirjoittamalla `[[` ja valitsemalla ehdotuksista tiedosto.

**Esimerkki: uusi pelaaja**

Luo tiedosto `01 Hallinta/Pelaajat/Virtanen Ville.md`, lisää pohja `_Pelaaja` ja täytä:

```yaml
---
tyyppi: pelaaja
etunimi: Ville
sukunimi: Virtanen
lempinimi: Ville
syntymäaika: 2013-05-20
joukkueet:
  - "[[Mallilan Pallo T13]]"
tags:
  - miehet
---
```

## Tietojen hyödyntäminen

Koska kaikilla tiedoilla on yhteinen rakenne, niitä voi koota yhteen näkymään:

- **Bases** (Obsidianin ydinosa, käytössä tässä vaultissa): luo taulukkonäkymä, joka listaa esimerkiksi kaikki tiedostot, joiden `tyyppi` on `pelaaja`, ja näyttää niiden nimen, syntymäajan ja joukkueen.
- **Haku** (`Ctrl/Cmd + Shift + F`): esimerkiksi haku `[tyyppi:pelaaja]` listaa kaikki pelaajat.
- **Taustalinkit**: avaa joukkue ja katso taustalinkkipaneelista, mitkä pelaajat ja toimihenkilöt siihen kuuluvat.
- **Verkkonäkymä**: hahmottaa, miten seura, joukkueet ja henkilöt liittyvät toisiinsa.
- **Dataview-lisäosa** (valinnainen): mahdollistaa kyselyt ja ominaisuuksien näyttämisen leipätekstissä, esim. `` `= this.etunimi` ``.

## Obsidian-asetukset

Versionhallinnassa olevat asetukset `.obsidian`-kansiossa:

| Tiedosto | Sisältö |
|---|---|
| `templates.json` | Mallipohjakansioksi on asetettu `99 Pohjat`. |
| `types.json` | Ominaisuuksien tyypit, esim. `syntymäaika` (päivämäärä), `joukkueet` (lista), `virallinen` (valintaruutu). |
| `core-plugins.json` | Käytössä olevat ydinosat: mm. tiedostoselain, haku, verkkonäkymä, taustalinkit, ominaisuudet, mallipohjat, Bases, Sync. |
| `app.json`, `appearance.json` | Oletusasetukset (tyhjät). |

## Versionhallinta (Git)

Projektia voi käyttää Gitin kanssa, jolloin muutoshistoria säilyy ja vaultin voi jakaa usean käyttäjän kesken.

`.gitignore` jättää pois käyttäjäkohtaiset työtilatiedostot, jotka muuttuvat jatkuvasti ja aiheuttaisivat turhia konflikteja:

```
.obsidian/workspace.json
.obsidian/workspace-mobile.json
```

**Käytännön vinkkejä:**

- Commitoi pienissä erissä ja kirjoita selkeä kuvaus (esim. "Lisää pelaaja Virtanen Ville").
- Jos useampi henkilö muokkaa samaa vaultia, hae muutokset (`git pull`) ennen työn aloittamista.
- **Älä tallenna arkaluonteisia henkilötietoja julkiseen repositorioon.** Pelaajien ja huoltajien nimet, syntymäajat ja yhteystiedot ovat henkilötietoja. Käytä oikeaa dataa vain yksityisessä repositoriossa ja huomioi tietosuojalainsäädäntö (GDPR). Tässä repositoriossa olevat tiedot ovat pelkkiä esimerkkejä.

## Nimeämiskäytännöt

- **Tiedostonimet**: henkilöillä `Sukunimi Etunimi`, joukkueilla seuran ja ikäluokan mukaan (`Mallilan Pallo T13`), kausilla `Kausi VVVV-VVVV`.
- **Pohjat**: alkavat alaviivalla (`_Pelaaja`), jotta ne erottuvat muista tiedostoista.
- **Kentät**: pienillä kirjaimilla, välilyönnin sijaan alaviiva (`y_tunnus`). Vältä välilyöntejä kenttien nimissä, koska ne voivat aiheuttaa ongelmia kyselyissä.
- **Päivämäärät**: muodossa `VVVV-KK-PP`.
- **Listat**: kentät, joihin voi tulla useita arvoja (`joukkueet`, `roolit`, `pelaajat`), kirjoitetaan aina listana.

## Tunnetut huomiot ja jatkokehitys

Huomioita nykyisestä tilasta:

- Kansioissa `Seurat` ja `Toimihenkilöt` on tyhjät `Nimetön.md`-tiedostot, jotka voi poistaa.
- Tiedosto `Pelaajat/Milla Mallila.md` on vanhentunut esimerkki: siitä puuttuu `tyyppi`-kenttä, eikä sitä ole täytetty. Varsinainen esimerkki on `Mallila Milla.md`. Tiedoston voi poistaa.
- `types.json` sisältää sekä `ikäryhmä`- että `ikäluokka`-kentän. Pohjissa käytetään vain `ikäluokka`-kenttää, joten kenttien nimet kannattaa yhtenäistää.
- Pohjissa ei ole vielä tietoa esimerkiksi pelinumerosta, pelipaikasta tai jalkaisuudesta.

Ideoita jatkokehitykseen:

- Turnaus- ja ottelutiedot omina tietotyyppeinään (`02 Turnaukset`).
- Ilmoittautumiset: joukkue → turnaus -linkitys ja kausi linkiksi.
- Bases-näkymät valmiiksi: pelaajalista joukkueittain, toimihenkilöiden yhteystiedot, huoltajat lapsineen.
- Pohjien laajentaminen (pelinumero, pelipaikka, jalkaisuus, terveystiedot tms.).
- Dataview-pohjainen näkymä, joka näyttää tiedot luettavana tekstinä.

## Lisenssi

Lisenssiä ei ole vielä määritelty. Lisää tähän haluamasi lisenssi (esim. MIT) ja tarvittaessa `LICENSE`-tiedosto juureen.
