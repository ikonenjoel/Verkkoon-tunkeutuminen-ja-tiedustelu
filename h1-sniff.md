## Läksyt: [h1](https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#:~:text=Page%20Using%20Github-,h1,-Sniff) - sniff.

1. Karvinen 2025: [Wireshark - getting started](https://terokarvinen.com/wireshark-getting-started/)
   - Wiresharkin asennus ja sen konfigurointia
   - Käyttäjän lisääminen tarkkailua varten
   - Miten avataan wireshark komentokehotteen avulla
   - Pakettien "sniffailua"
   - Valitaan mitä halutaan etsiä
     - "any" valinta valitsee kaiken liikenteen ja helpottaa etsimistä
     - Pakettien kaappauksen pystyy lopettamaan painamalla "Stop". Uuden kaappauksen voi aloittaa menemällä "Capture" menun "Options" kohtaan ja painamalla sinistä hainevää vasemmassa yläkulmassa.

   - Jos paketteja ei näy, kokeile esim. selata webbiä, jos ei vieläkään näy tarkista, että olet jossain ryhmässä "groups" komennolla.
   - Pakettien tallentaminen ja lataaminen:
     - Tallennetaan paketti: File -> Save as
     - Dialog: Save Capture file as: filenameexample.pcap -> Save as "Wireshark/tcpdump/... -pcap"
     - Tiedoston avaaminen: File -> Open ja painetaan "Select your file"
       - Ladattua tiedostoa voi analysoida samalla tavalla kuin reaaliaikaista pakettien "sniffausta"
   - Statistiikka:
       - Päätepisteet: Lista isännöistä/palvelimista joita voit tarkistella.
       - I/O kaaviot: Millon ns. liikenne palvelimella tapahtui ja kauan paketteja kaapattiin.
       - Protokollan hierarkia: Kertoo, onko jokin HTTPS vai telnet, filterit vaikuttavat mitä täällä näkyy. Nähdäksesi kaiken nollaa filterit.
   - Filteröinti:
     - Voit filteröidä, mitä kaapatusta datasta näytetään:
       - DNS(Domain Name System) Näyttää, mitä DNS käytetään.
       - TLS(Transport layer security) Näyttää tsl-suojatut paketit, tähän sisältyy lähes kaikki internetselailu
       - HTTP(Hypertext transfer protocol)Suojaamattomat HTTP yhteydet
       - tcp.port == 443, etsii portilla 443 ulostulevan ja menevän liikenteen.
       - ip.addr == 192.167.122.7, sama kuin aikaisempi, mutta ip:n kautta.
       - frame contains "terokarvinen.com", hakee kaiken tietyllä merkkijonolla.
     - Voit myös filteröidä painamalla pakettia hiiren oikealla napilla ja valitsemalla "Apply as Filter..." ominaisuuden.
    
2. Karvinen 2025: [Network Interface Names on Linux](https://terokarvinen.com/network-interface-linux/)

   - Network interface on melkein kuin verkkokortti, ei vain aineellinen sellainen.
   - Linuxissa verkkokortit nimeää systemd.



| Prefiksi | Interface type |
| :--- | :--- |
| en | Wired Ethernet |
| wl | WLAN, Wireless local area network |
| lo | Loopback adapter |

   - loopback adapteria käytetään yhteyksille, joita ei kuulu ohjata pois tietokoneesta. Jokainen tietokone kutsuu itseään "localhostiksi", jonka IP on 127.0.0.1.

Esimerkkejä yleisistä verkkoliitäntänimistä.



| Interface | Selitys |
| :--- | :--- |
| wlp4s0 | wifikortti |
| enp1s0 | Langallinen ethernet-kortti |
| lo | loopback adapteri |
| enx738899738899 | Langallinen ethernet-kortti, numero x:n jälkeen on kortin MAC-numero


### a) Linux. Asenna Debian tai Kali Linux virtuaalikoneeseen. (Tätä alakohtaa ei poikkeuksellisesti tarvitse raportoida, jos sinulla ei ole mitään ongelmia. Jos on mitään haasteita, tee täsmällinen raportti)

Käytin Kalin valmiina olevaa asennustiedostoa. 

### b) Ei voi kalastaa. Osoita, että pystyt katkaisemaan ja palauttamaan virtuaalikoneen Internet-yhteyden.

<img width="438" height="178" alt="kuva" src="https://github.com/user-attachments/assets/096532d8-f5ec-4b3e-b169-c9a277c290fe" /> 
Yhteys katkaistaan ja laitetaan päälle uudestaan samasta kohdasta. 

### c) Wireshark. Asenna Wireshark. Sieppaa liikennettä Wiresharkilla. (Vain omaa liikennettäsi. Voit käyttää tähän esimerkiksi virtuaalikonetta).

<img width="1185" height="777" alt="kuva" src="https://github.com/user-attachments/assets/e79e3e70-e1d9-4e6b-a28e-96782de9c49d" />

Kuvakaappaus kali linuxissa pyörivästä wiresharkista, joka sieppaa liikennettä.

### d) Oikeesti TCP/IP. Osoita TCP/IP-mallin neljä kerrosta yhdestä siepatusta paketista. Voit selityksen tueksi laatikoida ne ruutukaappauksesta. (Voit käyttää vastauksesi osana ruutukaappaustasi h0-tehtävästä, mutta tässä tehtävässä tarvitaan myös sanallinen selitys.)

<img width="690" height="78" alt="kuva" src="https://github.com/user-attachments/assets/ac5d9811-c196-45f1-890a-b0147704a812" />

Listattuna kaikki neljä TCP/IP-mallin kerrosta kuvakaappauksessa. 

### e) Mitäs tuli surffattua? Avaa surfing-secure.pcap. Tutustu siihen pintapuolisesti ja kuvaile, millainen kaappaus on kyseessä. Tässä siis vain lyhyesti ja yleisellä tasolla. Voit esimerkiksi vilkaista, montako konetta näkyy, mitä protokollia pistää silmään. Määrästä voit arvioida esimerkiksi pakettien lukumäärää, kaappauksen kokoa ja kestoa.

Ainakin googlea ja terokarvinen.com sivua selattu. Näyttäisi olevan yksityishenkilön selailua internetissä. Tietokoneita vaikuttaisi olevan kaksi ethernet-yhteyksien perusteella.

### g) Minkä merkkinen verkkokortti käyttäjällä on? surfing-secure.pcap

En saanut sitä selville, sillä kaappauksessa on käytetty virtuaalikonetta, joten käyttäjän verkkokorttia ei voi tunnistaa.


### h) Millä weppipalvelimella käyttäjä on surffaillut? surfing-secure.pcap

mm. google.com, terokarvinen.com ja goatcounter.

### i) Analyysi. Sieppaa pieni määrä omaa liikennettäsi. Analysoi se, eli selitä mahdollisimman perusteellisesti, mitä tapahtuu. (Tässä pääpaino on siis analyysillä ja selityksellä, joten liikennettä kannattaa ottaa tarkasteluun todella vähän - vaikka vain pari pakettia. Gurut huomio: Selitä myös mielestäsi yksinkertaiset asiat.)


<img width="2550" height="219" alt="kuva" src="https://github.com/user-attachments/assets/afb4fe60-0ed0-4ca4-9d37-2a927247f020" />

Yritin selata reddittiä, mutta pääsy sivulle estettiin. Nimipalvelimen kautta selvittämään redditin IP ja siihen yhteys, data tulee HTTPS:n kautta joten salattu ja sitä ei pääse tarkemmin tutkimaan. 



Lähteet:

* Karvinen, T. 2025. Wireshark - Getting Started.
https://terokarvinen.com/wireshark-getting-started/

* Karvinen, T. 2025. Network Interface Names on Linux.
https://terokarvinen.com/network-interface-linux/
