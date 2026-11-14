# Nummirock Kauppa 2.0 – standalone-prototyyppi

Versio 14.11.2026. Keskustelun ja hyväksytyn suunnitelman havainnollistamiseen Jussille, Leealle ja Terolle.

## GitHub Pages -julkaisu

Demo: https://jupanula.github.io/nummirock-kauppa2-proto/

Repositorio: https://github.com/jupanula/nummirock-kauppa2-proto

GitHub Pages tarjoaa tämän hakemiston `index.html`-tiedoston `main`-haaran juuresta. Ei build-vaihetta. Päivitys HTML:ään ja commit julkaisee uuden version Pagesin kautta. Tuotantokauppaa ei kytketä mukaan.

## Vaihtoehtoinen julkaisu omalle palvelimelle

1. Pura ZIP. Siinä on kansio `kauppa2-proto`.
2. Siirrä kansiosta **index.html** palvelimen hakemistoon, joka vastaa osoitetta `https://nummirock.fi/kauppa2-proto/`. README:tä ei tarvita palvelimelle.
3. Avaa osoite selaimessa. Palvelin voi ohjata loppukauttaviivalliseen osoitteeseen. Vaihtoehtoisesti kokeile `https://nummirock.fi/kauppa2-proto/index.html`.
4. Testaa sekä liput että tuotteet yläosan navigaatiosta. Linkit `#liput` ja `#tuotteet` vaihtavat saman HTML:n näkymää.

Tämä on **kokonainen itsenäinen HTML-dokumentti**, ei CMS:n sisältökenttään liitettävä katkelma. Sitä ei liitetä nykyiseen sivupohjaan: muuten pohja voisi ladata oikean Liveto-kaupan. Ei palvelinpuolen asennuksia, npm-paketteja tai build-vaihetta.

Sama HTML voidaan julkaista myös omalla tiedostonimellä, esimerkiksi `/kauppa2-proto.html`. Tässä tapauksessa tiedostonimi näkyy osoitteessa. Jos CMS:n uudelleenohjaus ottaa kansio-osoitteen itselleen, palvelimen ylläpitäjä voi käyttää suoraa HTML-osoitetta tai sallia hakemiston tarjoamisen.

## Mitä proto tekee

- Kaksi Nummirockin näköistä sivunäkymää: Liput ja sijainti sekä Tuotteet.
- Kaksi Liveton API:sta 14.11.2026 luettua lippuvaihtoehtoa tallennettuna esimerkkiaineistona.
- Kaikki nykyisen tuotesivun 10 merch-tuotetta kuvineen, nimineen ja hintoineen.
- Tuotekohtainen lisääminen, plus/miinus, paikallinen yhteenveto ja eri kokojen/värien erilliset rivit. Vaihtoehtojen valinta vaaditaan ennen lisäämistä.
- Vaatevaihtoehdot ovat demoja. Esimerkiksi vuoden 2026 hupparissa LadyFit XS–XL ja Miehet S–5XL.
- Kelluva Ostoskori-nappi näyttää tuotteiden kappalemäärän ja tuotteiden välisumman. Toimituskulu lisätään demokassalla erikseen.
- Nappi siirtää valinnat **simuloituun** Liveto-koriin ja avaa korin suoraan, ilman erillistä siirtopainiketta.
- Korissa voi vain poistaa tuoterivin, ei muuttaa kappalemäärää. Poistaminen poistaa rivin koko määrän. Määrää voi muuttaa palattuaan Nummirockin sivulle.
- Sulkeminen ja poistaminen synkronoivat demokorin ja paikalliset valinnat. Uudelleen avaaminen korvaa demokorin täsmällisellä tilannekuvalla, ei lisää samoja tuotteita uudelleen.
- Demotilaajatiedot, toimitustavan valinta, maksutavan simulointi, epäonnistunut maksu ja tilausvahvistus.
- Onnistunut demotilaus tyhjentää molemmat korit. Epäonnistunut maksu ja pelkkä sulkeminen eivät tyhjennä niitä.
- Valinnat ja varianttivalinnat säilyvät selaimen paikallisessa tallennuksessa. Jos tallennus on estetty, sivu kertoo siitä ja toimii nykyisen sivulatauksen ajan.
- Tuotekuvan suurentaminen modaaliin, responsiivinen mobiilinäkymä sekä näppäimistöllä käytettävät dialogit.

## Olennainen rajaus Livetolle

**Tämä proto näyttää toivotun toiminnan, ei todista sen olevan mahdollinen nykyisellä Liveton rajapinnalla.**

Korin suora avaus, koko korin tilannekuvan korvaaminen, korista poistamisen tiedon välittäminen omalle sivulle sekä onnistuneen tilauksen tapahtuma ovat tässä itse toteutettuja simulaatioita. Liveton ostoskori on tarkoitusta varten mallattu valkoinen modaalinäkymä, ei nykyisen käyttöliittymän täydellinen kopio. Tässä on erotettu korin tarkistus, tilaajatiedot ja maksu omiksi askelikseen selkeyden vuoksi. Liveto voi ehdottaa todelliseen tuotteeseensa sopivaa vastaavaa polkua.

Näytön yläreunassa on **Mitä tässä simuloidaan?** -painike. Se kertoo toiminto kerrallaan nykyisestä tuesta ja puuttuvista vahvistuksista. Sieltä voi myös simuloida siirtovirheen, korin vanhenemisen ja tyhjentää proton valinnat.

Liveton kanssa ratkaistava ennen oikeaa toteutusta:

1. Tuettu tapa siirtää monta erilaista tuotetta määriensä kanssa ja saada luotettavat onnistumis-/virhevastaukset.
2. Olemassa olevan Liveto-korin lukeminen ja yhteensovitus: uudelleenavaus, uudelleenyritys tai määrän pienentäminen ei saa tuplata rivejä. Proto käyttää täyden tilannekuvan korvausta; tämän tukea ei ole vahvistettu.
3. Suora korin/kassan avaava tuettu komento ilman välissä olevaa tapahtuma- tai tuotelistaa, myös kun tuotteita ei lisätä uudestaan.
4. Poistojen, vanhenemisen ja muussa Liveto-näkymässä tehtyjen muutosten palautuminen Nummirockille luotettavasti.
5. Onnistuneen tilauksen luotettava tunnistus. Valintoja ei saa tyhjentää vain siksi, että modaali suljettiin tai maksusivu avattiin.
6. Ajantasaiset hinnat, koko-/mallikohtaiset tuotetunnukset, saatavuus, toimituskulut ja osittain epäonnistunut siirto. Proto ei sisällä oikeaa varastonhallintaa, hinnoittelun tarkistusta tai osittaista siirtokäsittelyä.

Pelkkä peräkkäinen `cart/add` ilman yllä olevia takeita ei toteuta tämän proton synkronointimallia.

## Testaa näin

1. Lisää kaksi tavallista lippua. Tarkista 478 € välisumma.
2. Vaihda Tuotteet-näkymään. Lisää vuoden 2026 huppari, LadyFit XS, ja toinen samaa hupparia koossa M. Paikallisia rivejä on nyt kolme ja kappaleita neljä; tuotteiden summa 608 €.
3. Avaa Ostoskori. Kori avautuu suoraan. Demopaketti 10 € tekee summaksi 618 €.
4. Poista XS-huppari. Sulje kori. XS-rivi puuttuu myös paikallisesta listasta; tuotteet 543 €, 3 kpl.
5. Muuta lipun määrä yhdestä kahteen tai kahdesta yhteen ja avaa kori uudestaan. Määrä vastaa valintaa, ei lisäänny aiemman korin päälle.
6. Päivitä sivu. Paikalliset valinnat säilyvät.
7. Jatka tilaajatietoihin ja paina Täytä demotiedot. Muuta toimitustapaa; maksuyhteenveto päivittyy. Älä käytä oikeita henkilötietoja.
8. Siirry demomaksuun. Simuloi epäonnistunut maksu; valinnat säilyvät. Tee sen jälkeen demotilaus loppuun. Näkyy vahvistus ja molemmat korit tyhjenevät.
9. Palaa sivulle ja päivitä sivu; valinnat ovat edelleen tyhjät.
10. Teknisen selitteen siirtovirhekytkin säilyttää paikalliset valinnat epäonnistuneen avauksen jälkeen. Seuraava avaus onnistuu.

## Aineistot ja ulkoiset pyynnöt

**Ainoa tarvittava paikallinen tiedosto on `index.html`.** Proton toimintalogiikka, tyylit ja tuote-esimerkit ovat sen sisällä. Se ei lataa tuotannon JavaScriptiä, Livetoa, GESTiä, analytiikkaa tai maksupalvelua. Tuotannon yleisiä skriptejä ei tarvita eikä niiden toimintaa sekoiteta protoon.

Ulkoiset visuaaliset aineistot:

- `https://nummirock.fi/2017/fonts.css` – Nummirockin otsikkofontit.
- `https://fonts.googleapis.com/css?family=Anaheim&display=swap` ja sen fonttitiedostot `fonts.gstatic.com`-palvelusta – sama leipätekstifontti kuin nykyisillä sivuilla.
- `https://nummirock.fi/2017/images/Alasivu_tausta_1_2027.jpg` – tausta.
- `https://nummirock.fi/2017/images/Otsikon_grafiikat_Alasivu_1_2027.png` – otsikkologo.
- `https://nummirock.fi/2017/images/otsikko-PVM-levea-2027A.png` – päivämääräkuva.
- Kymmenen tuotekuvaa `https://www.nummirock.fi/2017/images/`-hakemistosta. Täydelliset osoitteet löytyvät HTML:n `catalog`-aineistosta.

Sisällön lähteet 14.11.2026:

- `https://nummirock.fi/tuotteet`
- `https://nummirock.fi/liput_ja_sijainti-kauppa2`
- `https://api.liveto.io/api/v1/events/nummirock-2027/products/`

API:in **ei tehdä kutsua proton käytön aikana**. Näin myöhemmät oikean kaupan muutokset eivät muuta kesken arvioinnin proton esimerkkipolkua. Hinnat ja vaihtoehdot eivät ole julkaistava hinnasto.

Fontit tai kuvat voivat vaihtua tai poistua tuotantopalvelimelta. Internet-yhteys tarvitaan niiden lataamiseen. Paikallisessa esikatselussa palvelimen CORS-asetukset voivat vaikuttaa otsikkofonttiin; samalta Nummirock-verkkotunnukselta tarjottuna tuotantofonttien tulisi toimia tavallisesti. Fontille on varafontti.

## Tallennus ja eristäminen

Paikalliset avaimet ovat `nummirock.kauppa2.proto.v1` ja `nummirock.kauppa2.proto.selection.v1`. Niitä ei jaeta oikean Liveton korin kanssa. Tallennukseen menevät vain tunnettu tuote, demo-vaihtoehdot ja määrä. Tilaajatiedot ovat vain selaimen muistissa ja ne poistetaan modaalin sulkemisen, sivun päivityksen tai onnistuneen tilauksen yhteydessä.

HTML:n Content Security Policy estää verkkoyhteydet `connect-src 'none'` ja lomakelähetykset `form-action 'none'`. Se sallii vain tarvittavat kuva- ja fonttilähteet sekä sivun sisäisen proton koodin ja tyylit. Jos palvelimen oma CSP on tiukempi, se voi estää sisäisen koodin suorittamisen; tällöin palvelimen asetukset pitää sovittaa standalone-protoon.

`noindex,nofollow,noarchive` pyytää hakukoneita jättämään sivun indeksoimatta, mutta osoite ei ole salainen tai pääsynhallinnalla suojattu.

## Varmistus 14.11.2026

Selaimessa kokeiltu: lippujen lisääminen ja määrän muutos, eri vaatekokojen erilliset rivit, poiston synkronointi, toistuva korin avaus ilman tuplaamista, toimitusmaksun muutos, maksun epäonnistuminen, onnistunut demotilaus ja tyhjän korin säilyminen päivityksen jälkeen. Tarkistettu myös mobiilinäkymä 390 px leveydellä, tyhjän korin näkymä ja simuloitu siirtovirhe. JavaScriptin syntaksi tarkistettu.

Proto ei ole palvelimelle julkaistu tuotantointegraatio. Varsinainen Liveto-yhteys tehdään vasta tuettujen ohjeiden ja yhteisen hyväksynnän perusteella.
