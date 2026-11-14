# Nummirock Kauppa 2.0 – toiminnallinen prototyyppi

Versio **14.11.2026 / 2**. Täysin simuloitu kauppa; ei Liveto-yhteyttä, oikeita varauksia tai maksuja.

- **Demo:** https://jupanula.github.io/nummirock-kauppa2-proto/
- **Repositorio:** https://github.com/jupanula/nummirock-kauppa2-proto
- GitHub Pages: `main`, `/ (root)`, `.nojekyll`. HTML ja toiminta yhdessä `index.html`-tiedostossa.

## Tämän version muutokset

- Poistettu erillinen ”Valitut tuotteet” -osio. Tuotekohtaiset määräsäätimet ja kelluva Ostoskori riittävät.
- Poistettu lippusivun ”Juhannuksen raskain kyläjuhla” -teksti.
- Lisätty kolme tavallista **havainnelippua**: 4 päivän ennakko 259 €, 2 päivää TO–PE 199 € ja 2 päivää PE–LA 199 €. Tuotteita tai hintoja ei ole vahvistettu oikeaan kauppaan. Ne on merkitty demoiksi myös kassalla.
- Kassalla luetellaan jokainen valittu tuotevariantti ja määrä. Liput ja merch ryhmitellään Nummirock 2027 / Nummirock shop -otsikoiden alle. Saman vaatteen eri koot näkyvät eri riveillä.
- Korvattu aiempi kolmivaiheinen oma kassapolku käyttäjän toimittamia nykyisen Liveton kuvakaappauksia mukailevalla **yhdellä kassasivulla**. Desktopissa tilaaja, kori ja maksutiedot kolmessa palstassa. Mobiilissa samat osuudet peräkkäin. Jokainen tuoterivi on vieritettävissä näkyviin.
- Punainen yläpalkki, Tapahtumat-/kieli-/sulkemiskuvakkeet, alareunan Kauppiaan tiedot / Liveto sekä lomakkeet, korin tyhjennys ja maksuyhteenveto mukailevat kuvakaappauksia. Tapahtumat-painike palauttaa tässä protossa Nummirockin tuotevalintoihin; kielikuvake on koriste, proto on suomeksi.

## Toimintamalli

1. Valitse liput ja merch Nummirockin kahdesta sivunäkymästä. Vaatteen koko, malli tai väri on valittava ensin. Plus/miinus säätää vain paikallista valintaa.
2. Kelluva Ostoskori näyttää yhteisen kappalemäärän ja tuotteiden välisumman. Toimitus ja valinnainen tekstiviestimaksu eivät sisälly napin summaan.
3. Nappi siirtää paikallisten valintojen täsmällisen tilannekuvan **demokoriin** ja avaa suoraan yhteisen kassasivun. Uusi avaus ei lisää samoja tuotteita vanhojen määrien päälle.
4. Kassalla voi poistaa kokonaisen tuoterivin tai tyhjentää korin. Määräsäätimiä ei ole, kuten Leean kuvaamassa nykyisessä Liveton kassassa. Määrää muutetaan palaamalla Nummirockin sivulle.
5. Poistaminen päivittää myös paikalliset valinnat. Määrän muutos omalla sivulla korvaa demokorin määrän seuraavalla avauksella.
6. Tilaajatiedot, maksutavan valinta ja maksettava summa näkyvät samalla kassasivulla. ”Täytä demotiedot” täyttää pakolliset kentät. Demokäyttöehdot merkitään erikseen. Maksunappi aktivoituu vasta, kun tiedot ja maksutapa ovat kunnossa ja korissa on tuotteita.
7. Onnistunut demotilaus tyhjentää molemmat korit. Keskeyttäminen, pelkkä sulkeminen ja maksuvirhe eivät tyhjennä niitä.

## Tuotteet, hinnat ja erittelyt

Kaksi #OISPANUMMI3-lippua perustuvat Liveton julkisen API:n tilanteeseen 14.11.2026. Kolme muuta lippua ovat kuvitteellisia tulevaa valikoimaa havainnollistavia esimerkkejä. Kaikki nykyisen Nummirockin tuotesivun 10 merch-tuotetta ovat mukana kuvineen, nimineen ja hintoineen. Koko-/väri-/mallivaihtoehdot ovat vahvistamattomia demoja, eivät varastosaldoja. Esimerkiksi 2026-hupparin mallivalinta vaihtaa kokoja: Miehet S–5XL / LadyFit XS–XL.

Lipun 1,50 € palvelumaksu esitetään omana rivinään vähentämällä se ensin tuotteiden välisummasta; **sitä ei lisätä hintaan toistamiseen**. Merch-palvelumaksuja ei tässä demossa mallinneta. Demotoimitus: nouto 0 €, kirje 5 € tai paketti 10 €. Tekstiviestivalinta lisää 1 €. Toimitustapojen soveltuvuutta tuotteille ei ole vahvistettu. ALV-sarake mukailee nykyistä käyttöliittymää, mutta näyttää viivan: oikeaa veroerittelyä ei ole mallinnettu.

Maksutavat ovat simuloituja pankki-/korttivalintoja ilman pankki- tai korttitietojen kysymistä. Etukoodi `DEMO` näyttää esimerkkikoodin käytön mutta ei muuta hintaa. Uutiskirjevalinta ei tilaa mitään. Kirja ei kuulu tähän protoon eikä sen GEST-myynti muutu.

## Livetolta edelleen tarvittava tuki

**Toimiva demo ei vahvista oikean Liveto-rajapinnan tukea.** Käyttöliittymän nykyistä ulkoasua on jäljitelty, mutta alla olevat toiminnallisuudet on simuloitu itse:

1. Monen erilaisen tuotteen ja määrän luotettava siirto sekä yksiselitteinen onnistumis-/virhekuittaus.
2. Olemassa olevan korin lukeminen ja yhteensovitus ilman tuplaamista. Proto korvaa koko demokorin täsmällisellä tilannekuvalla; tämän tukea ei ole vahvistettu.
3. Suora avaus olemassa olevaan koriin/kassaan ilman uuden tuotteen lisäämistä tai tapahtumalistan kautta kiertämistä. Leea kertoi tämän olevan työlistalla.
4. Poistojen ja vanhenemisen palautuminen omalle sivulle luotettavasti.
5. Onnistuneen tilauksen tapahtuma paikallisten valintojen tyhjentämiseen. Pelkkä sulkeminen tai maksusivulle siirtyminen ei riitä.
6. Oikeat hinnat, saatavuus, tuotekohtaiset kokotunnukset, toimitusmaksut ja osittain epäonnistuneen siirron käsittely.

Tekninen selite sivun yläreunassa avaa nämä rajaukset ja sisältää siirtovirheen, korin vanhenemisen ja proton tyhjennyksen kokeilut.

## Testaus

- Lisää kaksi tavallista #OISPANUMMI3-lippua, yksi Premium ja yksi 2 päivän havainnelippu. Lisää M- ja L-kokoiset 40v-hupparit ja kaulanauha. Kassalla pitää olla **6 tuoteriviä, 7 kappaletta**.
- Tuotteiden yhteishinta 1 091 €. Erittely: tuotteet 1 085 € + palvelumaksut 6 €. Demopaketin kanssa maksettavaksi 1 101 €. Tekstiviestin kanssa 1 102 €.
- Poista M-huppari. Jäljellä 5 riviä, 6 kappaletta, maksettavaksi tekstiviestin ja paketin kanssa 1 047 €.
- Sulje modaali: tuotteen poistuminen näkyy sen omalla sivulla. Muuta määriä ja avaa kori uudelleen; määrät eivät summaudu vanhojen päälle.
- Täytä demotiedot, merkitse demokäyttöehdot ja valitse demomaksutapa. Kokeile maksuvirhettä ja sen jälkeen onnistunutta demotilausta. Vain onnistuminen tyhjentää korit.
- Tarkista mobiilissa tilaajatiedot, niiden jälkeen kaikki koririvit, sitten maksutiedot ja yhteenveto samalla vieritettävällä sivulla.

## Tiedostot ja aineistolähteet

`index.html` sisältää toimintalogiikan, tyylit ja tallennetun tuoteaineiston. `README.md` on tämä ohje, `.nojekyll` estää sivusisällön Jekyll-käsittelyn. Ei npm- tai palvelinasennuksia. Sivu voidaan tarjota myös muulta staattisen HTML:n palvelimelta; sitä ei liitetä Nummirockin nykyiseen CMS-sivupohjaan.

Kuvat ladataan suoraan tuotantopalvelimelta. Nummirockin alkuperäinen otsikkofontti on kopioitu tuotantosivulta tiedostoon `nummirock-heading.woff` ja tarjoillaan proton omalta verkkotunnukselta, jotta selaimen CORS-rajoitus ei vaihda otsikoita varafonttiin. Otsikko-, leipäteksti- ja merch-koot vastaavat tuotantosivujen CSS-määrityksiä. Anaheim ladataan Google Fontsista kuten nykyisillä sivuilla. Internet-yhteys tarvitaan niihin. Proton toiminta ei lataa tuotannon yleisiä skriptejä, oikeaa Livetoa, GESTiä, analytiikkaa tai maksupalvelua.

- Otsikkofontin lähde: `https://nummirock.fi/2017/fonts/nummirockonethreecustomthre-webfont.woff` (proton mukana `nummirock-heading.woff`).
- `https://fonts.googleapis.com/css?family=Anaheim&display=swap`
- `https://nummirock.fi/2017/images/Alasivu_tausta_1_2027.jpg`
- `https://nummirock.fi/2017/images/Otsikon_grafiikat_Alasivu_1_2027.png`
- `https://nummirock.fi/2017/images/otsikko-PVM-levea-2027A.png`
- Tuotekuvat: tarkat URL:t HTML:n `catalog`-aineistossa, `https://www.nummirock.fi/2017/images/`.
- Tuotetietojen lähteet: `https://nummirock.fi/tuotteet` ja `https://api.liveto.io/api/v1/events/nummirock-2027/products/`, tilanne 14.11.2026.

API:in ei tehdä kutsuja käytön aikana. Paikallinen tallennus käyttää vain avaimia `nummirock.kauppa2.proto.v1` ja `nummirock.kauppa2.proto.selection.v1`; tuotannon tai Liveton tallennusavaimiin ei kosketa. Tallennukseen menevät tunnetut tuotteet, määrät ja demo-vaihtoehdot. Tilaajatiedot ovat vain muistissa ja tyhjentyvät suljettaessa modaali, päivitettäessä sivu tai tilauksen valmistuessa.

Content Security Policy estää yhteyskutsut (`connect-src 'none'`) ja lomakelähetykset (`form-action 'none'`). `noindex` pyytää hakukoneita jättämään proton indeksoimatta; demo ja lähdekoodi ovat julkisia.
