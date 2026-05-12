## Läksyt: [h7](https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#tehtavanannot) - Aaltoja harjaamassa

# x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva.)

- dekoodaus tapahtuu rtl_433 softalla, josta saadaan selville laitteen malli sekä perustietoja kuten laitteen ID, kanava ja lämpötilatiedot. 
- Lähetystä nauhoitetaan Universal Radio Hacker-työkalulla ja se tallennetaan tietokoneelle jotta sitä voi myöhemmin käyttää analysointiin.
- Signaalia tulee nauhoittaa noin 20-100KHz ohi tavoitteesta jotta ohjelma voi laskea tavoitteen ja taajuuden välistä eroa.


# b)  rtl_433. Asenna rtl_433 automaattista analyysia varten. Kokeile, että voit ajaa sitä. './rtl_433' vastaa "rtl_433 version 25.02 branch..."

Näyttäisi toimivan.

<img width="1174" height="946" alt="kuva" src="https://github.com/user-attachments/assets/b2fc40e8-237a-4a11-b804-093d38fbe1ab" />


# c) Automaattinen analyysi. Mitä tässä näytteessä tapahtuu? Mitä tunnisteita (id yms) löydät? Converted_433.92M_2000k.cs8. Analysoi näyte ‘rtl_433’ ohjelmalla.

<img width="1320" height="903" alt="kuva" src="https://github.com/user-attachments/assets/615662a2-8a6b-4e23-a394-0741713122cf" />

Mitä löysin: 

tag: Converted_433.92M. Sama kaikissa
model: Proove-Security, Nexa-Security, KlikAanKlikUit-Switch.
Channel: 0 (KlikAanKlikUit-Switch), 3 (Proove-Security ja Nexa-Security).
id: 8785315, sama kaikissa, joissa on id.
House Code: 8785315 - Sama kuin ID
State: OFF. Kytketty pois päältä, muistelisin, että tämä on verkkovirtaan kytkettävä pistorasia josta opettaja puhui tunnilla.

# d) Too compex 16? Olet nauhoittanut näytteen 'urh' -ohjelmalla .complex16s-muodossa. Muunna näyte rtl_433-yhteensopivaan muotoon ja analysoi se. Näyte Recorded-HackRF-20250411_183354-433_92MHz-2MSps-2MHz.complex16s

Muutin tiedoston cs8 muotoon ja ajoin samna komennon kuin aikaisemmin, jolla saatiin tulostettua tämä:

<img width="1062" height="870" alt="kuva" src="https://github.com/user-attachments/assets/efe13094-44ba-4b6c-9fe6-2c6b5710026f" />

# e) Ultimate 

Asensin UHR:n jo aikaisemmin katsoakseni d) kohdassa olevaa näytettä. 

<img width="622" height="67" alt="kuva" src="https://github.com/user-attachments/assets/27e85708-a7b7-41d4-816c-bf07ed683e40" />


<img width="2067" height="809" alt="kuva" src="https://github.com/user-attachments/assets/b9c6dca5-606d-45df-826b-8f0cc2dc1ec1" />

Kaiken datan valitsemalla saadaan selville pituus joka on kyseisellä tiedostolla 5.49 sekuntia.

<img width="2558" height="659" alt="kuva" src="https://github.com/user-attachments/assets/0babab62-27ce-4cb1-891d-2e05ba40b3ea" />

# f) Yleiskuva. Kuvaile näytettä yleisesti: kuinka pitkä, millä taajuudella, milloin nauhoitettu? Miltä näyte silmämääräisesti näyttää?

URH:n infonappulalla saatiin hyvä määrä lisätietoa, kuten tiedoston koko: 10.47mb ja näyttenottotaajuus 1,0M.

# g) Bittistä. Demoduloi signaali niin, että saat raakabittejä. Mikä on oikea modulaatio? Miten pitkä yksi raakabitti on ajassa? Kuvaile tätä aikaa vertaamalla sitä johonkin. (Monissa singaaleissa on line encoding, eli lopullisia bittejä varten näitä "raakabittejä" on vielä käsiteltävä)

ASK vaikuttaisi olevan oikea modulaatio, sain sillä raakabittejä esiin. Yksi raakabitti on 250μs pitkä ja sillä niitä on kaksi niin yhden databitin pituus on 500μs. Kesto on samaa luokkaa kuin kameran sulkimen suljinaika.

Kuvakaappaus yhdestä databitistä: 

<img width="2557" height="852" alt="Screenshot 2026-05-12 140339" src="https://github.com/user-attachments/assets/50cb528c-8e49-4a53-93b8-99fe66f62c46" />

Lähteet: Karvinen, T. Aaltoja Harjaamassa. Luettavissa: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/. Luettu 12.5.2026
