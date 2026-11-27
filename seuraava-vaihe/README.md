# Nummirock × Liveto — seuraava vaihe

27.11.2026. Erillinen toteutuskelpoisen toimintamallin simulaatio; alkuperäinen tavoitemalli säilyy repositorion juuressa muuttumattomana.

## Vastuut

- Nummirock esittelee liput ja tuotteet. Painike avaa tapahtuman liput tai tuotteet Liveton kaupassa.
- Liveto hoitaa tuotevaihtoehdot, määrän valinnan, yhteisen korin, poistamisen, tilaajatiedot ja maksamisen.
- Nummirockilla ei ole paikallista koria, korimäärää, summaa tai korien synkronointia.
- Avaa kauppa näkyy aina. Keskeneräiseen koriin palataan kaupan oman korivalikon kautta; erillistä open/checkout-komentoa ei oleteta.
- Kassalla ei ole määräsäätimiä. Lisääminen tapahtuu kaupan tuoteluettelossa. Vähentäminen: poista rivi ja lisää haluttu määrä uudelleen.

## Simulaatio

Ei Liveton skriptiä, API-kutsuja, oikeita tilauksia, varauksia tai maksuja. Ulkoiset kuvat tulevat Nummirockilta; Anaheim Google Fontsista ja otsikkofontti repositorion juuresta. Tuoteaineisto perustuu aiemman proton 14.11.2026 tilannekuvaan. Valikoima, hinnat, koot ja 10 € toimitusmaksu eivät vahvista nykyistä tuotantokauppaa. Tuotekohtaiset Nummirockin painikkeet avaavat tuotevalikoiman, eivät lupaa tuotekohtaista Liveto-syvälinkkiä.

Demon maksupalvelu on samassa ikkunassa; oikeassa Livetossa se avautuu uuteen välilehteen. Keskeytetty maksu jättää tilauksen lukittuun pending-tilaan. Jatkaminen, peruminen ja onnistuminen on mallinnettu. Menestyksekäs demomaksu tyhjentää vain Liveton demokorin. Analytiikkaevästeitä ei tarvita toimintamalliin.

Koritila tallentuu vain tämän demon sessionStorage-avaimeen `nummirock.kauppa2.next.v1`. Henkilötietoja ei tallenneta. Varaus vanhenee 15 minuutin kuluttua viime muutoksesta, paitsi kesken maksamisen. Sivun yläreunan selitteestä voi nollata demon tai simuloida vanhenemista.

Toimitusmaksu on erillinen tuote. Merch-tuotteet jäävät koriin, vaikka toimitusmaksu puuttuu; maksu estetään kunnes se lisätään. Todellinen vaatimus ja käyttöliittymä asetetaan ja testataan Livetossa.

## Seuraavaksi

1. Tero ja Leea arvioivat toimintamallin sekä myyntiin tulevat tuotteet.
2. Leea toimittaa sandbox-kaupan, testituotteet ja ympäristökohtaiset API- ja upotusosoitteet.
3. Vahvistetaan varianttitunnisteet, kapasiteetit, toimitusmaksun vaatimussääntö, tilaajatietolomake ja visut.
4. Testataan oikea upotus ja maksut sandboxissa. Säilytetään 1.0 tuotannossa hyväksyntään asti.
5. Päätetään aikataulu ja tuotantoon vienti. Tässä muutoksessa ei julkaista oikeaa kauppaa.

Lähde: Liveton tekninen vastausdokumentti 24.11.2026 sekä Leean tarkennus 27.11.2026. Puuttuvat komennot ovat kehitysehdotuksia ilman toteutus- tai aikataululupausta. Tämä proto ei todenna Liveton tuotantotoimintaa.

## Päivitys 27.11.2026: lippusivu ja kuvaviite

- Kelluva **Osta liput** vie proton kaikista sivunäkymistä `#liput`-näkymän lippuosioon. Liveto avataan sen omista ostopainikkeista.
- Liveton lippulista on ensisijainen; Tiketti ja Epassi/Edenred/Zevoy/Wolt Benefits esitellään erillisessä alemmassa osiossa. Logot linkitetään Tiketin julkisiin aineistoihin. Maksutapaehdot: https://www.tiketti.fi/info/kulttuuriedut .
- Lippujen käyttöohjeet sekä sijainti, karttalinkki, ajo-ohjeet ja saapuminen on erotettu. Sisältöviite: https://nummirock.fi/liput_ja_sijainti . Kartta ei lataudu automaattisesti; karttalinkki avaa Googlen kartan.
- Modaalin visualisointi noudattaa käyttäjän toimittamia **1.0-kuvakaappauksia**: musta ylätunniste, Info/Liput, tuotevalinta, tilaajatiedot, maksutaparuudukko, oikean palstan kori ja loppusumma sekä Maksua odotetaan -näkymä. Tämä EI vahvista 2.0-version näkymien vastaavuutta. Aiemmissa 2.0-kuvissa kassa on kolmipalstainen. Tekninen PDF määrittelee toimintoja, ei ulkoasun yhtäläisyyttä. Tämä versioero tarkistetaan sandboxissa Leealta.
- Määrän muutokset ovat nyt kaupan oman tuotevalinnan sisällä, eivät Nummirockin sivulla. Ne eivät esitä puuttuvia ulkoisen API:n komentoja tuettuina.
- Demomaksu avautuu erilliseen välilehteen. Välilehden sulkeminen jättää maksun odottamaan. Sivulla on jatkopainike ja tilauksen peruminen; vasta hyväksytty demomaksu näyttää onnistumisen. Viestin alkuperä, lähettäjäikkuna ja satunnainen tunniste tarkistetaan. Ei oikeaa maksupalvelua.

Aiemmat maininnat demomaksun samasta ikkunasta ja kolmipalstaisesta demokassasta kuvaavat ensimmäistä versiota ja korvautuvat yllä olevalla. Vanha tavoitemalli repositorion juuressa säilyy muuttumattomana.

### Lippusivun tyylit ja toteutusrajaus

Maksutapalogot ovat nyt tuotteet-sivun tapaan harmaat, keskitetyt ja ilman taustakortteja. Sijainti ja saapuminen käyttää pääotsikon fonttia, kokoa ja riviväliä. Sivun sisäiset pikalinkit sekä ensisijaisuus- ja tilannekuvatekstit poistettiin käyttäjän pyynnöstä.

Lippupainikkeen avaus vastaa dokumentoitua komentoa `window.LIVETO_JS_API("open/event", {event: "nummirock-2027", view: "tickets"})`. Yksittäisen lipun syvälinkkiä tai erillistä open/checkout-komentoa ei oleteta tuetuksi. Merch vastaa tapahtumaa `nummirock-shop`, näkymää `merchandise`. Proto simuloi näitä, eikä lataa oikeaa Livetoa.

**Käyttäjän pysyvä ohje:** jos tuleva muutospyyntö vaatii Livetolta kehitystä, jota ei voi toteuttaa nykyisellä aikataululla, huomauta ensin. Älä toteuta tällaista muutosta ilman huomautuksen jälkeen annettua erillistä pyyntöä.
