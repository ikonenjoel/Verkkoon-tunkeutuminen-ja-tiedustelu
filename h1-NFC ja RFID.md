## Läksyt: [h4](https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#tehtavanannot) - NFC ja RFID.

# a)

Käytössä on mm. iLOQ:n kotiavain, HSL:n matkakortti, pankkikortteja ja Samsungin NFC-tunniste. Mielestäni, olen suojautunut hyvin urkkimiselta, sillä kotiavain tarvitsee lukkopesän luodakseen virtaa ja ei toimi muuten, pankkikortit ovat hyvin suojattuja ja lompakossani, joten niihn ei noin vain työnnetä laitetta kiinni. 
Samsungin NFC-tunnisteet ovat jossain laatikossa piilossa ja ovat tällä hetkellä tyhjiä, joten niiden urkkiminen on turhaa. 

# b)

APDU-komennot (Application Protocol Data Unit) ovat viestiyksiköitä, joita käytetään tiedonsiirtoon älykortin, kuten SIM-kortin, pankkikortin tai henkilökortin ja kortinlukijan välillä.

Kommunikaatiko perustuu isäntä-orja-malliin, jossa lukija lähettää aina komennon ensin ja kortti vastaa siihen. Se käyttää ISO/IEC 7816-4 -standardia. (ISO/IEC 7816-4 2020.)

Lukija lähettää kortille komennon, joka koostuu pakollisesta ostikosta ja valinnaisesta runko-ostasta. 

Ensimmäisenä kerrotaan komennon tyyppi sekä käytetty kanava (Class), sen jälkeen määritetään suoritettava toiminto, esim. SELECT tiedoston valitsemiseksi tai READ tiedoston lukemiseksi.

Niitä seuraa parametrit, jotka antavat lisätietoa komennolle, kuten muistiosoitteita, eli mistä lukea tietoa.

Lopussa lähetetään datan pituus, itse data (esim. PIN-koodi) ja kortilta odotetun vastausdatan maksimipituus. 



Kortti vastaa suoritettuun komentoon valinnaisella vastausdatalla, sekä kaksitavuisella vastausdatalla, joka kertoo onnistuiko komento. (Rytkönen, 2013)

## **Tämän kappaleen sisällön ideoinnissa on hyödynnetty Gemini Fast -kielimallia. Syötteenä käytettiin: ”APDU käyttökohteita”:**

Käyttökohteita ovat mm. maksukortit ja henkilökortit, maksukorttien kohdalla voidaan tarkistaa sirun aitous ja suorittaa maksu kun taas henkilökortista voidaan vaikka lukea henkilön nimi ja syntymäaika. 

# c)

Löysin kiinnostavan uutisen dormakaban Saflok-lukoista, joista löytyit haavoittuvuus jonka avulla yli 3 miljoonaa hotellilukkoa saatiin avattua väärennetyllä RFID-kortilla. Lukkoja löytyy 131 eri maasta. Lukkojen päivitys ja vaihtaminen alkoi jo, mutta en löydä uutta tietoa siitä, onko asialle tehty mitään.

Viimeisin päivitys on maaliskuulta 2024, jolloin n. 36% lukoista oli joko vaihdettu tai päivitetty. (unsaflok, 2024)


Lähteet: 

ISO/IEC 7816-4 2020. Identification cards — Integrated circuit cards — Part 4: Organization, security and commands for interchange. International Organization for Standardization. Luettu 17.4.2026. Luettavissa: [Iso.org](https://www.iso.org/standard/77180.html#lifecycle)
Rytkönen, J. 2013. Kulunvalvonnan toteutus tehden-ohjelmistoon. AMK-opinnäytetyö. Turun ammattikorkeakoulu. Tietojenkäsittely, tietojärjestelmät. Luettu 17.4.2026. Luettavissa: [theseus.fi](https://www.theseus.fi/bitstream/handle/10024/65209/Rytkonen_Janne.pdf?sequence=1)
unsaflok. Unlocking Millions of Hotel Locks. Luettu 17.4.2026. Luettavissa: [https://unsaflok.com/](https://unsaflok.com/)
