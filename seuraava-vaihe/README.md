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
